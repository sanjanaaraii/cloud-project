# FestPass Assignment Completion

## Completed source changes

1. Added the required Jenkins SCM polling trigger:
   `pollSCM('H/1 * * * *')`.
2. Personalized the `help` output with the Git author alias: **Sanjana Rai**.
3. Fixed the seeded cancellation defect in `BookingService.cancel()` by removing the cancelled student from the event's registration set.
4. Left the supplied 28 tests unchanged.

## Diagnosis

The starter failed three tests related to cancellation:

- `cancellationFreesSeat`: cancelling a booking did not free the seat, so the next booking was rejected as SOLD OUT.
- `cancellationsSurviveReload`: the cancellation was not persisted because the in-memory booking remained.
- `cliWorkflowPersistsAcrossCommands`: the CLI still reported the cancelled student as booked.

The violated business rule was: **a successful cancellation must remove the student's booking and make that seat available again.**

## Local verification

Final verification:

- **28 tests, 0 failures**
- Real JAR smoke test: **7/7 scenarios passed**
- Sold-out rejection, cancellation, persistence, and seat reuse verified.
- Final JAR: `submission/artifacts/festpass.jar`

## Git trace prepared for Jenkins

1. `fab9d99` — Add FestPass starter and pipeline
2. `f05d17c` — Configure my Jenkins assignment
3. `0a8c530` — Personalize my help introduction
4. `c8b34ce` — Fix cancellation to free the booked seat

The repository is on branch `main`, with author name `Sanjana Rai`.

## Submission codes

Instructor-issued values have been entered in `submission.properties`:

- `class.code=001`
- `challenge.code=00487`

The evidence collector accepts the single-digit class code and uses these values when Jenkins generates the final submission evidence.
