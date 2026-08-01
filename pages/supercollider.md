# SuperCollider

## How to configure SuperCollider to ease plugin installs

1. Install [Plugins.quark](https://github.com/madskjeldgaard/plugins.quark) in SuperCollider
   `Quarks.install("https://github.com/madskjeldgaard/plugins.quark")`
1. Install `cmake` with Homebrew (other package managers may work too).
1. Add Homebrew `bin` to SuperCollider's `PATH` in SuperCollider:
    ```scd
    {
        var path = getenv("PATH");
        if(path.isEmpty.not) { path = path ++ ":"; };
        setenv("PATH", path ++ "/opt/homebrew/bin"); // Adjust the path as necessary
    }.value
    ```
    Verify if you please: `getenv("PATH").postln`
1. Print SuperCollider's extension path: `Platform.userExtensionDir`
