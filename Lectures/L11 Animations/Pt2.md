## CIS-444
## Lecture 11: Part 2

In this section, you’ll connect the basic user interface (UI) of the CaptionThat app to code and define some actions a user can perform in that UI.

## Learning Objectives

At the end of the lesson, you’ll be able to:

* (Review) Explain the relationship between a scene in a storyboard and the underlying view controller
* (Review) Create outlet and action connections between UI elements in a storyboard and source code
* Process user input from a text field and display the result in the UI
* Make a class conform to a protocol
* Understand the delegation pattern
* Follow the target-action pattern when designing app architecture

## Connect the UI to Source Code
### This is review from concepts you already know but a more detailed explanation step-by-step guide

Elements in a [storyboard](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW8) are linked to source code. It’s important to understand the relationship that a storyboard has to the code you write.  

In a storyboard, a [scene](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW62) represents one screen of content and typically one view controller. [View controllers](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW7) implement your app’s behavior. A view controller manages a single content view with its hierarchy of subviews. View controllers coordinate the flow of information between the app’s [data model](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW35), which encapsulates the app’s data, and the views that display that data, manage the life cycle of their content views, handle orientation changes when the device is rotated, define the navigation within your app, and implement the behavior to respond to user input. All view controller objects in iOS are of type UIViewController or one of its subclasses.  

You define the behavior of your view controllers in code by creating and implementing custom view controller [subclasses](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW14). You can then create a connection between those classes and scenes in your storyboard to get the behavior you defined in code and the user interface you defined in your storyboard.

In your first coding assignment, you created such classes, `LandingViewController.swift` and `CaptionedViewController.swift`, and connected them to the scenes you’re working on in your storyboard right now. You added these scenes by making the connections yourself in the Identity inspector. The Identity inspector let you edit properties of an object in your storyboard related to that object’s identity, such as what class the object belongs to.

![inline][IDInspector]

[IDInspector]: https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Art/CUIC_inspector_identity_2x.png


At runtime, your storyboard creates an instance of ViewController, your custom view controller subclass. The scene from your storyboard appears on the device’s screen, and the user interface’s behavior is defined in `LandingViewController.swift` and `CaptionedViewController.swift`

As you know, the scene connection is not the only connection that needs to be made. To define interaction in your app, your view controller source code needs to be able to communicate with the views in your storyboard. You do this by defining additional connections—called outlets and actions—between the views in the storyboard and the view controller source code files.

## Create Outlets for UI Elements

[Outlets](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW55) provide a way to reference interface objects—the objects you added to your storyboard—from source code files. To create an outlet, Control-drag from a particular object in your storyboard to a view controller file. This operation creates a [property](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW58) for the object in your view controller file, which lets you access and manipulate that object from code at runtime.

You’ll need to create outlets for the text field and label in your user interface to be able to reference them.

## To connect the text field to the `CaptionedViewController.swift` code

1. Open your storyboard, `Main.storyboard`.

2. Open the [assistant editor](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW76)

![inline][AsstEditor]

[AsstEditor]: https://i.imgur.com/OU2JHXA.png

3. If you want more space to work, collapse the [project navigator](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW57) and [utility area](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW72) by clicking the Navigator and Utilities buttons in the Xcode toolbar.

![inline][CollapseSides]

[CollapseSides]: https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Art/navigator_utilities_toggle_on_2x.png

4. In the outline view, select `CaptionedViewControllerScene`

5. In the editor selector bar, which appears at the top of the assistant editor, change the assistant editor from Preview to Automatic > `CaptionedViewController.swift`

![inline][PreviewCaptioned]

[PreviewCaptioned]: https://i.imgur.com/b0E82lu.png
   
   `CaptionedViewController.swift` displays in the editor on the right.


6. In  `CaptionedViewController.swift`, find the class line, which should look like this:


```swift
   class CaptionedViewController: UIViewController {
```

7. Below the `class` line, add the following:

```swift
   //MARK: Properties
```

   You just added a [comment](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW31) to your source code. Recall that a comment is a piece of text in a source code file that doesn’t get compiled as part of the program but provides context or useful information about individual pieces of code.
A comment that begins with the characters //MARK: is a special type of comment that’s used to organize your code and to help you (and anybody else who reads your code) navigate through it. You’ll see this in action later. Specifically, the comment you added indicates that this is the section of your code that lists properties.

   A comment that begins with the characters `//MARK:` is a special type of comment that’s used to organize your code and to help you (and anybody else who reads your code) navigate through it. You’ll see this in action later. Specifically, the comment you added indicates that this is the section of your code that lists properties.

8. In your storyboard, select the text field.

9. Control-drag from the text field on your canvas to the code display in the editor on the right, stopping the drag at the line below the comment you just added in `CaptionedViewController.swift`.

![inline][TextfieldOutlet]

[TextfieldOutlet]: https://media.giphy.com/media/jtLSkngLhrkOx5vpvA/giphy.gif

10. In the dialog that appears, for Name, type `captionTextField`. Leave the rest of the options as they are.

![inline][CaptionTextField]

[CaptionTextField]: https://i.imgur.com/ee8ke3R.png

11. Click Connect.
   Xcode adds the necessary code to `CaptionedViewController.swift` to store a reference to the text field and configures the storyboard to set up that connection.
   
   ```swift
       @IBOutlet weak var captionTextField: UITextField!
   ```

Take a minute to understand what’s happening in this line of code.

The `IBOutlet` attribute tells Xcode that you can connect to the captionTextField property from Interface Builder (which is why the attribute has the `IB` prefix). The `weak` keyword indicates that the reference does not prevent the system from deallocating the referenced object. Weak references help prevent reference cycles; however, to keep the object alive and in memory you need to make sure some other part of your app has a strong reference to the object. In this case, it’s the text field’s superview. A superview maintains a strong reference to all of its subviews. As long as the superview remains alive and in memory, all of the subviews remain alive as well. Similarly, the view controller has a strong reference to its content view—keeping the entire view hierarchy alive and in memory.  
captionTextField

The rest of the declaration defines an [implicitly unwrapped optional](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW50) variable of type UITextField named `captionTextField`. Pay careful attention to the exclamation point at the end of the type declaration. This exclamation point indicates that the type is an implicitly unwrapped optional, which is an optional type that will always have a value after it is first set. When you access an implicitly unwrapped optional, the system assumes it has a valid value and automatically unwraps it for you. Note that this causes the app to terminate if the variable’s value has not yet been set.

When a view controller is loaded from a storyboard, the system instantiates the view hierarchy and assigns the appropriate values to all the view controller’s outlets. By the time the view controller’s `viewDidLoad()` method is called, the system has assigned valid values to all of the controller’s outlets, and you can safely access their contents.

Now, connect the label to your code in the same way you connected the text field.

## To connect the label to the `CaptionedViewController.swift` code

1. In your storyboard, select the label.
2. Control-drag from the label on your canvas to the code display in the editor on the right, stopping the drag at the line just below your `captionTextField` property in CaptionedViewController.swift.

![inline]{CaptionLabelOutlet]

[CaptionLabelOutlet]: https://i.imgur.com/NGzNIVy.png

3. In the dialog that appears, for Name, type `captionValueLabel`. Leave the rest of the options as they are.

4. Click Connect.

![inline][CaptionLabelOutletResult]

[CaptionLabelOutletResult]: https://i.imgur.com/iKsAfsZ.png

  Again, Xcode adds the necessary code to `CaptionedViewController.swift` to store a reference to the label and configures the storyboard to set up that connection. This outlet is similar to the text field, except for its name and its type (which is `UILabel`, to match the type of object that’s in the storyboard).

```swift
    @IBOutlet weak var captionValueLabel: UILabel!
```

  You only need an outlet to an interface object if you plan to either access a value from the interface object or modify the interface object in your code. In this case, you need to set the text field’s delegate property and set the label’s text property. You won’t be modifying the button, so there’s no reason to create an outlet for it.

  Outlets let you refer to your interface elements in code, but you still need a way to respond whenever the user interacts with the elements. That’s where actions come in.

## Define an Action to Perform

iOS apps are based on [event-driven programming](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW38). That is, the flow of the app is determined by events: system events and user actions. The user performs actions in the interface that trigger events in the app. These events result in the execution of the app’s logic and manipulation of its data. The app’s response to user action is then reflected back in the user interface. Because the user, rather than the developer, is in control of when certain pieces of the app code get executed, you want to identify exactly which actions a user can perform and what happens in response to those actions.

An [action](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW23) (or an action method) is a piece of code that’s linked to an event that can occur in your app. When that event takes place, the system execute’s the action’s code. You can define an action method to accomplish anything from manipulating a piece of data to updating the user interface. You use actions to drive the flow of your app in response to user or system events.

You create an action the same way you create an outlet: Control-drag from a particular object in your storyboard to a view controller file. This operation creates a method in your view controller file that gets triggered when a user interacts with the object that the action method is attached to.

Start by creating a simple action that sets the label to Default Text whenever the user taps the Set Default Text button. (The code to set the label to the text in the text field is a bit more involved, so you’ll write that in the Process User Input section.)


## To create a setDefaultLabelText action in the CaptionedViewController.swift code

1. in `CaptionedViewController.swift`, just above the last curly brace (}), add the following:

```swift
   /// Mark: Actions
```
   This comment indicates that this is the section of your code that lists actions.

2. In your storyboard, select the Set Default Label Text button.
3. Control-drag from the Set Default Label Text button on your canvas to the code display in the editor on the right, stopping the drag at the line below the comment you just added in `CaptionedViewController.swift`.

![inline][AddActionSetDefault]

[AddActionSetDefault]: https://media.giphy.com/media/KAvl4pdWe13DUfYl7E/giphy.gif

4. In the dialog that appears, for Connection select Action.

5. For Name, type `setDefaultLabelText`.

6. For Type, select `UIButton`.

You may have noticed that the value of the Type field defaults to AnyObject. As discussed in previous lectures, In Swift, `AnyObject` is a type used to describe an object that can belong to any class. Specifying the type of this action method to be `UIButton` means that only button objects can connect to this action. Although this isn’t significant for the action you’re creating right now, it’s important to remember for later.

Leave the rest of the options as they are.

![inline][AddActionDetails]

[AddActionDetails]: https://i.imgur.com/PqWoyeN.png


7. Click Connect
   Xcode adds the necessary code to `CaptionedViewController.swift` to set up the action method.
   
   ```swift
   @IBAction func setDefaultLabelText(_ sender: UIButton) {
    }
```

8. The `sender` parameter refers to the object that was responsible for triggering the action—in this case, a button. The `IBAction` attribute indicates that the method is an action that you can connect to from your storyboard in Interface Builder. The rest of the declaration declares a method by the name of `setDefaultLabelText(_:)`.

Right now, the method declaration is empty. The code to reset the value of the label is quite simple.

## To implement the label reset action in the ViewController code


