# Building WolvenKit with Visual Studio

## **Install .NET 6**

[https://dotnet.microsoft.com/download/dotnet/6.0](https://dotnet.microsoft.com/en-us/download/dotnet/6.0)

## **Install the latest Visual Studio release**

[https://visualstudio.microsoft.com/downloads/](https://visualstudio.microsoft.com/downloads/)

## **Required files**

1. All the required files are either NuGet packages, which will automatically be downloaded on pressing `Build`, or readily included in the package in the [Libs directory](https://github.com/WolvenKit/WolvenKit/blob/463-Import-Export-Tool/Libs).
2. If, for some reason, the LFS quota is depleted, the renderer prerequisite libs can be acquired here: [https://outwa.it/lib.zip](https://outwa.it/lib.zip)

## **Build and Run**

1. Open WolvenKit.sln
2. Build WolvenKit.sln on Debug or Release doesn't matter.
3. Run `WolvenKit.exe` (in `WolvenKit\bin\<Debug|Release>\net5.0-windows\win-x64\`).
