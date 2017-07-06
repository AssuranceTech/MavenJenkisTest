# Initial Environment

1. Jenkins
1. Pipeline Plugin
1. Pipeline Stage View Plugin
1. Checkstyle Plugin
1. Findbugs Plugin
1. PMD Plugin
1. Two agents: linux1, linux2
1. This repository

#Continuous Deployment Pipeline

### Compile

mvn clean install -DskipTests

### Test

1. linux1: mvn test -Diterations=5
1. linux2: mvn test -Diterations=10

Fail fast: do not wait for one branch to finish if the other one already failed.

### Code Quality

Checkstyle, Findbugs, PMD

### Deploy

1. Only one simultaneous deploy.
1. Wait human interaction before deploy.
1. Ask where to deploy.
1. Simulated by copying the JAR to localhost by scp.
