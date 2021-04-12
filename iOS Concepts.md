Description of ios topics.

**View Controller Life Cycle Methods:**
1. viewDidLoad - This is the first method which is called in the view controller class. This is called only once during the view controllers life time.
2. viewWillAppear - Every time when user is navigating to a screen, just before the screen is displayed this method is called and this is called everytime user is navigated to screen.
3. viewDidAppear - Every time when user is navigating to the screen, after the screen is displayed this method is called and this is called everytime user is navigated to screen.
4. viewWillDisappear - This is method is called everytime just before user is navigating away from current screen to other screen.
5. viewDidDisappear - This method is called everytime just after user is navigating away from current screen to other screen.

**Application States:**
Below are the iOS Application States:
1. Not Running : The app is not running.
2. InActive : The app is in foreground and not receving any events. For ex: Call or SMS.
3. Active : The app is in foreground and receiving events.
4. Background : App is in background and executing code.
5. Suspended : App is in background and not executing any code.

**Dependency Injection :**
It is process where dependency of an object is injected to itself rather making that object to create the dependency itself inorder to avoid the tight coupling.

**iOS Application Life Cycle :**
When user launches the application the UIApplicationObject is first created and view is loaded in the memory. The following methods are called :
appDidFinishLaunch and viewDidLoad for the controller.

UIApplicationObject setup the run loop during the launch. Run loop manages in processing of the events. UIApplicationObject is first object to receive the event.
It delegates the app state events to ApplicationDelegate object and other evtns such as touch event is first submitted to window and it is then passed to the view on which touch has occured.



          

         
