# Virtual Scroll Access System (VSAS)

The **Virtual Scroll Access System (VSAS)** is a console-based Java application for storing, discovering, downloading, and managing virtual scrolls. It provides account management for registered users, administrative controls, scroll metadata tracking, download statistics, and automated tests for the core workflows.

The project was created for the **Lab01 Richard Group04 A2** coursework and demonstrates object-oriented Java, file-based persistence, Gradle build automation, unit testing, and collaborative development practices.

## Features

### Account management

- Register a new account with a name, email address, phone number, username, and password
- Prevent duplicate usernames during registration
- Log in as a registered user or administrator
- Update a registered username or password
- Store account information locally in a text file

### Scroll management

- View available scrolls and their metadata
- Preview the first five lines of a scroll
- Upload a new scroll with a unique name and Whisker ID
- Edit a scroll's name, Whisker ID, or file content
- Download a scroll to the local downloads directory
- Remove a scroll and its metadata
- Record upload and update activity in a log

### Search and filtering

Scrolls can be filtered using:

- Uploader username
- Whisker ID
- Scroll name
- Upload date

### Administration

Administrators can:

- View all registered users
- Add a user
- Delete a user
- View per-scroll download statistics
- View upload and update statistics from the activity log
- Log out of the administrative interface

## Technology Stack

- **Language:** Java
- **Build tool:** Gradle 7.5.1 Wrapper
- **Testing:** JUnit Jupiter 5.8.x
- **Mocking:** Mockito 3.12.4
- **Code coverage:** JaCoCo
- **Utility library:** Google Guava 31.0.1-jre
- **Interface:** Command-line interface (CLI)
- **Persistence:** Local text files

## Project Structure

```text
Agile-Development-Tools-2/
├── app/
│   ├── build.gradle
│   └── src/
│       ├── main/java/lab01/richard/group04/a2/
│       │   ├── App.java
│       │   ├── Registration.java
│       │   ├── UserLogin.java
│       │   ├── UserInterface.java
│       │   ├── ProfileManagement.java
│       │   ├── ScrollManager.java
│       │   ├── Admin.java
│       │   ├── registration.txt
│       │   ├── Scrolls/
│       │   │   ├── Scrolls_details.txt
│       │   │   ├── log.txt
│       │   │   └── <scroll files>.txt
│       │   └── Downloads/
│       │       ├── ScrollStats.txt
│       │       └── <downloaded scrolls>.txt
│       └── test/java/lab01/richard/group04/a2/
│           ├── AppTest.java
│           ├── RegistrationTest.java
│           ├── AdminTest.java
│           ├── AddScrollTest.java
│           ├── ViewScrollTest.java
│           ├── PreviewScrollTest.java
│           ├── DownloadScrollTest.java
│           ├── RemoveScrollTest.java
│           ├── RemoveScrollsTest.java
│           └── SearchScrollsTest.java
├── gradle/wrapper/
├── gradlew
├── gradlew.bat
├── settings.gradle
└── README.md
```

## Main Components

| Component | Responsibility |
| --- | --- |
| `App` | Starts the application and routes users to registration or login |
| `Registration` | Validates usernames and saves new accounts |
| `UserLogin` | Loads credentials and authenticates users and administrators |
| `UserInterface` | Presents user-facing menu options |
| `ProfileManagement` | Loads, edits, and saves account information |
| `ScrollManager` | Handles scroll upload, viewing, preview, editing, search, download, and removal |
| `Admin` | Manages users and displays system statistics |
| `Scroll` | Represents scroll metadata such as ID, name, uploader, date, and path |

## Data Files

The application uses text files instead of a database.

| File or directory | Purpose |
| --- | --- |
| `registration.txt` | Stores registered account details |
| `Scrolls/Scrolls_details.txt` | Stores scroll names, Whisker IDs, and upload dates |
| `Scrolls/log.txt` | Records upload and update activity |
| `Scrolls/*.txt` | Stores scroll content |
| `Downloads/ScrollStats.txt` | Stores download counts by scroll |
| `Downloads/*.txt` | Contains downloaded scroll copies |

## Prerequisites

Install a Java Development Kit before running the project:

- JDK 11 or later
- Git, if cloning the repository

Gradle does not need to be installed separately because the project includes the Gradle Wrapper.

Verify Java is available:

```bash
java -version
```

## Installation

Clone the repository and enter its root directory:

```bash
git clone <repository-url>
cd Agile-Development-Tools-2
```

Replace `<repository-url>` with the repository's actual Git URL.

On macOS or Linux, make the wrapper executable if required:

```bash
chmod +x gradlew
```

## Running the Application

Run all commands from the repository root so the application's relative data paths resolve correctly.

### macOS or Linux

```bash
./gradlew run
```

### Windows

```powershell
gradlew.bat run
```

At the opening prompt, enter:

```text
register
login
exit
```

Commands are matched without regard to letter case.

## Usage

### Registering and logging in

1. Start the application.
2. Enter `register`.
3. Provide your name, email address, phone number, username, and password.
4. Return to the opening screen and enter `login`.
5. Enter the saved username and password.

### Managing scrolls

After logging in, use the numbered menu to:

1. View scrolls.
2. Preview a scroll.
3. Edit or update a scroll.
4. Add a scroll.
5. Download a scroll.
6. Remove a scroll.
7. Search and filter scrolls.
8. Manage the current user profile.

Some operations request a **Whisker ID**, which acts as a unique identifier for a scroll.

## Running Tests

Run the complete automated test suite from the repository root.

### macOS or Linux

```bash
./gradlew test
```

### Windows

```powershell
gradlew.bat test
```

The generated HTML test report can be opened at:

```text
app/build/reports/tests/test/index.html
```

The suite covers:

- Application startup
- User registration
- Administrative user deletion
- Adding scrolls and validating unique identifiers
- Viewing and previewing scrolls
- Downloading scrolls
- Removing scrolls
- Filtering by scroll ID, name, and upload date
- Missing files and invalid input cases

## Building the Project

Compile the application and run verification tasks:

```bash
./gradlew build
```

On Windows:

```powershell
gradlew.bat build
```

Build output is generated under `app/build/`.

Clean generated build files with:

```bash
./gradlew clean
```

## Code Coverage

The project applies the JaCoCo Gradle plugin. After running the tests, generate a coverage report with:

```bash
./gradlew jacocoTestReport
```

The report is normally generated under:

```text
app/build/reports/jacoco/test/html/index.html
```

## Security Notice

VSAS is an educational application. Account passwords and profile details are currently stored as plain text. Do not use real personal information or passwords when running it.

A production implementation should:

- Hash and salt passwords using a dedicated password-hashing algorithm
- Store users and scroll metadata in a managed database
- Enforce explicit role-based authorisation
- Validate file names, paths, and all user input
- Prevent path traversal and unsafe file access
- Keep runtime data outside the source-code directory
- Avoid committing personal data, activity logs, and downloaded files

## Known Limitations

- The application is available only through a command-line interface.
- Data is stored in text files instead of a transactional database.
- Runtime file paths are coupled to the source-tree layout.
- Passwords are stored without hashing.
- Some prompts and navigation paths require further input validation.
- Scroll content is represented by text files despite references to binary files in the interface.
- The project is intended for coursework and demonstration purposes.

## Suggested Improvements

- Replace file-based persistence with a relational database
- Introduce password hashing and secure session handling
- Separate presentation, business, and persistence layers
- Create domain models for users, roles, scrolls, and download events
- Add reliable guest-mode support
- Improve exception handling and menu navigation
- Add validation for email addresses, phone numbers, file names, and dates
- Store runtime data in configurable directories
- Expand unit and integration test coverage
- Add a web or desktop graphical interface

## Contributing

1. Create a feature branch.
2. Make focused changes.
3. Add or update relevant tests.
4. Run `./gradlew test` locally.
5. Commit using a clear message.
6. Open a pull request describing the change and test results.

## Academic Context

This repository was created for the **Lab01-Richard-Group04-A2** group assignment. Follow your institution's academic-integrity and attribution policies when reusing any part of the project.

## License

No project-specific license was identified in the supplied directory. Unless the project owners add a license, the source code should be treated as all rights reserved.
