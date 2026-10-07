# Code Audit Checklist

## 1. Code Style and Formatting

- [ ] Consistent naming conventions (camelCase, snake_case, PascalCase)
- [ ] Proper indentation and line lengths
- [ ] Import order and organization
- [ ] Linter/formatter configuration present and enforced
- [ ] No dead code or unused imports

## 2. Documentation

- [ ] Functions/methods have docstrings or JSDoc comments
- [ ] Complex logic has inline comments
- [ ] Type hints/annotations used consistently
- [ ] README is up to date with setup instructions
- [ ] API endpoints documented

## 3. Error Handling

- [ ] Try/catch blocks used appropriately (not overly broad)
- [ ] Custom error types for domain-specific errors
- [ ] Structured logging with appropriate levels
- [ ] Errors propagated with context (not swallowed)
- [ ] Graceful degradation for external service failures

## 4. Testing

- [ ] Unit tests for business logic
- [ ] Integration tests for API endpoints
- [ ] Test fixtures and mocking patterns
- [ ] Edge cases and error paths tested
- [ ] CI runs tests automatically

## 5. Dependencies Management

- [ ] Lock file committed (package-lock.json, yarn.lock, poetry.lock)
- [ ] Versions pinned appropriately
- [ ] No known vulnerabilities (npm audit, safety check)
- [ ] Unused dependencies removed
- [ ] Dev vs production dependencies separated

## 6. Code Organization

- [ ] Clear module/package boundaries
- [ ] Single responsibility per module/class
- [ ] No circular dependencies
- [ ] Shared code properly abstracted
- [ ] Configuration separated from business logic

## 7. Performance

- [ ] No N+1 query patterns
- [ ] Appropriate caching strategies
- [ ] Async operations used for I/O
- [ ] No memory leaks (event listeners, intervals)
- [ ] Efficient data structure choices

## 8. Security

- [ ] Input validation at system boundaries
- [ ] No secrets in source code
- [ ] SQL injection / XSS / CSRF protection
- [ ] Authentication and authorization checks
- [ ] Dependencies scanned for vulnerabilities
- [ ] HTTPS enforced for external calls
