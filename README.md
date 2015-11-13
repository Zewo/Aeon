Aeon
====

[![Swift 2.1](https://img.shields.io/badge/Swift-2.1-orange.svg?style=flat)](https://developer.apple.com/swift/)
[![Platforms OS X | iOS](https://img.shields.io/badge/Platforms-OS%20X%20%7C%20iOS-lightgray.svg?style=flat)](https://developer.apple.com/swift/)
[![Cocoapods Compatible](https://img.shields.io/badge/Cocoapods-Compatible-4BC51D.svg?style=flat)](https://cocoapods.org/pods/Aeon)
[![Carthage Compatible](https://img.shields.io/badge/Carthage-Compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![License MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat)](https://github.com/Carthage/Carthage)

**Aeon** is a GCD based HTTP server for **Swift 2**.

## Features

- [x] No `Foundation` dependency (**Linux ready**)
- [x] Completely Asynchronous

## Dependencies

**Aeon** is made of:

- [Currents](https://github.com/Zewo/Currents) - TCP/IP
- [Luminescence](https://github.com/Zewo/Luminescence) - HTTP parser
- [Kalopsia](https://github.com/Zewo/Kalopsia) - GCD wrapper

## Usage

```swift
struct HTTPServerResponder : HTTPResponder {
    func respond(request: HTTPRequest, completion: HTTPResponse -> Void) {
        
        // do something based on the HTTPRequest
        
        completion(
            HTTPResponse(
                statusCode: 200,
                reasonPhrase: "OK",
                majorVersion: 1,
                minorVersion: 1,
                headers: [:],
                body: []
            )
        )
    }
}

let responder = HTTPServerResponder()
let server = HTTPServer(port: 8080, responder: responder)
server.start()
```

## Performance

Start *Aeon Command Line Application* and then run:

```bash
> ab -n 12800 -c 128 http://localhost:8080/   
```

Results in a Macbook Pro early 2013:

```
Concurrency Level:      128
Time taken for tests:   4.223 seconds
Complete requests:      12800
Failed requests:        0
Total transferred:      243200 bytes
HTML transferred:       0 bytes
Requests per second:    3031.00 [#/sec] (mean)
Time per request:       42.230 [ms] (mean)
Time per request:       0.330 [ms] (mean, across all concurrent requests)
Transfer rate:          56.24 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        2   21  14.3     20     189
Processing:     5   21  14.1     21     189
Waiting:        3   20  14.5     20     189
Total:         10   42  22.6     42     210

Percentage of the requests served within a certain time (ms)
  50%     42
  66%     50
  75%     54
  80%     58
  90%     61
  95%     63
  98%     64
  99%    203
 100%    210 (longest request)
```

To make this results have any meaning you should create, for example, a node.js server that responds with 200 OK and compare it with **Aeon**.

## Installation

### CocoaPods

[CocoaPods](http://cocoapods.org) is a dependency manager for Cocoa projects. You can install it with the following command:

```bash
$ gem install cocoapods
```

> CocoaPods 0.39.0+ is required to build Aeon.

To integrate Aeon into your Xcode project using CocoaPods, specify it in your `Podfile`:

```ruby
source 'https://github.com/CocoaPods/Specs.git'
use_frameworks!

pod 'Aeon'
```

Then, run the following command:

```bash
$ pod install
```

### Carthage

[Carthage](https://github.com/Carthage/Carthage) is a decentralized dependency manager that automates the process of adding frameworks to your Cocoa application.

You can install Carthage with [Homebrew](http://brew.sh/) using the following command:

```bash
$ brew update
$ brew install carthage
```

To integrate **Aeon** into your Xcode project using Carthage, specify it in your `Cartfile`:

```ogdl
github "Zewo/Aeon"
```

### Manually

If you prefer not to use a dependency manager, you can integrate **Aeon** into your project manually.

#### Embedded Framework

- Open up Terminal, `cd` into your top-level project directory, and run the following command "if" your project is not initialized as a git repository:

```bash
$ git init
```

- Add **Aeon** as a git [submodule](http://git-scm.com/docs/git-submodule) by running the following command:

```bash
$ git submodule add https://github.com/Zewo/Aeon.git
```

- Open the new `Aeon` folder, and drag the `Aeon.xcodeproj` into the Project Navigator of your application's Xcode project.

    > It should appear nested underneath your application's blue project icon. Whether it is above or below all the other Xcode groups does not matter.

- Select the `Aeon.xcodeproj` in the Project Navigator and verify the deployment target matches that of your application target.
- Next, select your application project in the Project Navigator (blue project icon) to navigate to the target configuration window and select the application target under the "Targets" heading in the sidebar.
- In the tab bar at the top of that window, open the "General" panel.
- Click on the `+` button under the "Embedded Binaries" section.
- You will see two different `Aeon.xcodeproj` folders each with two different versions of the `Aeon.framework` nested inside a `Products` folder.

    > It does not matter which `Products` folder you choose from, but it does matter whether you choose the top or bottom `Aeon.framework`.

- Select the top `Aeon.framework` for OS X and the bottom one for iOS.

    > You can verify which one you selected by inspecting the build log for your project. The build target for `Aeon` will be listed as either `Aeon iOS` or `Aeon OSX`.

- And that's it!

> The `Aeon.framework` is automagically added as a target dependency, linked framework and embedded framework in a copy files build phase which is all you need to build on the simulator and a device.

License
-------

**Aeon** is released under the MIT license. See LICENSE for details.
