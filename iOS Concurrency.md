# iOSLearning
Description of ios topics.

iOS Concurrency :
1. GCD
2. NSOperation Queue

1. GCD 
Serial Queue : It is queue where task are added in the form of blocks. It executes only one task at a time. Tasks are executed
in the order they are added in the queue.
Concurrent Queue :  It is queue where task are added in the form of blocks. It executes tasks concurrently. At a time multiple tasks 
are executed in the concurrent queue.
dispatch_syc : It adds the block to the queue and wait till the execution of the block and then it returns. It blocks the calling thread.
dispatch_async : It adds the block to the queue and return immediately.It doesnot block the calling thread.

GCD has :
1. Main queue
2. 5 global queues
3. We can also create private serial or private concurrent queue.

DispatchWorkItem : It encapsulates the work needs on dispatch queue.
It can be used to execute a work item after other workitem. For ex : Refer code snippet below
**userQueue.async(execute: backgroundWorkItem)
backgroundWorkItem.notify(queue: mainQueue, execute: uiWorkItem)**

Result type : Can be used to return type of the method. If has 2 possible values i.e. success and failure. Both cases are associated with some value.
failure is associated with object confirming to the Error protocol.
Writing asyncrhornous functions.

DispatchGroup - It will let us know the completion of the group of tasks. Below is the code snippet :(Below code is adding synchrnous function in dispatch group)
**let numberArray = [(0,1),(2,3),(4,5),(6,7),(8,9)]
let workGroup = DispatchGroup()
for inValue in numberArray {
    userQueue.async(group: workGroup) {
        let result = slowAdd(input: inValue)
        print("Result = \(result)")
    }
}
workGroup.notify(queue: mainQueue) {
    print("All task are executed successfully....")
}**

Below code is adding asynchonous function in dispatch group :

**func asyncAdd(input:(Int,Int),
              runQueue:DispatchQueue = DispatchQueue.global(qos:.userInitiated),
              completionQueue:DispatchQueue = DispatchQueue.main,
              completionHandler:@escaping (Result<Int,SlowAddError>) -> ()
              ){
    runQueue.async {
        let res = slowAddPlus(input: input)
        completionQueue.async {
            completionHandler(res)
        }
    }
}

**func asyncAddGroup(
    input : (Int,Int),
    runQueue:DispatchQueue = DispatchQueue.global(qos: .userInitiated),
    group:DispatchGroup,
    completionQueue:DispatchQueue = DispatchQueue.main,
    completionHandler:@escaping (Result<Int,SlowAddError>) -> ()
) {
    group.enter()
    asyncAdd(input: input) { result in
        defer {
            group.leave()
        }
        completionQueue.async {
            completionHandler(result)
        }
    }
}
let newGroup = DispatchGroup()
for val in numberArray {
    asyncAddGroup(input: val, group: newGroup) { result in
        print("Resut : \(result)")
    }
}

newGroup.notify(queue: mainQueue) {
    print("Complete")
}****


Dispatch_Semaphor : It gives you control over how many group tasks run at a same time.

Concurrrency Problems :

1. Priority Inversion : Lower priority task runs ahead of higher priority task bcoz the resource required for the higher priority task is locked by the lower priority task. For ex : 
                      Low Priority task needs resource so it locks it. When medium priority task executes processor puts Low Priority task on sleep but it still     have lock. Higher priority task runs due to which medium priority task is sleep. Since high priority task tries to acquire the lock but as it is with low priority task it goes on sleep. Hence since medium priority task doesnot want resouce it starts. Here medium priority task is running before high priority task so priority inversion took place.
2. Race Condition
    This happens when multiple threads try to access same resource and corrupts it.
    For this we can use Dispatch barrier. Queue becoems when barried task is added.
4. Deadlock : It happens when 2 threads get struck as they are waiting to each other to finish.

**dispatch_queue_t queue = dispatch_queue_create("my.label", DISPATCH_QUEUE_SERIAL);
dispatch_async(queue, ^{
    dispatch_sync(queue, ^{
        // outer block is waiting for this inner block to complete,
        // inner block won't start before outer block finishes
        // => deadlock
    });

    // this will never be reached
}); **

