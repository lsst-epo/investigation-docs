# Unit Testing React Components

### Main Dependencies
We use [Jest](https://jestjs.io/docs/en/tutorial-react) to run our test.
We use [React Testing Library](https://testing-library.com/docs/react-testing-library/intro) along with the [jest-dom](https://github.com/testing-library/jest-dom) assertion library to write our tests.

#### Jest Config
Gatsby provides [an easy to follow tutorial](https://www.gatsbyjs.org/docs/unit-testing/) for installing, configuring, and setting up your first test using Jest.  Our set up does not diverge from this tutorial, but our tests themselves do.

#### React Testing Library
React Testing Library is a collection of javascript utilities and helper methods designed to encourage test writing that matches how a user interacts with your app.  Whereas a testing library such as Enzyme is predicated on testing your implementation of a react component, React Testing Library is predicated on testing how a user might interact with your app.
>The more your tests resemble the way your software is used, the more confidence they can give you.

#### What to Test
Writing tests that pass is easy.  Writing tests worth having is hard.  The first step is identifying what React components are worth testing.  We are utilizing a Material UI React Component Library called [react-md](https://react-md.mlaursen.com/).  It is not our responsibility to ensure those components preform in the way were designed (and/or as we would expect).  It *is* our responsibility to test our implementation of those components.  For example, we may have a `nav` that have a collection of `react-md` `Button` components.  Clicking each of those buttons does `something`.  Each of those buttons has a [whole collection of props](https://react-md.mlaursen.com/components/buttons?tab=1) dictating their appearance and behavior.  Now we will not test whether those buttons' appearance and behavior works as advertised, but we will test whether clicking each button does the `something` our code says it should, and we will measure that effect on the DOM.

Don't bother testing that every single prop has the presentational effect you expect; Only test effects of the props (or state changes) that undergo significant manipulation *or* have measureable effects on the DOM *or* have a measureable effect on other props (or state changes).

#### How to Test
The best way to add test coverage is to create new tests as you build new components.  This is know as [Test Driven Development (or Behavioral Driven Development)](https://www.freecodecamp.org/news/test-driven-development-what-it-is-and-what-it-is-not-41fa6bca02a2/) and it is, in a nutshell:
>Write only enough of a unit test to fail

>Write only enough code to make the failing unit test pass

In practice that looks something like:
1. Identify a new necessary feature
2. Write a test that describes that feature's success
2. Verify that test fails (if it passes you either need to write a better test, or, congratulations, you're done!)
3. Make the test pass (i.e. write code that adds the new feature)
4. Verify the test passes
5. Refactor (and if you do, verify the test still tests what you think it does, and re-verify the test still passes)

Think about writing tests from the perspective of the user: the user doesn't know about or care about state or prop changes, but they do know if they click on a button, or enter text into a form field, or really if they're ever presented with any oprotunity to interact with the DOM in any way, they expect something to happen.  Write a test that describes cause and effect.  These tests often take the form of *Arrange*, *Act*, and *Assert*:
- *Arrange* the elemnts you need to run your test
- *Act* on those elements to trigger whatever behavior you're testing
- *Assert* what outcome you expect from that behavior

#### Further Reading
*React Testing Library*
- [Cheatsheet](https://testing-library.com/docs/react-testing-library/cheatsheet)
- [Composing Queries](https://testing-library.com/docs/dom-testing-library/api-queries)
- [Firing Events](https://testing-library.com/docs/dom-testing-library/api-events)
- [Events API](https://github.com/testing-library/dom-testing-library/blob/master/src/events.js)
- [Async Utilities](https://testing-library.com/docs/dom-testing-library/api-async)
- [Special Considerations for simulating events](https://testing-library.com/docs/guide-events)
- [How to test appear/dissapearing elements](https://testing-library.com/docs/guide-disappearance)
- [Great Examples](https://react-testing-examples.com/)

*jest-dom*
- [jest-dom assertions/matchers API](https://github.com/testing-library/jest-dom#custom-matchers)
