swift_tip_calculator
====================

<h2>Getting Started</h2>
- Start up Xcode and go to <em>File\New\Project</em>. Select <em>iOS\Application\Single View Application</em>, and click <em>Next</em>.<br />
- Enter TipCalculator for the Product Name, set the Language to Swift, and Devices to iPhone. Make sure Use Core Data is not checked, and click <em>Next.</em><br />
- Choose a directory to save your project, and click <b>Create</b>.<br />
- Let’s see what Xcode has built for you. In the upper left corner of Xcode, select the iPhone 5 Simulator and click Play to test your app.<br />
- You should see a blank white screen appear. Xcode has created a single blank screen in your app <br />

<h2>Creating Your Model</h2>

- First things first – before you create the user interface for your app, you should create your app’s model. A model is a class (or set of classes) that represents your class’s data, and operations that your app will perform on that data.<br />
- Let’s add this class to your project. To do this, go to <em>File\New\File</em> and select <em>iOS\Source\Swift File</em>. Name the file TipCalculatorModel.swift, and click <b>Create</b>.

<h2>Creating your Views</h2>

Let’s build this user interface one piece at a time.<br />
- Navigation bar. Rather than adding a navigation bar directly, select your view controller and go to Editor\Embed In\Navigation Controller. This will set up a Navigation Bar in your view controller. Double click the Navigation Bar (the one inside your view controller), and set the text to Tip Calculator.<br />
- Labels. From the Object Library, drag a Label into your view controller. Double click the label and set its text to Bill Total (Post-Tax):. Select the label, and in the Inspector‘s fifth tab (the Size Inspector), set X=33 and Y=81. Repeat this for another label, but set the text to Tax Percentage (0%):, X=20, and Y=120.<br />
- Text Field. From the Object Library, drag a Text Field into your view controller. In the Attributes Inspector, set Keyboard Type=Decimal Pad. In the Size Inspector, set X=192, Y=72, and Width=268.<br />
- Slider. From the Object Library, drag a Slider into your view controller. In the Attribute Inspector, set Minimum Value=0, Maximum Value=10, and Current Value=6. In the Size Inspector, set X=190, Y=111, and Width=272.<br />
- Button. From the Object Library, drag a Button into your view controller. Double click the Button, and set the text to Calculate. In the Size Inspector, set X=208 and Y=149.<br />
- Text View. From the Object Library, drag a Text View into your View Controller. Double click the Text View, and delete the placeholder text. In the Attributes Inspector, make sure Editable and Selectable are not checked. In the Size Inspector, set X=20, Y=187, Width=440, and Height=288.<br />
- Tap Gesture Recognizer. From the Object Library, drag a Tap Gesture Recognizer onto your main view. This will be used to tell when the user taps the view to dismiss the keyboard.<br />
- Auto Layout. Interface Builder can often do a great job setting up reasonable Auto Layout constraints for you automatically; and it definitely can in this case. To do this, click on the third button in the lower left of the Interface Builder (which looks like a Tie Fighter) and select Add Missing Constraints.<br />

Build and run on iPhone 5 simulator, and you should see a basic user interface working already! <br />

<h2>A View Controller Tour</h2>
- Open ViewController.swift. This is the Swift code for your single view controller (“screen”) in your app. It is responsible for managing the communication between your views and your model.<br />

<code>
import UIKit

class ViewController: UIViewController {<br />
override func viewDidLoad() {<br />
super.viewDidLoad()<br />
// Do any additional setup after loading the view, typically from a nib.<br />
}<br />

override func didReceiveMemoryWarning() {<br />
super.didReceiveMemoryWarning()<br />
// Dispose of any resources that can be recreated.<br />
}<br />
}
</code>

There are some new elements of Swift here that you haven’t learned about yet, so let’s go over them one at a time.<br />

1. iOS is split up into multiple frameworks, each of which contain different sets of code. Before you can use code from a framework in your app, you have to import it like you see here. <b>UIKit</b> is the framework that contains the base class for view controllers, various controls like buttons and text fields, and much more.<br /><br />
2. There is a class that subclasses another class. Here, you are declaring a new class ViewController that subclasses Apple’s UIViewController.<br /><br />
3. This method is called with the root view of this view controller is first accessed. Whenever you override a method in Swift, you need to mark it with the override keyword. This is to help you avoid a situation where you override a method by mistake.<br /><br />
4. This method is called when the device is running low on memory. It’s a good place to clean up any resources you can spare.<br />

<h2>Connecting your View Controller to your Views</h2>
let’s add some properties for its subviews, and hook them up in interface builder. To do this, add these following properties to your <b>ViewController</b> class (right before viewDidLoad):<br />

<code>@IBOutlet var totalTextField : UITextField!</code><br />
<code>@IBOutlet var taxPctSlider : UISlider!</code><br />
<code>@IBOutlet var taxPctLabel : UILabel!</code><br />
<code>@IBOutlet var resultsTextView : UITextView!</code><br />

Here you are declaring four variables just as you learned in the first Swift tutorial – a UITextField, a UISlider, a UILabel, and a UITextView.<br /><br />
There’s only two differences:<br />

1. You’re prefixing these variables with the @IBOutlet keyword. Interface Builder scans your code looking for any properties in your view controller prefixed with this keyword. It exposes any properties it discovers so you can connect them to views.<br />
2. You’re marking the variables with an exclamation mark (!). This indicates the variables are optional values, but they are implicitly unwrapped. This is a fancy way of saying you can write code assuming that they are set, and your app will crash if they are not set.<br />

Let’s try connecting these properties to the user interface elements. <br />
- Open <b>Main.storyboard</b> and select your View Controller in the Document Outline. Open the Connections Inspector (6th tab), and you will see all of the properties you created listed in the Outlets section.<br />
- You’ll notice a small circle to the right of resultsTextView. Control-drag from that button down to the text view below the Calculate button, and release to connect your Swift property to this view.<br />
- Now repeat this for the other three properties, connecting each one to the appropriate UI element.<br />

<h2>Connecting Actions to your View Controller</h2>
Just like you connected views to properties on your view controller, you want to connect certain actions from your views (such as a button click) to methods on your view controller.<br />
To do this, open ViewController.swift and add these three new methods anywhere in your class:<br />

<code>@IBAction func calculateTapped(sender : AnyObject) {
}</code><br />
<code>@IBAction func taxPercentageChanged(sender : AnyObject) {
}</code><br />
<code>@IBAction func viewTapped(sender : AnyObject) {
}</code><br />
- When you declare callbacks for actions from views, they always need to have this same signature – a function with no return value, that takes a single parameter of type AnyObject as a parameter, which represents a class of any type.<br />
- To make Interface Builder notice your new methods, you need to mark these methods with the <b>@IBAction</b> keyword (just as you marked properties with the <b>@IBOutlet</b> keyword).<br />
- Next, switch back to <b>Main.storyboard</b> and make sure that your view controller is selected in the Document Outline. Make sure the Connections Inspector is open (6th tab) and you will see your new methods listed in a the <b>Received Actions</b> section.<br />
- Find the circle to the right of calculateTapped:, and drag a line from that circle up to the Calculate button.<br />
In the popup that appears, choose <b>Touch Up Inside: </b><br />
This is effectively saying “when the user releases their finger from the screen when over the button, call my method <b>calculateTapped:</b>“.<br />
Now repeat this for the other two methods:<br />
- Drag from <b>taxPercentageChanged:</b> to your slider, and connect it to the Value Changed action, which is called every time the user moves the slider.<br />
- Drag from <b>viewTapped: </b>to the <b>Tap Gesture Recognizer</b> in the document outline. There are no actions to choose from for gesture recognizers; your method will simply be called with the recognizer is triggered.<br />

<h2>Connecting Your View Controller to your Model</h2>

- You’re almost done – all you have to do now is hook your view controller to your model.<br />
- Open <b>ViewController.swift</b> and add a property for the model to your class and a method to refresh the UI:<br />
```
let tipCalc = TipCalculatorModel(total: 33.25, taxPct: 0.06)

func refreshUI() {
    totalTextField.text = String(format: "%0.2f", tipCalc.total)
    taxPctSlider.value = Float(tipCalc.taxPct) * 100.0
    taxPctLabel.text = "Tax Percentage (\(Int(taxPctSlider.value))%)"
    resultsTextView.text = ""
}
```

Let’s go over refreshUI one line at a time:<br />
1. In Swift you must be explicit when converting one type to another. Here you convert tipCalc.total from a Double to a String. <br />
2. You want the tax percentage to be displayed as an Integer (i.e. 0%-10%) rather than a decimal (like 0.06). So here you multiply the value by 100.<br />
Note: The cast is necessary because the taxPctSlider.value property is a Float. <br />
3. Here you use string interpolation to update the label based on the tax percentage.<br />
4. You clear the results text view until the user taps the calculate button. <br />
Next, add a call to <b>refreshUI</b> at the bottom of <b>viewDidLoad</b>:
<code>refreshUI()</code><br />
Also implement <b>taxPercentageChanged</b> and <b>viewTapped</b> as follows:<b />
```
@IBAction func taxPercentageChanged(sender : AnyObject) {
    tipCalc.taxPct = Double(taxPctSlider.value) / 100.0
    refreshUI()
}
@IBAction func viewTapped(sender : AnyObject) {
    totalTextField.resignFirstResponder()
}
```
taxPercentageChanged simply reverses the “multiply by 100″ behavior, while viewTapped calls resignFirstResponder on the totalTextField when the view is tapped (which has the effect of dismissing the keyboard).<br />
One method left. Implement calculateTapped as follows:<br />
```
@IBAction func calculateTapped(sender : AnyObject) {
tipCalc.total = Double((totalTextField.text as NSString).doubleValue)
let possibleTips = tipCalc.returnPossibleTips()
var results = ""
for (tipPct, tipValue) in possibleTips {
    results += "\(tipPct)%: \(tipValue)\n"
}
resultsTextView.text = results
```

Let’s go over this line by line:<br />
1. Here you need to convert a String to a Double. This is a bit of a hack to do this; hopefully there will be an easier way in a future update to Swift.<br />
2. Here you call the returnPossibleTips method on your tipCalc model, which returns a dictionary of possible tip percentages mapped to tip values.<br />
3. This is how you enumerate through both keys and values of a dictionary at the same time in Swift. Handy, eh?<br />
4. Here you use string interpolation to build up the string to put in the results text filed. \n is the newline character.<br />
5. Finally you set the results text to the string you have been building.<br />
And that’s it! Build and run, and enjoy your hand-made tip calculator!


