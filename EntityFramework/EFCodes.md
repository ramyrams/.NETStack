
# Hello EF

1. Create new Console application
2. Install EntityFramework from NuGet 
3. Add Connection string in App.config.
```xml
  <connectionStrings>
    <add name="MFCConnectionString" connectionString="Server=(local)\TIBURON;Database=EFDB;Trusted_Connection=True;" providerName="System.Data.SqlClient" />
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
        public MyBDContext()
            : base("name=MFCConnectionString")
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
            Student stu = new Student();
            stu.StudentName = "Rams";
            ctx.Employees.Add(stu);
            ctx.SaveChanges();
        }
```        
