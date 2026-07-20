# Contributing to FinFlow Loan Management System

First off, thank you for considering contributing to FinFlow! 🎉

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check the existing issues to avoid duplicates. When you create a bug report, include as many details as possible:

* **Use a clear and descriptive title**
* **Describe the exact steps to reproduce the problem**
* **Provide specific examples to demonstrate the steps**
* **Describe the behavior you observed and what you expected**
* **Include screenshots if relevant**
* **Include your environment details** (OS, Docker version, etc.)

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion, include:

* **Use a clear and descriptive title**
* **Provide a detailed description of the suggested enhancement**
* **Explain why this enhancement would be useful**
* **List any examples of where this enhancement exists in other projects**

### Pull Requests

1. **Fork the repository** and create your branch from `main`
2. **Make your changes** following the code style guidelines
3. **Test your changes** thoroughly
4. **Update documentation** if needed
5. **Write clear commit messages**
6. **Submit a pull request**

## Development Setup

### Prerequisites

* Java 21
* Maven 3.9+
* Docker & Docker Compose
* Git

### Local Development

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/Loan-Management-System.git
cd Loan-Management-System

# Start infrastructure services
docker-compose up mysql rabbitmq eureka-server config-server

# Run a specific service locally for development
cd auth_service
./mvnw spring-boot:run
```

## Code Style Guidelines

### Java

* Follow standard Java naming conventions
* Use meaningful variable and method names
* Keep methods small and focused (single responsibility)
* Add JavaDoc comments for public methods and classes
* Use proper indentation (4 spaces)
* Maximum line length: 120 characters

### Spring Boot Best Practices

* Use constructor injection instead of field injection
* Properly handle exceptions with appropriate HTTP status codes
* Use DTOs for API requests and responses
* Validate input using `@Valid` annotations
* Keep controllers thin, business logic in services

### Git Commit Messages

* Use present tense ("Add feature" not "Added feature")
* Use imperative mood ("Move cursor to..." not "Moves cursor to...")
* First line should be 50 characters or less
* Reference issues and pull requests after the first line

Examples:
```
Add user profile update feature

Implement PUT /users/{id} endpoint to allow users to update their profile information. Includes validation and authorization checks.

Fixes #123
```

### Branch Naming

* `feature/short-description` - New features
* `bugfix/short-description` - Bug fixes
* `hotfix/short-description` - Critical fixes
* `docs/short-description` - Documentation updates
* `refactor/short-description` - Code refactoring

## Testing

* Write unit tests for new features
* Ensure all tests pass before submitting PR
* Maintain or improve code coverage
* Test edge cases and error scenarios

```bash
# Run tests
mvn test

# Run tests with coverage
mvn test jacoco:report
```

## Documentation

* Update README.md if you change functionality
* Update API documentation (Swagger annotations)
* Add comments for complex logic
* Update CHANGELOG.md for significant changes

## Code Review Process

1. At least one maintainer must review and approve
2. All CI checks must pass
3. Code must follow style guidelines
4. Tests must be included and passing
5. Documentation must be updated if needed

## Community

* Be respectful and inclusive
* Follow the [Code of Conduct](CODE_OF_CONDUCT.md)
* Help others in issues and discussions
* Share your knowledge and experience

## Recognition

Contributors will be acknowledged in:
* README.md contributors section
* Release notes for significant contributions
* Project documentation

## Questions?

Feel free to:
* Open an issue for questions
* Join discussions
* Reach out to maintainers

Thank you for contributing! 🙏
