
# Hello EF

1. Create new Console application
2. Install EntityFramework from NuGet 
3. Add Connection string in App.config.
```xml
<connectionStrings>
    <add name="MFCConnectionString" connectionString="Server=(local)\MYDBINSTANCE;Database=EFDB;Trusted_Connection=True;" providerName="System.Data.SqlClient" />
</connectionStrings>
```
4. Add Model Class: Student.cs
```cs
public class Student
{
  public Student() { }

  public int StudentID { get; set; }
  public string StudentName { get; set; }
}   
```
5. Add DB Context Class: MyBDContext.cs
```cs
public class MyBDContext : DbContext
{
  public MyBDContext() : base("name=MFCConnectionString")
  {
  }
  
  public DbSet<Student> Employees { get; set; }
}   
```
6. Client Code
```cs
static void Main(string[] args)
{
    var ctx = new MyBDContext();
    //Adding New Entities
    Student stu = new Student();
    stu.StudentName = "Rams";
    ctx.Students.Add(stu);
    ctx.SaveChanges();

    //Changing Existing Entities
    var student = (from d in ctx.Students
                    where d.StudentName == "Rams"
                    select d).Single();
    student.StudentName = "Ramaswamy";
    ctx.SaveChanges();

    //Deleting Existing Entities
    var stu1 = (from d in ctx.Students where d.StudentName == "Ramaswamy" select d).Single();
    ctx.Students.Remove(stu1);
    ctx.SaveChanges();

    //Add two students
    Student newStu1 = new Student();
    newStu1.StudentName = "Student 1";
    ctx.Students.Add(newStu1);

    Student newStu2 = new Student();
    newStu2.StudentName = "Student 2";
    ctx.Students.Add(newStu2);
    ctx.SaveChanges();

    //Query DB
    var queryResult = from b in ctx.Students
                orderby b.StudentID
                select b;

    Console.WriteLine("All student in the database:");

    //Print the result
    foreach (var item in queryResult)
    {
        Console.WriteLine(item.StudentID + " " + item.StudentName);
    }

    Console.WriteLine("Press any key to exit...");
    Console.ReadKey();
}
```        
