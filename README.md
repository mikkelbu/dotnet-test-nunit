# NUnit 3 Test Runner for .NET Core

## Deprecated

This project is deprecated. The test adapter API changed when .NET Core switched from
`project.json` to the new `csproj` format. For newer .NET Core and .NET Standard
projects, use the [NUnit 3 Visual Studio Test adapter](https://github.com/nunit/nunit3-vs-adapter)
to run tests at the command line using `dotnet test`, in CI or in Visual Studio.

For more information on how to test .NET Core, see the
[.NET Core/.NET Standard documentation](https://github.com/nunit/docs/wiki/.NET-Core-and-.NET-Standard).

If you are reporting **issues**, only report them here if you are using `dotnet-test-nunit` and `project.json`. Otherwise issues should be reported against the [NUnit 3 Visual Studio Test adapter](https://github.com/nunit/nunit3-vs-adapter).


[![Build status](https://ci.appveyor.com/api/projects/status/yg7dawcy1106g1li/branch/master?svg=true)](https://ci.appveyor.com/project/CharliePoole/dotnet-test-nunit/branch/master) [![Travis Build Status](https://travis-ci.org/nunit/dotnet-test-nunit.svg?branch=master)](https://travis-ci.org/nunit/dotnet-test-nunit)

`dotnet-test-nunit` is the unit test runner for .NET Core for running unit tests with NUnit 3.

## Usage

`dotnet-test-nunit` is still an alpha release, so you need to select `show prereleases` if you are using Visual Studio.

Your `project.json` in your test project should look like the following;

### project.json

```json
{
    "version": "1.0.0-*",

    "dependencies": {
        "NUnit": "3.5.0",
        "dotnet-test-nunit": "3.4.0-beta-3"
    },

    "testRunner": "nunit",

    "frameworks": {
        "netcoreapp1.0": {
            "imports": "portable-net45+win8",
            "dependencies": {
                "Microsoft.NETCore.App": {
                    "version": "1.0.0-*",
                    "type": "platform"
                }
            }
        }
    }
}
```

The lines of interest here are the dependency on `dotnet-test-nunit`. I have added `"testRunner": "nunit"` to specify NUnit 3 as the test adapter. I also had to add to the imports for both the test adapter and NUnit to resolve.

You can now run your tests using the Visual Studio Test Explorer, or by running `dotnet test` from the command line.

```sh
# Restore the NuGet packages
dotnet restore

# Run the unit tests in the current directory
dotnet test

# Run the unit tests in a different directory
dotnet test test/NUnitWithDotNetCoreRC2.Test
```

### Notes

Note that the `dotnet` command line swallows blank lines and does not work with color.
The NUnit test runner's output is in color, but you won't see it. These are known issues with
the `dotnet` CLI and not an NUnit bug.
