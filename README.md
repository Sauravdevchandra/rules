# AI Agent Rules

A collection of reusable AI development rules for Cursor, Claude Code, GitHub Copilot, ChatGPT, and other AI coding assistants.

The purpose of this repository is to standardize how AI generates code by enforcing consistent engineering practices across every project.

---

## Repository Structure

```
.
├── README.md
└── .agents
    └── rules
        ├── 01-ponytail.md
        ├── 02-code-standards.md
        └── ...
```

---

## Available Rules

| File | Description |
|------|-------------|
| `01-ponytail.md` | General AI behavior and project development workflow. |
| `02-code-standards.md` | Coding standards including validation, naming conventions, responsive UI, security, formatting, and best practices. |

More rules can be added over time as the collection grows.

---

## Goals

These rules help AI assistants generate code that is:

- Production-ready
- Clean and maintainable
- Secure by default
- Fully validated
- Responsive
- Accessible
- Consistent across projects
- Easy to review
- Easy to extend

---

## What These Rules Cover

The rule set includes standards for:

- Code Quality
- Input Validation
- Naming Conventions
- API Design
- Database Best Practices
- Error Handling
- Logging
- Security
- Responsive UI
- Accessibility
- Performance
- Project Structure
- Documentation
- Refactoring

---

## Core Principles

Every AI-generated implementation should:

- Follow the existing project architecture.
- Reuse existing components before creating new ones.
- Validate every input.
- Handle edge cases gracefully.
- Keep functions focused on a single responsibility.
- Use descriptive naming.
- Remove unused code.
- Avoid duplicate logic.
- Produce production-ready implementations rather than placeholders.

---

## UI Standards

Every generated interface should:

- Be fully responsive.
- Work correctly on mobile, tablet, laptop, and desktop.
- Use semantic HTML.
- Maintain consistent spacing and typography.
- Support keyboard navigation.
- Follow accessibility best practices.
- Avoid fixed layouts whenever possible.

---

## Security Standards

Generated code should:

- Validate and sanitize all inputs.
- Prevent SQL Injection.
- Prevent XSS.
- Prevent CSRF where applicable.
- Never expose secrets.
- Use secure authentication and authorization.
- Handle sensitive data safely.

---

## Contributing

When adding a new rule:

1. Keep each file focused on one topic.
2. Use clear, concise language.
3. Include examples when appropriate.
4. Avoid project-specific assumptions.
5. Ensure compatibility with modern development practices.

---

## License

This repository is available for personal and team use. Feel free to modify and extend the rules to match your own engineering standards.
