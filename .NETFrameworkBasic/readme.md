.NET Framework Basics

* .NET Framework Architecture
* CLR Architecture
* CLR Features
* CLR Execution
* Role of CLR
* MSIL (Microsoft Intermediate Language) 
* Just In Time Compilers (JITers)
* Framework Class Library (FCL)
* Base Class Library (BCL)
* Common Intermediate Language (CIL)
* Common Language Specification (CLS)
* Common Type System (CTS)
* Garbage Collector (GC)
* .NET Assemblies
* Application Domain


# .NET Framework Architecture
![1](https://i-msdn.sec.s-msft.com/dynimg/IC104620.jpeg)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/09f663/net-architecture-and-net-framework-basics/Images/NET1.gif)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/09f663/net-architecture-and-net-framework-basics/Images/NET2.gif)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/09f663/net-architecture-and-net-framework-basics/Images/NET3.gif)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/puranindia/net-framework-and-architecture/Images/managed_code.gif)
![1](http://www.codeproject.com/KB/dotnet/DotNetWhitePaper/image002.gif)
![1](http://www.codeproject.com/KB/dotnet/DotNetWhitePaper/image003.gif)
![1](http://www.codeproject.com/KB/dotnet/DotNetWhitePaper/image004.jpg)
![1](http://www.codeproject.com/KB/dotnet/DotNetWhitePaper/image005.jpg)
![1](http://www.codeproject.com/KB/dotnet/DotNetWhitePaper/image006.jpg)
![1](http://www.codeguru.com/images/article/8245/Image1.jpg)
![1](https://blogs.utmb.edu/watercooler/wp-content/uploads/sites/9/2013/09/net-300x252.jpg)
![1](https://i.ytimg.com/vi/yL3cNP0-tFc/maxresdefault.jpg)
![1](https://silvrback.s3.amazonaws.com/uploads/971abb6a-0664-4cfc-8ebc-ea574cbc2416/ASP.NET%205_large.png)
![1](http://www.galcho.com/Blog/content/binary/WindowsLiveWriter/fd2ae95312ea.NETLayerCake_1219C/dotNet4_thumb.png)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/8911c4/code-execution-process/Images/Code-Execution-Process.jpg)
![1](http://www.developerin.net/include/ArticleImages/1/dotnet%20framework%20stack.png)
![1](http://www.arihantsatiate.com/ACD/marquee/asp.net/ASP.NET2.jpg)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC148840.jpg)
![1](http://www.heikniemi.net/hardcoded/wp-content/uploads/2011/10/WhatsNewNET45-en.png)
![1](https://www.safaribooksonline.com/library/view/c-60-in/9781491927090/assets/csn6_0101.png)
![1](http://www.bogotobogo.com/CSharp/images/framework/assembly2.png)
![1](http://image.slidesharecdn.com/csharpjn-090514144345-phpapp02/95/c-sharp-jn-21-728.jpg?cb=1242312262)
![1](http://kishore1021.files.wordpress.com/2012/02/image24.png)
![1](http://images.slideplayer.com/24/7321493/slides/slide_35.jpg)
![1](http://1.bp.blogspot.com/-NH5ybIP8lA4/UajDd8GVPGI/AAAAAAAACRM/jWJ6wpz2dDo/s1600/AppDomains.png)
![1](http://www.academictutorials.com/images/dotnet-framework.gif)
![1](http://www.academictutorials.com/images/languages.gif)
![1](https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcQS7n1n3bmvwVrNM1GESlUy1qfiKwShVO6CIrOZmCq3asN8nTTQuQ)
![1](http://2.bp.blogspot.com/-uZW0W4MeQ8I/UiWICb7-_TI/AAAAAAAABMM/UonVL6mZJu8/s1600/clr.jpg)
![1](http://3.bp.blogspot.com/-pWtfuKXU9-U/UwZYHUJ-QuI/AAAAAAAAAL0/gv02vauZQdU/s1600/Code+Execution+in+Dot+Net.PNG)
![1](https://rthumati.files.wordpress.com/2009/05/visual-studio2.jpg?w=490&h=539)
![1](https://abdelrahmanhosny.files.wordpress.com/2012/07/untitled5.png)
![1](https://abdelrahmanhosny.files.wordpress.com/2012/07/untitled6.png?w=768)
![1](http://mattblagden.com/blog/acronyms_galore/dotnetacronymvenndiagram.png)
![1](http://nikgrozev.com/images/blog/NET%20for%20Java%20Devs%20in%20a%20nutshell/dot_net.jpg)


# CLR
![1](http://archive.cnx.org/resources/ef7359b3c8d9f5e872afaad0a99ccd9d92d80ca5/graphics1.jpg)
![1](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6f/CLR_diag.svg/400px-CLR_diag.svg.png)
![1](http://www.academictutorials.com/images/clr.gif)
![1](http://www.academictutorials.com/images/clr-simple.gif)
![1](https://coddertube.wordpress.com/files/2009/08/clr.jpg)
![1](http://i.stack.imgur.com/5RjWm.jpg)
![1](http://flylib.com/books/4/320/1/html/2/files/0102fig03.gif)
![1](http://4.bp.blogspot.com/-GFJ_9pm3KLc/U-rZNCw79ZI/AAAAAAAABjw/4XpcJLOdFXQ/s1600/Load%2BThe%2BCLR.PNG)

# CLR Architecture
* Class loader - This will loads classes into CLR.
* IL Compiler - Convert MSIL code into native code.
* Code manager - Manages the code during execution.
* Garbage collector - This performs automatic memory management.
* Security engine - This enforces security restrictions as code level * security folder level and machine level security.
* Type checker - Enforces strict type checking.
* Thread support - Provides multithreading support to applications.
* Exception manager - Provides a mechanism to handle the run-time exceptions handling.
* Debug engine - Allows developer to debug different types of applications.
* COM Marshaler - Allows .NET applications to exchange data with COM applications.
* Base class library - Provides the classes (types) that the applications need at run time.


![1](http://www.infinitezest.com/images/dotnet-framework-structure.jpg)
![1](http://www.techstrikers.com/images/dotnetclr.png)


# CLR Execution
![1](http://flylib.com/books/4/320/1/html/2/files/0102fig04.gif)
![1](http://flylib.com/books/4/320/1/html/2/files/0102fig03.gif)
![1](http://images.cnblogs.com/cnblogs_com/huangyu/net.gif)
![1](https://abdelrahmanhosny.files.wordpress.com/2012/07/untitled8.png?w=768)
![1](https://abdelrahmanhosny.files.wordpress.com/2012/07/untitled9.png?w=768)


## Role of CLR
![1](http://www.onlinebuff.com/artimages/clr.jpg)
![1](http://etutorials.org/shared/images/tutorials/tutorial_10/nfe3_0204.gif)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/puranindia/benefits-of-the-net-framework/Images/sss.gif)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/puranindia/benefits-of-the-net-framework/Images/runningOfApplication.gif)
![1](http://images.slideplayer.com/25/7654501/slides/slide_9.jpg)

# MSIL (Microsoft Intermediate Language)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC156451.gif)
![1](http://image.slidesharecdn.com/lsauer-microsoftdotnetframework2003-2004overviewandwebservicesms-net-130313035655-phpapp02/95/microsoft-net-dotnet-framework-2003-2004-overview-and-web-services-15-638.jpg?cb=1363572651)
![1](https://ttdoanst.files.wordpress.com/2007/08/wordpress.png)
![1](http://photos1.blogger.com/blogger/3259/1944/1600/Tarea%202-1.gif)
![1](http://dotnet.edu.vn/Upload/Blog/2013/Thang8_2012/msil.jpg)
![1](http://dotnet.edu.vn/Upload/Blog/2013/Thang8_2012/quatrinhbiendichvachay2.jpg)
![1](http://dotnet.edu.vn/Upload/Blog/2013/Thang8_2012/clr2.jpg)



# Just In Time Compilers (JITers)

## Different Types of JIT
* Normal JIT
* Econo JIT
* Pre JIT

### Normal JIT
Normal JIT Compiler compile the methods at run time and then they are stored in memory cache. This memory cache is commonly referred as "JITTED".

Once stored in cache, no further compilation is required for the same method. Subsequent method calls are accessible directly from the memory cache.

### Econo JIT
This compiler compile methods when called at runtime and removes them from memory once execution completed.

### Pre JIT
This compiles entire assembly into native code instead of used methods.


http://www.techstrikers.com/images/Compile.PNG
![1](http://4.bp.blogspot.com/-5uexl8g32GQ/UiWKNW5ZoyI/AAAAAAAABMg/AOTw3UuxKOo/s640/jit.jpg)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/8ef97c/interview-question-on-net-framework-or-clr/Images/JIT%20Types.jpg)
![1](http://1.bp.blogspot.com/-KymNpDMPmf0/UTHJqDVD8VI/AAAAAAAAHO8/ZCse_fVljX4/s1600/meta.png)

http://www.techstrikers.com/images/normaljitcompiler.PNG
http://www.techstrikers.com/images/econojitcompiler.PNG
http://www.techstrikers.com/images/prejitcompiler.PNG


# CLR Features
* Manages memory
* Thread execution support
* Code execution
* Code safety verification
* Compilation
* Code Security 

# Framework Class Library (FCL)
![1](http://i.stack.imgur.com/SxbSG.jpg)
![1](http://www.codeproject.com/KB/dotnet/NETBasics/FCL.jpg)

# Base Class Library (BCL)
![1](http://modernpathshala.com/Images/dot-net-interview/Question/1947177520160401113030Base-class-library.JPG)
![1](https://devreminder.files.wordpress.com/2011/03/aspnetbcl.gif)
![1](https://abdelrahmanhosny.files.wordpress.com/2012/07/untitled7.png?w=768)

# Common Intermediate Language (CIL)
![1](http://4.bp.blogspot.com/-wuiRLJOJfCY/U-ru1od5DJI/AAAAAAAABkY/iqjQMyPaeDw/s1600/.NET.png)


# Common Language Specification (CLS)
![1](http://image.slidesharecdn.com/1philosophyofnet-1326119636943-phpapp02-120109083526-phpapp02/95/1philosophy-of-net-25-728.jpg?cb=1326098809)
![1](http://3.bp.blogspot.com/-1rKKRUyiU2c/U-rcyQkw2EI/AAAAAAAABj8/wi4l-MoKM2c/s1600/The%2BCommon%2BLanguage%2BSpecification.PNG)


# Common Type System (CTS)
![1](http://3.bp.blogspot.com/-BH1SXgx2TGM/U-rSMMAy1CI/AAAAAAAABjk/3RiwLG15DP0/s1600/CTS%2BDataType%2BRelationship.PNG)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/puranindia/benefits-of-the-net-framework/Images/cts-type-hei.gif)
![1](http://2.bp.blogspot.com/-lEr9_U40J1A/UiWI0qzbCsI/AAAAAAAABMU/epiiI4jkA38/s640/Common+Type+System+Architecture.jpg)
![1](http://image.slidesharecdn.com/csharpjn-090514144345-phpapp02/95/c-sharp-jn-13-728.jpg?cb=1242312262)
![1](https://rthumati.files.wordpress.com/2009/05/visual-studio7.jpg?w=637&h=352)
![1](http://dotnetcoderclues.com/StudyImages/common-type-system.png)
![1](http://ecomputernotes.com/images/Comman-type-System.jpg)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC161031.gif)
![1](http://image.slidesharecdn.com/introductionto-140916042152-phpapp02/95/introduction-to-net-framework-by-quontrasolutions-35-638.jpg?cb=1410841557)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC56291.gif)


# Garbage Collector (GC)
![1](http://4.bp.blogspot.com/-1obqc0tpclc/UZe6inxIzOI/AAAAAAAAA0s/CSl5tGU_8QQ/s640/GC.jpg)
![1](http://jbcdn2.b0.upaiyun.com/2012/12/Net-GC-05.gif)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC112504.gif)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC57444.gif)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC658910.jpeg)
![1](http://www.c-sharpcorner.com/article/garbage-collector-algorithm/Images/GC.gif)
![1](http://images.techhive.com/images/article/2015/09/garbage-collection-in-.net-100617168-primary.idge.png)
![1](http://www.telerik.com/sfimages/default-source/blogs/figure-3-png)
![1](http://www.codeproject.com/KB/aspnet/DONETBestPracticeNo2/8.jpg)


## URL
http://www.telerik.com/blogs/understanding-net-garbage-collection
http://www.codeproject.com/Articles/39246/NET-Best-Practice-No-2-Improve-garbage-collector
http://www.csharpque.com/2013/05/understanding-garbage-collection-in-net.html
https://msdn.microsoft.com/en-us/library/ms973837.aspx
http://www.c-sharpcorner.com/uploadfile/riteshratna/garbage-collection-memory-management-in-net/
https://msdn.microsoft.com/en-us/library/ee787088(v=vs.110).aspx


# .NET Assemblies
![1](http://1.bp.blogspot.com/-5jjtRrek4OU/U-ekAEzxkpI/AAAAAAAABjE/LMvHqynlmxc/s1600/.NET-Aware+Compilers.PNG)


# Application Domain
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/8ef97c/interview-question-on-net-framework-or-clr/Images/Windows%20process.jpg)
