---
Title: Gyro Documentation
---

# Gyro

Gyro is an unofficial package manager for the Zig programming language. It
improves a developer's life by giving them a package experience similar to
cargo. Dependencies are declared in a `gyro.zzz` file in the root of your
project, and are exposed to you programmatically in the `build.zig` file by
importing `@import("gyro").pkgs`. In short, all that's needed on your part is
how you want to add packages to different objects you're building:

```zig
const Builder = @import("std").build.Builder;
const pkgs = @import("gyro").pkgs;

pub fn build(b: *Builder) void {
    const exe = b.addExecutable("main", "src/main.zig");
    pkgs.addAllTo(exe);
    exe.install();
}
```

To make the job of finding suitable packages to use in your project easier, gyro
is paired with a package index located at [astrolabe.pm](https://astrolabe.pm).
A simple `gyro add mecha` will add the latest version of `mecha` (parser
combinator library) as a dependency. To build your project all that's needed is
`gyro build` and gyro will fetch anything that hasn't been downloaded.

If you want code that's not in the package index don't fret because I have you
covered, if it's in a github repository, then all you have to do is `gyro add
<user>/<repo>`, and if it's located elsewhere gyro supports downloading `tar.gz`
archives over https (see "Types of packages" section for more information).
