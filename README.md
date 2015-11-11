# BITalino .NET API
  
The BITalino .NET API is a .NET class library which enables Windows .NET applications to communicate
with a BITalino device through a simple interface. The class library is composed of an assembly file ([BITalino_x86.dll](BITalino_x86.dll) for 32-bit systems or [BITalino_x64.dll](BITalino_x64.dll) for 64-bit systems).

An XML documentation file is also provided for each of the assembly versions. This file can be used by Visual Studio's IntelliSense and Object Browser to provide the library reference documentation.

The .NET API is a wrapper built on top of the [BITalino C++ API](../../../cpp-api). The wrapper code was written in C++/CLI and it is also provided ([dotNet_wrapper.cpp](dotNet_wrapper.cpp)) in case you want to build the .NET assembly yourself.

The provided assembly was built for .NET Framework 4.5 on Windows Vista or later. If you need an assembly for Windows XP or for a different version of the .NET Framework, you can build it from the [C++ API](../../../cpp-api) and wrapper source codes following the instructions below.

A sample test application in C# ([test.cs](test.cs)) is also provided.
  
There are three ways to connect to a BITalino device:
- direct Bluetooth connection using the device Bluetooth MAC address;
- indirect Bluetooth connection using a virtual serial port;
- wired UART connection using a serial port.
  
The API exposes a single class (Bitalino). Each instance of this class represents a connection to a BITalino device. The connection is established in the constructor and released while calling the Dispose() method or in the destructor/finalizer. An application can create several instances (to distinct devices). The library is thread-safe between distinct instances.

The API was tested in Windows 7 (32-bit and 64-bit).
    
## About the sample application
  
The sample application ([test.cs](test.cs)) creates an instance to a BITalino device. Then it starts acquiring all channels on the device at 1000 Hz and enters a loop while dumping one frame out of 100 and toggling the device green LED. Pressing the Enter key exits the loop, destroys the instance and closes the application.
  
One of the provided constructor calls must be used to connect to the device. The string passed to the constructor can be a Bluetooth MAC address (you must change the one provided) or a serial port.
  
## Compiling the sample application

To compile the sample application:
- create a C# Empty Project in Visual Studio;
- copy [test.cs](test.cs) and [BITalino_x86.dll](BITalino_x86.dll) or [BITalino_x64.dll](BITalino_x64.dll) to the project directory;
- add test.cs to the project;
- edit test.cs as described in previous section to assign the appropriate constructor string parameter;
- add a reference to BITalino_x86.dll or BITalino_x64.dll in the “References” folder;
- build the solution and run the application.

## Compiling the class library

You can compile the class library if you don't want to use the pre-built assemblies or if you need to build an assembly for Windows XP or for a different version of the .NET Framework. You will need [bitalino.cpp](../../../cpp-api/tree/master/bitalino.cpp) and [bitalino.h](../../../cpp-api/tree/master/bitalino.h) from the [C++ API](../../../cpp-api).

To compile the class library:
- create a CLR Class Library project in Visual Studio;
- remove from project all files added automatically to the project;
- disable Precompiled Headers in Project Properties → Configuration Properties → C/C++ → Precompiled Headers → Precompiled Header: Not Using Precompiled Headers
- copy [bitalino.cpp](../../../cpp-api/tree/master/bitalino.cpp), [bitalino.h](../../../cpp-api/tree/master/bitalino.h) and [dotNet_wrapper.cpp](dotNet_wrapper.cpp) to the project directory;
- add bitalino.cpp and dotNet_wrapper.cpp files to the project at the “Source Files” folder;
- add a reference to `ws2_32.lib` in Project Properties → Configuration Properties → Linker → Input → Additional Dependencies;
- build the solution.
