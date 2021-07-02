# Snapshot Testing Guide for Beginners

This is a guide for beginners who wants to start with snapshot testing and they don't understand what snapshot testing is all about.

## What is **Snapshot Testing** and what it is not?

- Snapshot testing is mainly for UI components
- Snapshot tests will only check for rendering changes like css stylings and html elements
- Snapshot testing is a type of **_Regression Testing_** and it only ensures that the UI has not changed after code changes
- Snapshot testing can complement **_unit and functional tests_** and sometime you don't need to unit test a component and only snapshot test is enough
- Snapshot tests do not cover the business logic of components which means if onClick an API call is made or not, snapshot can't ensure that

## What happens in Snapshot testing?

1. The snapshot test case renders a UI component, you provide to it
2. Then, it takes a snapshot and save it to a separate folder `__snapshots__` with `<<testFileName>>.snap` name
3. After that it compares it to a reference snapshot file

## Why do we need it?

- It helps to prevent regression means if anything causes a component to change, the test will catch it

## When to use it?

1. If a component is not updated often means new css stylings and html elements are not added to the component. Because, updating the snapshot kills the purpose of test
2. If a component is not too complex means it should not contain tons of business logic and conditional statements
3. If you can easily see what you are actually testing and it is not not complex to check and understand the `.snap` the changes

## Pros

1. Faster and easier to create and maintain

## Cons

1. Give a false sense of security/coverage as they are too easy to update
2. Not suitable for TDD?
   - Snapshots can only assert existing behavior, they cannot be used when following TDD
3. Snapshot tests aren’t inherently well suited to dynamic content or components with tons of business logic

## Best Practices

1. Always use descriptive test case names for snapshots
   - The best names describe the expected snapshot content
2. Snapshot tests should be deterministic
   - for e.g. if a component use `Data.now()` then the value will be different each time and it will ask for snapshot update each time.
   - So, what you can do is mock the `Date.now()` method like `Date.now = jest.fn(() => 1234);` and now it will always return 1234

## Is snapshot testing TDD?

- TDD tests are written before coding whereas snapshot tests are written after you have done coding a feature
- We can't use it for TDD

## Visual Regression Testing vs Snapshot Testing

- **Visual regression testing** tools take screenshots of web pages and compare the resulting images pixel by pixel
- With **Snapshot testing** values are serialized, stored within text files, and compared using a diff algorithm.

## Libraries for snapshot testing

**1. Jest**

- For JS projects, Jest can be used and Jest is also considered as a defacto standard for testing JS projects

**2. react-test-renderer**

- A npm package used with Jest in ReactJS projects
- Its renderer method is used to render a component outside browser
- Then, we take the rendered output to create the snapshot (.snap) file

**3. Enzyme**

## Shallow and Mount Rendering (Enzyme)

- **Mount** rendering goes all the way down the hierarchy until it reaches the end of the tree, the DOM elements
- **Shallow** rendering merely goes to the immediate node of the tree
- By default, the snapshots reflect the **mount** rendered output for both `enzyme` and `react-test-renderer`

## Snapshot Test Components with Dynamic Props

- If a component accepts props and based on a prop a different JSX is returned, then, it is better that you should snapshot test every possible case.
- If you do this, you will have to write multiple snapshot tests in the test file but there will be only one `.snap` file and it will contain all the snapshots

## Misc.

- In Jest **_Inline Snapshots_**, the output of snapshot test is written to the same file in which test is written and not to external `.snap` file
- When the Jest test runner spots the `toMatchSnapshot()` of a test for the first time, it will generate a snapshot artifact (`.snap`) in a **snapshots** directory
