# SIMATS ENGINEERING

## Department of Computer Science and Engineering

### Course: Internet Programming (Course Code: CSA43)

### Assessment Tool 1 (AT1) — Application-Based Questions

**Course Outcome (CO-1):** Develop well-structured, standards-compliant web pages using HTML/XHTML and XML, and apply Internet protocols and HTTP communication mechanisms for web content delivery. (L2)

\---

## Student Declaration \& Code of Conduct

> \*\*Declaration:\*\*  
> I, \*\*K.nanda Kishore Reddy\*\* (Register Number: \*\*192411161\*\*), certify that this submission is my original work and that I have adhered to the guidelines specified for this assessment. I understand that any violation of academic integrity rules will result in disciplinary action.
> 
> \*\*Student Signature:\*\* K.Nanda Kishore Reddy (Reg No: 192411161)

\---

# Table of Contents

1. [Question 1: Online Symposium Portal](#question-1-online-symposium-portal)

   * [1.1 HTML5 Semantic Elements Missing](#11-identify-appropriate-html5-semantic-elements-missing-in-the-structure)
   * [1.2 Modified Standards-Compliant HTML Structure](#12-modify-the-structure-to-make-it-standards-compliant)
   * [1.3 Interpretation of the HTTP Request Generated](#13-interpret-the-http-request-generated-during-form-submission)
   * [1.4 Analysis of the HTTP Response Cycle](#14-analyze-the-http-response-cycle-from-server-to-browser)
   * [1.5 Usability and Accessibility Improvements](#15-suggest-improvements-for-usability-and-accessibility)
2. [Question 2: Cross-Browser Compatibility Issue](#question-2-cross-browser-compatibility-issue)

   * [2.1 Improper Nesting \& Missing Closing Tags](#21-identify-improper-nesting-and-missing-closing-tags)
   * [2.2 Browser Parsing \& Interpretation Analysis](#22-analyze-how-different-browsers-may-interpret-this-structure)
   * [2.3 Missing Semantic Elements](#23-identify-missing-semantic-elements)
   * [2.4 Corrected W3C-Compliant HTML Structure](#24-provide-a-corrected-w3c-compliant-html-structure)
   * [2.5 Cross-Browser Compatibility Techniques](#25-suggest-techniques-to-ensure-cross-browser-compatibility)
3. [Question 3: Form Submission Failure](#question-3-form-submission-failure)

   * [3.1 Issues in Form Configuration](#31-identify-issues-in-the-form-configuration)
   * [3.2 Analysis of Why HTTP Request is Not Triggered](#32-analyze-why-the-http-request-is-not-triggered)
   * [3.3 Role \& Exposure Risks of GET Method](#33-interpret-the-role-of-get-method-in-this-scenario)
   * [3.4 Corrected Implementation](#34-propose-a-corrected-implementation)
   * [3.5 Secure Data Transmission Improvements](#35-suggest-improvements-for-secure-data-transmission)

\---

## Question 1: Online Symposium Portal

### Scenario

A college is developing an online symposium registration portal. The following HTML structure and HTTP interaction is observed:

```html
<form action="/register" method="POST">
 <input type="text" name="name">
 <input type="email" name="email">
 <button>Submit</button>
</form>
```

When a student submits the form, the browser sends an HTTP request to the server, and the server responds accordingly.

\---

### 1.1 Identify appropriate HTML5 semantic elements missing in the structure.

The provided HTML snippet lacks essential structural, grouping, and labeling semantic elements:

1. **Document Landmark \& Sectioning Elements**:

   * **`<main>`**: Missing to define the core content area of the webpage.
   * **`<section>` / `<article>`**: Missing to encapsulate the symposium registration module within a distinct thematic block.
   * **`<header>`**: Missing to contain the document heading (`<h1>`) describing the symposium title.
2. **Form Structure \& Grouping Elements**:

   * **`<fieldset>`**: Missing to visually and programmatically group related input fields (e.g., Personal Details).
   * **`<legend>`**: Missing to provide a descriptive caption for the `<fieldset>` group.
3. **Form Control Labeling**:

   * **`<label>`**: Completely absent. Without `<label>` elements linked via `for` attributes to the input `id`s, screen readers cannot announce input purposes to visually impaired users, and users cannot click text to focus fields.
4. **Document Metadata \& Root Wrappers**:

   * `<!DOCTYPE html>`, `<html>`, `<head>`, `<title>`, `<meta charset="UTF-8">`, and `<body>` tags are missing.

\---

### 1.2 Modify the structure to make it standards-compliant.

Below is the complete, standards-compliant HTML5 document:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Online Symposium Registration Portal</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <h1>Annual Tech Symposium 2026</h1>
    <p>Register below to participate in events and workshops.</p>
  </header>

  <main>
    <section aria-labelledby="registration-heading">
      <h2 id="registration-heading">Student Registration Form</h2>

      <form action="/register" method="POST" id="symposiumForm">
        <fieldset>
          <legend>Participant Information</legend>

          <div class="form-group">
            <label for="student-name">Full Name <span class="required">\*</span></label>
            <input 
              type="text" 
              id="student-name" 
              name="name" 
              required 
              autocomplete="name" 
              placeholder="e.g., Alex Johnson"
              aria-required="true">
          </div>

          <div class="form-group">
            <label for="student-email">Email Address <span class="required">\*</span></label>
            <input 
              type="email" 
              id="student-email" 
              name="email" 
              required 
              autocomplete="email" 
              placeholder="e.g., alex@university.edu"
              aria-required="true">
          </div>

          <div class="form-group">
            <button type="submit" id="submitBtn">Submit Registration</button>
          </div>
        </fieldset>
      </form>
    </section>
  </main>

  <footer>
    <p>\&copy; 2026 SIMATS Engineering. All rights reserved.</p>
  </footer>
</body>
</html>
```

\---

### 1.3 Interpret the HTTP request generated during form submission.

When the student submits the form with `method="POST"` and `action="/register"`, the browser packages the input values and sends an HTTP Request over TCP/IP (or SSL/TLS if HTTPS):

#### Structural Anatomy of the HTTP POST Request:

```http
POST /register HTTP/1.1
Host: symposium.simats.edu
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_15\_7) AppleWebKit/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,\*/\*;q=0.8
Accept-Language: en-US,en;q=0.9
Content-Type: application/x-www-form-urlencoded
Content-Length: 37
Origin: https://symposium.simats.edu
Referer: https://symposium.simats.edu/register
Connection: keep-alive

name=Alex+Johnson\&email=alex%40university.edu
```

#### Detailed Component Breakdown:

|HTTP Request Field|Description \& Purpose|
|-|-|
|**Request Line**|`POST /register HTTP/1.1` defines the HTTP method (`POST`), target endpoint URI (`/register`), and protocol version (`HTTP/1.1`).|
|**`Host` Header**|Indicates the domain name of the destination server (`symposium.simats.edu`).|
|**`Content-Type`**|`application/x-www-form-urlencoded` specifies that form keys/values are URL-encoded (`+` for spaces, `%40` for `@`).|
|**`Content-Length`**|Specifies the exact byte count of the request body payload (37 bytes).|
|**Request Body Payload**|Data is encapsulated inside the message payload body rather than the URL bar: `name=Alex+Johnson\&email=alex%40university.edu`.|

\---

### 1.4 Analyze the HTTP response cycle from server to browser.

The HTTP request-response communication cycle follows 5 distinct steps:

```
+----------------+          1. Submit Form (HTTP POST)          +----------------+
|                | -------------------------------------------> |                |
|                |                                              |                |
|                |          2. Validate \& Process Request       |                |
|                | <------------------------------------------  |                |
|                |          3. HTTP 303 Redirect / 200 OK       |                |
|    Browser     |                                              |  Web Server /  |
|    (Client)    |                                              |    Backend     |
|                |          4. HTTP GET Confirmation Page       |                |
|                | -------------------------------------------> |                |
|                |                                              |                |
|                |          5. HTTP 200 OK + Render HTML        |                |
|                | <------------------------------------------  |                |
+----------------+                                              +----------------+
```

1. **Client Request Initiation**:

   * The user clicks the `<button type="submit">`.
   * The browser performs HTML5 input validation. If valid, it serializes input data into `application/x-www-form-urlencoded` format and transmits the TCP payload to the server.
2. **Server-Side Request Handling**:

   * The server (e.g., Express.js, Django, Spring Boot) parses the incoming HTTP POST headers and body.
   * The backend validates student identity, saves records to the SQL/NoSQL database, and prepares a response.
3. **Server Response Generation (Post/Redirect/Get Pattern)**:

   * To prevent duplicate form submission if the user refreshes, the server responds with a `303 See Other` (or `302 Found`) status code along with a `Location: /confirmation` header.
4. **Client Redirect Execution**:

   * Upon receiving the `303 See Other` status code, the browser automatically sends an HTTP `GET /confirmation` request to the server.
5. **Final Rendering**:

   * The server sends `HTTP/1.1 200 OK` with HTML confirmation content. The browser DOM parser constructs the layout tree and renders the final success message to the user.

\---

### 1.5 Suggest improvements for usability and accessibility.

1. **Accessibility (WCAG 2.1 Guidelines)**:

   * **Explicit `<label>` Binding**: Connect `<label for="id">` to every `<input id="id">`.
   * **ARIA Attributes**: Use `aria-required="true"` and `aria-describedby` for field context and error messages.
   * **Keyboard Navigation \& Visible Focus**: Style `:focus-visible` outlines cleanly so motor-impaired keyboard users can easily identify active controls.
2. **Usability \& UX Enhancements**:

   * **HTML5 Input Types \& Attributes**: Use `type="email"` for automatic mobile keyboard optimizations (`@` symbol displayed on keypad) and set `autocomplete="name"` / `autocomplete="email"`.
   * **Real-Time Client-Side Validation**: Display instant feedback on `blur` events (e.g. invalid email format) using JavaScript or HTML pattern matching.
   * **Submit Button State Management**: Disable the submit button and show a loading spinner upon click to prevent accidental double submissions.

\---

## Question 2: Cross-Browser Compatibility Issue

### Scenario

A company website shows inconsistent layout across browsers. The following HTML snippet is used:

```html
<html>
 <head>
 <title>Company</title>
 </head>
 <body>
 <div>
 <h1>Welcome
 <p>About us
 </div>
 </body>
</html>
```

\---

### 2.1 Identify improper nesting and missing closing tags.

The given HTML snippet contains severe structural errors:

1. **Missing `<!DOCTYPE html>`**:

   * Omission of the document type declaration forces browsers into **Quirks Mode**, causing legacy CSS rendering rules to apply.
2. **Missing Closing Tags**:

   * `<h1>Welcome`: Missing explicit `</h1>` closing tag.
   * `<p>About us`: Missing explicit `</p>` closing tag.
3. **Improper Tag Nesting**:

   * The `<p>` paragraph element is placed directly inside the open `<h1>` heading element without closing `<h1>` first.
   * According to W3C HTML specifications, block-level elements like `<p>` are forbidden inside heading elements (`<h1>`-`<h6>`).

\---

### 2.2 Analyze how different browsers may interpret this structure.

Modern web browsers handle syntax errors using built-in HTML5 error recovery algorithms:

```
Raw Markup: <h1>Welcome <p>About us </div>
                         │
                         ▼ (HTML Parsing Algorithm)
Browser Action: Auto-closes <h1> when encountering block-level <p> tag
                         │
                         ▼
Generated DOM: <h1>Welcome</h1><p>About us</p>
```

#### Differential Parsing \& Rendering Behaviors:

* **Chromium / WebKit / Gecko Engines**:

  * HTML parser encounters `<p>` inside open `<h1>`. Because `<p>` cannot be nested inside `<h1>`, the parser implicitly inserts `</h1>` right before `<p>`, yielding `<h1>Welcome</h1><p>About us</p>`.
* **Quirks Mode Layout Inconsistencies**:

  * Without `<!DOCTYPE html>`, browsers switch from **Standards Mode** to **Quirks Mode**.
  * In Quirks Mode, browsers emulate legacy Internet Explorer behavior:

    * **Box Model Calculation**: Border and padding calculations differ across browsers.
    * **Font Inheritance**: Heading font size inheritance inside `<div>` behaves inconsistently across Safari, Chrome, and Firefox.
    * **Default Margins**: Margin collapsing for unclosed paragraph tags defaults to vendor-specific stylesheet defaults (`user agent stylesheet`), leading to visual layout breaks across platforms.

\---

### 2.3 Identify missing semantic elements.

The layout uses generic `<div>` wrappers instead of HTML5 structural semantic elements:

1. **Missing `<header>`**: Should encapsulate top-level welcome headings.
2. **Missing `<main>`**: Should wrap the central topic content.
3. **Missing `<section>` / `<article>`**: Should encapsulate the "About Us" topic.
4. **Missing `<footer>`**: Should contain copyright and footer navigation.
5. **Missing `<html>` attributes**: Missing `lang="en"` (essential for screen readers \& language detection).
6. **Missing `<head>` metadata**: Missing `<meta charset="UTF-8">` and `<meta name="viewport" content="width=device-width, initial-scale=1.0">`.

\---

### 2.4 Provide a corrected W3C-compliant HTML structure.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Company - Official Website</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  
  <header>
    <h1>Welcome to Our Company</h1>
  </header>

  <main>
    <section aria-labelledby="about-heading">
      <h2 id="about-heading">About Us</h2>
      <p>We are a global provider of innovative technology solutions dedicated to excellence and quality.</p>
    </section>
  </main>

  <footer>
    <p>\&copy; 2026 Company Inc. All rights reserved.</p>
  </footer>

</body>
</html>
```

\---

### 2.5 Suggest techniques to ensure cross-browser compatibility.

1. **Enforce Standards Mode with Valid DOCTYPE**:

   * Always place `<!DOCTYPE html>` at line 1 of every HTML document.
2. **Automated W3C Markup Validation**:

   * Integrate `w3c-xmlserializer` or run HTML through the **W3C Markup Validation Service** (`https://validator.w3.org/`) in CI/CD pipelines to catch unclosed or improperly nested tags.
3. **CSS Normalization / Resets**:

   * Include `normalize.css` or a modern CSS Reset (e.g., `box-sizing: border-box; margin: 0; padding: 0;`) to standardize default element margins, font sizes, and line heights across browsers.
4. **Cross-Browser Automated Testing**:

   * Use cross-browser testing tools like **Playwright**, **Selenium**, or **BrowserStack** to test across Chrome, Firefox, Safari, and Edge.
5. **Feature Detection vs User-Agent Sniffing**:

   * Use CSS `@supports` queries or JS feature detection to apply modern features gracefully.

\---

## Question 3: Form Submission Failure

### Scenario

A web application fails to send form data to the server. The following configuration is observed:

```html
<form action="/submit" method="GET">
 <input type="text" name="username">
 <input type="password" name="password">
 <button type="button">Login</button>
</form>
```

\---

### 3.1 Identify issues in the form configuration.

The form configuration contains three major technical flaws:

1. **Incorrect Button Type (`type="button"`)**:

   * `<button type="button">Login</button>` explicitly specifies `type="button"`.
   * A button with `type="button"` is a standard clickable button with **no default submission behavior**. It does not trigger a form submit event when clicked.
2. **Insecure Data Transmission Method (`method="GET"`)**:

   * Using `GET` for credentials appends username and password values directly to the URL query string (`/submit?username=admin\&password=secret123`), exposing sensitive data in browser history, proxy logs, and referer headers.
3. **Missing Accessibility \& Security Attributes**:

   * Missing `<label>` tags and `id` bindings for fields.
   * Missing `autocomplete="username"` and `autocomplete="current-password"` attributes.
   * Missing input validation (`required`).

\---

### 3.2 Analyze why the HTTP request is not triggered.

#### Technical Mechanism:

```
User Clicks <button type="button">
          │
          ▼
Fires 'click' Event
          │
          ▼
Is button type="submit"? ──► NO ──► Form Submit Event is NOT Fired ──► Browser does NOT send HTTP Request
```

1. Browsers only generate and transmit an HTTP request when a `<form>` element dispatches a **submit** event.
2. The HTML specification defines three button types:

   * `type="submit"`: Triggers form submission (default if type is omitted).
   * `type="reset"`: Resets form controls to default values.
   * `type="button"`: Has no default action.
3. Because the button has `type="button"` and no JavaScript `onclick` handler is attached to invoke `form.submit()`, clicking the button triggers a `click` event but **never triggers a submit event**.
4. Consequently, the browser remains idle and no HTTP network request is constructed or transmitted to `/submit`.

\---

### 3.3 Interpret the role of GET method in this scenario.

#### Purpose of HTTP `GET`:

According to RFC 7231, `GET` is a **safe** and **idempotent** HTTP method meant solely for retrieving data without altering server state.

#### Security Vulnerabilities of using GET for Passwords:

|Risk Vector|Description of Security Exposure|
|-|-|
|**URL Parameter Exposure**|Credentials appended to URL: `https://example.com/submit?username=john\&password=Password123!`|
|**Browser History Logging**|Cleartext passwords stored permanently in user browser history.|
|**Web Server Access Logs**|Web servers (Apache, Nginx, IIS) log full URL requests in plaintext access logs (`access.log`).|
|**HTTP Referer Header Leakage**|If the user navigates away from the page, the full URL with password is transmitted in the `Referer` header to external websites.|
|**Network Interception**|URLs are easily visible in unencrypted network traffic and corporate proxy logs.|

\---

### 3.4 Propose a corrected implementation.

Below is the complete, secure, standards-compliant HTML5 login form:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Secure Student Login</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  
  <main class="login-container">
    <section class="login-card" aria-labelledby="login-heading">
      <h2 id="login-heading">Account Login</h2>

      <!-- Corrected: method="POST", action URL, HTTPS -->
      <form action="https://symposium.simats.edu/api/login" method="POST" autocomplete="on">
        
        <div class="form-group">
          <label for="username">Username or Email</label>
          <input 
            type="text" 
            id="username" 
            name="username" 
            required 
            autocomplete="username" 
            placeholder="Enter your username"
            aria-required="true">
        </div>

        <div class="form-group">
          <label for="password">Password</label>
          <input 
            type="password" 
            id="password" 
            name="password" 
            required 
            autocomplete="current-password" 
            placeholder="Enter your password"
            aria-required="true">
        </div>

        <div class="form-group">
          <!-- Corrected: type="submit" -->
          <button type="submit" id="loginSubmitBtn">Login</button>
        </div>

      </form>
    </section>
  </main>

</body>
</html>
```

\---

### 3.5 Suggest improvements for secure data transmission.

1. **Mandatory HTTPS (TLS/SSL Encryption)**:

   * Ensure the form action uses `https://` protocol to encrypt all payload data in transit between client and server, protecting against Man-in-the-Middle (MitM) eavesdropping.
2. **Use HTTP `POST` Method**:

   * Always submit sensitive form data using `method="POST"`, placing credentials inside the HTTP payload body rather than the visible URL query string.
3. **Cross-Site Request Forgery (CSRF) Protection**:

   * Include a cryptographically secure, hidden CSRF token in the form:

```html
     <input type="hidden" name="csrf\_token" value="d9a8f7c6b5a43210e">
     ```

4. **Secure HTTP Headers on Server Response**:

   * `Strict-Transport-Security (HSTS)`: Forces browser to communicate only via HTTPS.
   * `Cache-Control: no-store, no-cache, must-revalidate`: Prevents sensitive login responses from being cached in browser disk caches.
   * `Content-Security-Policy (CSP)`: Protects against Cross-Site Scripting (XSS) and data exfiltration.
5. **Client \& Server-Side Security Enhancements**:

   * Set `autocomplete="current-password"` for password managers.
   * Implement backend rate-limiting (IP-based throttling) and multi-factor authentication (MFA) to mitigate brute-force attacks.

\---

## Conclusion \& Summary

This assessment demonstrates comprehensive understanding of HTML5 semantic web standards, W3C structural compliance, HTTP request/response communication cycles, cross-browser rendering mechanics, and secure web application form submission protocols in accordance with CO-1 learning outcomes.

