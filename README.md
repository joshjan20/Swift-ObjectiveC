# Swift-ObjectiveC
Template to handle both swift and Objective C

Combining both Swift and Objective-C in a single iOS project is quite common when migrating from Objective-C to Swift or when you want to reuse Objective-C code in a new Swift project. Here's a step-by-step guide with a basic example to demonstrate how to create a sample project that uses both Swift and Objective-C.

### Step 1: Create a New iOS Project in Xcode
1. Open Xcode and create a new project.
2. Choose **App** under iOS and click **Next**.
3. Enter a project name (e.g., "MixedLanguageProject").
4. Choose **Swift** as the main language and proceed to create the project.

### Step 2: Add Objective-C Files to the Project
1. Go to **File** > **New** > **File**, select **Cocoa Touch Class**, and click **Next**.
2. Name the class (e.g., `MyObjectiveCClass`) and make sure the language is set to **Objective-C**.
3. Once you create the file, Xcode will ask you if you want to create a **bridging header**. Click **Yes**.

   This bridging header allows you to use Objective-C code in Swift files. Xcode will automatically create a file named `<ProjectName>-Bridging-Header.h`.

### Step 3: Use Objective-C in Swift
Now that you have the bridging header, you can import Objective-C files into your Swift code.

1. Open the newly created bridging header file, which should be named something like `MixedLanguageProject-Bridging-Header.h`.
2. Add the following line to import your Objective-C class:

```objc
#import "MyObjectiveCClass.h"
```

Now, you can use your Objective-C class in any Swift file in your project.

#### Example `MyObjectiveCClass.h` (Objective-C Header File)
```objc
#import <Foundation/Foundation.h>

@interface MyObjectiveCClass : NSObject

- (NSString *)greetWithName:(NSString *)name;

@end
```

#### Example `MyObjectiveCClass.m` (Objective-C Implementation File)
```objc
#import "MyObjectiveCClass.h"

@implementation MyObjectiveCClass

- (NSString *)greetWithName:(NSString *)name {
    return [NSString stringWithFormat:@"Hello, %@! Welcome from Objective-C.", name];
}

@end
```

### Step 4: Using Objective-C Code in Swift
Now let's use this Objective-C class in a Swift file.

1. Open `ViewController.swift` (or any Swift file in your project).
2. Create an instance of `MyObjectiveCClass` and call the method defined in Objective-C.

```swift
import UIKit

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        
        // Using Objective-C code in Swift
        let objCInstance = MyObjectiveCClass()
        let greeting = objCInstance.greet(withName: "John")
        print(greeting)
    }
}
```

### Step 5: Add Swift Files to the Project
If you want to use Swift code in Objective-C files, there are a few additional steps.

1. In the **Build Settings** of your project, search for **Defines Module** and set it to **Yes**.
2. Go to the **Objective-C** file (e.g., `MyObjectiveCClass.m`) and import your Swift code by using the project’s auto-generated module.

For example:
```objc
#import "<ProjectName>-Swift.h"
```

### Step 6: Using Swift Code in Objective-C
You can now use Swift classes in your Objective-C code.

#### Example Swift Class (`MySwiftClass.swift`)
```swift
import Foundation

@objc class MySwiftClass: NSObject {
    
    @objc func greetInSwift(name: String) -> String {
        return "Hello, \(name)! Welcome from Swift."
    }
}
```

#### Using Swift Code in Objective-C (`MyObjectiveCClass.m`)
```objc
#import "MyObjectiveCClass.h"
#import "MixedLanguageProject-Swift.h" // Import Swift class

@implementation MyObjectiveCClass

- (NSString *)greetWithName:(NSString *)name {
    MySwiftClass *swiftInstance = [[MySwiftClass alloc] init];
    return [swiftInstance greetInSwiftWithName:name]; // Call Swift method
}

@end
```

### Step 7: Compile and Run the Project
When you build and run the project, you'll see that both Swift and Objective-C classes work together seamlessly.

---

### Full Project Breakdown
- **Swift File (MySwiftClass.swift)**: Contains a class `MySwiftClass` that can be used in Objective-C.
- **Objective-C File (MyObjectiveCClass.h/m)**: Contains `MyObjectiveCClass`, an Objective-C class used in Swift.
- **Bridging Header (MixedLanguageProject-Bridging-Header.h)**: Connects Objective-C code to Swift.

This is a basic setup, but the concept can be expanded to much larger projects with both Swift and Objective-C code.
