
### Testing Vue apps

Traditional Software Testing Pyramid, and the different types of testing available through the development life cycle.

![](https://i.imgur.com/O9CgeXD.png)

#### Unit Testing

Unit testing is a method that looks at individual units of code. It’s a crucial part of [Continuous Integration (CI)](https://codeship.com/continuous-integration-essentials). It isolates individual functions to check inputs against outputs, making sure each part of the software functions as expected.

#### Integration Testing

While unit testing focuses on individual functions in the source code, [integration testing](http://softwaretestingfundamentals.com/integration-testing/) is done on a higher level of abstraction. Integration testing checks the communication between:

- One component and another, or one page and another.
- Your application, and the backend database engine.
- One subsystem/module, and another

#### End-to-End Testing

Functional testing- also known as End-to-End or E2E testing- sits at the top of the pyramid. When writing a functional test script, you focus on testing the logic of the application, as well as
verifying, and implementing, all the features requested by your client. Functional testing usually follows a scenario testing path, taken in your application, starting from a certain point, and
ending at another point. For instance, a possible functional test could test the entire Login process:

- The user navigates to the Login page.
- They enter their credentials, and submit the form.
- If the credentials are correct, the user is redirected to the secure access pages.
- Otherwise, the user is denied access, and is left with an error message stating a
possible reason for the login failure.

Only when the test runs, and succeeds, will you have verified, and fulfilled one functional requirement, requested by your client. Then, you move on to write the next tests.

#### Visual Testing

With the way technology is evolving, the need for visual testing has never been stronger. It's unacceptable to have any type of bug in your application. The general public is unforgiving. This challenge is growing exponentially with the constant introduction of new devices, operating systems, browsers, and screen resolutions.

With unit, integration, and functional testing, you can obtain a certain level of confidence in the function of the application, and to what extent it serves its purpose. However, with visual testing,
you can be sure your application works across all platforms without any hiccups. If your apps run smoothly on all platforms, you should expect consumer confidence.

The special relationship between functional and visual testing distinguishes the two among all forms of testing. Functional testing has been around for a long time. It’s reputable, and the testing frameworks supporting functional testing are robust.

Visual testing takes advantage of existing functional testing infrastructure and builds its tools on top of it. Given a functional test, you can easily integrate a visual testing framework by injecting function calls inside of your tests. These function calls serve the purpose of taking snapshots, sending them to the backend servers for analysis and comparison, and finally, generating a report of the results.

If you are interested in learning about visual testing, I’ve written thirteen [articles](https://applitools.com/blog/author/bilalhaidar) exploring Applitools as a visual testing framework.
