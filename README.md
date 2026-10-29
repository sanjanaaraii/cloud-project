# cloud assignment

It manages
multiple events, seat limits, student registrations, cancellations, and local
file persistence.

## Requirements

Full JDK 21, Git, an editor, and the separate Jenkins setup folder.
No Maven, Gradle, Docker, database, web framework, or cloud account is needed.
Before-class software setup is in `Student_Prerequisites_Standalone.pdf`.
The code is introduced during the lecture, not required for preparation.

## Build and run

Open a terminal inside `festpass-java`:

```text
java ci/Build.java verify
```

The completed project should pass all 28 tests. After verification, continue:

```text
java ci/SmokeTest.java
java -jar build/festpass.jar help
java -jar build/festpass.jar add-event java "Java Workshop" 2
java -jar build/festpass.jar add-event music "Campus Music" 1
java -jar build/festpass.jar list
java -jar build/festpass.jar book java S1
java -jar build/festpass.jar book java S2
java -jar build/festpass.jar book java S3
java -jar build/festpass.jar cancel java S1
java -jar build/festpass.jar book java S3
java -jar build/festpass.jar roster java
java -jar build/festpass.jar summary
```

The repaired app must pass **28 tests**. The first `book java S3` deliberately reports
SOLD OUT and exits with code 2; continue with cancellation, then retry.
Final summary: 2 events, 2 booked seats, 1 available seat. Running `list`
in a new terminal shows the same saved data.

The default file is `data/festpass.tsv`, relative to your working directory.
For an independent run, put `--data FILE` before the command:

```text
java -jar build/festpass.jar --data data/second-demo.tsv add-event java "Java Workshop" 2
```

Events cannot be added twice. If repeating the walkthrough, choose a new data
file or remove only your known demo data file after stopping all commands.
The `data` directory is ignored by Git; do not commit personal or runtime data.

## Commands and rules

| Command | Behavior |
|---|---|
| `add-event ID "TITLE" CAPACITY` | Unique event ID; capacity 1-10000; title 1-80 characters. |
| `list` | Show events, bookings, capacity, and available seats. |
| `book EVENT STUDENT` | One booking per student per event; reject duplicates and full events. |
| `cancel EVENT STUDENT` | Remove an existing booking and free its seat; reject missing bookings. |
| `roster EVENT` | Show students in registration order. |
| `summary` | Show event count and total booked/available seats. |

## Read the architecture

- `FestPass.java`: CLI parsing, output, exit codes, and load/mutate/save flow.
- `BookingService.java`: validation, event management, and booking rules.
- `BookingStore.java`: versioned UTF-8 TSV persistence and atomic file replacement.
- `FestPassTest.java`: unit, persistence, CLI, corruption, and lock tests.
- `ci/Build.java`: compile all Java sources with `-Xlint:all -Werror`, test, package.
- `ci/SmokeTest.java`: launch the real JAR seven times against temporary data.
- `ci/BuildEvidence.java`: records pseudonymous submission evidence for both outcomes.
- `Jenkinsfile`: Checkout -> Submission setup -> Test -> Build JAR -> Smoke test JAR -> Save artifact; always archive evidence afterward.

]

