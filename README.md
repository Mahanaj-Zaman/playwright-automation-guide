<div align="center">

# 🎭 Playwright Automation Mastery

### A complete, practical documentation guide for learning Playwright from absolute basics to intermediate — written for QA engineers who want to get productive fast.

<br/>

![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=for-the-badge&logo=playwright&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-F7DF1E?style=for-the-badge&logo=opensourceinitiative&logoColor=black)
![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen?style=for-the-badge)
![Maintained](https://img.shields.io/badge/Maintained-Yes-2EAD33?style=for-the-badge)

</div>

---

## 🧭 What is this repository?

This repository is a **free, open-source documentation guide** for learning Microsoft's Playwright end-to-end testing framework. It is designed to take a complete beginner from zero knowledge to writing real, structured, production-style test suites.

Every concept is explained in plain language with annotated code examples. Nothing is assumed — every term is defined, every code block is commented line by line.

This is not a copy of the official docs. It is a **learning guide written by a QA engineer, for QA engineers** — with the kind of practical context, gotchas, and real-world patterns that official documentation rarely gives you.

### 🎯 Who is this for?

| Audience | Why this helps |
|---|---|
| **Junior QA Engineers** | Start from zero — installation through writing your first test |
| **Manual testers moving to automation** | Concepts explained without assumed knowledge |
| **Developers writing their own tests** | Page Object Model and advanced patterns covered |
| **QA leads and hiring managers** | A reference to share with teams onboarding to Playwright |
| **Career switchers entering QA** | Portfolio-quality knowledge presented clearly |

---

## 📋 Table of Contents

- [📖 Documentation Guide](#-documentation-guide)
  - [1. What is Playwright?](#1-what-is-playwright)
  - [2. Setting Up Playwright](#2-setting-up-playwright)
  - [3. Core Concepts](#3-core-concepts)
  - [4. Locators and Selectors](#4-locators-and-selectors)
  - [5. Actions](#5-actions)
  - [6. Assertions](#6-assertions)
  - [7. Writing Tests](#7-writing-tests)
  - [8. Page Object Model](#8-page-object-model-pom)
  - [9. Advanced Features](#9-advanced-features)
  - [10. Real World Example](#10-real-world-example)
- [📅 30 Day LinkedIn Series](#-30-day-linkedin-series)
- [🤝 Contributing](#-contributing)
- [🔗 Connect With Me](#-connect-with-me)
- [📄 License](#-license)

---

## 📖 Documentation Guide

The full guide lives in [`playwright-guide.md`](./playwright-guide.md). Here is a summary of every section and what it covers.

---

### 1. What is Playwright?

> *File: [`playwright-guide.md → Section 1`](./playwright-guide.md#1-what-is-playwright)*

Covers the origin and purpose of Playwright, the specific problems it was built to solve, and an honest side-by-side comparison with Selenium and Cypress across 12 dimensions including browser support, speed, parallelism, mobile emulation, and debugging tools. Also explains why engineering teams and companies are adopting Playwright at scale.

**You will learn:**
- What Playwright is and why Microsoft built it
- How it compares to Selenium and Cypress (with a detailed table)
- The real-world reasons companies choose Playwright

---

### 2. Setting Up Playwright

> *File: [`playwright-guide.md → Section 2`](./playwright-guide.md#2-setting-up-playwright)*

A complete walkthrough from a blank terminal to a running test suite. Covers every interactive prompt during `npm init playwright@latest`, what the generated project structure means, and a full line-by-line breakdown of `playwright.config.ts` including every option and when to change it.

**You will learn:**
- Prerequisites and how to verify them
- Step-by-step installation with `npm init playwright@latest`
- What every file and folder in the project does
- How to read and configure `playwright.config.ts`

---

### 3. Core Concepts

> *File: [`playwright-guide.md → Section 3`](./playwright-guide.md#3-core-concepts)*

Explains the three fundamental Playwright objects — Browser, BrowserContext, and Page — using plain language analogies. Includes a diagram of how they relate to each other and a technical explanation of how Playwright communicates with browsers using the Chrome DevTools Protocol. Also covers the auto-waiting mechanism that makes Playwright reliable.

**You will learn:**
- The Browser → Context → Page hierarchy
- Why BrowserContext isolation prevents test interference
- How auto-waiting works (and why it eliminates flaky tests)

---

### 4. Locators and Selectors

> *File: [`playwright-guide.md → Section 4`](./playwright-guide.md#4-locators-and-selectors)*

The most comprehensive section on finding elements. Covers all nine locator strategies with real code examples for each. Includes a priority-ordered "best practices" ranking so you always know which locator to reach for first, and a clear list of patterns to avoid with explanations of why they break.

**You will learn:**
- `getByRole`, `getByLabel`, `getByPlaceholder`, `getByText`, `getByTestId`, `getByAltText`, `getByTitle`, `locator()` (CSS + XPath)
- How to filter and chain locators
- The locator priority order (and why `getByRole` is almost always the right first choice)
- Anti-patterns that create brittle tests

---

### 5. Actions

> *File: [`playwright-guide.md → Section 5`](./playwright-guide.md#5-actions)*

Every interaction a user can perform, translated into Playwright code. Each action includes a working code example with inline comments explaining every parameter and option.

**You will learn:**
- `click()`, `dblclick()`, right-click, modifier-click
- `fill()`, `clear()`, `pressSequentially()` for inputs
- `hover()` for revealing menus and tooltips
- `selectOption()` for native and custom dropdowns
- Keyboard shortcuts, Tab navigation, and arrow key control
- File uploads, drag and drop, scrolling, and explicit waits

---

### 6. Assertions

> *File: [`playwright-guide.md → Section 6`](./playwright-guide.md#6-assertions)*

Why assertions are the difference between a real test and a script that just clicks around. Covers the auto-retrying behaviour of `expect()`, every commonly used assertion with full code examples, soft assertions for collecting multiple failures, and value-based assertions for JavaScript primitives.

**You will learn:**
- Visibility, text, URL, title, input value, checked state, count assertions
- How to negate any assertion with `.not`
- Soft assertions — when and why to use them
- The difference between locator assertions and value assertions

---

### 7. Writing Tests

> *File: [`playwright-guide.md → Section 7`](./playwright-guide.md#7-writing-tests)*

The full anatomy of a Playwright test file. Covers `test.describe`, `test.beforeEach`, `test.afterEach`, `test.beforeAll`, `test.afterAll`, and the fixture system. Includes a step-by-step walkthrough of writing a complete test from a blank file against a live public demo app, plus how to read terminal output and the HTML report.

**You will learn:**
- Test file structure and grouping with `describe`
- How hooks (`beforeEach`, `afterAll`, etc.) work
- What fixtures are and which ones come built-in (`page`, `context`, `browser`, `request`)
- Every `npx playwright test` command you'll use daily
- How to read failures in the terminal and HTML report

---

### 8. Page Object Model (POM)

> *File: [`playwright-guide.md → Section 8`](./playwright-guide.md#8-page-object-model-pom)*

The most important design pattern in professional test automation. Explains exactly why tests written without POM become impossible to maintain, then builds a complete POM implementation from scratch — including `LoginPage`, `DashboardPage`, and how to wire them into clean, readable test files.

**You will learn:**
- The maintainability problem that POM solves
- How to structure a Page class with typed locators and action methods
- The difference between locators as properties vs. methods
- How to import and use page objects in test files
- Why your tests should read like business scenarios, not CSS selectors

---

### 9. Advanced Features

> *File: [`playwright-guide.md → Section 9`](./playwright-guide.md#9-advanced-features)*

Four production-level capabilities that take tests from basic to enterprise-grade: HTTP API testing without a browser, saving and restoring authentication sessions with `storageState`, capturing screenshots and trace files, and controlling parallel execution including CI sharding across multiple machines.

**You will learn:**
- Making GET, POST, and authenticated API requests with `request` fixture
- Combining API setup with UI test flows
- Saving a logged-in session once and reusing it across all tests
- Configuring automatic screenshots, video, and trace recording
- `fullyParallel`, `workers`, `--shard` for scaling test execution

---

### 10. Real World Example

> *File: [`playwright-guide.md → Section 10`](./playwright-guide.md#10-real-world-example)*

A production-style, end-to-end test suite that ties together every concept from the guide. Includes `LoginPage`, `DashboardPage`, and `ProfilePage` page objects, test data managed in a JSON file, positive and negative login tests, navigation and search tests, a logout flow that verifies route protection, and an API-to-UI sync verification test.

**You will learn:**
- How a real-world test suite is structured
- Positive testing, negative testing, and edge case coverage
- Verifying that API and UI data stay in sync
- Managing test data with external JSON files
- The complete set of commands for running, filtering, and reporting on your suite

---

## 📅 30 Day LinkedIn Series

This documentation is being published as a **30-day LinkedIn learning series** — one post per day, each covering a key Playwright concept with a practical code example and a takeaway for QA engineers at every level.

> 🔗 **Follow the full series here:** [LinkedIn Series Playlist → `https://www.linkedin.com/in/mahanaj-zaman-marufa/`](#)

Each post in the series maps directly to a section of this guide, so you can read deeper on any topic that resonates.

| Day | Topic | Status |
|-----|-------|--------|
| 01 | What is Playwright and why should QA engineers care? | 🔜 Coming soon |
| 02 | Playwright vs Selenium vs Cypress — the honest comparison | 🔜 Coming soon |
| 03 | Installing Playwright in under 5 minutes | 🔜 Coming soon |
| 04 | Understanding `playwright.config.ts` | 🔜 Coming soon |
| 05 | Browser, Context, and Page — the core hierarchy | 🔜 Coming soon |
| 06 | Auto-waiting: why Playwright tests are more reliable | 🔜 Coming soon |
| 07 | `getByRole` — the locator you should use by default | 🔜 Coming soon |
| 08 | `getByLabel`, `getByPlaceholder`, `getByTestId` explained | 🔜 Coming soon |
| 09 | Locator chaining and filtering | 🔜 Coming soon |
| 10 | Locator anti-patterns to avoid | 🔜 Coming soon |
| 11 | Click, double-click, right-click with Playwright | 🔜 Coming soon |
| 12 | Filling forms — `fill()`, `clear()`, `pressSequentially()` | 🔜 Coming soon |
| 13 | Hover, select dropdowns, and file uploads | 🔜 Coming soon |
| 14 | Keyboard actions and shortcuts | 🔜 Coming soon |
| 15 | What are assertions and why they matter | 🔜 Coming soon |
| 16 | The complete `expect()` assertion cheat sheet | 🔜 Coming soon |
| 17 | Soft assertions — collecting failures without stopping | 🔜 Coming soon |
| 18 | Test structure — `describe`, `beforeEach`, hooks | 🔜 Coming soon |
| 19 | Writing your first Playwright test from scratch | 🔜 Coming soon |
| 20 | Running tests and reading the HTML report | 🔜 Coming soon |
| 21 | What is the Page Object Model (POM)? | 🔜 Coming soon |
| 22 | Building a LoginPage class from scratch | 🔜 Coming soon |
| 23 | Using page objects to write clean test files | 🔜 Coming soon |
| 24 | API testing with Playwright's `request` fixture | 🔜 Coming soon |
| 25 | Combining API setup with UI test flows | 🔜 Coming soon |
| 26 | Saving authentication state with `storageState` | 🔜 Coming soon |
| 27 | Screenshots, video, and the Trace Viewer | 🔜 Coming soon |
| 28 | Parallel execution and CI sharding | 🔜 Coming soon |
| 29 | Real-world test suite walkthrough | 🔜 Coming soon |
| 30 | What to learn next — beyond this guide | 🔜 Coming soon |

---

## 🤝 Contributing

Contributions are welcome and appreciated. This guide exists to help QA engineers — any improvement that makes it clearer, more accurate, or more useful is a good contribution.

**Ways to contribute:**

- 🐛 **Found a bug or error?** Open an [issue](../../issues) with the section name and what's wrong
- ✏️ **Want to improve an explanation?** Fork the repo, make your changes, and open a pull request
- 💡 **Have a topic idea?** Open an issue with the label `enhancement` and describe what's missing
- ⭐ **Found this useful?** Star the repo — it helps other QA engineers find it

**To contribute code or documentation:**

```bash
# 1. Fork this repository on GitHub

# 2. Clone your fork
git clone https://github.com/Mahanaj-Zaman

# 3. Create a new branch with a descriptive name
git checkout -b improve/section-4-locator-examples

# 4. Make your changes

# 5. Commit with a clear message
git commit -m "docs: add XPath locator examples to Section 4"

# 6. Push to your fork
git push origin improve/section-4-locator-examples

# 7. Open a Pull Request on GitHub
```

**Contribution guidelines:**
- Keep the tone consistent — plain language, no jargon without explanation
- Every code example must have inline comments explaining each line
- Test any code examples before submitting
- One topic per pull request keeps reviews focused

---

## 🔗 Connect With Me

I'm a QA Automation Engineer sharing everything I know about test automation, Playwright, and building quality engineering careers.

<div align="center">

[![LinkedIn](https://www.linkedin.com/in/mahanaj-zaman-marufa/)]

</div>

If this guide helped you land a job, level up your skills, or finally make sense of Playwright — I'd love to hear about it. Connect with me on LinkedIn and drop a message.

---

## 📄 License

This project is licensed under the **MIT License** — you are free to use, share, adapt, and build on this work for any purpose, including commercially, as long as you include the original license notice.

```
MIT License

Copyright (c) 2025 [Mahanaj Zaman Marufa]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

<div align="center">

Made with 🎭 for the QA engineering community

**If this helped you — please consider giving it a ⭐ — it helps other engineers find this resource.**

</div>
