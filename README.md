![Excellent Webworld Company Logo](https://eww-wp-new.s3.ap-south-1.amazonaws.com/wp-content/uploads/2021/10/21124036/Excellent-Webworld-logo-svg.jpg)

# How to Develop A Foldable Expanding Cardview in iOS Mobile Applications?

The folding animation in iOS pierced its way through mobile app development. It became easy and comfortable for the users to consume information from the screen. It obviously is an easy way to shuffle through a series of digital containers with a few finger taps.

Compatibility is another integral reason foldable card design in iOS became a popular choice in app development. The rectangular aesthetics of cards make the content on screen look super organized.

Two **characteristics** that make foldable layout an integral part of iOS mobile applications are:
* Good design
* Great usability

## Language
Swift

## Use Cases for such a Concept
Booking apps (Rail, Flight, Bus, Movie, Appointment Errands, etc.) and Payment Gateways.

## Requirement
Supported OS 13.0 to 15.0

We bring to you a step-by-step guide to deploy the code stack for Foldable View in iOS mobile apps.
Step

### Step 1 - Creating a File & Getting Started With the Foldable Expanding Cardview in iOS App Development
Take one Tableview and make a TableviewCell file. This will help in displaying the content in a tabular format.

### Step 2 - Write the Basic Animation Code
Now, add the following code in the View Controller TableviewCell file. This will help you in animating the graphics of the folding cell in iOS.

    add configureDefaultState()
    add createAnimationItemView()
    add configureAnimationItems()

**NOTE -** The above functions are for basic animation. There is a code stack for advanced animation later in the steps. 

### Step 3 - Level up Your Animation Game - Advanced Animation Code Stack
This step will improve the animation quality, speed and will help in enhancing the overall UI. Delegate the below two functions in the View Controller TableviewCell file to move the graphics in an ultra-modern and advanced way.

    add createAnimationView()
    add addImageItemsToAnimationView() function

### Step 4 - Logic - Unfolding the Cards To Display More Information
In TableviewCell, add the below function to remove and unfold the image into the original small card format.

    removeImageItemsFromAnimationView() //To remove
    @objc open func unfold(_ value: Bool, animated: Bool = true, completion: (() -> Void)? = nil) {
    if animated {
    value ? openAnimation(completion) : closeAnimation(completion)
    } else {
    foregroundView.alpha = value ? 0 : 1
    containerView.alpha = value ? 1 : 0
    }
    }
    
    @objc open func isAnimating() -> Bool {
    return animationView?.alpha == 1 ? true : false
    }

    animationDuration() //use this method to set the duration of the animation.
    openAnimation() //use this method to open or unfold the cardview with animation.
    closeAnimation() //Use this method to close the cardview with animation.

### Step 5 - Control Folding Animation in iOS - Expression & Behavior Control
This will help you in rotating the cardview’s direction. Create one swift file and all functions of RotatedView. The foldable card UX and UI in iOS apps depends on this step. It can make or break the experience of the user.

    extension RotatedView: CAAnimationDelegate {

    //To rotate angle 
    func rotatedX(_ angle: CGFloat) {
    var allTransofrom = CATransform3DIdentity
    let rotateTransform = CATransform3DMakeRotation(angle, 1, 0, 0)
    allTransofrom = CATransform3DConcat(allTransofrom, rotateTransform)
    allTransofrom = CATransform3DConcat(allTransofrom, transform3d())
    self.layer.transform = allTransofrom
    }
    
    //type of animation transform
    func transform3d() -> CATransform3D {
    var transform = CATransform3DIdentity
    transform.m34 = 2.5 / -2000
    return transform
    }
    
    // folding animation
    
    func foldingAnimation(_ timing: String, from: CGFloat, to: CGFloat, duration: TimeInterval, delay: TimeInterval, hidden: Bool) {
        
    let rotateAnimation = CABasicAnimation(keyPath: Const.transformRotationX)
    rotateAnimation.timingFunction = CAMediaTimingFunction(name: convertToCAMediaTimingFunctionName(timing))
    rotateAnimation.fromValue = from
    rotateAnimation.toValue = to
    rotateAnimation.duration = duration
    rotateAnimation.delegate = self
    rotateAnimation.fillMode = CAMediaTimingFillMode.forwards
    rotateAnimation.isRemovedOnCompletion = false
    rotateAnimation.beginTime = CACurrentMediaTime() + delay
        
    self.hiddenAfterAnimation = hidden
        
    self.layer.add(rotateAnimation, forKey: Const.rotationX)
    }
    
    //for starting animation
    public func animationDidStart(_: CAAnimation) {
    self.layer.shouldRasterize = true
    self.alpha = 1
    }
    
    //for stopping animation
    public func animationDidStop(_: CAAnimation, finished _: Bool) {
    if hiddenAfterAnimation {
    self.alpha = 0
    }
    self.layer.removeAllAnimations()
    self.layer.shouldRasterize = false
    self.rotatedX(CGFloat(0))
    }
    }

### Step 6 - Logic Implementation
Just like scripted below, deploy the following code for the common Tableview method. In the same, add two more methods to fold and unfold cards.

    func tableView(_: UITableView, willDisplay cell: UITableViewCell, for RowAt indexPath: IndexPath) {
    guard case let cell as DemoCell = cell else {
    return
    }
    cell.backgroundColor = .clear
    if cellHeights[indexPath.row] == Const.closeCellHeight {
    cell.unfold(false, animated: false, completion: nil)
    } else {
    cell.unfold(true, animated: false, completion: nil)
    }
    cell.number = indexPath.row
    }

To open another cardview, this method will help you:

    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
    let cell = tableView.cellForRow(at: indexPath) as! TblFoldingCell

    if cell.isAnimating() {
    return
    }

    var duration = 0.0
    let cellIsCollapsed = cellHeights[indexPath.row] == Const.closeCellHeight
    if cellIsCollapsed {
    cellHeights[indexPath.row] = Const.openCellHeight
    cell.unfold(true, animated: true, completion: nil)
    duration = 0.5
    } else {
    cellHeights[indexPath.row] = Const.closeCellHeight
    cell.unfold(false, animated: true, completion: nil)
    duration = 0.8
    }

    UIView.animate(withDuration: duration, delay: 0, options: .curveEaseOut, animations: { () -> Void in
    tableView.beginUpdates()
    tableView.endUpdates()
    if cell.frame.maxY > tableView.frame.maxY {
    tableView.scrollToRow(at: indexPath, at: UITableView.ScrollPosition.bottom, animated: true)
    }
    }, completion: nil)
    }

### Step 7 - Project is Ready!
Everything is set up! You can run the project. Thank You! Hope this will help you!

## Endnote - Concluding Foldable Expanding Cardview in iOS Mobile Apps
We hope the above-mentioned card folding and unfolding code stack helps you to deploy the foldable card concept in your app easily. 

**Credits - Our experienced iOS developer Nishee developed this code.**


## Support
If you have any questions, issues, or propositions, please create a new issue in this repository. Or, place an enquiry for [iPhone application development services](https://www.excellentwebworld.com/iphone-application-development-services/?utm_source=github&utm_campaign=iphone-app-development) and [hire iPhone app developers](https://www.excellentwebworld.com/hire-iphone-app-developers/?utm_source=github&utm_campaign=hire+iphone-developers) from Excellent Webworld. You can also send an email to biz@excellentwebworld.com or fill out the form on the contact page for our business development team to reach you out!
