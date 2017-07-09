stage 'Compile'
node('master') 
{    
    checkout scm    // use for non multibranch: git 'https://github.com/amuniz/maven-helloworld.git'    
    def mvnHome = tool 'maven-3.3.9'    
    sh "${mvnHome}/bin/mvn clean install -DskipTests"    
    stash 'working-copy'
}
stage 'Test'
parallel one: {
    node('master') {
        unstash 'working-copy'
        def mvnHome = tool 'maven-3.3.9'
        sh "${mvnHome}/bin/mvn test -Diterations=10"
    }
}, two: {
    node('master') {
        unstash 'working-copy'
        def mvnHome = tool 'maven-3.3.9'
        sh "${mvnHome}/bin/mvn test -Diterations=5"
    }
}, failFast: true
