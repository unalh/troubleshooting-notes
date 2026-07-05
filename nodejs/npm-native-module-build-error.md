# NPM Native Module Build Error

## Problem
During `npm install`, packages with native C++ bindings (e.g., bcrypt, node-sass) fail to build with errors related to Python or C++ compilation.

## Symptoms
- `node-gyp` errors complaining about missing Python or can't find `python2`.
- Errors such as `gyp ERR! find Python` or `TypeError: Cannot read property 'split' of null`.
- Build fails and package installation aborts.

## Investigation
Many Node.js native modules rely on Python 3 and a C++ compiler to build from source. I checked:
- That Python was installed (`python --version`) and available in PATH.
- The npm configuration `python` path (`npm config get python`).
- Node-gyp and npm versions.
- Whether prebuilt binaries existed for the package.

I found Python not installed, so node-gyp could not find a valid Python executable.

## Solution
1. Install Python 3 from python.org and ensure the option to "Add Python to PATH" is selected.
2. Verify Python installation and path:
   ```
   python --version
   ```
3. Configure npm to use this Python:
   ```
   npm config set python python3
   ```
4. Update npm and node-gyp to the latest versions:
   ```
   npm install -g npm
   npm install -g node-gyp
   ```
5. Re-run `npm install`.

After installing Python and setting npm to use it, the module built successfully.

## What I Learned
Native modules require a proper build environment on Windows, including Python and C++ compilers. Setting up these dependencies once saves time across multiple projects.
