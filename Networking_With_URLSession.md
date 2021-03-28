
URLSession provides the way for the iOS apps to communicate with server. 
Concurrency : Its a process of executing non ui work in seperate threads to make app more responsive. In iOS concurrency is achieved using GCD or Operation Queue.

URLSession is a set of related tasks. We can make all tasks run in the background or make few run in privacy mode i.e we can run the task based on the app requirement.
URLSessionConfiguration - Used to configure the URLSession
Types : 
1. Default - Uses disk based persistance cache, stores credentials in keychain.
2. Empheral - Similar to Default but doesnot store any cache. Its basically used for the privacy mode.
3. Background - Used to execute task in the background.

To create URLSession you need instance of URLSessionConfiguration object.
Then we use URLSession object to create instance of URLSessionTask.

3 concrete subclasses of the URLSession are as below:
1. URLSessionDataTask : This is used to fetch the data from the server. Response is Data format.
2. URLSessionDownloadTask : This is used to download a file from the serever. Response is temp place location wer file is downloaded. We need to copy that in permanent location.
3. URLSessionUploadTask

Ex for URLSessionDataTask:
**let configuration = URLSessionConfiguration.default
let session = URLSession(configuration: configuration)
guard let url = URL(string: "https://itunes.apple.com/search?media=music&entity=song&term=cohen") else {
    fatalError()
}
let task = session.dataTask(with: url) { (data, response, error) in
    guard let data = data else {
        return
    }
    if let result = String(data: data, encoding: .utf8) {
        print(result)
    }
}
task.resume()**

**We can set the priority for the task. It can be:
lowPriority ----- 0
defaultPriority ------ 0.5
highPriority ------- 1
priority is a property for the task that could be set with any of the above values.




Below is example for the Download task :
**
**class SongDownload : NSObject {
    var downloadTask : URLSessionDownloadTask?
    var donwloadURL : URL?
    func fetchSongAtURL(url:URL)  {
        donwloadURL = url
        downloadTask = URLSession(configuration: .default).downloadTask(with: donwloadURL!)
    }
}

**extension SongDownload : URLSessionDownloadTask {
    //Implement the delegate methods**.**
**}**
Download Task - When using download task with delegate. We need to confirm to URLSessionDownloadDelegate. Delegate method is called when download finishes with location of file download. In app we need to copy file from that location to the destination location.
We can also show the download progress. One of the delegate method return totalbytesWritten and totalExpectedByte. Using these values we can calculate the download progress.
We can also simulate the different network speed in iOS.
Pause, resume and cancel of download can be done.
Cancel ----- It will cancel the download. We need to call cancel()
Pause ------ Call cancelWithProducingResumedData() - It returns the data. We can store and utilise this to resume the downlaod process.
Resume ----- Need to create a task with resumed data and resume the task.


UploadTask:
It is used to upload the data to the server.

URLSession can be used to perform the operation in the background mode as well(i.e donwload and upload can be done in the background).
For this URLSession should be created using the background session configuration object and it should have an identifier. NetworkServiceType property should be set to .background

when system kills app when background task is running it continues to run in seperate process and once done it invokes app delegate method :
handleEventsForBackgroundURLSession method. It will have completion handler and background identifier. We need to store that completion handler and create url session object using that identifier. This is associated with background task. Once task is finished sesion delegate method is called : didfinishtaskforbackground. Here we need to call the completion handler on main thread. it says to OS that its safe to suspend the app again.

---- When user manually kills the app then OS willl stop all the background transfers.
Socket - In a single stream we can send and receive the data. Establishing socket communication between the client and the server.

URLSessionWebSocketTask : It allows client to communicate with server over the websocket.
Refer this link to understand diff between http and websocket protocol : https://www.geeksforgeeks.org/what-is-web-socket-and-how-it-is-different-from-the-http/

Authentication :
If one of the session task requires authentication then session task delegate method is called : didReceiveAuthentication. If it doesnot habdle it then delegate method from session delegate is called to handle.

App Transport Security : It is to make sure that app is connecting to secured server. Like https and not http. For example if we are connecting to server which does not have valid certificate from certificate authority urlsession throws ssl error and if we try to connect to http url then urlsession wont allow this.
But info.plist have allowArbitrary Loads option which can be set as true to allow the same.

Cookie is a text file generated by the server to identify the user in the subsequent requests.

