# .NET Framework Basics

* .NET Platform vs .NET framework Vs .NET Environment 
* .NET Framework Architecture
* .NET Framework Components
* CLR Architecture
* CLR Features
* CLR Execution (.NET Execution Model)
* Role of CLR
* Managed/UnManaged Code
* Common Language Infrastructure(CLI)
* Intermediate Language
* Just In Time Compilers (JITers)
* Framework Class Library (FCL)
* Base Class Library (BCL)
* Common Intermediate Language (CIL)
* MSIL (Microsoft Intermediate Language)
* Common Language Specification (CLS)
* Common Type System (CTS)
* Garbage Collector (GC)
* .NET Assemblies
* .NET Assemblies Metadata
* .NET Applications
* Application Domain
* NET Garbage Collection

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

# .NET Platform Standard
![1](http://www.talkingdotnet.com/wp-content/uploads/2016/02/NET-Platform-Standard.png)
![1](http://image.slidesharecdn.com/movingforwardwithasp-160530064824/95/moving-forward-with-aspnet-core-12-638.jpg)



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

# Managed/Unmanaged
![1](http://image.slidesharecdn.com/sharepointunderground-100502110607-phpapp01/95/sharepoint-underground-unmanaged-code-and-sharepoint-internals-7-728.jpg)
![1](http://images.slideplayer.com/25/7612974/slides/slide_17.jpg)
![1](http://image.slidesharecdn.com/sharepointunderground-100502110607-phpapp01/95/sharepoint-underground-unmanaged-code-and-sharepoint-internals-6-728.jpg)
![1](http://www.bass.radio42.com/help/media/PInvoke.bmp)
![1](http://www.jot.fm/issues/issue_2006_11/article1/images/figure3.gif)
![1](http://foxcentral.net/microsoft/NETforVFPDevelopers_Chapter01_files/image003.jpg)
![1](http://www.codemag.com/Article/Image/070013/01fig02.jpg)


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
![1](http://modernpathshala.com/Images/dot-net-interview/Question/1947177520160401113030Base-class-library.JPG)
![1](https://devreminder.files.wordpress.com/2011/03/aspnetbcl.gif)
![1](https://abdelrahmanhosny.files.wordpress.com/2012/07/untitled7.png?w=768)


# Framework Class Library (FCL) - 
* Superset of BCL
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


## URL
http://www.telerik.com/blogs/understanding-net-garbage-collection
http://www.codeproject.com/Articles/39246/NET-Best-Practice-No-2-Improve-garbage-collector
http://www.csharpque.com/2013/05/understanding-garbage-collection-in-net.html
https://msdn.microsoft.com/en-us/library/ms973837.aspx
http://www.c-sharpcorner.com/uploadfile/riteshratna/garbage-collection-memory-management-in-net/
https://msdn.microsoft.com/en-us/library/ee787088(v=vs.110).aspx


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

# Stong Name Key
![1](http://al-atari.net/wp-content/uploads/2009/10/3.jpg)


# Portable executable (PE)
![1](https://srinivasgandu.files.wordpress.com/2011/05/assemblyheader.jpg)
![1](http://etutorials.org/shared/images/tutorials/tutorial_10/nfe3_0202.gif)
![1](http://images.slideplayer.com/16/5175061/slides/slide_28.jpg)


# Global Assembly Cache (GAC)
![1](http://help.infragistics.com/Help/Doc/ASPNET/2011.2/CLR4.0/html/images/Web_DeploymentGuide_DeploymentUsingtheGAC_02.png)
![1](http://help.infragistics.com/Help/Doc/WinForms/2012.1/CLR2.0/html/images%5CWin_DeploymentGuide_DeploymentUsingtheGAC_01.png)
![1](http://www.onlinebuff.com/artimages/gac6.jpg)


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

# Assembly
![1](http://images.slideplayer.com/24/7317073/slides/slide_20.jpg)

# Satellite Assembly
![1](http://www.lingobit.com/solutions/dotnet/dotnet.png)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC102672.jpeg)
![1](http://www.codeproject.com/KB/cs/352105/UI.jpg)
![1](http://www.codeproject.com/KB/cs/352105/1.jpg)
![1](http://www.codeproject.com/KB/cs/352105/assemblynew.jpg)
![1](http://www.codeproject.com/KB/cs/801343/LanguageFolder.png)


# Strong-Named Assemblies

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


# Assembly Versioning
![1](http://www.codemag.com/Article/Image/0207071/Figure%201.jpg)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC164166.jpeg)

# Assembly Locating Binding and Ddeploying
![1](http://www.codeproject.com/KB/install/assemblydeployment/assemblydeployment1.gif)
![1](http://www.codeproject.com/KB/install/assemblydeployment/assemblydeployment2.gif)
![1](http://www.codeproject.com/KB/install/assemblydeployment/assemblydeployment3.gif)

http://www.codeproject.com/Articles/12215/Assemblies-locating-binding-and-deploying

## Side-by-side Assembly Sharing
![1](https://i-msdn.sec.s-msft.com/dynimg/IC534359.png)
![1](https://i-msdn.sec.s-msft.com/dynimg/IC534360.png)

# Manifest
![1](http://2we26u4fam7n16rz3a44uhbe1bq2.wpengine.netdna-cdn.com/wp-content/uploads/071613_1201_NETAssembly3.png)
![1](http://2we26u4fam7n16rz3a44uhbe1bq2.wpengine.netdna-cdn.com/wp-content/uploads/071613_1201_NETAssembly1.png)
![1](http://2we26u4fam7n16rz3a44uhbe1bq2.wpengine.netdna-cdn.com/wp-content/uploads/071613_1201_NETAssembly8.png)
![1](http://2we26u4fam7n16rz3a44uhbe1bq2.wpengine.netdna-cdn.com/wp-content/uploads/071613_1201_NETAssembly10.png)
![1](https://msdnshared.blob.core.windows.net/media/TNBlogsFS/BlogFileStorage/blogs_msdn/vsto/WindowsLiveWriter/ResigningClickOncemanifests101_AC30/clip_image006_05d1e115-155e-4b0c-8701-ae598a169596.gif)

# Managed/Unmanged Code
![1](http://www.codeproject.com/KB/COM/cominterop/RCWCOMInterop.gif)
![1](http://www.codeproject.com/KB/COM/cominterop/ConnectPointDelegates_small.gif)
![1](http://www.codeproject.com/KB/COM/cominterop/CollectionEnumeration.gif)
![1](http://www.codeproject.com/KB/COM/cominterop/CCWInteraction_small.gif)

