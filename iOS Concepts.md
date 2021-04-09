Description of ios topics.

iOS Application Life Cycle :

1. Initially when user taps on the application icon.
2. Application is lauched.
3. main function is called(First method that is invoked).
4. It invokes UIApplicationMain function. It performs the following things :
          4.1 Creates the UIApplication object(It is basically instance of the app)
          4.2 Loads the view in the memory.
5. Following methods are invoked in the order :
          5.1 main function
          5.2 didFinishLaunch
          5.3 viewDidLoad
          5.4 viewDidAppear
          
UIApplication object sets up the run loop, which handles the user events. UIApplication object delegates app state events to AppDelegate object.

When any event is occured it is added in event queue. Then sequentially it is passed to the run loop. UIApplicatiomn object decides to delegate the event to respective core object. 

**View Controller Life Cycle Methods:**
1. viewDidLoad - This is the first method which is called in the view controller class. This is called only once during the view controllers life time.
2. viewWillAppear - Every time when user is navigating to a screen, just before the screen is displayed this method is called and this is called everytime user is navigated to screen.
3. viewDidAppear - Every time when user is navigating to the screen, after the screen is displayed this method is called and this is called everytime user is navigated to screen.
4. viewWillDisappear - This is method is called everytime just before user is navigating away from current screen to other screen.
5. viewDidDisappear - This method is called everytime just after user is navigating away from current screen to other screen.




          

         
