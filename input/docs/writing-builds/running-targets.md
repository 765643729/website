Order: 30
RedirectFrom: docs/fundamentals/running-targets
---

To run a target, use the `RunTarget` method. The `RunTarget` method should be placed at the end of the script.

```csharp
Task("Default")
    .Does(() =>
{
    Information("Hello World!");
});

RunTarget("Default");
```

# Passing a target to the script

All arguments passed to `Cake.exe` will also be accessible from the Cake script. You can access the arguments by using the [argument DSL](/dsl/#arguments).

```csharp
var target = Argument("target", "Build");

Task("Build")
    .Does(() =>
{
});

Task("Publish")
    .IsDependentOn("Build")
    .Does(() =>
{
});

RunTarget(target);
```

With this Cake script, you can run a specific target by passing the `-Target` argument to `Cake.exe`. Thus, we can run the `"Publish"` target by calling:

```powershell
./build.ps1 -Target Publish
```

The `--exclusive` parameter causes `RunTarget` to run only the specified target and no dependencies. This command runs the Publish target without running the Build target:

```powershell
./build.ps1 --target Publish --exclusive
```
