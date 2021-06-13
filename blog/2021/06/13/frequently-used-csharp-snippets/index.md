---
title: .NET Commands
description: 13.06.2021
---
# Frequently Used C# Snippets
#### Single-File Releases
`dotnet publish -r win-x64 -c Release /p:PublishSingleFile=true`
#### Custom URLs
`sudo dotnet run --urls='http://localhost:80;https://localhost:443'`

#### Runtime Identifiers
| Platform | RID         |
| -------: |:------------|
|  Windows | `win-x64`   |
|    macOS | `osx-x64`   |
|    Linux | `linux-x64` |
#### Build Configurations
|  Release|Debug  |
|--------:|:------|
|`Release`|`Debug`|
#### Preprocessor Directives
```CSharp
#region Private Members
    private string PrivateMemberFunction() => return string.Empty;
#endregion
```
```CSharp
#if DEBUG
    Console.WriteLine("Debug version only");
#endif
#if !DEBUG
    Console.WriteLine("Release version only");
#endif
```
#### Yield Return
```CSharp
using System.Collections.Generic;

static void Main() => Power(2, 8).ForEach(i => Console.Write("{0} ", i);

public static IEnumerable<int> Power(int number, int exponent)
{
    int result = 1;
    for (int i = 0; i < exponent; i++)
    {
        result = result * number;
        yield return result;
    }
}
```
#### Tuples
```CSharp
var t = (Sum: 4.5, Count: 3);

(double Sum, int Count) d = (4.5, 3);

(int min, int max) FindMinMax(int[] input)
{
    if (input is null || input.Length == 0)
        throw new ArgumentException("Cannot find minimum and maximum of a null or empty array.");
    var min = int.MaxValue;
    var max = int.MinValue;
    foreach (var i in input)
    {
        if (i < min)
            min = i;
        if (i > max)
            max = i;
    }
    return (min, max);
}
```
#### Disable Compression (for Blazor WebAssembly)
`dotnet publish -p:BlazorEnableCompression=false`