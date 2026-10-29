# Final Jenkins Steps

1. The instructor-issued values are already entered in `submission.properties`: `class.code=001` and `challenge.code=00487`.
2. Commit the updated `submission.properties`.
3. Create a new Jenkins **Pipeline** job using **Pipeline script from SCM**.
4. Git repository: `git://127.0.0.1:9418/festpass-java` (or the URL printed by the supplied local Git launcher).
5. Branch: `*/main`.
6. Script path: `Jenkinsfile`.
7. Credentials: none.
8. Use the `student-laptop` agent supplied by the lab.
9. Click **Build Now once** only to bootstrap the committed polling trigger.
10. For assessment evidence, make/observe the required automatic red build after the help-personalization commit, then the automatic green build after the cancellation fix.
11. Download the final `festpass.jar` and both Jenkins `submission-evidence.csv` files into separate build folders.
12. Run `java -jar festpass.jar help` and show the personalized introduction.
