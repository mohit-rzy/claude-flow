# Git Commit Generator

Generate conventional commit messages following the Conventional Commits 1.0.0 specification.

## Instructions

1. Analyze staged files using `git status` and `git diff --staged`
2. Generate a conventional commit message based on changes
3. Present the commit message for approval
4. Execute the commit after approval
5. Keep simple changes concise

## Format

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

## Common Types

- `feat`: New feature (MINOR version)
- `fix`: Bug fix (PATCH version)
- `docs`: Documentation changes
- `style`: Code style changes (formatting, semicolons, etc.)
- `refactor`: Code refactoring without feature/bug changes
- `perf`: Performance improvements
- `test`: Adding or updating tests
- `build`: Build system or dependencies
- `ci`: CI configuration changes
- `chore`: Maintenance tasks

## Breaking Changes

- Add `!` after type/scope: `feat!:` or `feat(api)!:`
- Add footer: `BREAKING CHANGE: description`
- Correlates with MAJOR version bump

## Examples

### Simple
```
fix: resolve authentication timeout issue
docs: update API documentation
feat(auth): add OAuth2 support
```

### With Breaking Change
```
feat!: migrate to new authentication system

BREAKING CHANGE: Legacy auth tokens are no longer supported
```

### With Scope and Body
```
fix(parser): handle edge case in JSON parsing

Addresses issue where nested objects with special characters
were incorrectly parsed, causing validation errors.

Closes #123
```

## Workflow

1. **Stage your changes**: `git add .`
2. **Run this command** to generate commit message
3. **Review and approve** the suggested message
4. **Commit automatically** or manually with the message