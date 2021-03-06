![alt tag](https://github.com/ermalkaleci/CarbonTabSwipeNavigation/blob/master/CarbonKit.jpg)
[![Carthage Compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)

CarbonKit is an open source iOS library that includes powerful and beauty UI components.

CarbonKit includes:
- CarbonSwipeRefresh
- CarbonTabSwipeNavigation

#Installation
CarbonKit is available on CocoaPods. Add to your Podfile:
```ruby
use_frameworks!
pod 'CarbonKit', '~>2.1'
```
and run
```ruby
pod install
```

### Carthage

[Carthage](https://github.com/Carthage/Carthage) is a decentralized dependency manager that builds your dependencies and provides you with binary frameworks.

You can install Carthage with [Homebrew](http://brew.sh/) using the following command:

```bash
$ brew update
$ brew install carthage
```

To integrate CarbonKit into your Xcode project using Carthage, specify it in your `Cartfile`:

```ogdl
github "ermalkaleci/CarbonKit"
```

Run `carthage update` to build the framework and drag the built `CarbonKit.framework` into your Xcode project.


# CarbonSwipeRefresh

![alt tag](https://github.com/ermalkaleci/CarbonTabSwipeNavigation/blob/master/Examples/CarbonSwipeRefresh.gif)

# SAMPLE CODE
```objective-c
#import "CarbonKit.h"

@interface ViewController ()
{
	CarbonSwipeRefresh *refresh;
}
@end

@implementation ViewController
- (void)viewDidLoad {
	[super viewDidLoad];

	refresh = [[CarbonSwipeRefresh alloc] initWithScrollView:self.tableView];
	[refresh setColors:@[
		[UIColor blueColor],
	 	[UIColor redColor],
		[UIColor orangeColor],
		[UIColor greenColor]]
	]; // default tintColor

	// If your ViewController extends to UIViewController
	// else see below
	[self.view addSubview:refresh];

	[refresh addTarget:self action:@selector(refresh:) forControlEvents:UIControlEventValueChanged];
}

- (void)refresh:(id)sender {
	[refresh endRefreshing];
}
@end
```

If you are using UITableViewController you must add the refreshControl into self.view.superview after viewDidAppear
```objective-c
- (void)viewDidAppear:(BOOL)animated {
	[super viewDidAppear:animated];

	if (!refreshControl.superview) {
		[self.view.superview addSubview:refreshControl];
	}
}
```

# CarbonTabSwipeNavigation

![alt tag](https://github.com/ermalkaleci/CarbonTabSwipeNavigation/blob/master/Examples/CarbonTabSwipeNavigation.gif)

# SAMPLE CODE

```objective-c
#import "CarbonKit.h"

@interface ViewController () <CarbonTabSwipeNavigationDelegate>
@end

@implementation ViewController

- (void)viewDidLoad {
	[super viewDidLoad];

	NSArray *items = @[[UIImage imageNamed:@"home"], [UIImage imageNamed:@"hourglass"],
	[UIImage imageNamed:@"premium_badge"], @"Categories", @"Top Free",
	@"Top New Free", @"Top Paid", @"Top New Paid"];

	CarbonTabSwipeNavigation *carbonTabSwipeNavigation =
	[[CarbonTabSwipeNavigation alloc] initWithItems:items delegate:self];
	[carbonTabSwipeNavigation insertIntoRootViewController:self];
	// or [carbonTabSwipeNavigation insertIntoRootViewController:self andTargetView:yourView];
}

// delegate
- (UIViewController *)carbonTabSwipeNavigation:(CarbonTabSwipeNavigation *)carbonTabSwipeNavigation
			 viewControllerAtIndex:(NSUInteger)index {
	// return viewController at index
}

@end
```

Swift Sample
```swift
import CarbonKit

class ViewController: UIViewController, CarbonTabSwipeNavigationDelegate {

    // MARK: Override methods
    override func viewDidLoad() {
        super.viewDidLoad()
        let items = ["Features", "Products", "About"]
        let carbonTabSwipeNavigation = CarbonTabSwipeNavigation(items: items, delegate: self)
        carbonTabSwipeNavigation.insertIntoRootViewController(self)
		// or carbonTabSwipeNavigation.insertIntoRootViewController(self, andTargetView: yourView)
    }

    func carbonTabSwipeNavigation(carbonTabSwipeNavigation: CarbonTabSwipeNavigation, viewControllerAtIndex index: UInt) -> UIViewController {
        // return viewController at index
    }
}
```

# THANKS TO
[Contributors](https://github.com/ermalkaleci/CarbonKit/graphs/contributors)

# LICENSE
[The MIT License (MIT)](https://github.com/ermalkaleci/CarbonKit/blob/master/LICENSE)
