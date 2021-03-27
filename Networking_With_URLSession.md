
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
1. URLSessionDataTask
2. URLSessionDownloadTask
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
