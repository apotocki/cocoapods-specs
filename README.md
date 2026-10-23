# cocoapods-specs

CocoaPods spec repo for the `*-iosx` pods by [apotocki](https://github.com/apotocki).

[CocoaPods Trunk becomes read-only on December 2, 2026](https://blog.cocoapods.org/CocoaPods-Specs-Repo/)
and accepts no new versions after that. New versions of these pods are published here; all
versions previously published to Trunk are mirrored here as well.

## Pods

| Pod | Library |
| --- | --- |
| [openssl-iosx](https://github.com/apotocki/openssl-iosx) | [OpenSSL](https://github.com/openssl/openssl) |
| [icu4c-iosx](https://github.com/apotocki/icu4c-iosx) | [ICU](https://github.com/unicode-org/icu) |
| [boost-iosx](https://github.com/apotocki/boost-iosx) | [Boost](https://github.com/boostorg/boost) C++ libraries |
| [lzma-iosx](https://github.com/apotocki/lzma-iosx) | liblzma from [XZ Utils](https://github.com/tukaani-project/xz) |
| [lz4-iosx](https://github.com/apotocki/lz4-iosx) | [LZ4](https://github.com/lz4/lz4) |
| [lua-iosx](https://github.com/apotocki/lua-iosx) | [Lua](https://github.com/lua/lua) |
| [libssh2-iosx](https://github.com/apotocki/libssh2-iosx) | [libssh2](https://github.com/libssh2/libssh2) |

Each pod provides XCFrameworks for macOS, iOS, watchOS, tvOS and visionOS, including Mac Catalyst
and the simulators.

**No prebuilt binaries.** The pods are built from the upstream sources on your machine during
`pod install` (by the podspec's `prepare_command`, which runs the pod repository's
`scripts/build.sh`). You can read exactly what is built and how. The first install of a version
takes a while, Boost especially; CocoaPods caches the result.

## Usage

Add this repo as a source of the pod in your `Podfile`:

```ruby
pod 'openssl-iosx', '~> 4.1', :source => 'https://github.com/apotocki/cocoapods-specs.git'
```

`:source` applies only to that pod: CocoaPods looks up its dependencies in the Podfile's global
sources, which is Trunk by default. Of these pods only `libssh2-iosx` has one (`openssl-iosx`,
through the default `libssh2-iosx/OpenSSL` subspec), so give it the same source:

```ruby
pod 'libssh2-iosx', '~> 1.11', :source => 'https://github.com/apotocki/cocoapods-specs.git'
pod 'openssl-iosx', :source => 'https://github.com/apotocki/cocoapods-specs.git'
```

Or declare it as a source for the whole Podfile. Then it must come **before** Trunk: CocoaPods
takes a pod from the first source that has it, so with Trunk listed first you would never see the
versions published here. Declaring any source also disables the implicit Trunk source, so keep
Trunk listed for your other pods:

```ruby
source 'https://github.com/apotocki/cocoapods-specs.git'
source 'https://cdn.cocoapods.org/'

pod 'openssl-iosx', '~> 4.1'
pod 'boost-iosx/json'
```

Updates work as with Trunk: `pod outdated` lists new versions and `pod update` installs them.
This repo is a git source, so a plain `pod install` uses your local copy of it; run
`pod install --repo-update` or `pod update` to fetch new versions.

### Moving from Trunk

Add the source as shown above and run `pod update <pod>` (or `pod install --repo-update`).
Versions already in your `Podfile.lock` are available here too, so nothing else changes.

## Versions

Pod versions follow the upstream version with one extra component for the package revision:
`openssl-iosx 4.1.0.0` is OpenSSL 4.1.0, and `4.1.0.1` is a rebuild of the same OpenSSL release.

## Contents

Specs are added by `pod repo push` when a new version is released; please do not open pull
requests with specs. Report problems with a pod in that pod's repository.
