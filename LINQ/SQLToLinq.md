```c#
// SELECT * FROM Customers
from c in Customers
select c
```

//SELECT FirstName, Age FROM Customers
from c in Customers
select new {c.FirstName, c.Age}

//SELECT TOP 3 * FROM Customers Order By Age 
Customers.OrderBy (c => c.Age).Take (3)
Customers.OrderByDescending (c => c.Age).Take (100)

//SELECT * FROM Customers WHERE CustomerID = 2
from c in Customers
where c.CustomerID == 7
select c

//SELECT * FROM Customers WHERE age > 36
from c in Customers
where c.Age >= 7
select c

Customers.Where (c => c.Age >= 7)

//SELECT * FROM Customers WHERE age > 36 AND FirstName = 'Selvi'
from c in Customers
where  c.FirstName == "Selvi" && c.Age >= 26
select c


//SELECT * FROM Customers  INNER JOIN Addresses ON Customers.CustomerID = Addresses.CustomerID
from c in Customers join a in Addresses on c.CustomerID equals a.CustomerID 
select new  
{  
    c.CustomerID,  c.FirstName, a.City
}  

//SELECT Max(Age) AS record_count FROM Customers
(from c in Customers
select c.Age).Max()

//SELECT SUM(Age) AS record_count FROM Customers
(from c in Customers
select c.Age).Sum()

//SELECT COUNT(Age) AS record_count FROM Customers
(from c in Customers
select c).Count()

Customers.Count()

// SELECT TOP 3 * FROM Customers
Customers.Take (3)

https://medium.com/@heitorhherzog/converting-t-sql-queries-in-linq-aa59afbf6dbe

//Select with TOP
T-SQL 
SELECT TOP 2 Name FROM Artist;
LINQ
var result = (from a in context.Artist select a.Name).Take(2);
LAMBDA
var result = context.Artist.Select(a => a.Name).Take(2);


//Select with WHERE
T-SQL
SELECT Name  FROM Artist WHERE Name = "InFlames";
LINQ
var result = (from a in context.Artist
                    where a.Name.Equals("InFlames") 
                    select a.Name).ToList();
LAMBDA
var result = context.Artist
                    .Where(a => a.Name.Equals("InFlames"))
                    .Select(a => a.Name).ToList();

//Select with INNER JOIN
T-SQL
SELECT a.Name, al.Tile FROM Artist a 
       		INNER JOIN Album al ON al.ArtistId = a.ArtistId;
LINQ
var result = (from a in context.Artist
            join al in context.Album on a.ArtistId equals al.ArtistId
            select new
            {
                a.Name,
                al.Title
            }).ToList();
LAMBDA
var result = context.Artist
            .Join(context.Album, artist => artist.ArtistId, album => album.ArtistId,
            (artist, album) => new { Artist = artist, Album = album })
            .Select(a => new { 
                Name = a.Artist.Name, 
                Title = a.Album.Title
            }).ToList();

//Select with two conditions in the same Inner Join
T-SQL
SELECT DISTINCT a.Name, al.Title FROM Artist a 
        		INNER JOIN Album al ON al.ArtistId = a.ArtistId AND al.Title = a.Name;
LINQ
var result = (from a in context.Artist
            join al in context.Album on
            new { C1 = a.ArtistId, C2 = a.Name } equals 
            new { C1 = al.ArtistId, C2 = al.Title}
            select new
            {
                a.Name,
                al.Title
            }).ToList();
LAMBDA
var result = context.Artist
        .Join(context.Album, artist => new { C1 = artist.ArtistId, C2 = artist.Name }, 
            album => new { C1 = album.ArtistId, C2 = album.Title},
            (artist, album) => new { Artist = artist, Album = album })
        .Select(a => new { 
            Name = a.Artist.Name, 
            Title= a.Album.Title
        }).ToList();

//Select with two INNER JOINS
T-SQL
SELECT a.Name, al.Title, f.Name FROM Artist a
INNER JOIN Album al ON al.ArtistId = a.ArtistId
INNER JOIN Track f ON f.AlbumId = al.AlbumId;
LINQ
var result = (from a in context.Artist
        join al in context.Album on a.ArtistId equals al.ArtistId
        join f in context.Track on al.AlbumId equals f.AlbumId
        select new
        {
            Artist = a.Name,
            Album = al.Title,
            Track = f.Name
         }).ToList();
LAMBDA
var result = context.Artist
        .Join(context.Album, artist => artist.ArtistId, album => album.ArtistId,
            (artist, album) => new { Artist = artista, Album = album })
        .Join(context.Track, album => album.Album.AlbumId, track=> track.AlbumId,
            (album, track) => new { Album = album, Track= track})
        .Select(a => new { 
            Name = a.Album.Artist.Name, 
            Titulo = a.Album.Album.Title, 
            Track= a.Track.Name 
        }).ToList();

//Select with LEFT JOIN
T-SQL
SELECT a.Name, al.Title FROM Artist a
        	LEFT JOIN Album al ON al.ArtistId = a.ArtistaId;
LINQ
var result = (from a in context.Artist
            join al in context.Album on a.ArtistId equals al.ArtistId 
                into All from al in All.DefaultIfEmpty()
            select new
            {
                a.Name,
                al.Title
            }).ToList();
LAMBDA
var result = context.Artist
            .GroupJoin(context.Album, artist => artist.ArtistId, album => album.ArtistId,
                (artist, album) => new { Artist = artist, Album = album.DefaultIfEmpty() })
            .SelectMany(a => a.Album, (a, album) => new { 
                a.Artist.Name, 
                album.Title
            }).ToList();

//Select with two LEFT JOINS, GROUP BY and COUNT
T-SQL
SELECT DISTINCT a.Name, 
              (SELECT COUNT(*) AS Album FROM Album WHERE ArtistId = a.ArtistId) AS Album, 
            	COUNT(f.TrackId) AS Track
        	FROM Artist a
LEFT JOIN Album al ON al.ArtistId = a.ArtistId
LEFT JOIN Track f ON f.AlbumId = al.AlbumId
GROUP BY a.Name, a.ArtistId;
LINQ
var result = (from a in context.Artist
        join al in context.Album on a.ArtistId equals al.ArtistId 
            into All1 from al in All1.DefaultIfEmpty()
        join f in context.Track on al.AlbumId equals f.AlbumId 
            into All2
        from f in All2.DefaultIfEmpty()
        group a by a into grouped
        let totalAlbuns = grouped.Key.Album.Count()
        let totalTracks = grouped.Count(x => x.Album.Count > 0)
        select new
        {
            Artist = grouped.Key.Name,
            Albuns = totalAlbuns,
            Tacks = totalTracks
        }).ToList();
LAMBDA
var result = context.Artist
            .GroupJoin(context.Album, artist => artista.ArtistId, album => album.ArtistId,
                (artist, album) => album
.Select(x => new
            { 
               Artist = artist, 
               Album = x 
           })
            .DefaultIfEmpty(new { 
                Artista = artist, 
                Album = (Albuns)null 
            }))
            .SelectMany(x => x)
            .GroupJoin(context.Track, 
				album => album.Album.AlbumId, 
				track => track.Album.AlbumId,
               	 (album, track) => track.Select(y => new { 
                                                Artist = album.Artista, 
                                                Album = album.Album, 
                                                Track= y 
                                            })
            .DefaultIfEmpty(new { 
                Artist = album.Artist, 
                Album = album.Album, 
                Track = (Tracks)null 
            }))
            .SelectMany(y => y)
            .GroupBy(grouped => new { grouped.Artist })
            .Select(g => new
            {
                Artist = g.Key.Artist.Name,
                Albuns = g.Key.Artist.Album.Count(),
                Tracks = g.Count(x => x.Album.Track.Count > 0)
            }).ToList();
