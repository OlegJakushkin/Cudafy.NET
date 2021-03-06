# Cudafy.NET

This is an update of the original Cudafy.NET library hosted on CodePlex to support Mono on macOS and Linux.

## Compiling

The solution was updated to create a single DLL by using ilmerge on the Cudafy.NET project. Compile with VS 2017, target Release/AnyCPU.

## General Tips

After compiling, create a file named Cudafy.NET.dll.config, with the following contents:

```xml
<configuration>
  <dllmap dll="OpenCL" target="/opt/intel/opencl/lib64/libOpenCL.so" os="!windows,osx" />
  <dllmap dll="OpenCL" target="/System/Library/Framework/OpenCL.framework/OpenCL" os="osx" />
</configuration>
```

For OpenCL support on Linux with Intel Processors, install the Intel OpenCL Runtimes: https://software.intel.com/en-us/articles/opencl-drivers#cpu-lin-rh

No further action is required on macOS.

## Remarks

Dynamic launching of gpu functions is not supported on Linux, i.e.

```csharp
gpu.Launch().thekernel();
```

will throw a "Missing Member" exception. Only the Standard Launch will work:

```csharp
gpu.Launch(1,1, “thekernel”);
```

## Screenshots

Cudafy working on [DWSIM](https://github.com/DanWBR/dwsim5 "DWSIM") on macOS and Linux:

![macOS](https://i.snag.gy/BfZETh.jpg "macOS")

![Linux](https://i.snag.gy/v5kUHp.jpg "Linux")


