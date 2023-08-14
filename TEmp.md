# Generating jacoco-report on local

#### 1. Run the project with test-cases on local which will generate jacoco.exec files at the path mentioned in each module's pom.xml or parent's pom.xml depends on the project structure
#### 2. Here in the case of dmp projects, we have functional test's exec files saved in dmp-shared repo which will also contribute to the coverage percentage which we can download using the
      `download-functional-test-exec-files` profile in code-coverage/pom.xml.
#### 3. Now, after generating all exec files, to generate report we'll run the project using code-coverage/pom with `complete-report-coverage` profile.

> Commands :-

1. `mvn clean test -f pom.xml`
2. `mvn clean install -f code-coverage/pom.xml -Pdownload-functional-test-exec-files`
3. `mvn clean install -f code-coverage/pom.xml -Pcomplete-report-coverage`
4. Get the coverage-report.xml from code-coverage/target/coverage-report/coverage-report.xml
   Or viewable `index.html` form code-coverage/target/coverage-report/html/index.html
<br/>

> Note: For some projects, `mvn clean test` may not work on local due to which we can't generate the report on local, for which a catch we can do is to comment out the `cleanWS(...)` from
> JenkinsFile *only for testing/debugging* by which you can get the coverage-report files directly from ci-build's workspace location.
  <br/><br/> Or to get the jacoco-ut.exec, jacoco-it.exec files the same we can get from ci-workspace, save it on local at project/target/coverage-reports, and then run `mvn clean install -f code-coverage/pom.xml -Pcomplete-report-coverage`
