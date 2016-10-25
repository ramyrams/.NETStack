# .NET Framework Basics

* .NET Platform vs .NET framework Vs .NET Environment 
* .NET Platform Standard
* .NET Framework Architecture
* .NET Application Type
* .NET Framework Components
* Common Language Runtime (CLR)
  * CLR Architecture
  * CLR Features
  * CLR Run-time services
  * CLR Compiler
  * CLR Execution (.NET Execution Model)
  * Role of CLR
  * Virtual Execution System (VES)
* Common Language Infrastructure(CLI)
* Intermediate Language
  * Common Intermediate Language (CIL)
  * Microsoft Intermediate Language (MSIL)
* Framework Class Library (FCL)
* Base Class Library (BCL)
* Common Language Specification (CLS)
* Common Type System (CTS)
* Just In Time Compilers (JITers)
* .NET Assemblies
  * Portable executable (PE)
  * CLR Header
  * Metadata
  * Resources
* Assembly Versioning
* Satellite Assembly
* Global Assembly Cache (GAC)
* Managed/UnManaged Code
* .NET Applications
* Strong Named Assemblies
* Side-By-Side Execution
* Application Domain
* NET Garbage Collection (GC)
* Code Access Security
* CLR Hosting
* .NET Framework Tools

# .NET Framework Architecture
![1](https://i-msdn.sec.s-msft.com/dynimg/IC104620.jpeg)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/09f663/net-architecture-and-net-framework-basics/Images/NET1.gif)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/09f663/net-architecture-and-net-framework-basics/Images/NET3.gif)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/puranindia/net-framework-and-architecture/Images/managed_code.gif)
![1](http://www.galcho.com/Blog/content/binary/WindowsLiveWriter/fd2ae95312ea.NETLayerCake_1219C/dotNet4_thumb.png)
![1](http://www.developerin.net/include/ArticleImages/1/dotnet%20framework%20stack.png)
![1](http://www.arihantsatiate.com/ACD/marquee/asp.net/ASP.NET2.jpg)
![1](http://www.heikniemi.net/hardcoded/wp-content/uploads/2011/10/WhatsNewNET45-en.png)
![1](https://www.safaribooksonline.com/library/view/c-60-in/9781491927090/assets/csn6_0101.png)
![1](http://www.academictutorials.com/images/languages.gif)
![1](https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcQS7n1n3bmvwVrNM1GESlUy1qfiKwShVO6CIrOZmCq3asN8nTTQuQ)
![1](http://2.bp.blogspot.com/-uZW0W4MeQ8I/UiWICb7-_TI/AAAAAAAABMM/UonVL6mZJu8/s1600/clr.jpg)
![1](http://www.codeguru.com/images/article/8245/Image1.jpg)
![1](http://image.slidesharecdn.com/overviewofmicrosoftdotnetplatforms-151027112620-lva1-app6891/95/overview-of-microsoft-dot-net-platforms-11-638.jpg)
![1](http://www.pixytech.com/rajnish/uploads/images/CLS.jpg)
![1](http://image.slidesharecdn.com/2-net-framework-overview-120201085125-phpapp01/95/net-framework-overview-14-638.jpg)
![1](https://anylinewebsiteresource.blob.core.windows.net/wordpressmedia/2016/03/dotnetframework45.png)

# .NET Platform Standard
![1](http://www.talkingdotnet.com/wp-content/uploads/2016/02/NET-Platform-Standard.png)
![1](http://image.slidesharecdn.com/movingforwardwithasp-160530064824/95/moving-forward-with-aspnet-core-12-638.jpg)

# .NET Application Type
* Console Application
* Windows or Desktop Application
* Web Application
* NT Services - Service Control Manager Sercies
* Web services
* REST API
* Mobile applications
* Components/libraries 
* Windows Store Applications



# CLR
![1](http://archive.cnx.org/resources/ef7359b3c8d9f5e872afaad0a99ccd9d92d80ca5/graphics1.jpg)
![1](http://kishore1021.files.wordpress.com/2012/02/image24.png)
![1](http://www.academictutorials.com/images/clr.gif)
![1](http://www.academictutorials.com/images/clr-simple.gif)


# CLR Architecture
* **Class loader** - This will loads classes into CLR. It is used to load all the classes (MSIL Code) at runtime into CLR. The class loader component of the CLR uses metadata to locate specific classes within assemblies, either locally or across networks.
* **IL Compiler** - Convert MSIL code into native code. It is a JIT (Just In Time) compiler it will convert MSIL code to native code.
* **Code manager** - Manages the code during execution.
* Garbage collector** - This performs automatic memory management. Memory allocation and Garbage collector, this performs automatic memory management.
* **Security engine** - This enforces security restrictions as code level * security folder level and machine level security. this enforces security restrictions as code level security folder level and machine level security using tools provided by Microsoft .NET and using .NET Framework setting under control panel.
* **Type checker** - Enforces strict type checking.
* **Thread support** - Provides multithreading support to applications. It provides multithreading support to .Net applications.
* **Exception manager** - Provides a mechanism to handle the run-time exceptions handling.
* **Debug engine** - Allows developer to debug different types of applications.
* **COM Marshaler** - Allows .NET applications to exchange data with COM applications.
* **Base class library** - Provides the classes (types) that the applications need at run time. Which provides the classes (types) that the applications need at run time.

![1](http://www.onlinebuff.com/artimages/clr.jpg)
![1](http://www.infinitezest.com/images/dotnet-framework-structure.jpg)
![1](http://www.techstrikers.com/images/dotnetclr.png)
![1](http://www.pixytech.com/rajnish/uploads/images/CLRInternal.jpg)

http://flylib.com/books/en/4.320.1.27/1/
http://www.cnblogs.com/sunkang/archive/2011/04/28/2038821.html
http://www.cnblogs.com/huangyu/archive/2004/08/07/31000.html
https://abdelrahmanhosny.com/2012/07/24/introduction-to-microsoft-net-framework-solution/
http://www.c-sharpcorner.com/uploadfile/8ef97c/interview-question-on-net-framework-or-clr/

# CLR Features
* Manages memory
* Thread execution support
* Code execution
* Code safety verification
* Compilation
* Code Security 

# CLR Run-time services
* Memory management
* Type safety
* Enforces Security
* Exception Management
* Thread support
* Debugging support


# Virtual Execution System (VES)
* The Common Language Runtime (CLR) is the .NET Framework's implementation of the VES.

* It provides direct support for a set of built-in data types, defines a hypothetical machine with an associated machine model and state, a set of control flow constructs, and an exception handling model.
* To a large extent, the purpose of the VES is to provide the support required to execute the Common Intermediate Language instruction set.
![1](http://mattblagden.com/blog/acronyms_galore/dotnetacronymvenndiagram.png)
![1](https://www.safaribooksonline.com/library/view/net-framework-essentials/0596001657/tagoreillycom20070221oreillyimages74612.png)




# CLR Compiler
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/09f663/net-architecture-and-net-framework-basics/Images/NET2.gif)
![1](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6f/CLR_diag.svg/400px-CLR_diag.svg.png)
![1](https://coddertube.wordpress.com/files/2009/08/clr.jpg)
![1](http://3.bp.blogspot.com/-pWtfuKXU9-U/UwZYHUJ-QuI/AAAAAAAAAL0/gv02vauZQdU/s1600/Code+Execution+in+Dot+Net.PNG)
![1](https://i.ytimg.com/vi/yL3cNP0-tFc/maxresdefault.jpg)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/8911c4/code-execution-process/Images/Code-Execution-Process.jpg)
![1](https://abdelrahmanhosny.files.wordpress.com/2012/07/untitled8.png?w=768)
![1](https://abdelrahmanhosny.files.wordpress.com/2012/07/untitled9.png?w=768)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/puranindia/benefits-of-the-net-framework/Images/sss.gif)

# CLR Execution
![1](http://i.stack.imgur.com/5RjWm.jpg)
![1](http://etutorials.org/shared/images/tutorials/tutorial_10/nfe3_0204.gif)
![1](http://flylib.com/books/4/320/1/html/2/files/0102fig03.gif)
![1](http://flylib.com/books/4/320/1/html/2/files/0102fig04.gif)
![1](http://4.bp.blogspot.com/-GFJ_9pm3KLc/U-rZNCw79ZI/AAAAAAAABjw/4XpcJLOdFXQ/s1600/Load%2BThe%2BCLR.PNG)
![1](http://images.cnblogs.com/cnblogs_com/huangyu/net.gif)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/puranindia/benefits-of-the-net-framework/Images/runningOfApplication.gif)
![1](http://www.codemag.com/Article/Image/070013/01fig03.jpg)

# Common Language Infrastructure (CLI)
![1](http://4.bp.blogspot.com/-wuiRLJOJfCY/U-ru1od5DJI/AAAAAAAABkY/iqjQMyPaeDw/s1600/.NET.png)
![1](http://nikgrozev.com/images/blog/NET%20for%20Java%20Devs%20in%20a%20nutshell/dot_net.jpg)
![1](https://abdelrahmanhosny.files.wordpress.com/2012/07/untitled6.png?w=768)
![1](https://abdelrahmanhosny.files.wordpress.com/2012/07/untitled5.png)
![1](http://www.uadnan.com/media/u/2014/07/common-language-infrastructure.png)

# Base Class Library (BCL)
* The Base Class Library (BCL), part of the Framework Class Library (FCL), is a library of functionality available to all languages using the.NET Framework. 
* The BCL provides classes which encapsulate a number of common functions, including file reading and writing,graphical rendaring, database interaction and XML document manipulation. 

![1](http://modernpathshala.com/Images/dot-net-interview/Question/1947177520160401113030Base-class-library.JPG)
![1](https://devreminder.files.wordpress.com/2011/03/aspnetbcl.gif)
![1](https://abdelrahmanhosny.files.wordpress.com/2012/07/untitled7.png?w=768)


# Framework Class Library (FCL) - 
* Superset of BCL
* Framework Class Library is the standard.NET Framework library of out-of-the-box reusable classes and components (APIs) 
* The Framework class library (FCL) is a comprehensive collection of reusable types including classes, interfaces and data types included in the .NET Framework to provide access to system functionality.

![1](http://image.slidesharecdn.com/architectureof-netframework-110303000929-phpapp02/95/architecture-of-net-framework-10-728.jpg)
![1](http://image.slidesharecdn.com/2-net-framework-overview-120201085125-phpapp01/95/net-framework-overview-43-638.jpg)
![1](http://i.stack.imgur.com/SxbSG.jpg)
![1](http://www.codeproject.com/KB/dotnet/NETBasics/FCL.jpg)
![1](http://image.slidesharecdn.com/netintroduction-1221908697118367-9/95/net-introduction-4-728.jpg)
![1](http://csharpprogramming.ru/wp-content//img/4/fcl_bcl.png)
![1](http://3.bp.blogspot.com/_QottG71972s/S13xZZiujeI/AAAAAAAAAAk/6d8eahYkoUA/s400/bcl_fcl.png)
![1](http://www.codemag.com/Article/Image/070013/01fig04.jpg)

http://chennadi.blogspot.com/2010/01/what-are-components-of-dotnet-framework.html

# Common Language Specification (CLS)
* CLS is a document that says how computer programs can be turned into MSIL code. 
* When several languages use the same bytecode, different parts of a program can be written in different languages. 
* Microsoft uses a Common Language Specification for their .NET Framework. 
* It was always a dream of Microsoft to unite all different languages into one umbrella and CLS is one step towards that. 
* Microsoft has defined CLS which are nothing but guidelines for languages to follow so that it can communicate with other .NET languages in a seamless manner.
* Common Language Specification (CLS) defines a subset of Common Type System (CTS). 
* (CTS) describes a set of types that can use different .Net languages have in common, which ensure that objects written in different languages can interact with each other. 
* Most of the members defined by types in the .NET Framework Class Library (FCL) are Common Language Specification (CLS) compliant Types. 
* Moreover Common Language Specification (CLS) standardized by ECMA .

![1](http://image.slidesharecdn.com/1philosophyofnet-1326119636943-phpapp02-120109083526-phpapp02/95/1philosophy-of-net-25-728.jpg)
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
![1](http://images.slideplayer.com/21/6309780/slides/slide_3.jpg)
![1](http://www.uadnan.com/media/u/2014/07/common-type-structure.png)

# Common Intermediate Language (CIL)
![1](https://abdelrahmanhosny.files.wordpress.com/2012/07/untitled6.png?w=768)
![1](https://abdelrahmanhosny.files.wordpress.com/2012/07/untitled5.png)
![1](http://images.slideplayer.com/24/7317073/slides/slide_8.jpg)


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


![1](http://www.techstrikers.com/images/Compile.PNG)
![1](http://4.bp.blogspot.com/-5uexl8g32GQ/UiWKNW5ZoyI/AAAAAAAABMg/AOTw3UuxKOo/s640/jit.jpg)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/8ef97c/interview-question-on-net-framework-or-clr/Images/JIT%20Types.jpg)
![1](http://www.techstrikers.com/images/normaljitcompiler.PNG)
![1](http://www.techstrikers.com/images/econojitcompiler.PNG)
![1](http://www.techstrikers.com/images/prejitcompiler.PNG)






# .NET Assemblies

## DLL HELL
![1](http://i1.wp.com/codehotfix.com/wp-content/uploads/2015/11/Dll-hell-problem.jpg?resize=1024%2C591)
![1](http://lh5.ggpht.com/kaushik810/SPrs3VulKLI/AAAAAAAADGs/ojPlyayORes/remove-dll%5B4%5D.gif?imgmax=800)
![1](http://www.itwriting.com/images/vcrterr1.gif)


![1](http://1.bp.blogspot.com/-5jjtRrek4OU/U-ekAEzxkpI/AAAAAAAABjE/LMvHqynlmxc/s1600/.NET-Aware+Compilers.PNG)
![1](http://images.slideplayer.com/24/7321493/slides/slide_35.jpg)
![1](http://www.bogotobogo.com/CSharp/images/framework/assembly2.png)
![1](http://image.slidesharecdn.com/csharpjn-090514144345-phpapp02/95/c-sharp-jn-21-728.jpg?cb=1242312262)
![1](http://foxcentral.net/microsoft/NETforVFPDevelopers_Chapter01_files/image005.jpg)

# Application Domain
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/8ef97c/interview-question-on-net-framework-or-clr/Images/Windows%20process.jpg)
![1](http://1.bp.blogspot.com/-NH5ybIP8lA4/UajDd8GVPGI/AAAAAAAACRM/jWJ6wpz2dDo/s1600/AppDomains.png)
![1](http://diranieh.com/NET/Figures/AppDomain.gif)

# # Managed/Unmanaged code
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/8ef97c/interview-question-on-net-framework-or-clr/Images/CLR.jpg)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/puranindia/managed-code-and-unmanaged-code-in-net/Images/unmanaged_code_RCW.gif)
![1](http://www.codeproject.com/KB/COM/cominterop/RCWCOMInterop.gif)
![1](http://www.codeproject.com/KB/COM/cominterop/ConnectPointDelegates_small.gif)
![1](http://www.codeproject.com/KB/COM/cominterop/CollectionEnumeration.gif)
![1](http://www.codeproject.com/KB/COM/cominterop/CCWInteraction_small.gif)
![1](http://image.slidesharecdn.com/sharepointunderground-100502110607-phpapp01/95/sharepoint-underground-unmanaged-code-and-sharepoint-internals-7-728.jpg)
![1](http://images.slideplayer.com/25/7612974/slides/slide_17.jpg)
![1](http://image.slidesharecdn.com/sharepointunderground-100502110607-phpapp01/95/sharepoint-underground-unmanaged-code-and-sharepoint-internals-6-728.jpg)
![1](http://www.bass.radio42.com/help/media/PInvoke.bmp)
![1](http://www.jot.fm/issues/issue_2006_11/article1/images/figure3.gif)
![1](http://foxcentral.net/microsoft/NETforVFPDevelopers_Chapter01_files/image003.jpg)
![1](http://www.codemag.com/Article/Image/070013/01fig02.jpg)






# Assembly

# Types of assemblies:

* **Private Assemblies** are accessible by a single application. They reside within the application folder and are unique by name. They can be directly used by copying and pasting them to the bin folder.
* **Shared Assemblies** are shared between multiple applications to ensure reusability. They are placed in GAC.
* **Satellite Assemblies** are the assemblies to provide the support for multiple languages based on different cultures. These are kept in different modules based on the different categories available.

![1](http://images.slideplayer.com/24/7321493/slides/slide_12.jpg)

# Static Assemblies vs Dynamic assemblies

Static assemblies can include .NET Framework types (interfaces and classes), as well as resources for the assembly (bitmaps, JPEG files, resource files, and so on). Static assemblies are stored on disk in portable executable (PE) files. You can also use the .NET Framework to create dynamic assemblies, which are run directly from memory and are not saved to disk before execution. You can save dynamic assemblies to disk after they have executed.

## Static Assemblies
Static Assemblies are those Assemblies which are stored on the disk permanently. 
They may include .NET Framework classes, interfaces as well as resource file. 
These assemblies are not loaded directly from the memory instead they are directly loaded from the disk when CLR (Common Language RunTime) requests for them. These Assemblies used to store on the disk as a file or set of file. 
Whenever one compiles the C# code, one gets STATIC assemblies.

##  Dynamic assemblies
Dynamic assemblies are those assemblies which are not stored on the disk before execution in fact after execution they get stored on the disk. When .NET runtime calls them they are directly loaded from the memory not from the disk. 
Reflection emit provides many ways to create dynamic assemblies means These are created in the memory using System.Reflection.emit namespace.
The System.Reflection.Emit namespace contains classes that allow a compiler or tool to emit metadata and Microsoft intermediate language (MSIL) and optionally generate a PE file on disk. 
When an application requires the types within these assemblies these dynamic assemblies are created dynamically at run time

![1](http://images.slideplayer.com/24/7321493/slides/slide_9.jpg)



![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/ajyadav123/net-assembly-internals-part-1/Images/Assembly%20Structure.jpg)
![1](http://images.slideplayer.com/24/7317073/slides/slide_20.jpg)
![1](http://image.slidesharecdn.com/assembliesversioningandsigning-110426033320-phpapp01/95/assemblies-versioning-and-signing-3-728.jpg)
![1](http://etutorials.org/shared/images/tutorials/tutorial_10/nfe3_0202.gif)
![1](http://images.slideplayer.com/27/9257993/slides/slide_30.jpg)

# Portable executable (PE)
* The standard of windows portable executable file format header is similar to common object filr format (COFF) headers. 
* Header contains information about type of the file. That whether it is DLL, GIF etc.
* Header contains information about time stamp that when file built. 
* If the managed module is having only IL then PE 32 (+) header is ignored by CLR. 
* If the managed module contains CPU Instructions then PE 32 (+) header contains information about CPU instructions. 

![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/dhananjaycoder/demystifying-clr-part-i/Images/5.gif)
![1](https://srinivasgandu.files.wordpress.com/2011/05/assemblyheader.jpg)
![1](http://etutorials.org/shared/images/tutorials/tutorial_10/nfe3_0202.gif)
![1](http://images.slideplayer.com/16/5175061/slides/slide_28.jpg)
![1](https://srinivasgandu.files.wordpress.com/2011/05/assemblyheader.jpg)
![1](https://www.simple-talk.com/blogbits/simon.cooper/PE%20Headers%20annotated.png)

https://srinivasgandu.wordpress.com/2011/05/31/how-operating-system-understands-and-executes-a-net-application/

# CLR Header 
* This contains the information interpreted by CLR.
* This contains information about version of CLR needed to interpret the managed module. 
* This contains Flags information.
* CLR header contains MethodOF token which says what is entry point (main method) of managed module. 

https://www.simple-talk.com/wp-content/uploads/blogbits/simon.cooper/CLI%20Contents%20annotated.png


# Metadata
* Every compiler targeting the CLR must emit a full set of Meta data. Meta Data is set of tables that contain all the information about what defines in the module. 
* This contains information about all the types and members used in the code. This also contains all the type and members referenced in the code.  
* Meta Data is always associated with the files contain the IL. Meta Data packaged in the same dll or exe file. 
* Each managed modules contain Meta Data table. 
* Data about data contained in the assembly 
* Integral part of the assembly 
* Generated by the.NET languages compiler 
* Describes all classes, their class members, versions, resources, etc. 

* Uses of Meta Data table 
  * Meta Data removes the natives' code like header files. 
  * Visual Studio uses Meta Data to perform work of IntelliSense. IntelliSense feature of visual studio uses Meta data tables to give suggestion while writing codes. 
  * CLR code verification uses Meta Data tables to make sure code only performs type safe operations. 
  * Meta Data performs work of serialization and deserialization. 
  * Garbage collector reads life time of object from Meta data table. 


![1](http://player.slideplayer.com/14/4294897/data/images/img7.jpg)
![1](http://images.slideplayer.com/14/4294897/slides/slide_33.jpg)
![1](http://images.slideplayer.com/23/6586025/slides/slide_3.jpg)
![1](http://images.slideplayer.com/23/6586025/slides/slide_4.jpg)
![1](http://player.slideplayer.com/23/6586025/data/images/img0.jpg)
![1](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/dhananjaycoder/demystifying-clr-part-i/Images/6.gif)
Read More - [Metadata in the.NET assemblies](http://slideplayer.com/slide/6586025/)


# Manifest
* An Assembly Manifest is a file that containing Metadata about .NET Assemblies. 
* Assembly Manifest contains a collection of data that describes how the elements in the assembly relate to each other. 
* It describes the relationship and dependencies of the components in the Assembly, versioning information, scope information and the security permissions required by the Assembly.
* The Assembly Manifest can be stored in Portable Executable (PE) file with Microsoft Intermediate Language (MSIL) code. 
* You can add or change some information in the Assembly Manifest by using assembly attributes in your code. 
* The Assembly Manifest can be stored in either a PE file (an .exe or .dll) with Microsoft Intermediate Language (MSIL) code or in a standalone PE file that contains only assembly manifest information. Using ILDasm, you can view the manifest information for any managed DLL.

![1](http://2we26u4fam7n16rz3a44uhbe1bq2.wpengine.netdna-cdn.com/wp-content/uploads/071613_1201_NETAssembly3.png)
![1](http://2we26u4fam7n16rz3a44uhbe1bq2.wpengine.netdna-cdn.com/wp-content/uploads/071613_1201_NETAssembly1.png)
![1](http://2we26u4fam7n16rz3a44uhbe1bq2.wpengine.netdna-cdn.com/wp-content/uploads/071613_1201_NETAssembly8.png)
![1](http://2we26u4fam7n16rz3a44uhbe1bq2.wpengine.netdna-cdn.com/wp-content/uploads/071613_1201_NETAssembly10.png)
![1](https://msdnshared.blob.core.windows.net/media/TNBlogsFS/BlogFileStorage/blogs_msdn/vsto/WindowsLiveWriter/ResigningClickOncemanifests101_AC30/clip_image006_05d1e115-155e-4b0c-8701-ae598a169596.gif)


# Global Assembly Cache (GAC)
![1](http://help.infragistics.com/Help/Doc/ASPNET/2011.2/CLR4.0/html/images/Web_DeploymentGuide_DeploymentUsingtheGAC_02.png)
![1](http://help.infragistics.com/Help/Doc/WinForms/2012.1/CLR2.0/html/images%5CWin_DeploymentGuide_DeploymentUsingtheGAC_01.png)
![1](http://www.onlinebuff.com/artimages/gac6.jpg)

# Assembly Versioning
![1](http://www.codemag.com/Article/Image/0207071/Figure%201.jpg)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC164166.jpeg)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC164166.jpeg)
![1](http://2.bp.blogspot.com/-a8cBxKWXZGs/T3tLZr-pCCI/AAAAAAAANEA/EzehnTb3RgI/s320/assembly+version+1.PNG)
![1](http://3.bp.blogspot.com/-HLTErxY9QOY/T3vfncMxAFI/AAAAAAAANEI/ZE0Ud-XR3yA/s320/assemblyInfo.PNG)
![1](http://1.bp.blogspot.com/-DN_SHjSlod4/T3vg3r8WH9I/AAAAAAAANEQ/_Ui7KaINUc0/s400/Assembly+Version+2.PNG)
![1](http://4.bp.blogspot.com/-CSF4igsTBYs/T3yPki578bI/AAAAAAAANEY/kDOofk6oF-A/s400/AssemblyInfo+2.PNG)
![1](http://image.slidesharecdn.com/assembliesversioningandsigning-110426033320-phpapp01/95/assemblies-versioning-and-signing-7-728.jpg)
![1](http://image.slidesharecdn.com/assembliesversioningandsigning-110426033320-phpapp01/95/assemblies-versioning-and-signing-8-728.jpg)
![1](http://player.slideplayer.com/24/7321493/data/images/img1.jpg)
Read More - [.NET Assembly Version Numbers](http://oncoding.blogspot.com/2012/04/net-assembly-version-numbers.html)


# Satellite Assembly
![1](http://www.lingobit.com/solutions/dotnet/dotnet.png)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC102672.jpeg)
![1](http://www.codeproject.com/KB/cs/352105/UI.jpg)
![1](http://www.codeproject.com/KB/cs/352105/1.jpg)
![1](http://www.codeproject.com/KB/cs/352105/assemblynew.jpg)
![1](http://www.codeproject.com/KB/cs/801343/LanguageFolder.png)

# Strong-Named/Shared Assemblies
![1](http://image.slidesharecdn.com/assembliesversioningandsigning-110426033320-phpapp01/95/assemblies-versioning-and-signing-9-728.jpg)
![1](http://image.slidesharecdn.com/assembliesversioningandsigning-110426033320-phpapp01/95/assemblies-versioning-and-signing-10-728.jpg)
![1](http://image.slidesharecdn.com/assembliesversioningandsigning-110426033320-phpapp01/95/assemblies-versioning-and-signing-11-728.jpg)
![1](http://image.slidesharecdn.com/assembliesversioningandsigning-110426033320-phpapp01/95/assemblies-versioning-and-signing-12-728.jpg)
http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/puranindia/deployment-and-packaging-in-net/Images/Table-26.1.gif

# Assembly Resolution summary
http://www.diranieh.com/NETAssemblies/Figures/LocatingAssemblies.jpg

	
Concerning resolving assemblies, there are a few basic things to consider:
* **Probing** The loader attempts to locate assemblies using a basic directory "probing" technique. This means that it will try to locate "MyAssembly.dll" (for instance) in the application's startup directory, if not there, then in subdirectories below that. If probing fails to locate "MyAssembly.dll", then the AppDomain's AssemblyResolve event is fired.
* **Machine/User/System configuration** The machine.config, user.config and system.config are configuration files stored locally on the system which one can use to change the behavior of the assembly resolver on a "machine", "user" or "system"-wide setting.
* **Publisher Policy** One can use the "<assemblyIdentity>" XML token in your application's configuration file (for instance, "MyApp.exe.config") to point to resolver to a certain version of an assembly or to load an assembly from a different location.
* **Custom resolution** Handle the "AssemblyResolve" event of the AppDomain. This event is raised whenever an assembly could not be resolved via "traditional" methods


# Assemblies: locating, binding and deploying
http://www.codeproject.com/Articles/12215/Assemblies-locating-binding-and-deploying
https://msdn.microsoft.com/en-us/library/yx7xezcf(v=vs.110).aspx

# Stong Name Key
![1](http://al-atari.net/wp-content/uploads/2009/10/3.jpg)

### Strong-name with no-delay sign
![1](http://www.diranieh.com/NETAssemblies/Figures/StrongName_NoDelay.jpg)

### Strong-name with delay sign
![1](http://www.diranieh.com/NETAssemblies/Figures/StrongName_Delay.jpg)

## Loading and Resolving Assemblies
![1](http://www.diranieh.com/NETAssemblies/Figures/AssemblyLoadResolver.jpg)
![1](http://www.diranieh.com/NETAssemblies/Figures/LocatingAssemblies.jpg)

# Side-By-Side Execution
![1](https://i-msdn.sec.s-msft.com/dynimg/IC17891.jpeg)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC123595.jpeg)
![1](http://i.stack.imgur.com/ZFVzN.png)
![1](http://i.stack.imgur.com/ZFVzN.png)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC79106.gif)

## Side-by-side Assembly Sharing
![1](https://i-msdn.sec.s-msft.com/dynimg/IC534359.png)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC534360.png)



# Assembly Locating Binding and Ddeploying
![1](http://www.codeproject.com/KB/install/assemblydeployment/assemblydeployment1.gif)
![1](http://www.codeproject.com/KB/install/assemblydeployment/assemblydeployment2.gif)
![1](http://www.codeproject.com/KB/install/assemblydeployment/assemblydeployment3.gif)

http://www.codeproject.com/Articles/12215/Assemblies-locating-binding-and-deploying

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
![1](http://dailydotnettips.com/wp-content/uploads/2014/01/15-01-2014-04-18-35.jpg)
https://ramanisandeep.wordpress.com/2010/01/20/net-memory-management-garbage-collection-2/
http://www.telerik.com/blogs/understanding-net-garbage-collection
http://www.codeproject.com/Articles/39246/NET-Best-Practice-No-2-Improve-garbage-collector
http://www.csharpque.com/2013/05/understanding-garbage-collection-in-net.html
https://msdn.microsoft.com/en-us/library/ms973837.aspx
http://www.c-sharpcorner.com/uploadfile/riteshratna/garbage-collection-memory-management-in-net/
https://msdn.microsoft.com/en-us/library/ee787088(v=vs.110).aspx



# Code Access Security
![1](https://i-technet.sec.s-msft.com/dynimg/IC25758.gif)
![1](http://www.codeproject.com/KB/aspnet/CASSecurity/1.JPG)
![1](http://www.codeproject.com/KB/aspnet/CASSecurity/2.JPG)
![1](http://www.codeproject.com/KB/aspnet/CASSecurity/3.JPG)
![1](http://www.codeproject.com/KB/aspnet/CASSecurity/7.JPG)
![1](http://www.codeproject.com/KB/aspnet/CASSecurity/9.JPG)
![1](http://www.codeproject.com/KB/aspnet/CASSecurity/10.JPG)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC92522.gif)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC54972.gif)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC3440.jpeg)


# CLR Hosting
![1](http://flylib.com/books/4/331/1/html/2/images/0735619883/graphics/02fig01.jpg)

http://www.codeproject.com/Articles/416471/CLR-Hosting-Customizing-the-CLR

# .NET Framework Tools
* Assembly Generation Utility (al.exe) 
* Assembly Registration Utility (gacutil.exe) 
* MSIL Assembler (ilasm.exe) 
* MSIL Disassembler (ildasm.exe) 
* C++ Compiler (cl.exe) 
* C# Compiler (csc.exe) 
* Visual Basic Compiler (vbc.exe) 
* PE File Format Viewer (dumpbin.exe) 
* Type Library Exporter (tlbexp.exe) 
* Type Library Importer (tlbimp.exe) 
* XML Schema Definition Tool (xsd.exe) 
* Shared Name Utility (sn.exe) 
* Web Service Utility (wsdl.exe) 

* [More Tools](https://msdn.microsoft.com/en-us/library/d9kh6s92(v=vs.110).aspx)



# How the CLR Resolves Type References
![1](https://ekrishnakumar.files.wordpress.com/2006/06/untitled2.JPG?w=595)


# Native Image Generator (Ngen.exe)
![1](https://i0.wp.com/msdn.microsoft.com/msdnmag/issues/05/04/NGen/fig01.gif)
