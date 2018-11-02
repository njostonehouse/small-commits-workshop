<!-- Docs: https://github.com/gnab/remark/wiki -->
<!-- Example: https://github.com/gnab/remark/blob/gh-pages/index.html -->

class: center, middle

# Small Commits in Practice: A Hands-on Workshop

Carl Pacey and Mark Tse

---

# Introduction

---

# Agenda

* Goals
* Quick refresher on techniques
* Exercise 1: Breaking up a pull request (~45 minutes)
* Break (~10 minutes)
* Exercise 2: Plan implementing a feature using small commits (~45 minutes)

---

# Goals

Get some practice breaking up PRs:

1. _After_ the code is written
1. _Before_ the code is written

---

# Techniques

1. Add a new class, method, property, etc
  * Test it, but don't use it
1. Add new tests to existing code
  * Tr to limkit or isolate changes to production code
1. Refactor existing production code
  * Specifically to make your next change(s) easier, safer, or smaller
  * Try to limit or isolate changes to test code
  * Try to avoid (or isolate) functional changes
1. Functional changes
  * Thesae get small after you've done the above
  * New tests end up being for new production code

---

# Exercise 1: Breaking up a pull request

* The app currently supports a "get all users" route
  * `small-commits-workshop/SmallCommitsWorkshop/Controllers/UsersController.cs`
* The `users/bigpr` branch does the following:
  * Adds GET single user
  * Adds POST user, which creates or updates
  * Adds DELETE user
  * Adds an index on User.Id
  * Adds a new property User.IsActive
  * Refactors test (`AddUsers()` method)

---

# Exercise 1: Breaking up a pull request

Tasks:
1. Fork the repository (https://github.com/neverendingqs/small-commits-workshop)
1. Using `users/bigpr`, break up the code into smaller commits
    * You can view the changes at
      https://github.com/neverendingqs/small-commits-workshop/pull/13
1. For each commit, create a pull request onto `<user>/master`
    * Either add Carl, Mark, or another person in the workshop as your reviewer
1. Continue until your `<user>/master` branch is functionally similar to
    `users/bigpr`

---

# Exercise 2: Let's add a new feature

* You're hopefully familiar with Users after Exercise #1.
* Now we're going to expand some functionality to include user information.

---

# Exercise 2: FizzBuzz

FizzBuzz is a famous interview question:

> Write a program that prints the numbers from 1 to 100. But for multiples of three print "Fizz" instead of the number and for the multiples of five print "Buzz". For numbers which are multiples of both three and five print "FizzBuzz".

https://blog.codinghorror.com/why-cant-programmers-program/

---

# Exercise 2: Existing Functionality

You may have noticed that the app already supports `/fizzbuzz/{number}`.

```
GET /fizzbuzz/14: 14
GET /fizzbuzz/15: FizzBuzz
GET /fizzbuzz/16: 16
GET /fizzbuzz/17: 17
GET /fizzbuzz/18: Fizz
GET /fizzbuzz/19: 19
GET /fizzbuzz/20: Buzz
GET /fizzbuzz/21: Fizz
GET /fizzbuzz/22: 22
```

---

# Exercise 2: New Functionality

We want to add the following route:

```
/fizzbuzz/{number}/users/{userId}
```

This route will return a modified FizzBuzz:

1. Instead of "Fizz", this route will use the user's UserName.
1. Instead of "Buzz", this route will use a new user property, BuzzWord.

---

# Exercise 2: Examples

```json
GET /users/1045
{
  "id": 1045,
  "userName": "cpacey",
  "isActive": true,
  "buzzWord": "isawesome"
}
```

```json
GET /fizzbuzz/14/users/1045: 14
GET /fizzbuzz/15/users/1045: cpaceyisawesome
GET /fizzbuzz/16/users/1045: 16
GET /fizzbuzz/17/users/1045: 17
GET /fizzbuzz/18/users/1045: cpacey
GET /fizzbuzz/19/users/1045: 19
GET /fizzbuzz/20/users/1045: isawesome
GET /fizzbuzz/21/users/1045: cpacey
GET /fizzbuzz/22/users/1045: 22
```

---

# Closing
