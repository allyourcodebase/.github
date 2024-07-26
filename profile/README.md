## All Your Codebase
...are belong to Ziguanas, but we'd also be delighted to give them back!

## What is this organization?
We package C/C++ projects for the Zig build system so that you can reliably 
compile (and cross-compile!) them with ease.

This both provides convenience for users of the Zig compier toolchain and 
also showcases to C/C++ project maintainers what a `build.zig` file for 
their project looks like.

## I maintain one of the projects you packaged, what value does your work provide?
As a general answer, we add a dependency on Zig to your project but in exchange we remove a dependency on:
- ***Make / GNUMake / CMake / autoconf / bash scripts / batch scripts / powershell scripts***: Zig is a complete build system that works on all supported platforms and can do **everything** those other tools do.
- ***Clang***: Zig is a full compiler toolchain and happens to also bundle all of `clang`.
- ***The system package manager***: Zig is also a package manager and can download and build dependences packaged for it, if you want it to.
- ***Docker / CI matrix jobs***: Zig can cross-compile C/C++/Zig code, making a release is as simple as running [`zig build release`](https://github.com/kristoff-it/superhtml/blob/ca52633557bf07ce5ab228e99b543756d7905446/build.zig#L213-L261).
 
More in general Zig removes all dependency on system-wide settings, while still leaving you the ability to opt-in when you need to.
  
## I maintain one of the projects you packaged and I like your work, how can I upstream it?

**If you're the maintainer of a project packaged by us and decide that you
want to upgrade your build pipeline, then you are free to upstream everything 
you need from our repos.**

If you decide to do so, please let us know by opening an Issue so that we can 
archive our repo and point people to your upstream. Feel also free to use our repos' Issues 
section to ask questions about how to integrate everything correctly in your project 
(say, because we didn't implement a secondary build step for example).

One last thing to note: for us to be able to archive our repository, your integration 
of our `build.zig` must not add more sytem dependencies than our version. So, for example, 
if our packaged version is able to depend on zstd via [allyourcodebase/zstd](https://github.com/allyourcodebase/zstd),
then we kindly ask you either keep depending on it (until its `build.zig` gets upstreamed)
or that you at least expose a flag to allow us to continue to do so.

Tha said, you're obviously welcome to upstream any build code as you see fit even if 
you don't plan to keep depending on other packages via the Zig build system. We'll still be happy
to help you in this case, of course, but we'll also keep maintaining our downstream fork.

## How does a C/C++ project packaged for the Zig build system by you look like?
We use two main strategies:

1. Add the upstream project as a dependency (in `build.zig.zon`) and define the corresponding `build.zig` script in our repo.
2. Fork the upstream project (optionally remove other -- now useless :^) -- build scripts), add Zig build scripts to it and apply any necessary patch to the original project. This last part is usually not necessary but some build steps might benefit by making some config scripts and such more amenable to be used by the Zig build system. One example of that would be to have scripts accept an output path as an argument instead of hardcoding where their output goes (this is very useful to integrate properly with Zig build cache).

If you're a maintainer of the upstream project, (1) shows clearly that you will only need two files (`build.zig`, `build.zig.zon`) but it will up to you to clean up all other build scripts and possibly improve the build script as described above, while (2) will require you to be a bit more careful when upstreaming the work but everything will have been done for you more thoroughly.

## I want to contribute a repository, how can I do it?

Ping [kristoff](https://github.com/kristoff-it) and ask to be added to the organization.

Here are some ground rules to be able to contribute a repo:

1. The license must be at least as permissive as the original project (to make things simple you can just use MIT and will never be wrong).
2. The repo should pakage the original C/C++ project without adding extra Zig-specific stuff like bindings, for example.  
You are welcome to put bindings in a separate repo owned directly by you.
3. You must target the latest tagged version of Zig.
4. You have interest in doing occasional maintainership work to update your build script when a new version of the upstream project is released.

