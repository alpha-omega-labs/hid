[![Go Reference][docimg]][docurl]
[![AppVeyor][appveyorimg]][appveyorurl]

[appveyorimg]: https://ci.appveyor.com/api/projects/status/plroy54odykb0ch3/branch/master?svg=true
[appveyorurl]: https://ci.appveyor.com/project/dolmen-go/hid
[docimg]:      https://pkg.go.dev/badge/github.com/dolmen-go/hid.svg
[docurl]:      https://pkg.go.dev/github.com/dolmen-go/hid

# Gopher Interface Devices (USB HID)

Note: This package is a fork of [github.com/karalabe/hid](https://github.com/karalabe/hid) as the original author
did not respond to bug fixes and co-maintainership proposals.

The `hid` package is a cross platform library for accessing and communicating with USB Human Interface
Devices (HID).

The package wraps [`hidapi`](https://github.com/libusb/hidapi) for accessing OS specific USB HID APIs
directly instead of using low level USB constructs, which might have permission issues on some platforms.
On Linux the package also wraps [`libusb`](https://github.com/libusb/libusb). Both of these dependencies
are vendored directly into the repository and wrapped using CGO, making the `hid` package self-contained
and go-gettable.

Supported platforms at the moment are Linux, macOS and Windows (exclude constraints are also specified
for Android and iOS to allow smoother vendoring into cross platform projects).

## Cross-compiling

Using `go get` the embedded C library is compiled into the binary format of your host OS. Cross compiling to a different platform or architecture entails disabling CGO by default in Go, causing device enumeration `hid.Enumerate()` to yield no results.

To cross compile a functional version of this library, you'll need to enable CGO during cross compilation via `CGO_ENABLED=1` and you'll need to install and set a cross compilation enabled C toolkit via `CC=your-cross-gcc`.

## Acknowledgements

This package is a fork of [`github.com/karalabe/hid`](https://github.com/karalabe/hid) as the maintainer is
not responding to issues, e-mail or Twitter queries.

Although the `karalabe/hid` package is an implementation from scratch, it was heavily inspired by the existing
[`go.hid`](https://github.com/GeertJohan/go.hid) library, which seems abandoned since 2015; is incompatible
with Go 1.6+; and has various external dependencies. Given its inspirational roots, I thought it important
to give credit to the author of said package too.

Wide character support in the `hid` package is done via the [`gowchar`](https://github.com/orofarne/gowchar)
library, unmaintained since 2013; non buildable with a modern Go release and failing `go vet` checks. As
such, `gowchar` was also vendored in inline (copyright headers and origins preserved).

## License

The components of `hid` are licensed as such:

 * `hidapi` is released under the [3-clause BSD](https://github.com/hidapi/hidapi/blob/master/LICENSE-bsd.txt) license.
 * `libusb` is released under the [GNU LGPL 2.1](https://github.com/libusb/libusb/blob/master/COPYING)license.
 * `go.hid` is released under the [2-clause BSD](https://github.com/GeertJohan/go.hid/blob/master/LICENSE) license.
 * `gowchar` is released under the [3-clause BSD](https://github.com/orofarne/gowchar/blob/master/LICENSE) license.

Given the above, `hid` is licensed under GNU LGPL 2.1 or later on Linux and 3-clause BSD on other platforms.
