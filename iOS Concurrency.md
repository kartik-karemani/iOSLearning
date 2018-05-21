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

