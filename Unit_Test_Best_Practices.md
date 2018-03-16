### Keep tests clean, Readability is #1
If you change requirements to a project, the number one thing developers complain is that the test suite is dirty. If your project requires that 100% of unit tests are required to passed before the product is shipped, developers will sloth through test code to figure out why a test portion is broken when they change the source code. As the source code grows, the test code grows and soon your test code will become a pile of useless mess. When it comes time for requirement changes, they are hindered by not able to manipulate the test suite to their liking.

Even though quality of production code vs. test code are different, test code is all about failing quickly and verbosely as possible. To be able to identify an issue quickly is all connected to how readable it is.

To measure the flexiblity of production code is by measuring your test code. You can change poorly made architecture and code with readable test code. But you cannot change very good designed source code with dirty tests.

How many times did you have to go into test source code to figure why it failed because it gave you some "it failed somewhere over here" answer versus just looking at the test function's name to tell you where you messed up?

Or wtf is this test trying to do? Why is it doing all these other things?

### More comments does NOT increase readability
That's right folks, you read that correctly. Having more comments does NOT mean your code is more readable.

Think of it this way, why did you write that comment in the first place? You wanted to explain what you did or intended to do right? But again, that means your code isn't written in a way that is intuitive. Ideal code is code that is written that even without documentation, you are able to understand what it is happening. How do you solve this problem? You must use encapsulation by function calls. Allow your function names do the 'commenting' for you. You want your code to tell a story. Comments create clutter, I don't need comments about you getting or setting when your functions are getters and setters, since we don't comment getters and setters, why not apply this idea to your other functions?

Another thing to consider is that by commenting, you usually need to explain a complex task. Why is this task complex in the first place? It is usually related to the fact that your task is doing TOO MANY things. Your function is not abiding to the single responsibility principle. So break this code into atomic sub tasks, once that is accomplished, you don't need anymore comments. Your functions are broken up enough that the function does ONE THING only.

### Setup and Teardown
Your unit tests should have API code that abstracts away the setup and teardown of your tests. When someone glances at one of your test cases, it is easily identified what the intended 'test' portion of your code is. That way your tests don't have extra lines of setup and teardown that are taking up screen real estate.

```
public void testGetResponseAsXml() throws Exception {
   makePageWithContent("TestPageOne", "test page");
   submitRequest("TestPageOne", "type:data");
   assertResponseIsXML();
}
```

### One assert per test per intent
Assuming your tests only return TRUE for PASS and FALSE for FAIL.

By having multiple asserts in a test, if that test fails, you won't know which assertion failed therefore requiring more time spent to identify the problem, making developers furious. Or it will tell you the line that broke.

Again, our objective is to be readable, having multiple asserts and grouping them all together does not support readability. It abstracts TOO much of what the tests really should be intended to do. Ulitmate ideal is for a developer to look at the test's function name and immedately identify the problem without looking at the source code. THe name given to the test function would probraly be very generic since you are testing multiple things. If you have multiple asserts, the developer would have to spend time searching for the problem. Not a good use of his/her time.

Having the one assert per test rule will force tests to test one thing and only ONE thing at a time. Knowing the exact problem is better than knowing that the problem exists "somewhere over here". Also having one assert eliminates many other variables and dependencies that may affect the test now or later.

Another point to make, you should have one assert per intended behavior. That means, if you have a method where you can pass multiple parameters and it outputs different results each time, then you should make separate tests for each. For example, a method that checks if a string has numbers, special characters, size limit, etc.. this is a perfect example of having multiple tests. However, this is a general rule, if you had a combination problem, where your string could not have numbers in certain positions, best approach is to create a string generator loop that moves a number around the string and one assert within that loop.

DO NOT combine multiple methods together while asserting after each method call.

```
bool result_a = A();
assert(result_a);
bool result_b = B();
assert(result_b);
bool result_c = C();
assert(result_c);
```

This is a recipe for disaster. You want to create your tests in the perspective of the user. What can the user play with and see without looking at the source code? In this scenario, how are you so sure that by calling method A() it does not affect the behavior of B() or C()? You don't. 

*"But I already looked at the source code, they don't depend on each other!"*

My question to you is, how do you know that the behavior of A() wouldn't change in the future?

*"But then the test would fail and it would find a problem."*

Is it the correct problem? What if the intent was to make sure A(), B(), and C() were all indepent from each other. Then in the future a developer had to change it so B() and C() depends on A(). You created a test that was meant for the future and not the present. This is an example of writing the wrong test for the wrong reason.

Some scenarios require multiple asserts and for good reason, for example, the case of a parser. Obvious you have to read from the beginning to the end of a sentence. Being off by one letter will ruining the parser's behavior, so its natural to add the getNextWord() method over and over while asserting the result.

### Follow the Template Model
A good model to follow is the Template Method. usage of the given, when, then clauses to create your tests.

```
public void testGetPageAndHaveCorrectTags() throws Exception {
    givenPages("PageOne", "PageOne.ChildOne", "PageTwo");
    whenRequestIsIssued("root", "type:pages");
    thenResponseShouldContain("<title>PageOne</title>", "<title>ChildOne</title>","<title>PageTwo</title>");
}
```

### Test Independently
Test should not depend on each other. A test should never setup the configurations/conditions for the next test. When a test depends on another test, you fall into a cascade of failures that may require debugging in the future.

*"What did you mean it wasn't my code's problem? It was someone else's?"*

Make sure you maintain your dependencies between methods and classes appropriately and only include code if the class or method KNOWS of the existence of such a class/method.

For example, if you wanted to test the method A(), do not call a class that HAS your class to test your method, such as:

```
baseClass myBaseClass();
baseClassPtr* = myBaseClass;
myBaseClass->m_someClass->A();
```

How do you know that myBaseClass's constructor does not modify m_someClass before you were to call A()? Avoid dependencies like this and straight up make the class from scratch and call the method without any possible interference.
