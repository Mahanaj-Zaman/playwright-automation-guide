# 🎭 The Complete Playwright Guide
### From Zero to Intermediate — A Practical Reference for QA Engineers

---

> **Who is this for?**
> This guide is written for junior and mid-level QA engineers who want to learn Playwright from scratch. No prior experience with Playwright is required. Some basic familiarity with JavaScript and testing concepts will help, but every concept is explained from the ground up with real code examples.
>
> By the end of this guide, you will be able to install Playwright, write structured tests, use the Page Object Model, run tests in parallel, and test APIs — all with confidence.

---

## 📋 Table of Contents

1. [What is Playwright?](#1-what-is-playwright)
   - [What it is and why it exists](#what-it-is-and-why-it-exists)
   - [Problems Playwright solves](#problems-playwright-solves)
   - [Playwright vs Selenium vs Cypress](#playwright-vs-selenium-vs-cypress)
   - [Why companies use Playwright](#why-companies-use-playwright)

2. [Setting Up Playwright](#2-setting-up-playwright)
   - [Prerequisites](#prerequisites)
   - [Installation step by step](#installation-step-by-step)
   - [Project structure explained](#project-structure-explained)
   - [Config file breakdown](#config-file-breakdown)

3. [Core Concepts](#3-core-concepts)
   - [Browsers, Contexts, and Pages](#browsers-contexts-and-pages)
   - [How Playwright controls a browser](#how-playwright-controls-a-browser)

4. [Locators and Selectors](#4-locators-and-selectors)
   - [All locator types with examples](#all-locator-types-with-examples)
   - [Best practices for finding elements](#best-practices-for-finding-elements)
   - [What to avoid](#what-to-avoid)

5. [Actions](#5-actions)
   - [Click](#click)
   - [Fill](#fill)
   - [Hover](#hover)
   - [Select (Dropdowns)](#select-dropdowns)
   - [Keyboard Actions](#keyboard-actions)
   - [Other Common Actions](#other-common-actions)

6. [Assertions](#6-assertions)
   - [What assertions are and why they matter](#what-assertions-are-and-why-they-matter)
   - [All common assertions with examples](#all-common-assertions-with-examples)

7. [Writing Tests](#7-writing-tests)
   - [Test structure explained](#test-structure-explained)
   - [Writing your first test step by step](#writing-your-first-test-step-by-step)
   - [Running tests and reading results](#running-tests-and-reading-results)

8. [Page Object Model (POM)](#8-page-object-model-pom)
   - [What POM is and why you need it](#what-pom-is-and-why-you-need-it)
   - [Building a POM from scratch](#building-a-pom-from-scratch)

9. [Advanced Features](#9-advanced-features)
   - [API Testing with Playwright](#api-testing-with-playwright)
   - [Handling Authentication](#handling-authentication)
   - [Screenshots and Video Recording](#screenshots-and-video-recording)
   - [Parallel Test Execution](#parallel-test-execution)

10. [Real World Example](#10-real-world-example)
    - [Complete test suite for login and dashboard flow](#complete-test-suite-for-login-and-dashboard-flow)

---

## 1. What is Playwright?

### What it is and why it exists

**Playwright** is a modern, open-source end-to-end testing framework developed by **Microsoft**. It was released in 2020 and quickly became one of the most popular browser automation tools in the industry.

In simple terms: Playwright lets you write code that **controls a real web browser** — clicking buttons, filling out forms, navigating pages — just like a real user would. You can then add **assertions** to verify that the application behaves correctly.

**Why was it built?**

The Playwright team at Microsoft came from the same team that originally built Puppeteer at Google. They built Playwright to address real-world limitations they encountered with existing tools. The core goals were:

- Work across **all major browsers** (Chromium, Firefox, WebKit/Safari) with a single API
- Support **modern web patterns** out of the box (shadow DOM, iframes, network interception)
- Be **fast and reliable** with automatic waiting built in
- Run tests in **complete isolation** to prevent test interference
- Support **multiple programming languages** (JavaScript, TypeScript, Python, Java, C#)

---

### Problems Playwright solves

| Problem | How Playwright solves it |
|---|---|
| Tests are flaky (fail randomly) | Built-in auto-waiting — Playwright waits for elements to be ready before acting |
| Tests interfere with each other | Browser contexts provide complete isolation between tests |
| Only works in Chrome | Supports Chromium, Firefox, and WebKit natively |
| Hard to test modern web apps | Handles shadow DOM, iframes, service workers, and web sockets |
| Slow test execution | Parallel execution out of the box |
| Can't test APIs | Full HTTP request interception and API testing built in |
| Debugging is painful | Trace viewer, screenshot on failure, and video recording built in |

---

### Playwright vs Selenium vs Cypress

This is one of the most common questions asked by QA engineers. Here's an honest, practical comparison:

| Feature | Playwright | Selenium | Cypress |
|---|---|---|---|
| **Browser Support** | Chromium, Firefox, WebKit | All browsers | Chromium only (Firefox experimental) |
| **Language Support** | JS/TS, Python, Java, C# | All major languages | JavaScript/TypeScript only |
| **Auto-waiting** | ✅ Built-in | ❌ Manual waits required | ✅ Built-in |
| **Speed** | Fast | Slower | Fast |
| **Parallel Execution** | ✅ Native | ✅ With Selenium Grid | Limited (requires Dashboard) |
| **API Testing** | ✅ Built-in | ❌ Not built-in | ✅ Built-in |
| **Shadow DOM** | ✅ Full support | Limited | Limited |
| **Multiple Tabs** | ✅ Yes | ✅ Yes | ❌ No |
| **Network Interception** | ✅ Full | Limited | ✅ Yes |
| **Mobile Emulation** | ✅ Yes | Limited | Limited |
| **Debugging Tools** | Trace Viewer, Inspector | Limited | Time-travel debugging |
| **Setup Complexity** | Low | High | Low |
| **Community/Ecosystem** | Growing fast | Very mature | Mature |

**In plain English:**

- **Selenium** is the veteran — it's been around since 2004, works with every browser and language, but requires a lot of setup and manual waiting code. It's slower and more verbose.
- **Cypress** is developer-friendly, great for frontend teams, but only works in Chromium and can't handle multiple tabs or cross-origin requests well.
- **Playwright** hits a sweet spot — it's fast, cross-browser, has powerful built-in features, and requires minimal configuration. It's Microsoft's answer to the limitations of both tools above.

---

### Why companies use Playwright

Companies adopt Playwright for the following practical reasons:

1. **Cross-browser coverage** — A single test script runs on Chrome, Firefox, and Safari. No duplication.
2. **Reliability** — Auto-waiting means fewer flaky tests, which means less time debugging CI failures.
3. **Speed** — Tests run in parallel by default, cutting total test suite time significantly.
4. **TypeScript support** — Large engineering teams appreciate the type safety.
5. **Built-in tooling** — The Playwright Inspector, Trace Viewer, and code generator reduce the time to write and debug tests.
6. **API + UI testing** — One tool to test both your frontend and your backend API layer.
7. **Active development** — Microsoft actively maintains and improves it with frequent releases.

---

## 2. Setting Up Playwright

### Prerequisites

Before installing Playwright, make sure you have the following:

- **Node.js** version 16 or higher — [Download here](https://nodejs.org/)
- **npm** (comes with Node.js) or **yarn**
- A code editor — [VS Code](https://code.visualstudio.com/) is recommended
- A terminal / command line

Verify your Node.js installation:

```bash
# Check Node.js version — should be 16+
node --version

# Check npm version
npm --version
```

---

### Installation step by step

**Step 1 — Create a new project folder**

```bash
# Create a new directory for your project
mkdir my-playwright-project

# Navigate into it
cd my-playwright-project
```

**Step 2 — Initialize Playwright**

```bash
# This command installs Playwright and sets up the project interactively
npm init playwright@latest
```

You will be asked a series of questions in the terminal. Here's what each one means and what to select as a beginner:

```
Where to put your end-to-end tests? › tests
# Answer: tests (just press Enter — this is where your test files will live)

Add a GitHub Actions workflow? › false
# Answer: false for now (you can add CI later)

Install Playwright browsers? › true
# Answer: true — this downloads Chromium, Firefox, and WebKit to your machine
```

**Step 3 — Verify the installation**

After installation completes, run the example tests that Playwright generated:

```bash
# Run the example tests Playwright created for you
npx playwright test

# Open the HTML report to see results in the browser
npx playwright show-report
```

If tests pass and the report opens — you're all set!

---

### Project structure explained

After running `npm init playwright@latest`, your project will look like this:

```
my-playwright-project/
│
├── tests/                        ← Your test files live here
│   └── example.spec.ts           ← A sample test Playwright generated
│
├── tests-examples/               ← More complex example tests from Playwright
│   └── demo-todo-app.spec.ts
│
├── playwright.config.ts          ← The main configuration file (very important)
│
├── package.json                  ← Node.js project file with dependencies
│
└── node_modules/                 ← All installed packages (don't touch this)
```

**As your project grows, you'll add:**

```
my-playwright-project/
│
├── tests/
│   ├── login.spec.ts
│   ├── dashboard.spec.ts
│   └── checkout.spec.ts
│
├── pages/                        ← Page Object Model classes (covered in Section 8)
│   ├── LoginPage.ts
│   └── DashboardPage.ts
│
├── utils/                        ← Helper functions used across tests
│   └── helpers.ts
│
├── test-data/                    ← Test data files (JSON, CSV, etc.)
│   └── users.json
│
├── playwright.config.ts
└── package.json
```

---

### Config file breakdown

The `playwright.config.ts` file controls everything about how your tests run. Let's go through it line by line:

```typescript
// playwright.config.ts

import { defineConfig, devices } from '@playwright/test';
// defineConfig — wraps your config and provides type checking
// devices — a built-in list of browser/device presets (iPhone, iPad, etc.)

export default defineConfig({

  // ─── TEST DISCOVERY ────────────────────────────────────────────────────────
  
  testDir: './tests',
  // Playwright will look for test files ONLY inside the 'tests' folder

  // ─── TEST FILE PATTERN ─────────────────────────────────────────────────────
  
  // Playwright automatically picks up files matching: *.spec.ts or *.test.ts
  // You don't need to configure this unless you want a custom pattern

  // ─── PARALLEL EXECUTION ────────────────────────────────────────────────────
  
  fullyParallel: true,
  // Run all tests in all files at the same time (much faster)
  // Set to false if your tests depend on each other (not recommended)

  // ─── FAILURE BEHAVIOUR ─────────────────────────────────────────────────────
  
  forbidOnly: !!process.env.CI,
  // In CI environments, fail the build if someone committed a test.only()
  // test.only() is a debugging helper — it should never be committed to main

  retries: process.env.CI ? 2 : 0,
  // In CI: retry a failing test 2 times before marking it as failed
  // Locally: don't retry (you want to see failures immediately)

  workers: process.env.CI ? 1 : undefined,
  // In CI: run tests one at a time (safer for limited resources)
  // Locally: use as many CPU cores as available

  // ─── REPORTING ─────────────────────────────────────────────────────────────
  
  reporter: 'html',
  // Generate an HTML report after tests run
  // Other options: 'list', 'dot', 'json', 'junit'
  // You can combine: reporter: [['html'], ['list']]

  // ─── SHARED SETTINGS FOR ALL TESTS ─────────────────────────────────────────
  
  use: {
    
    baseURL: 'http://localhost:3000',
    // The base URL of the app you're testing
    // In your tests, you can then write: await page.goto('/login')
    // instead of: await page.goto('http://localhost:3000/login')

    trace: 'on-first-retry',
    // Record a trace (a detailed recording of everything that happened)
    // only when a test is being retried after a failure
    // Options: 'on', 'off', 'on-first-retry', 'retain-on-failure'

    screenshot: 'only-on-failure',
    // Take a screenshot automatically when a test fails
    // Options: 'on', 'off', 'only-on-failure'

    video: 'retain-on-failure',
    // Record video of the test browser session
    // Options: 'on', 'off', 'retain-on-failure', 'on-first-retry'

    headless: true,
    // Run browser without showing a visible window (faster for CI)
    // Set to false when debugging locally to watch the browser

    actionTimeout: 10000,
    // Maximum time (in milliseconds) for any single action like click, fill
    // If a click takes longer than 10 seconds, it will fail

    navigationTimeout: 30000,
    // Maximum time for page navigation (page.goto)
  },

  // ─── BROWSER PROJECTS ──────────────────────────────────────────────────────
  
  projects: [
    {
      name: 'chromium',
      // A human-readable name for this browser configuration
      use: { ...devices['Desktop Chrome'] },
      // Use the built-in Desktop Chrome device preset
    },

    {
      name: 'firefox',
      use: { ...devices['Desktop Firefox'] },
    },

    {
      name: 'webkit',
      // WebKit is the browser engine used by Safari
      use: { ...devices['Desktop Safari'] },
    },

    // ── Mobile Emulation Examples ────────────────────────────────────────────
    // Uncomment these to test on mobile viewports:
    
    // {
    //   name: 'Mobile Chrome',
    //   use: { ...devices['Pixel 5'] },
    // },
    // {
    //   name: 'Mobile Safari',
    //   use: { ...devices['iPhone 13'] },
    // },
  ],

  // ─── LOCAL DEV SERVER ──────────────────────────────────────────────────────
  
  // webServer: {
  //   command: 'npm run start',
  //   url: 'http://localhost:3000',
  //   reuseExistingServer: !process.env.CI,
  // },
  // Uncomment this if you want Playwright to start your app automatically
  // before running tests and shut it down when done
});
```

---

## 3. Core Concepts

### Browsers, Contexts, and Pages

Understanding these three objects is the most important foundation in Playwright. Everything you do will involve at least one of them.

Think of it like this:

```
Browser
  └── Browser Context (like an incognito window — isolated session)
        └── Page (a single browser tab)
```

**Browser**

The top-level object. A `Browser` instance represents a running browser application (Chromium, Firefox, or WebKit).

```typescript
import { chromium } from '@playwright/test';

// Launch a browser — this opens a real browser process
const browser = await chromium.launch();

// When you're done, close it
await browser.close();
```

> 💡 In normal tests you write with `test()`, you never interact with `Browser` directly. Playwright handles this for you. You only use it directly in advanced scripts outside of `test()`.

---

**Browser Context**

A `BrowserContext` is like an **incognito/private browsing session**. Each context is completely isolated from all others — separate cookies, storage, sessions, and cache.

Why this matters for testing:
- You can run **100 tests simultaneously** in 100 different contexts without them interfering
- You can simulate **multiple users** logged into the same app at the same time
- One test's login session will **never bleed into** another test

```typescript
// Create a new isolated browser context
const context = await browser.newContext({
  // Optional: simulate a mobile device
  viewport: { width: 390, height: 844 },
  
  // Optional: set a custom user agent string
  userAgent: 'Mozilla/5.0 (custom)',
  
  // Optional: grant permissions upfront
  permissions: ['geolocation'],
});

// Create a new page (tab) inside this context
const page = await context.newPage();

// Close the context when done — all pages inside it are also closed
await context.close();
```

---

**Page**

A `Page` represents a **single browser tab**. This is the object you will interact with the most. Every action you perform — clicking, typing, navigating — is done through a `page` object.

```typescript
// Navigate to a URL
await page.goto('https://example.com');

// Find an element and click it
await page.locator('button[type="submit"]').click();

// Type into an input field
await page.locator('#username').fill('john@example.com');

// Get the page title
const title = await page.title();

// Take a screenshot
await page.screenshot({ path: 'screenshot.png' });
```

---

### How Playwright controls a browser

When Playwright launches a browser, it communicates with it using the **Chrome DevTools Protocol (CDP)** for Chromium, and equivalent protocols for Firefox and WebKit. This is a low-level communication channel that allows code to:

- Navigate to URLs
- Find DOM elements
- Simulate user interactions (clicks, typing, scrolling)
- Intercept network requests
- Execute JavaScript directly in the page
- Read and set cookies and local storage

Here's a simplified picture of what happens when you run a Playwright test:

```
Your Test Code
      │
      │  (calls)
      ▼
Playwright Library
      │
      │  (speaks CDP / BiDi protocol over WebSocket)
      ▼
Browser Process (Chromium / Firefox / WebKit)
      │
      │  (renders)
      ▼
Your Web Application
```

**The auto-waiting mechanism** — one of Playwright's killer features:

When you write `await page.locator('button').click()`, Playwright doesn't just immediately send a click. It first:

1. Waits for the element to **exist** in the DOM
2. Waits for the element to be **visible** (not hidden or `display: none`)
3. Waits for the element to be **stable** (not animating or moving)
4. Waits for the element to be **enabled** (not disabled)
5. Waits for the element to **receive events** (not covered by another element)
6. **Then** performs the click

This is why Playwright tests are so much more reliable than older tools where you had to manually write `sleep(3000)` and hope the element was ready.

---

## 4. Locators and Selectors

A **locator** is how you tell Playwright which element on the page you want to interact with. Getting locators right is one of the most important skills in Playwright testing.

### All locator types with examples

**1. `getByRole` — Recommended first choice**

This finds elements by their ARIA role and accessible name. This is the most user-centric approach — you're finding elements the same way a screen reader or real user would.

```typescript
// Find a button with the visible text "Sign In"
await page.getByRole('button', { name: 'Sign In' }).click();

// Find a link with the text "Forgot password?"
await page.getByRole('link', { name: 'Forgot password?' }).click();

// Find a text input with the label "Email Address"
await page.getByRole('textbox', { name: 'Email Address' }).fill('test@example.com');

// Find a checkbox with the label "Remember me"
await page.getByRole('checkbox', { name: 'Remember me' }).check();

// Find a heading (h1, h2, etc.) with specific text
await page.getByRole('heading', { name: 'Welcome back' });

// Common ARIA roles you'll use:
// 'button', 'link', 'textbox', 'checkbox', 'radio', 'combobox',
// 'listbox', 'option', 'menuitem', 'tab', 'dialog', 'heading',
// 'img', 'table', 'row', 'cell', 'alert', 'status'
```

---

**2. `getByLabel` — Great for form inputs**

Finds an input element by its associated `<label>` text. This is how users identify form fields.

```typescript
// HTML: <label>Email</label><input type="email" />
await page.getByLabel('Email').fill('user@example.com');

// HTML: <label>Password</label><input type="password" />
await page.getByLabel('Password').fill('secret123');

// Works with aria-label too:
// HTML: <input aria-label="Search" type="text" />
await page.getByLabel('Search').fill('playwright');
```

---

**3. `getByPlaceholder` — For inputs with placeholder text**

Finds an input by its placeholder attribute.

```typescript
// HTML: <input placeholder="Enter your email address" />
await page.getByPlaceholder('Enter your email address').fill('test@test.com');

// HTML: <textarea placeholder="Write your message here..."></textarea>
await page.getByPlaceholder('Write your message here...').fill('Hello World');
```

---

**4. `getByText` — Find elements by their visible text**

Finds elements that contain specific visible text. Use this for paragraphs, labels, headings, list items, etc.

```typescript
// Find an element containing exactly "Welcome, John!"
await page.getByText('Welcome, John!');

// Find an element containing the text "Error" (partial match)
await page.getByText('Error', { exact: false });

// Use exact: true for exact full text match (default is false for getByText)
await page.getByText('Login successful', { exact: true });

// Click a menu item by its text
await page.getByText('Settings').click();

// Check that an error message is visible
await expect(page.getByText('Invalid credentials')).toBeVisible();
```

---

**5. `getByTestId` — Most stable for automation**

Finds elements by a `data-testid` attribute. Your development team adds these attributes specifically for testing. This is the most resilient locator because it doesn't break when the UI design changes.

```typescript
// HTML: <button data-testid="submit-login-btn">Login</button>
await page.getByTestId('submit-login-btn').click();

// HTML: <div data-testid="error-message">Invalid credentials</div>
await expect(page.getByTestId('error-message')).toBeVisible();

// HTML: <input data-testid="username-input" />
await page.getByTestId('username-input').fill('testuser');
```

> 💡 The default attribute is `data-testid`, but you can change it in your config:
> ```typescript
> // playwright.config.ts
> use: {
>   testIdAttribute: 'data-qa',  // Now getByTestId looks for data-qa="..."
> }
> ```

---

**6. `getByAltText` — For images**

Finds `<img>` elements by their `alt` attribute text.

```typescript
// HTML: <img alt="Company logo" src="logo.png" />
await page.getByAltText('Company logo').click();

// Verify a logo image is displayed
await expect(page.getByAltText('Company logo')).toBeVisible();
```

---

**7. `getByTitle` — For elements with a title attribute**

Finds elements by their `title` attribute (shown as a tooltip on hover).

```typescript
// HTML: <button title="Close dialog">X</button>
await page.getByTitle('Close dialog').click();

// HTML: <abbr title="HyperText Markup Language">HTML</abbr>
await page.getByTitle('HyperText Markup Language');
```

---

**8. `locator()` — CSS and XPath selectors**

The `locator()` method accepts CSS selectors and XPath expressions for when you need more specific targeting.

```typescript
// CSS selector — by ID
await page.locator('#login-button').click();

// CSS selector — by class
await page.locator('.error-message').waitFor();

// CSS selector — by attribute
await page.locator('input[type="email"]').fill('test@example.com');

// CSS selector — combined
await page.locator('form.login-form input[name="username"]').fill('john');

// XPath — use only when CSS doesn't work
await page.locator('//button[contains(text(), "Submit")]').click();

// Chaining locators — narrow down from a parent element
const loginForm = page.locator('form#login');
await loginForm.locator('input[name="email"]').fill('test@test.com');
// ^ This finds the email input INSIDE the login form only
```

---

**9. Filtering and chaining locators**

```typescript
// Filter by text when multiple elements match
await page.getByRole('listitem').filter({ hasText: 'Delete' }).click();
// ^ Gets all list items, then filters to ones containing "Delete"

// Filter by a child element
await page.getByRole('listitem')
  .filter({ has: page.getByRole('img', { name: 'avatar' }) })
  .first()
  .click();
// ^ Gets list items that contain an avatar image, then clicks the first one

// nth() — get a specific element from multiple matches
await page.getByRole('row').nth(2).click();
// ^ Gets the third row (0-indexed) — useful for tables

// first() and last()
await page.getByRole('button').first().click();
await page.getByRole('button').last().click();
```

---

### Best practices for finding elements

Follow this priority order when choosing a locator:

```
1. getByRole          — Best: mirrors how users interact
2. getByLabel         — Great for form elements
3. getByTestId        — Best for stability (requires dev cooperation)
4. getByPlaceholder   — Good for inputs without labels
5. getByText          — Good for non-interactive content
6. locator (CSS)      — Fallback when semantic locators don't work
7. locator (XPath)    — Last resort
```

**The golden rule:** If a human can find the element by looking at it (its label, its text, its role), use that. If not, ask your developers to add a `data-testid` attribute.

---

### What to avoid

```typescript
// ❌ AVOID: Fragile — breaks when CSS classes change (often done by developers)
await page.locator('.btn-primary-lg.mt-4.font-bold').click();

// ❌ AVOID: Long XPath — extremely brittle, breaks on any HTML restructure
await page.locator('/html/body/div[2]/form/div[1]/input').fill('test');

// ❌ AVOID: Overly generic — matches too many elements
await page.locator('div > p').click();

// ❌ AVOID: Using index on non-stable lists (list order can change)
await page.locator('li').nth(3).click();  // fragile if items are reordered

// ✅ PREFER: Stable, meaningful, readable
await page.getByRole('button', { name: 'Submit' }).click();
await page.getByLabel('Email address').fill('test@test.com');
await page.getByTestId('submit-btn').click();
```

---

## 5. Actions

Actions are the things you *do* to elements — clicking, typing, hovering, scrolling. Every action in Playwright automatically waits for the element to be ready before acting.

### Click

```typescript
// Basic click
await page.getByRole('button', { name: 'Login' }).click();

// Double click
await page.getByRole('cell', { name: 'Edit' }).dblclick();

// Right click (opens context menu)
await page.getByRole('img', { name: 'Profile photo' }).click({ button: 'right' });

// Click with modifier keys held down
await page.getByRole('link', { name: 'Dashboard' }).click({ modifiers: ['Control'] });
// ^ Ctrl+click to open in a new tab

// Click at a specific position within an element
await page.getByRole('slider').click({ position: { x: 50, y: 0 } });
// ^ Click at x=50, y=0 relative to the element's top-left corner

// Force a click even if the element is covered by something else
// Use sparingly — usually means something is wrong with your locator
await page.getByRole('button', { name: 'Hidden' }).click({ force: true });
```

---

### Fill

`fill()` is used to type text into input fields. It clears any existing value first, then types the new value.

```typescript
// Fill a text input
await page.getByLabel('Username').fill('johndoe');

// Fill a password input
await page.getByLabel('Password').fill('MySecretPassword123!');

// Fill a textarea
await page.getByLabel('Message').fill('This is a long message...');

// Fill and then clear (useful for testing empty state)
await page.getByLabel('Email').fill('wrong@email.com');
await page.getByLabel('Email').clear();  // Clears the field
await page.getByLabel('Email').fill('correct@email.com');

// Type slowly character by character (useful for autocomplete dropdowns)
await page.getByLabel('City').pressSequentially('New York', { delay: 100 });
// delay: 100 means 100ms pause between each character
```

---

### Hover

`hover()` moves the mouse over an element. Useful for revealing dropdown menus, tooltips, or hover states.

```typescript
// Hover over a menu item to reveal a dropdown
await page.getByRole('button', { name: 'Products' }).hover();

// Now click the revealed dropdown option
await page.getByRole('link', { name: 'Pricing Plans' }).click();

// Hover over an element to check that a tooltip appears
await page.getByRole('img', { name: 'Info' }).hover();
await expect(page.getByRole('tooltip')).toBeVisible();
```

---

### Select (Dropdowns)

For `<select>` elements (native HTML dropdowns), use `selectOption()`.

```typescript
// Select by visible text
await page.getByLabel('Country').selectOption('United States');

// Select by the option's value attribute
// HTML: <option value="us">United States</option>
await page.getByLabel('Country').selectOption({ value: 'us' });

// Select by the option's index (0 = first option)
await page.getByLabel('Country').selectOption({ index: 2 });

// Select multiple options (for multi-select dropdowns)
await page.getByLabel('Languages').selectOption(['JavaScript', 'Python', 'Go']);

// Verify the selected value
const selectedCountry = await page.getByLabel('Country').inputValue();
console.log(selectedCountry); // 'us'
```

> 💡 For custom dropdown components (built with `<div>` instead of `<select>`), you need to click the dropdown trigger, then click the option:
> ```typescript
> // Custom dropdown
> await page.getByRole('combobox', { name: 'Country' }).click(); // open it
> await page.getByRole('option', { name: 'United States' }).click(); // select
> ```

---

### Keyboard Actions

```typescript
// Press a single key
await page.getByLabel('Search').press('Enter');
// Other useful keys: 'Tab', 'Escape', 'ArrowDown', 'ArrowUp', 'Backspace', 'Delete'

// Press a keyboard shortcut (combination)
await page.keyboard.press('Control+A');  // Select all
await page.keyboard.press('Control+C');  // Copy
await page.keyboard.press('Control+V');  // Paste

// Type text using the keyboard (no clearing — appends to existing value)
await page.getByLabel('Search').click();
await page.keyboard.type('playwright automation');

// Tab through form fields
await page.getByLabel('First Name').fill('John');
await page.keyboard.press('Tab');  // Move focus to next field
await page.keyboard.type('Doe');   // Type in the next field (Last Name)
await page.keyboard.press('Tab');  // Move to Email field
await page.keyboard.type('john@example.com');

// Press a key while focused on a specific element
await page.getByRole('listbox').press('ArrowDown');  // Navigate list with arrow key
```

---

### Other Common Actions

```typescript
// ── CHECKING AND UNCHECKING ──────────────────────────────────────────────────

// Check a checkbox (makes it checked)
await page.getByLabel('Accept terms and conditions').check();

// Uncheck a checkbox
await page.getByLabel('Subscribe to newsletter').uncheck();

// Check a radio button
await page.getByLabel('Credit card').check();

// ── SCROLLING ────────────────────────────────────────────────────────────────

// Scroll the page down to the bottom
await page.evaluate(() => window.scrollTo(0, document.body.scrollHeight));

// Scroll a specific element into view
await page.getByTestId('footer-section').scrollIntoViewIfNeeded();

// Scroll by a specific number of pixels
await page.mouse.wheel(0, 500);  // Scroll down 500px

// ── FILE UPLOAD ──────────────────────────────────────────────────────────────

// Upload a file to a file input
await page.getByLabel('Upload document').setInputFiles('path/to/file.pdf');

// Upload multiple files
await page.getByLabel('Upload photos').setInputFiles([
  'photo1.jpg',
  'photo2.jpg',
]);

// Clear a file input
await page.getByLabel('Upload document').setInputFiles([]);

// ── DRAG AND DROP ────────────────────────────────────────────────────────────

// Drag one element and drop onto another
await page.getByTestId('draggable-card').dragTo(page.getByTestId('drop-zone'));

// ── WAITING ──────────────────────────────────────────────────────────────────

// Wait for an element to appear (explicit wait)
await page.getByTestId('loading-spinner').waitFor({ state: 'hidden' });
// ^ Waits until the spinner disappears

// Wait for navigation to complete after an action
await Promise.all([
  page.waitForURL('**/dashboard'),   // Wait for URL to change
  page.getByRole('button', { name: 'Login' }).click(),  // Trigger navigation
]);

// Wait for a network request to complete
await Promise.all([
  page.waitForResponse('**/api/user'),   // Wait for this API call
  page.getByRole('button', { name: 'Save' }).click(),
]);
```

---

## 6. Assertions

### What assertions are and why they matter

An **assertion** is a statement that checks whether something is true. Without assertions, a test that clicks through an entire flow but never verifies the results is worthless — it would pass even if your app was completely broken.

Think of assertions as your **checkpoints**:

> "After I click Login, I assert that the dashboard heading is visible."
> "After I submit the form, I assert that the success message appears."
> "After I delete an item, I assert that it no longer exists in the list."

Playwright uses `expect()` for all assertions. It has two modes:

- **`await expect(locator).toBeVisible()`** — Locator-based assertions (most common)
- **`await expect(value).toBe(something)`** — Value-based assertions

Playwright's `expect()` is **auto-retrying** — if an assertion fails, it keeps retrying until it passes or a timeout is reached (default: 5 seconds). This eliminates flaky test failures caused by elements loading slowly.

---

### All common assertions with examples

**Visibility and Existence**

```typescript
// Assert an element is visible on the page
await expect(page.getByText('Welcome back, John!')).toBeVisible();

// Assert an element is hidden (exists in DOM but not visible)
await expect(page.getByTestId('loading-spinner')).toBeHidden();

// Assert an element is attached to the DOM (may or may not be visible)
await expect(page.getByTestId('modal-dialog')).toBeAttached();

// Assert an element does NOT exist in the DOM at all
await expect(page.getByTestId('deleted-item')).not.toBeAttached();
// Note: .not inverts any assertion
```

---

**Text Content**

```typescript
// Assert an element has exact text
await expect(page.getByRole('heading', { level: 1 })).toHaveText('Dashboard');

// Assert an element contains some text (partial match)
await expect(page.getByTestId('user-greeting')).toContainText('John');

// Assert the page title
await expect(page).toHaveTitle('My App — Dashboard');

// Assert the page URL
await expect(page).toHaveURL('https://myapp.com/dashboard');

// Assert URL contains a pattern
await expect(page).toHaveURL(/.*dashboard.*/);
// ^ Uses a regular expression for flexible URL matching
```

---

**Input and Form State**

```typescript
// Assert the current value of a text input
await expect(page.getByLabel('Email')).toHaveValue('test@example.com');

// Assert a checkbox is checked
await expect(page.getByLabel('Remember me')).toBeChecked();

// Assert a checkbox is NOT checked
await expect(page.getByLabel('Newsletter')).not.toBeChecked();

// Assert an input is empty
await expect(page.getByLabel('Search')).toHaveValue('');

// Assert an element is disabled
await expect(page.getByRole('button', { name: 'Submit' })).toBeDisabled();

// Assert an element is enabled
await expect(page.getByRole('button', { name: 'Submit' })).toBeEnabled();
```

---

**Counts and Lists**

```typescript
// Assert the number of elements matching a locator
await expect(page.getByRole('listitem')).toHaveCount(5);
// ^ Verifies there are exactly 5 list items

// Assert an element has a specific CSS class
await expect(page.getByRole('button', { name: 'Active' })).toHaveClass(/active/);

// Assert an element has a specific attribute
await expect(page.getByRole('link', { name: 'Profile' })).toHaveAttribute('href', '/profile');

// Assert an element has a CSS property
await expect(page.getByTestId('success-banner')).toHaveCSS('background-color', 'rgb(0, 128, 0)');
```

---

**Soft Assertions — Continue after failure**

Normally, when an assertion fails, the test stops immediately. **Soft assertions** let you collect multiple failures and report them all at once at the end.

```typescript
// Soft assertions — the test continues even if these fail
await expect.soft(page.getByTestId('first-name')).toHaveValue('John');
await expect.soft(page.getByTestId('last-name')).toHaveValue('Doe');
await expect.soft(page.getByTestId('email')).toHaveValue('john@example.com');

// All failures above are reported together at the end
// This is useful for form validation checks where you want to see all issues
```

---

**Value-based assertions**

```typescript
// Assert a JavaScript value equals something
const count = await page.getByRole('listitem').count();
expect(count).toBe(5);           // exact equality
expect(count).toBeGreaterThan(0); // greater than
expect(count).toBeLessThan(10);   // less than

// Assert a string
const title = await page.title();
expect(title).toBe('Dashboard — MyApp');
expect(title).toContain('Dashboard');
expect(title).toMatch(/MyApp/);  // regex match

// Assert truthiness
const isVisible = await page.getByTestId('alert').isVisible();
expect(isVisible).toBeTruthy();
expect(isVisible).toBeFalsy();  // opposite
```

---

## 7. Writing Tests

### Test structure explained

A Playwright test file has a clear structure. Here's the anatomy of a test file:

```typescript
// tests/login.spec.ts

import { test, expect } from '@playwright/test';
// test — the function you use to define a test case
// expect — the function you use for assertions

// ── TEST SUITE (group of related tests) ────────────────────────────────────
test.describe('Login Page', () => {
  // All tests inside here share a common context: "Login Page"
  // This creates a logical group in your test reports

  // ── HOOKS ───────────────────────────────────────────────────────────────
  
  test.beforeEach(async ({ page }) => {
    // This runs BEFORE EACH test in this describe block
    // Common use: navigate to the page under test
    await page.goto('/login');
  });

  test.afterEach(async ({ page }) => {
    // This runs AFTER EACH test
    // Common use: cleanup (though Playwright's isolation usually handles this)
  });

  test.beforeAll(async () => {
    // Runs ONCE before all tests in this describe block
    // Common use: set up shared resources (database seeding, auth tokens)
  });

  test.afterAll(async () => {
    // Runs ONCE after all tests in this describe block
    // Common use: tear down shared resources
  });

  // ── TEST CASES ──────────────────────────────────────────────────────────
  
  test('should display the login form', async ({ page }) => {
    // { page } is a fixture — Playwright injects this automatically
    // Each test gets a fresh page in an isolated browser context
    
    // Assertions
    await expect(page.getByRole('heading', { name: 'Sign In' })).toBeVisible();
    await expect(page.getByLabel('Email')).toBeVisible();
    await expect(page.getByLabel('Password')).toBeVisible();
    await expect(page.getByRole('button', { name: 'Login' })).toBeVisible();
  });

  test('should log in with valid credentials', async ({ page }) => {
    await page.getByLabel('Email').fill('user@example.com');
    await page.getByLabel('Password').fill('password123');
    await page.getByRole('button', { name: 'Login' }).click();

    // Assert we landed on the dashboard
    await expect(page).toHaveURL('/dashboard');
    await expect(page.getByRole('heading', { name: 'Dashboard' })).toBeVisible();
  });

  test('should show error for invalid credentials', async ({ page }) => {
    await page.getByLabel('Email').fill('wrong@example.com');
    await page.getByLabel('Password').fill('wrongpassword');
    await page.getByRole('button', { name: 'Login' }).click();

    // Assert error message appears
    await expect(page.getByText('Invalid email or password')).toBeVisible();
    
    // Assert we did NOT navigate away from login
    await expect(page).toHaveURL('/login');
  });
});
```

**Available fixtures:**

```typescript
test('example', async ({ page, browser, context, request }) => {
  // page    — A fresh browser page (tab)
  // browser — The browser instance
  // context — The browser context (isolated session)
  // request — For making HTTP API requests (covered in Section 9)
});
```

---

### Writing your first test step by step

Let's write a real test from scratch, step by step, against `https://demo.playwright.dev/todomvc` — a public demo app.

**Step 1 — Create the test file**

```bash
touch tests/todo.spec.ts
```

**Step 2 — Import what you need**

```typescript
// tests/todo.spec.ts

import { test, expect } from '@playwright/test';
// Always start with this import
```

**Step 3 — Create a describe block**

```typescript
import { test, expect } from '@playwright/test';

test.describe('Todo App', () => {
  // All our todo tests will go here
});
```

**Step 4 — Navigate to the page before each test**

```typescript
import { test, expect } from '@playwright/test';

test.describe('Todo App', () => {

  test.beforeEach(async ({ page }) => {
    // Navigate to the todo app before each test
    await page.goto('https://demo.playwright.dev/todomvc');
  });

});
```

**Step 5 — Write the first test case**

```typescript
import { test, expect } from '@playwright/test';

test.describe('Todo App', () => {

  test.beforeEach(async ({ page }) => {
    await page.goto('https://demo.playwright.dev/todomvc');
  });

  test('should create a new todo item', async ({ page }) => {
    // Step 1: Find the input field where you type new todos
    const todoInput = page.getByPlaceholder('What needs to be done?');

    // Step 2: Type a new todo item
    await todoInput.fill('Buy groceries');

    // Step 3: Press Enter to add it to the list
    await todoInput.press('Enter');

    // Step 4: Assert the new item appears in the list
    await expect(page.getByRole('listitem').filter({ hasText: 'Buy groceries' })).toBeVisible();

    // Step 5: Assert the item count shows 1
    await expect(page.getByText('1 item left')).toBeVisible();
  });

  test('should mark a todo item as complete', async ({ page }) => {
    // Setup: Add a todo first
    await page.getByPlaceholder('What needs to be done?').fill('Write tests');
    await page.getByPlaceholder('What needs to be done?').press('Enter');

    // Action: Click the checkbox next to the todo to complete it
    await page.getByRole('listitem').filter({ hasText: 'Write tests' })
      .getByRole('checkbox')
      .check();

    // Assert: The item now has a 'completed' styling
    await expect(
      page.getByRole('listitem').filter({ hasText: 'Write tests' })
    ).toHaveClass(/completed/);
  });

  test('should delete a todo item', async ({ page }) => {
    // Setup: Add a todo
    await page.getByPlaceholder('What needs to be done?').fill('Delete me');
    await page.getByPlaceholder('What needs to be done?').press('Enter');

    // Action: Hover over the item to reveal the delete button, then click it
    const todoItem = page.getByRole('listitem').filter({ hasText: 'Delete me' });
    await todoItem.hover();
    await todoItem.getByRole('button', { name: 'Delete' }).click();

    // Assert: The item is gone
    await expect(page.getByText('Delete me')).not.toBeVisible();
  });

});
```

---

### Running tests and reading results

**Basic commands:**

```bash
# Run ALL tests
npx playwright test

# Run a specific test file
npx playwright test tests/todo.spec.ts

# Run tests matching a specific name (uses regex)
npx playwright test --grep "should create"

# Run tests in a specific browser only
npx playwright test --project=chromium

# Run tests in headed mode (you can watch the browser)
npx playwright test --headed

# Run with debug mode (pauses at each step — great for writing tests)
npx playwright test --debug

# Run with UI mode (interactive test runner — highly recommended)
npx playwright test --ui
```

**Reading the terminal output:**

```
Running 3 tests using 3 workers

  ✓  1 [chromium] › todo.spec.ts:10:3 › Todo App › should create a new todo item (2.1s)
  ✓  2 [chromium] › todo.spec.ts:24:3 › Todo App › should mark a todo item as complete (1.8s)
  ✗  3 [chromium] › todo.spec.ts:38:3 › Todo App › should delete a todo item (3.2s)

  1 failed
    [chromium] › todo.spec.ts:38:3 › Todo App › should delete a todo item

  Error: Timed out 5000ms waiting for expect(locator).not.toBeVisible()
  Received element is visible

  Call log:
  - expect.not.toBeVisible with timeout 5000ms
  - waiting for locator('text=Delete me') to be hidden
```

Reading this:
- `✓` = test passed
- `✗` = test failed
- The error tells you exactly which assertion failed and why
- The file path and line number help you find it instantly

**View the HTML report:**

```bash
npx playwright show-report
```

This opens a visual report in your browser with:
- Pass/fail status for every test
- Time taken per test
- Screenshots of failures
- Trace files you can explore step by step

---

## 8. Page Object Model (POM)

### What POM is and why you need it

The **Page Object Model** is a design pattern that separates your **test logic** from your **page interaction code**.

The core idea: create a class for each page in your application. That class contains all the locators and actions for that page. Your tests then use these classes instead of raw locators.

**Without POM — the painful way:**

Imagine you have the login button on 15 different test files:

```typescript
// test1.spec.ts
await page.getByRole('button', { name: 'Sign In' }).click();

// test2.spec.ts
await page.getByRole('button', { name: 'Sign In' }).click();

// test3.spec.ts
await page.getByRole('button', { name: 'Sign In' }).click();
// ... 12 more files
```

Now your developer changes the button text to "Log In". You have to update 15 files. 🤦

**With POM — the smart way:**

```typescript
// pages/LoginPage.ts
class LoginPage {
  loginButton = this.page.getByRole('button', { name: 'Sign In' });
  
  async clickLogin() {
    await this.loginButton.click();
  }
}

// All 15 test files use:
await loginPage.clickLogin();

// Button text changes? Update ONE place. Done.
```

**Benefits of POM:**
- **Maintainability** — one change in one place instead of many files
- **Readability** — tests read like plain English business scenarios
- **Reusability** — share page actions across multiple test files
- **Separation of concerns** — test logic is separate from UI interaction code

---

### Building a POM from scratch

Let's build a complete Page Object Model for a login and dashboard flow.

**Step 1 — Create the pages directory**

```bash
mkdir pages
```

**Step 2 — Build the LoginPage class**

```typescript
// pages/LoginPage.ts

import { Page, Locator } from '@playwright/test';
// Page  — type for the Playwright page object
// Locator — type for locators (used for type safety)

export class LoginPage {
  // ── PROPERTIES ──────────────────────────────────────────────────────────
  // Store the page reference so all methods can use it
  readonly page: Page;

  // Define all locators as class properties
  // This is where all selectors for this page live — one place to update
  readonly emailInput: Locator;
  readonly passwordInput: Locator;
  readonly loginButton: Locator;
  readonly errorMessage: Locator;
  readonly forgotPasswordLink: Locator;
  readonly rememberMeCheckbox: Locator;

  // ── CONSTRUCTOR ─────────────────────────────────────────────────────────
  constructor(page: Page) {
    // Receive the page object from the test
    this.page = page;

    // Initialize all locators
    // Locators are lazy — they don't search the DOM until you use them
    this.emailInput = page.getByLabel('Email');
    this.passwordInput = page.getByLabel('Password');
    this.loginButton = page.getByRole('button', { name: 'Sign In' });
    this.errorMessage = page.getByTestId('login-error-message');
    this.forgotPasswordLink = page.getByRole('link', { name: 'Forgot your password?' });
    this.rememberMeCheckbox = page.getByLabel('Remember me');
  }

  // ── ACTIONS ─────────────────────────────────────────────────────────────
  // Each method represents a user action or workflow on this page

  async goto() {
    // Navigate to the login page
    await this.page.goto('/login');
  }

  async fillEmail(email: string) {
    // Fill the email field with the provided email
    await this.emailInput.fill(email);
  }

  async fillPassword(password: string) {
    // Fill the password field
    await this.passwordInput.fill(password);
  }

  async clickLogin() {
    // Click the login button
    await this.loginButton.click();
  }

  async login(email: string, password: string) {
    // A convenience method — performs the entire login flow in one call
    // This is the most commonly used method
    await this.fillEmail(email);
    await this.fillPassword(password);
    await this.clickLogin();
  }

  async getErrorMessage(): Promise<string | null> {
    // Return the text of the error message
    // Useful when you want to assert specific error content in your test
    return await this.errorMessage.textContent();
  }

  async checkRememberMe() {
    // Check the "Remember me" checkbox
    await this.rememberMeCheckbox.check();
  }

  async clickForgotPassword() {
    // Click the forgot password link
    await this.forgotPasswordLink.click();
  }
}
```

**Step 3 — Build the DashboardPage class**

```typescript
// pages/DashboardPage.ts

import { Page, Locator } from '@playwright/test';

export class DashboardPage {
  readonly page: Page;

  // Locators for all elements on the dashboard
  readonly welcomeHeading: Locator;
  readonly userMenu: Locator;
  readonly logoutButton: Locator;
  readonly notificationsIcon: Locator;
  readonly searchBar: Locator;
  readonly sidebarNavigation: Locator;

  constructor(page: Page) {
    this.page = page;

    this.welcomeHeading = page.getByRole('heading', { name: /Welcome/ });
    // ^ Uses a regex — matches "Welcome, John!" or "Welcome back!" etc.
    
    this.userMenu = page.getByTestId('user-menu');
    this.logoutButton = page.getByRole('menuitem', { name: 'Logout' });
    this.notificationsIcon = page.getByRole('button', { name: 'Notifications' });
    this.searchBar = page.getByRole('searchbox');
    this.sidebarNavigation = page.getByRole('navigation', { name: 'Sidebar' });
  }

  async goto() {
    await this.page.goto('/dashboard');
  }

  async getUserGreeting(): Promise<string | null> {
    // Return the text of the welcome heading
    return await this.welcomeHeading.textContent();
  }

  async openUserMenu() {
    // Click the user menu to reveal options
    await this.userMenu.click();
  }

  async logout() {
    // Open the menu, then click logout
    await this.openUserMenu();
    await this.logoutButton.click();
  }

  async searchFor(query: string) {
    // Click the search bar and type a query
    await this.searchBar.click();
    await this.searchBar.fill(query);
    await this.searchBar.press('Enter');
  }

  async navigateTo(section: string) {
    // Click a navigation item in the sidebar by its name
    await this.sidebarNavigation.getByRole('link', { name: section }).click();
  }
}
```

**Step 4 — Use the Page Objects in tests**

```typescript
// tests/auth.spec.ts

import { test, expect } from '@playwright/test';
import { LoginPage } from '../pages/LoginPage';
import { DashboardPage } from '../pages/DashboardPage';

test.describe('Authentication', () => {
  let loginPage: LoginPage;
  let dashboardPage: DashboardPage;

  test.beforeEach(async ({ page }) => {
    // Create fresh instances of our page objects for each test
    loginPage = new LoginPage(page);
    dashboardPage = new DashboardPage(page);

    // Navigate to login before each test
    await loginPage.goto();
  });

  test('successful login takes user to dashboard', async ({ page }) => {
    // The test reads like a business scenario now — clean and clear
    await loginPage.login('user@example.com', 'correctpassword');

    // Assert: we're on the dashboard with a welcome message
    await expect(page).toHaveURL('/dashboard');
    await expect(dashboardPage.welcomeHeading).toBeVisible();
  });

  test('invalid credentials show error message', async () => {
    await loginPage.login('user@example.com', 'wrongpassword');

    await expect(loginPage.errorMessage).toBeVisible();
    await expect(loginPage.errorMessage).toContainText('Invalid credentials');
  });

  test('user can log out from dashboard', async ({ page }) => {
    // Login first
    await loginPage.login('user@example.com', 'correctpassword');

    // Then log out
    await dashboardPage.logout();

    // Should be back at login page
    await expect(page).toHaveURL('/login');
  });
});
```

Notice how clean and readable the tests are now. A non-technical person can understand what each test is doing just by reading it.

---

## 9. Advanced Features

### API Testing with Playwright

Playwright can make HTTP requests directly without a browser. This is useful for:

- Setting up test data before a UI test
- Verifying backend state after a UI action
- Writing fast API-only tests

```typescript
// tests/api/users.spec.ts

import { test, expect } from '@playwright/test';

test.describe('Users API', () => {

  test('GET /api/users returns a list of users', async ({ request }) => {
    // request is a Playwright APIRequestContext — like a built-in HTTP client

    // Make a GET request
    const response = await request.get('https://reqres.in/api/users');

    // Assert the response status is 200 OK
    expect(response.status()).toBe(200);

    // Parse the JSON response body
    const body = await response.json();

    // Assert the response structure
    expect(body.data).toBeDefined();     // The 'data' field exists
    expect(body.data.length).toBeGreaterThan(0);  // It has at least one user
    expect(body.data[0]).toHaveProperty('email'); // Each user has an email field
  });

  test('POST /api/users creates a new user', async ({ request }) => {
    // Make a POST request with a JSON body
    const response = await request.post('https://reqres.in/api/users', {
      data: {
        // This is the request body — sent as JSON automatically
        name: 'John Doe',
        job: 'QA Engineer',
      },
    });

    // Assert 201 Created
    expect(response.status()).toBe(201);

    const body = await response.json();

    // Assert the created user has the right data
    expect(body.name).toBe('John Doe');
    expect(body.job).toBe('QA Engineer');
    expect(body.id).toBeDefined();  // Server assigned an ID
  });

  test('API with authentication header', async ({ request }) => {
    // Make an authenticated request
    const response = await request.get('https://api.example.com/protected', {
      headers: {
        // Pass an auth token in the headers
        'Authorization': 'Bearer my-auth-token-here',
        'Content-Type': 'application/json',
      },
    });

    expect(response.status()).toBe(200);
  });

  test('combine API setup with UI test', async ({ page, request }) => {
    // Step 1: Create a user via API (fast — no browser needed)
    const createResponse = await request.post('/api/users', {
      data: { email: 'newuser@test.com', password: 'test123' },
    });
    expect(createResponse.status()).toBe(201);

    // Step 2: Log in via the UI (browser needed for visual testing)
    await page.goto('/login');
    await page.getByLabel('Email').fill('newuser@test.com');
    await page.getByLabel('Password').fill('test123');
    await page.getByRole('button', { name: 'Login' }).click();

    await expect(page).toHaveURL('/dashboard');

    // Step 3: Clean up via API (fast)
    const { id } = await createResponse.json();
    await request.delete(`/api/users/${id}`);
  });

});
```

---

### Handling Authentication

Logging in before every test is slow. Playwright provides **storageState** to save and reuse authentication sessions.

**Step 1 — Create a global setup file that logs in once**

```typescript
// global-setup.ts

import { chromium, FullConfig } from '@playwright/test';

async function globalSetup(config: FullConfig) {
  // Launch a browser just for setup
  const browser = await chromium.launch();
  const page = await browser.newPage();

  // Navigate to login and authenticate
  await page.goto('http://localhost:3000/login');
  await page.getByLabel('Email').fill('admin@example.com');
  await page.getByLabel('Password').fill('adminpassword');
  await page.getByRole('button', { name: 'Login' }).click();

  // Wait until we're logged in (URL changes to dashboard)
  await page.waitForURL('**/dashboard');

  // Save the browser state (cookies, localStorage, sessionStorage)
  // to a file — this is the "logged in" session
  await page.context().storageState({ path: 'auth-state.json' });

  await browser.close();
}

export default globalSetup;
```

**Step 2 — Configure Playwright to use the global setup and the saved state**

```typescript
// playwright.config.ts

export default defineConfig({
  globalSetup: './global-setup',
  // ^ Run global-setup.ts once before all tests begin

  use: {
    storageState: 'auth-state.json',
    // ^ Every test will start with this saved session (already logged in!)
  },
});
```

**Step 3 — Write tests that start already logged in**

```typescript
// tests/dashboard.spec.ts

import { test, expect } from '@playwright/test';

test('dashboard loads for logged-in user', async ({ page }) => {
  // No login steps needed! The session is already restored from auth-state.json
  await page.goto('/dashboard');

  await expect(page.getByRole('heading', { name: 'Dashboard' })).toBeVisible();
});
```

**Alternative: Using test fixtures for role-based auth**

```typescript
// fixtures.ts — define multiple user roles

import { test as base } from '@playwright/test';

type UserRole = 'admin' | 'standard';

const test = base.extend<{ userRole: UserRole }>({
  userRole: ['standard', { option: true }],

  page: async ({ browser, userRole }, use) => {
    // Load different saved sessions based on role
    const context = await browser.newContext({
      storageState: `auth-state-${userRole}.json`,
    });
    const page = await context.newPage();
    await use(page);
    await context.close();
  },
});

export { test };
```

---

### Screenshots and Video Recording

**Manual screenshots in tests:**

```typescript
test('capture screenshot at specific points', async ({ page }) => {
  await page.goto('/dashboard');

  // Take a full-page screenshot
  await page.screenshot({ path: 'screenshots/dashboard-full.png', fullPage: true });

  // Take a screenshot of a specific element only
  await page.getByTestId('stats-widget').screenshot({ path: 'screenshots/stats.png' });

  // Screenshot on a failed assertion (for debugging)
  try {
    await expect(page.getByText('Expected text')).toBeVisible({ timeout: 3000 });
  } catch (error) {
    await page.screenshot({ path: 'screenshots/failure.png' });
    throw error;  // Re-throw so the test still fails
  }
});
```

**Configure automatic screenshots and video in config:**

```typescript
// playwright.config.ts

use: {
  // Screenshot options:
  screenshot: 'only-on-failure',  // 'on' | 'off' | 'only-on-failure'

  // Video options:
  video: 'retain-on-failure',     // 'on' | 'off' | 'retain-on-failure' | 'on-first-retry'

  // Trace options (step-by-step recording with screenshots and network logs):
  trace: 'on-first-retry',        // 'on' | 'off' | 'on-first-retry' | 'retain-on-failure'
}
```

**Viewing a trace:**

```bash
# After a test fails, open the trace viewer
npx playwright show-trace trace.zip
```

The trace viewer shows you every step of the test with:
- A timeline of actions
- Before/after screenshots for every step
- Network requests that were made
- Console logs
- The exact point of failure

---

### Parallel Test Execution

Playwright runs tests in parallel by default. Here's how to control it:

**File-level parallelism (default):**

By default, different test files run in parallel. Tests within a single file run sequentially.

```typescript
// playwright.config.ts
export default defineConfig({
  fullyParallel: false,
  // ^ Files run in parallel (default)
  // Set to true to also parallelize tests within the same file
  
  workers: 4,
  // ^ Run up to 4 tests simultaneously
  // Default: uses all available CPU cores
});
```

**Controlling parallelism per file:**

```typescript
// tests/sequential.spec.ts

// Force all tests in this file to run one after another
// Use this when tests depend on each other (try to avoid this)
test.describe.configure({ mode: 'serial' });

test('step 1', async ({ page }) => { /* ... */ });
test('step 2', async ({ page }) => { /* ... */ });
test('step 3', async ({ page }) => { /* ... */ });
```

**Running in parallel explicitly:**

```typescript
// tests/parallel.spec.ts

// Force all tests in this file to run in parallel (even if fullyParallel is false)
test.describe.configure({ mode: 'parallel' });

test('independent test 1', async ({ page }) => { /* ... */ });
test('independent test 2', async ({ page }) => { /* ... */ });
test('independent test 3', async ({ page }) => { /* ... */ });
```

**Sharding — for large test suites across multiple machines:**

```bash
# Machine 1 — run the first half
npx playwright test --shard=1/2

# Machine 2 — run the second half
npx playwright test --shard=2/2

# This is how you scale test execution in CI with multiple runners
```

---

## 10. Real World Example

### Complete test suite for a login and dashboard flow

This is a complete, production-style test suite. It brings together everything from this guide: Page Object Model, authentication handling, API setup, assertions, and multiple test scenarios.

**The application under test:**
- A web app with login, dashboard, profile page, and settings

**File structure for this example:**

```
tests/
  real-world/
    login.spec.ts
    dashboard.spec.ts
    profile.spec.ts
pages/
  LoginPage.ts
  DashboardPage.ts
  ProfilePage.ts
test-data/
  users.json
```

---

**Test data file:**

```json
// test-data/users.json
{
  "validUser": {
    "email": "testuser@example.com",
    "password": "TestPass123!",
    "name": "Test User"
  },
  "adminUser": {
    "email": "admin@example.com",
    "password": "AdminPass123!",
    "name": "Admin User"
  },
  "invalidUser": {
    "email": "invalid@example.com",
    "password": "wrongpassword"
  }
}
```

---

**ProfilePage class:**

```typescript
// pages/ProfilePage.ts

import { Page, Locator } from '@playwright/test';

export class ProfilePage {
  readonly page: Page;

  readonly pageHeading: Locator;
  readonly nameInput: Locator;
  readonly emailDisplay: Locator;
  readonly saveButton: Locator;
  readonly successToast: Locator;
  readonly avatarImage: Locator;

  constructor(page: Page) {
    this.page = page;

    this.pageHeading = page.getByRole('heading', { name: 'My Profile' });
    this.nameInput = page.getByLabel('Full Name');
    this.emailDisplay = page.getByTestId('email-display');
    this.saveButton = page.getByRole('button', { name: 'Save Changes' });
    this.successToast = page.getByRole('alert').filter({ hasText: 'Profile updated successfully' });
    this.avatarImage = page.getByRole('img', { name: 'Profile avatar' });
  }

  async goto() {
    await this.page.goto('/profile');
  }

  async updateName(newName: string) {
    await this.nameInput.clear();
    await this.nameInput.fill(newName);
  }

  async saveChanges() {
    await this.saveButton.click();
  }

  async updateProfile(newName: string) {
    await this.updateName(newName);
    await this.saveChanges();
    // Wait for the success toast to appear
    await this.successToast.waitFor({ state: 'visible' });
  }
}
```

---

**Complete login test suite:**

```typescript
// tests/real-world/login.spec.ts

import { test, expect } from '@playwright/test';
import { LoginPage } from '../../pages/LoginPage';
import { DashboardPage } from '../../pages/DashboardPage';
import users from '../../test-data/users.json';
// Import test data — one source of truth for test credentials

test.describe('Login Flow', () => {
  let loginPage: LoginPage;
  let dashboardPage: DashboardPage;

  test.beforeEach(async ({ page }) => {
    loginPage = new LoginPage(page);
    dashboardPage = new DashboardPage(page);
    await loginPage.goto();
  });

  // ── POSITIVE TESTS ──────────────────────────────────────────────────────

  test('should render the login page correctly', async ({ page }) => {
    // Verify all essential elements are present
    await expect(page).toHaveTitle(/Sign In/);
    await expect(loginPage.emailInput).toBeVisible();
    await expect(loginPage.passwordInput).toBeVisible();
    await expect(loginPage.loginButton).toBeVisible();
    await expect(loginPage.forgotPasswordLink).toBeVisible();

    // Verify the login button is enabled (not disabled by default)
    await expect(loginPage.loginButton).toBeEnabled();
  });

  test('should successfully log in with valid credentials', async ({ page }) => {
    await loginPage.login(users.validUser.email, users.validUser.password);

    // Assert: redirected to dashboard
    await expect(page).toHaveURL(/.*dashboard.*/);

    // Assert: welcome message shows user's name
    await expect(dashboardPage.welcomeHeading).toContainText(users.validUser.name);

    // Assert: user menu shows the user's email
    await dashboardPage.openUserMenu();
    await expect(page.getByText(users.validUser.email)).toBeVisible();
  });

  test('should remember user when "Remember me" is checked', async ({ page, context }) => {
    await loginPage.checkRememberMe();
    await loginPage.login(users.validUser.email, users.validUser.password);

    await expect(page).toHaveURL(/.*dashboard.*/);

    // Check that a persistent cookie was set
    const cookies = await context.cookies();
    const authCookie = cookies.find(c => c.name === 'auth_token');
    
    expect(authCookie).toBeDefined();
    expect(authCookie?.expires).toBeGreaterThan(0);
    // ^ expires > 0 means it's a persistent cookie (not a session cookie)
  });

  // ── NEGATIVE TESTS ──────────────────────────────────────────────────────

  test('should show error for incorrect password', async () => {
    await loginPage.login(users.validUser.email, 'incorrectpassword');

    await expect(loginPage.errorMessage).toBeVisible();
    await expect(loginPage.errorMessage).toHaveText('Invalid email or password. Please try again.');
  });

  test('should show error for non-existent email', async () => {
    await loginPage.login('doesnotexist@example.com', 'anypassword');

    await expect(loginPage.errorMessage).toBeVisible();
  });

  test('should show validation error for empty email', async () => {
    // Leave email empty, fill password, try to submit
    await loginPage.fillPassword('somepassword');
    await loginPage.clickLogin();

    // Native HTML5 validation or custom validation message
    await expect(page.getByText('Email is required')).toBeVisible();
  });

  test('should show validation error for invalid email format', async () => {
    await loginPage.fillEmail('notanemail');
    await loginPage.fillPassword('somepassword');
    await loginPage.clickLogin();

    await expect(page.getByText('Please enter a valid email address')).toBeVisible();
  });

  test('should not navigate away from login page after failed login', async ({ page }) => {
    await loginPage.login(users.invalidUser.email, users.invalidUser.password);

    // Still on the login page
    await expect(page).toHaveURL('/login');
  });

  test('forgot password link navigates to reset page', async ({ page }) => {
    await loginPage.clickForgotPassword();

    await expect(page).toHaveURL('/forgot-password');
    await expect(page.getByRole('heading', { name: 'Reset your password' })).toBeVisible();
  });
});
```

---

**Complete dashboard test suite:**

```typescript
// tests/real-world/dashboard.spec.ts

import { test, expect } from '@playwright/test';
import { DashboardPage } from '../../pages/DashboardPage';
import { LoginPage } from '../../pages/LoginPage';
import users from '../../test-data/users.json';

// Use a describe block with beforeEach that logs in — all dashboard tests need auth
test.describe('Dashboard', () => {
  let dashboardPage: DashboardPage;

  test.beforeEach(async ({ page }) => {
    dashboardPage = new DashboardPage(page);

    // Log in before each dashboard test
    const loginPage = new LoginPage(page);
    await loginPage.goto();
    await loginPage.login(users.validUser.email, users.validUser.password);

    // Wait for dashboard to load fully
    await page.waitForURL(/.*dashboard.*/);
  });

  // ── CONTENT TESTS ────────────────────────────────────────────────────────

  test('should display the dashboard with all key sections', async ({ page }) => {
    // Verify all major dashboard sections are visible
    await expect(dashboardPage.welcomeHeading).toBeVisible();
    await expect(page.getByTestId('stats-overview')).toBeVisible();
    await expect(page.getByTestId('recent-activity')).toBeVisible();
    await expect(dashboardPage.sidebarNavigation).toBeVisible();
  });

  test('should show correct user greeting', async () => {
    const greeting = await dashboardPage.getUserGreeting();
    expect(greeting).toContain(users.validUser.name);
  });

  test('stats widgets display numerical data', async ({ page }) => {
    // Get all stat widgets
    const statWidgets = page.getByTestId('stat-widget');
    
    // There should be exactly 4 stats (or however many your app shows)
    await expect(statWidgets).toHaveCount(4);

    // Each widget should have a number displayed
    for (const widget of await statWidgets.all()) {
      const valueText = await widget.getByTestId('stat-value').textContent();
      // The value should be a number (possibly formatted like "1,234")
      expect(valueText?.replace(/,/g, '')).toMatch(/^\d+$/);
    }
  });

  // ── NAVIGATION TESTS ─────────────────────────────────────────────────────

  test('sidebar navigation links work correctly', async ({ page }) => {
    // Click each navigation item and verify the URL changes
    await dashboardPage.navigateTo('Profile');
    await expect(page).toHaveURL('/profile');

    await dashboardPage.navigateTo('Settings');
    await expect(page).toHaveURL('/settings');

    await dashboardPage.navigateTo('Dashboard');
    await expect(page).toHaveURL('/dashboard');
  });

  // ── SEARCH TESTS ─────────────────────────────────────────────────────────

  test('search functionality returns results', async ({ page }) => {
    await dashboardPage.searchFor('report');

    // Search results page should load
    await expect(page).toHaveURL(/.*search.*/);
    await expect(page.getByTestId('search-results')).toBeVisible();
    await expect(page.getByRole('listitem')).toHaveCount.greaterThan(0);
    // ^ At least one result returned for "report"
  });

  test('search with no results shows empty state', async ({ page }) => {
    await dashboardPage.searchFor('xyzzy12345nonexistent');

    await expect(page.getByTestId('empty-search-results')).toBeVisible();
    await expect(page.getByText('No results found')).toBeVisible();
  });

  // ── LOGOUT TEST ──────────────────────────────────────────────────────────

  test('user can log out successfully', async ({ page }) => {
    await dashboardPage.logout();

    // After logout, should be on login page
    await expect(page).toHaveURL('/login');

    // Should not be able to go back to dashboard (protected route)
    await page.goto('/dashboard');
    await expect(page).toHaveURL('/login');
    // ^ If we try to navigate directly to dashboard, we get redirected to login
  });
});
```

---

**Profile update test suite:**

```typescript
// tests/real-world/profile.spec.ts

import { test, expect } from '@playwright/test';
import { LoginPage } from '../../pages/LoginPage';
import { ProfilePage } from '../../pages/ProfilePage';
import users from '../../test-data/users.json';

test.describe('Profile Page', () => {
  let profilePage: ProfilePage;

  test.beforeEach(async ({ page }) => {
    profilePage = new ProfilePage(page);

    // Login and navigate to profile
    const loginPage = new LoginPage(page);
    await loginPage.goto();
    await loginPage.login(users.validUser.email, users.validUser.password);
    await profilePage.goto();
  });

  test('should display current user information', async () => {
    await expect(profilePage.pageHeading).toBeVisible();
    
    // Email should be displayed (but not editable)
    await expect(profilePage.emailDisplay).toHaveText(users.validUser.email);
    
    // Name field should contain current name
    await expect(profilePage.nameInput).toHaveValue(users.validUser.name);
  });

  test('should update user name successfully', async () => {
    const newName = 'Updated Test User';

    await profilePage.updateProfile(newName);

    // Success message appears
    await expect(profilePage.successToast).toBeVisible();

    // Reload the page and verify the change persisted
    await profilePage.goto();
    await expect(profilePage.nameInput).toHaveValue(newName);
  });

  test('should show error for empty name', async () => {
    await profilePage.updateName('');  // Clear the name
    await profilePage.saveChanges();

    await expect(page.getByText('Name cannot be empty')).toBeVisible();
    await expect(profilePage.successToast).not.toBeVisible();
  });

  test('profile avatar is displayed', async () => {
    await expect(profilePage.avatarImage).toBeVisible();
    await expect(profilePage.avatarImage).toHaveAttribute('src', /avatar/);
    // ^ Image src should contain "avatar" in the URL
  });

  test('API and UI are in sync after profile update', async ({ request }) => {
    // Update via UI
    await profilePage.updateProfile('API Sync Test Name');
    await expect(profilePage.successToast).toBeVisible();

    // Verify via API that the backend was actually updated
    const response = await request.get('/api/user/profile', {
      headers: {
        // Include auth — in real projects, this comes from your auth state
        'Authorization': `Bearer ${process.env.TEST_AUTH_TOKEN}`,
      },
    });

    expect(response.status()).toBe(200);

    const apiData = await response.json();
    expect(apiData.name).toBe('API Sync Test Name');
    // ^ Backend data matches what we set via the UI
  });
});
```

---

**Running the complete suite:**

```bash
# Run the entire real-world test suite
npx playwright test tests/real-world/

# Run with all browsers
npx playwright test tests/real-world/ --project=chromium --project=firefox --project=webkit

# Run with the visual UI (great for debugging)
npx playwright test tests/real-world/ --ui

# Generate and view the report
npx playwright test tests/real-world/ && npx playwright show-report
```

---

## Quick Reference Card

```typescript
// ── SETUP ────────────────────────────────────────────────────────────────────
npm init playwright@latest          // Install
npx playwright test                 // Run all tests
npx playwright test --headed        // Watch browser
npx playwright test --ui            // Interactive UI
npx playwright test --debug         // Debug mode
npx playwright show-report          // View HTML report
npx playwright codegen              // Record test by clicking (code generator)

// ── LOCATORS ─────────────────────────────────────────────────────────────────
page.getByRole('button', { name: 'Submit' })
page.getByLabel('Email')
page.getByPlaceholder('Enter email')
page.getByText('Welcome')
page.getByTestId('submit-btn')
page.getByAltText('Profile photo')
page.locator('#my-id')
page.locator('.my-class')

// ── ACTIONS ──────────────────────────────────────────────────────────────────
await locator.click()
await locator.fill('text')
await locator.hover()
await locator.check()
await locator.uncheck()
await locator.selectOption('value')
await locator.press('Enter')
await locator.dblclick()

// ── ASSERTIONS ───────────────────────────────────────────────────────────────
await expect(locator).toBeVisible()
await expect(locator).toBeHidden()
await expect(locator).toHaveText('exact text')
await expect(locator).toContainText('partial')
await expect(locator).toHaveValue('input value')
await expect(locator).toBeChecked()
await expect(locator).toBeEnabled()
await expect(locator).toBeDisabled()
await expect(locator).toHaveCount(5)
await expect(page).toHaveURL('/dashboard')
await expect(page).toHaveTitle('My App')
await expect(locator).not.toBeVisible()  // Negate any assertion
```

---

## Resources and Next Steps

Now that you've read this guide, here's where to go next:

**Official Resources:**
- [Playwright Official Documentation](https://playwright.dev/docs/intro) — The most comprehensive reference
- [Playwright API Reference](https://playwright.dev/docs/api/class-playwright) — Every method documented
- [Playwright GitHub](https://github.com/microsoft/playwright) — Source code and issue tracker

**Practice:**
- Use `npx playwright codegen https://demo.playwright.dev/todomvc` to practice generating tests by clicking
- The Playwright Inspector (`npx playwright test --debug`) is your best friend for debugging

**Community:**
- [Playwright Discord](https://aka.ms/playwright/discord) — Active community for questions
- [Stack Overflow — playwright tag](https://stackoverflow.com/questions/tagged/playwright)

**What to learn next:**
1. Custom fixtures — extend Playwright's base fixtures for your project
2. Environment variables — manage test configuration across environments
3. Visual comparisons — screenshot diffing with `toHaveScreenshot()`
4. Accessibility testing — `@axe-core/playwright` integration
5. CI/CD integration — GitHub Actions, Jenkins, Azure DevOps pipelines

---

*This guide was written to get you from zero to writing real Playwright tests as quickly as possible. Happy testing! 🎭*
