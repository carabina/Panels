# Panels

[![Carthage compatible](https://img.shields.io/badge/Carthage-Compatible-brightgreen.svg?style=flat)](https://github.com/Carthage/Carthage)
[![Platform](http://img.shields.io/badge/platform-ios-blue.svg?style=flat
)](https://developer.apple.com/iphone/index.action)
[![Language](http://img.shields.io/badge/language-swift-brightgreen.svg?style=flat
)](https://developer.apple.com/swift)
[![Twitter](https://img.shields.io/badge/twitter-@acaserop-blue.svg?style=flat)](http://twitter.com/acaserop)


Panels is a framework to easily add sliding panels to your application.
It takes care the safe area in new devices and moving your panel when keyboard
is presented/dismissed.

Updated to Swift 4.2

<p float="center">
    <img src="Resources/Demo1.gif" width="237" height="471" alt="Sliding Panel demo1">
    <img src="Resources/Demo2.gif" width="237" height="471" alt="Sliding Panel demo2">
</p>

## Usage

First create your own panel, you can use Interface Builder (freeform viewcontroller),
Make sure that you conform the protocol `Panelable`

```swift
import UIKit
import Panels

class PanelOptions: UIViewController, Panelable {
    @IBOutlet var headerHeight: NSLayoutConstraint!
    @IBOutlet var headerPanel: UIView!
}
```
This protocol defines the interface needed to be able to adjust the sliding panel
to the container, expanding and collapsing. It will take care of the safe area


Then in your main viewcontroller, where the panel is presented:

```swift
class YourViewController: UIViewController
    let panelManager = Panels()

    override func viewDidLoad() {
        super.viewDidLoad()
        var panelConfiguration = PanelConfiguration(storyboardName: "PanelOptions")
        panelConfiguration.panelSize = .oneThird
        panelManager.addPanel(with: panelConfiguration, target: self)
    }
}
```

If you want to get notifications when the panel is presented, collapsed or
expanded, just conform the protocol `PanelNotifications`

You can find extra options in the PanelConfiguration object:

```swift
    /// Storyboard name, the first viewcontroller will be instanciated
    public var panelName: String

    /// Panel height
    public var panelSize: PanelDimensions

    /// Panel margens between the header and the next views.
    public var panelMargen: CGFloat

    /// Visible area when the panel is collapsed
    public var panelVisibleArea: CGFloat

    /// Safe area is avoided if this flag is true.
    public var useSafeArea = true

    /// Collapse and expand when tapping the header view.
    public var respondToTap = true

    /// Collapse and expand when dragging the header view.
    public var respondToDrag = true

    /// Collapse when tapping outside the panel
    public var closeOutsideTap = true

    /// Animate the panel when the superview is shown.
    public var animateEntry = false

    /// If parent view is a navigationcontroller child, this flag allow a better calculation when the panelSize is .fullScreen
    public var enclosedNavigationBar = true
```


## Installation

### CocoaPods

Add the line `pod "Panels"` to your `Podfile`

### Carthage
Add the line `github "antoniocasero/Panels"` to your `Cartfile`

## Author

Project created by Antonio Casero ([@acaserop](https://twitter.com/acaserop) on Twitter).