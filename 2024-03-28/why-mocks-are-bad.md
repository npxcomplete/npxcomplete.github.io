It seems once upon a time the idea that unit tests should fully isolate a method became the "in thing to do"
and sheer laziness has resulted in the flagrant use of mocking libraries as the default way that many developers 
write tests. However, the presence of mocks in a test is a smell. They probably aren't needed and they almost 
certainly are making your code base worse. 

Now before anyone jumps in with an "ummm, actually....", yes, of course there are exceptions. But is the test you're
writing right now one of those exceptions? Probably not. 

The most common reason to use a mock library is not to mock, it's to stub. We stub out API calls & responses to avoid 
the performance cost of executing over a network and the fragility of interacting with a live service. Note that we 
usually don't do this for the most common API an application will interact with, the database. Most unit tests will 
still use a local/embedded/fake database that is validated by the provider as behaving the same as the real thing at 
the scale of the unit test. However, because other APIs are less complete or more difficult to fake we opt to stub 
their responses.

The second best use for a mock library is to handle specific, hard to produce error modes. For example if your test
coves a network connection and you want to simulate a network interrupt you would likely use a mock library. The 
trade-off is against the difficulty of reliably producing that error mode using an actual network connection.

My third and favorite reason to use a mock is because the library you depend on is badly implemented. For example,
several libraries will provide some functionality that relies on real world time. This may mean that it fails to 
expose the scheduler or clock. For example if you want to test that your system responds correctly to a poll function
that would be run every 5 minutes. Well you don't want your unit test to actually sit and wait those 5 minutes, right? 
As a result a powerful mocking library may be required to reflectively access the library internals so as to manipulate 
the scheduler.

Are the tests in these usecases going to be ideal? No, but optimal is rarely perfect. Let's lay it out. Why is it that 
using mocks gets your pull request rejected:

### It's a sign your writing tests wrong.
Let's start with what is an often accepted and rarely followed best practice, TDD. Would you write 
the test using mocks if you know only the interface and  nothing about the implementation? 

### It's a sign your system is poorly designed
...

### It binds your test to the implementation
Your test now makes very concrete assumptions about the implementation. A refactoring (changing only the implementation, 
making no externally visible changes to behavior) breaks your test, effectively requiring every test to be re-written.

### It hides the system interdependence
When the behavior of the underlying component is intentionally changed, then the underlying component's tests fail
and are changed to be consistent with the newly desired behavior. However, because the underlying component was mocked
in our test suite there is no signal to call attention to the fact that our component's assumptions (as expressed 
through mocking) are no longer valid. Your system is no longer cohesive, but all your tests pass.

### The tests become unreadable
Tests are documentation, they are an executable specification. When something breaks, when things change, the developer
needs to be able to understand the original intended behavior the test was trying to validate. A three block test 
(GIVEN/WHEN/THEN) carries the most clarity. 

See also, https://testing.googleblog.com/2024/02/increase-test-fidelity-by-avoiding-mocks.html


