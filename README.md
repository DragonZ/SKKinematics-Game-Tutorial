Sprite Kit and Inverse Kinematics with Swift
Step by Step coding with my own comments for this tutorial
	- https://www.raywenderlich.com/80917/sprite-kit-inverse-kinematics-swift
Great tutorial to help me learn Inverse Kinematics and understand Sprite Kit.
However, there are issues due to fast updating Swift and Xcode ... =\
Here is my notes while learning. Hope it can help other who want to read this tutorial =]
My environment:
	- Xcode 7.3
	- Swift 2.2
	- Simulator: iPhone 6s & iPhone 6s plus 

Tutorial Fix 
* Screen size is designed for iPhone 5s, there are black gap on 6/6 plus and above 
* Swift 2.2 updates, remove hash tag (#)
	- change made in CGFloat+Extensions.swift: func random
* New auto-generated GameViewController (in my opinion, API change)
	- create a new iOS game project, use the new auto-generated code to replace old one in the starting project 
* New API method, touchesBegan
	- use override func touchesBegan(touches: Set<UITouch>, withEvent event: UIEvent?)
* IK Constraints Min and Max Angle properties doesn't work on the scene editor for Xcode 7.3
	- workaround to programmatically create a zRotation constraint: 
	let range = SKRange(lowerLimit: CGFloat(0).degreesToRadians(),
            upperLimit: CGFloat(160).degreesToRadians())
	let rotationConstraint = SKConstraint.zRotation(range)
	lowerArmFront.constraints = [rotationConstraint]
* intersectsNode not working issue, more discussion on stack overflow, here is one possible solution
	- let effectorInNode = self.convertPoint(effectorNode.position, fromNode:effectorNode.parent!) 
	var shurikenFrame = node.frame 
	shurikenFrame.origin = self.convertPoint(shurikenFrame.origin, fromNode: node.parent!) 
	if shurikenFrame.contains(effectorInNode) { ...
	<=replace=>
	if node.intersectsNode(effectorNode) { ...
* GameOverScene some swift language update issues, including optional variables, as type cast. follow the Xcode hint to fix
* AVAudioPlayer in Swift is different from it in Objective-C! It throws exception not with return error parameter
	- use simple try catch
	do {
        audioPlayer = try AVAudioPlayer(contentsOfURL: NSURL(fileURLWithPath: path), fileTypeHint: "mp3")
    } catch {
    	...
    }