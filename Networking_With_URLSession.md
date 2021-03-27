
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



