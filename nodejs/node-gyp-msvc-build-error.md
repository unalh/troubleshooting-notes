# Node-gyp MSVC Build Error on Windows

## Problem
When installing a Node.js package with native extensions (e.g., Sharp, sqlite3) via npm, the installation fails with a node-gyp error about missing 'msbuild' or Visual Studio build tools.

## Symptoms
- `npm install` errors with output including `node-gyp rebuild` failure.
- Error messages mention "MSBUILD : error MSB3428: Could not load Visual C++ component 'VCBuild.exe'".
- The installation stops with `gyp ERR!`.

## Investigation
Node-gyp compiles native addons and requires Visual C++ build tools on Windows. I checked:
- Whether Visual Studio Build Tools (e.g., Build Tools for Visual Studio 2022) were installed.
- Running `npm config get msvs_version` to see if a specific VS version was set.
- The environment variable `PATH` included MSBuild paths.

I found no build tools installed.

## Solution
1. Download and install the **Build Tools for Visual Studio** from Microsoft's official site.
2. During installation, select the **Desktop development with C++** workload (which includes the C++ build tools and Windows SDK).
3. After installation, restart the terminal.
4. Set the MSVS version for node-gyp if necessary:
   ```
   npm config set msvs_version 2022
   ```
5. Re-run `npm install`.

After installing the build tools and setting the MSVS version, the package installed successfully.

## What I Learned
Node-gyp requires the correct Visual C++ build environment on Windows. Installing Build Tools for Visual Studio and selecting the C++ workload resolves most native addon build errors.
