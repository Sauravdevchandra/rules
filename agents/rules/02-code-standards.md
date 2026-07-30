---
trigger: always_on
---

# Code Quality & Development Standards

Apply the following standards to all generated code, refactoring, and UI development.

## 1. Input Validation

* Every input field must include explicit validation.
* Required fields must validate:

  * Presence
  * Correct data type
  * Non-empty values
  * Format (email, phone number, URL, etc.)
  * Minimum and maximum length
  * Allowed value ranges
* Optional fields must still validate:

  * Data type
  * Length
  * Value range
  * Format
  * Sanitization whenever a value is provided.
* Never trust client-side validation alone. Always validate inputs on the server as well.

## 2. Naming Conventions

* Use clear, descriptive, and meaningful names for:

  * Variables
  * Functions
  * Parameters
  * Classes
  * Components
  * Files
* Single-letter variables such as `d`, `z`, `i`, `e`, `x`, `y`, or cryptic abbreviations are not allowed unless they are universally accepted (for example, `id` or `URL`).
* Prefer names such as:

  * `userDocument`
  * `orderDetails`
  * `customerProfile`
  * `currentSubscription`
  * `validationErrors`
  * `requestPayload`

## 3. Formatting & Comments

* Do not use emojis in:

  * Source code
  * Comments
  * UI text
  * Commit messages
* Do not include:

  * `Created by`
  * `Author:`
  * `Co-authored-by:`
  * AI-generated signatures
* Keep comments technical, concise, and focused on explaining non-obvious logic rather than describing what the code already makes obvious.

## 4. UI & Responsive Design

* Every UI must be fully responsive.
* Ensure proper layouts for:

  * Mobile devices
  * Tablets
  * Laptops
  * Desktop screens
* Avoid fixed widths and heights unless absolutely necessary.
* Use responsive layouts with Flexbox, Grid, or equivalent responsive design techniques.
* Maintain consistent spacing, typography, and alignment across all screen sizes.
* Ensure buttons, forms, tables, and navigation remain usable on smaller screens.
* Follow accessibility best practices, including:

  * Proper semantic HTML
  * Keyboard navigation support
  * Sufficient color contrast
  * Visible focus states
  * Appropriate ARIA attributes when necessary

## 5. Code Quality

* Write clean, modular, and maintainable code.
* Follow the Single Responsibility Principle (SRP).
* Avoid duplicated logic by creating reusable functions and components.
* Keep functions small and focused on a single responsibility.
* Handle all possible error cases gracefully.
* Never leave unused code, imports, variables, or commented-out blocks in the final implementation.

## 6. Security

* Sanitize and validate all user input.
* Never expose secrets, API keys, or sensitive information.
* Use parameterized queries or ORM protections to prevent SQL injection.
* Escape user-generated content before rendering it in the UI.
* Enforce authentication and authorization checks where required.

## 7. Performance

* Avoid unnecessary re-renders.
* Optimize API requests and database queries.
* Implement lazy loading where appropriate.
* Use pagination or virtualization for large datasets.
* Cache data when appropriate to improve performance.

## 8. Error Handling

* Handle all expected and unexpected errors gracefully.
* Provide user-friendly error messages without exposing internal implementation details.
* Log technical errors for debugging while keeping sensitive information out of logs.

## 9. Consistency

* Maintain consistent coding style throughout the project.
* Follow the project's existing architecture and folder structure.
* Reuse existing utilities and components whenever possible instead of creating duplicate implementations.
