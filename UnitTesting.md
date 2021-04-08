In iOS we use XCTest framework to perform the unit testing.

- Subclass of XCTestCase contains a group of related test methods. where as each test method is used to test some functionality. It starts with prefix : test
  XCTestCase can be designed to contain unit test methods related to one module or functionality.
- Test methods are passed by default.
- We can test if test method pass or fail using the assertion methods. For ex : XCAssertNil, XCAssertNotNil, XCAssertTrue,XCAssertFalse.
- XCTAssertEqual : It will compare 2 arguments, if they are not equal then the test fails.

Code covergae indicates the percentage amount of code that has been tested.
Assert function for the comparison:
XCAssertGreaterThan
XCAssertGreaterThanEqualTo
XCAssertLessThan
XCAssertLessThanEqualTo

Test Driven Development : It is way to make the code written in the app is testable. Here we first write the test cases for the functionaliy before its implementation.

We can do test for synchronous and non- synchronous operation.
We can write test for asynchronous code using XCTestExpectation.
Steps :
1. We need to create instance of the expectation object.
2. call waitForExpectionn passing the time interval.
3. Fullfill the expectation in the completion block of the asynchronous operation.
4. If the expectation is fullfilled before time out then test method is success or else it fails.
