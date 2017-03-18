# Introduction

Guetzling is a simple script for macOS and Linux written in Bash, to automate (recursively finding files) the compression of jpegs using the Guetzli algorithm.

## Install
1. Install Guetzli, and copy it to an executable folder (`/usr/bin` for example), if it's not already there.
2. Copy Guetzling, copy it to `/usr/bin` or something like that.

## Usage
1. Simply `cd` to the parent directory of your choice, and `guetzling`. ***Voilà!***


[Guetzli](https://github.com/google/guetzli) is a JPEG encoder that aims for excellent compression density at high
visual quality. Guetzli-generated images are typically 20-30% smaller than
images of equivalent quality generated by libjpeg. Guetzli generates only
sequential (nonprogressive) JPEGs due to faster decompression speeds they offer.

# Building

## On POSIX systems

1.  Get a copy of the source code, either by cloning this repository, or by
    downloading an
    [archive](https://github.com/google/guetzli/archive/master.zip) and
    unpacking it.
2.  Install [libpng](http://www.libpng.org/pub/png/libpng.html) and
    [gflags](https://github.com/gflags/gflags). If using your operating system
    package manager, install development versions of the packages if the
    distinction exists.
    *   On Ubuntu, do `apt-get install libpng-dev libgflags-dev`.
    *   On Arch Linux, do `pacman -S libpng gflags`.
3.  Run `make` and expect the binary to be created in `bin/Release/guetzli`.

## On Windows

1.  Get a copy of the source code, either by cloning this repository, or by
    downloading an
    [archive](https://github.com/google/guetzli/archive/master.zip) and
    unpacking it.
2.  Install [Visual Studio 2015](https://www.visualstudio.com) and
    [vcpkg](https://github.com/Microsoft/vcpkg)
3.  Install `libpng` and `gflags` using vcpkg: `.\vcpkg install libpng gflags`.
4.  Cause the installed packages to be available system-wide: `.\vcpkg integrate
    install`. If you prefer not to do this, refer to [vcpkg's
    documentation](https://github.com/Microsoft/vcpkg/blob/master/docs/EXAMPLES.md#example-1-2).
5.  Open the Visual Studio project enclosed in the repository and build it.

## On macOS

To install using [Homebrew](https://brew.sh/):
1. Install [Homebrew](https://brew.sh/)
2. `brew install guetzli`

To install using the repository:
1.  Get a copy of the source code, either by cloning this repository, or by
    downloading an
    [archive](https://github.com/google/guetzli/archive/master.zip) and
    unpacking it.
2.  Install [Homebrew](https://brew.sh/) or [MacPorts](https://www.macports.org/)
3.  Install `libpng` and `gflags`
    *   Using [Homebrew](https://brew.sh/): `brew install libpng gflags`.
    *   Using [MacPorts](https://www.macports.org/): `port install libpng gflags` (You may need to use `sudo`).
4.  Run the following command to build the binary in `bin/Release/guetzli`.
    *   If you installed using [Homebrew](https://brew.sh/) simply use `make`
    *   If you installed using [MacPorts](https://www.macports.org/) use `CFLAGS='-I/opt/local/include' LDFLAGS='-L/opt/local/lib' make`

## With Bazel

There's also a [Bazel](https://bazel.build) build configuration provided. If you
have Bazel installed, you can also compile Guetzli by running `bazel build -c opt //:guetzli`.

# Using

**Note:** Guetzli uses a large amount of memory. You should provide 300MB of
memory per 1MPix of the input image.

To try out Guetzli you need to [build](#building) or
[download](https://github.com/google/guetzli/releases) the Guetzli binary. The
binary reads a PNG or JPEG image and creates an optimized JPEG image:

```bash
guetzli [--quality Q] [--verbose] original.png output.jpg
guetzli [--quality Q] [--verbose] original.jpg output.jpg
```

Note that Guetzli is designed to work on high quality images (e.g. that haven't
been already compressed with other JPEG encoders). While it will work on other
images too, results will be poorer. You can try compressing an enclosed [sample
high quality
image](https://github.com/google/guetzli/releases/download/v0/bees.png).

You can pass a `--quality Q` parameter to set quality in units equivalent to
libjpeg quality. You can also pass a `--verbose` flag to see a trace of encoding
attempts made.

Please note that JPEG images do not support alpha channel (transparency). If the
input is a PNG with an alpha channel, it will be overlaid on black background
before encoding.
