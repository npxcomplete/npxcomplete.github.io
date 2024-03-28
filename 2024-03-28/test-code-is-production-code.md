# Test Code IS Production Code

If you've ever had the (mis?)fortune to work with me you will quickly find out I have some strong opinions. 
Some of the strongest of these opinions are around what makes a good unit test. The first and not so controversial
of these is that test code is production code. The application code we normally think of as production code is 
required to be robust, readable, and maintainable. Is there a good reason we shouldn't expect these things of our 
test code?

To understand what makes a good test we also need to know why we write tests. If you've never though deeply about 
this question before you will of course find the first obvious answer, to check our code "works". However, it's 
worth listing out all the reasons:

* Specifying the behavior 
* Asserting completion
* Debugging / Defect detection
* Regression detection
* Validating system cohesion 

Tests aren't just production code, they are an executable specification / documentation. They say how your code
works and provide a limited way to verify that it does indeed work that way. Tests as specification applies at 
all levels but is most closely aligned with the practice of acceptance testing. When acceptance testing you write
tests against the public interface (API/UI/exposed library functions) using a user/customer friendly format AND THEN
implement the functionality. When the tests all pass your implementation is done (or you didn't write all the tests).

Whether you're doing Acceptance testing, BDD (Behavior driven development, i.e. TDD with better vocabulary), 
or DDT (Defect driven testing, writing tests to expose a bug) you should be following a red - green cycle. 
First write the test, run the test, see the test fail (red), then change the implementation, run the test, 
see the test pass (green). This gives us confidence that the test catches the bug and will catch the bug if 
it is ever re-introduced later. 

Following the above process and you should end up with a weakly coupled design that can be understood by 
future developers and has a strong regression suite to protect it from possible future defects. However, in
order for that test suite to be valuable it must not be brittle in the face of change. A brittle test suite 
results from poor judgment when selecting the scope to test against. A good rule of thumb is to test as broad 
a swath of the implementation as possible. This usually means testing everything within the scope of a single 
process. Conflicts with this rule of thumb come from: 

* performance intensive operations, 
* IO / network boundaries, and 
* true time.

For a deeper discussion, see [Why mocks are bad](/2024-03-28/why-mocks-are-bad.md).
