# iOSLearning
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


          
          

         
