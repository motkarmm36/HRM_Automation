# Selenium TestNG TDD Framework - OrangeHRM

This project is a Java + Maven Selenium TestNG automation framework for the OrangeHRM demo application:

- https://opensource-demo.orangehrmlive.com/web/index.php/auth/login

## Tech Stack

- Java 17
- Maven
- Selenium WebDriver
- TestNG
- WebDriverManager
- ExtentReports

## Project Structure

```text
src
├── main
│   └── java
│       └── framework
│           ├── base
│           │   ├── BaseTest.java
│           │   └── DriverFactory.java
│           ├── pages
│           │   ├── DashboardPage.java
│           │   └── LoginPage.java
│           └── utils
│               ├── ConfigLoader.java
│               ├── ScreenshotUtils.java
│               └── WaitUtils.java
└── test
    ├── java
    │   ├── framework
    │   │   └── reporting
    │   │       ├── ExtentManager.java
    │   │       └── TestListener.java
    │   └── tests
    │       └── smoke
    │           └── LoginSmokeTest.java
    └── resources
        ├── config
        │   └── config.properties
        └── suites
            └── testng-smoke.xml
```

## Prerequisites

- Java 17 or above
- Maven 3.8+
- Chrome browser installed (default browser configuration)

## Setup

1. Clone or copy this project.
2. Open terminal at project root.
3. Install dependencies and run tests:

```bash
mvn clean test
```

## Execution Commands

- Run default suite configured in `pom.xml`:

```bash
mvn test
```

- Run explicit smoke suite:

```bash
mvn test -DsuiteXmlFile=src/test/resources/suites/testng-smoke.xml
```

- Override runtime parameters:

```bash
mvn test -Dbrowser=chrome -Dheadless=true
```

## Configuration

Update `src/test/resources/config/config.properties`:

- `baseUrl`
- `browser` (`chrome`, `firefox`, `edge`)
- `headless` (`true` or `false`)
- `implicitWaitInSeconds`
- `explicitWaitInSeconds`

System properties passed via Maven override values in `config.properties`.

## Reporting

- Extent report: `test-output/extent-report.html`
- Screenshots on failure: `test-output/screenshots/`
- TestNG default report: `test-output/index.html`

## TDD Style: How to Add New Coverage

1. Add or update a page object in `framework.pages`.
2. Keep page methods action-oriented (e.g., `login`, `logout`, `navigateToX`).
3. Add behavior-focused assertions in `src/test/java/tests/...`.
4. Reuse `BaseTest`, `WaitUtils`, and listener-based reporting.
5. Keep each test independent and deterministic.
