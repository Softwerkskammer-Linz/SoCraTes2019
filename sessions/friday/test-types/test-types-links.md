## Types of tests and when to apply them
* The **[test pyramid](https://martinfowler.com/articles/practical-test-pyramid.html)** helps you to decide what types of test you need and how many of each sort.

* "Mocks" are just one type of [test doubles](https://www.martinfowler.com/bliki/TestDouble.html), think about which one you need. 

* If you're using PHP, follow the advice in "[Pick your test doubles wisely](https://matthiasnoback.nl/2014/07/test-doubles/)" and "[5 ways to write better mocks](https://www.entropywins.wtf/blog/2016/05/13/5-ways-to-write-better-mocks/)".

* [Extensive mocking setup can be code smell](https://medium.com/javascript-scene/mocking-is-a-code-smell-944a70c90a6a)

If you have two teams working on client and server side code, you could use [contract testing](https://martinfowler.com/bliki/ContractTest.html) with a tool like [Pact](https://docs.pact.io/)

Use the [Page Object Pattern](https://www.pluralsight.com/guides/getting-started-with-page-object-pattern-for-your-selenium-tests) to isolate the low-level DOM access from the high-level test language. 
