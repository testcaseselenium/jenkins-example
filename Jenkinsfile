pipeline {
   agent any

   stages {
      stage('Build') {
         steps {
            // Run Maven on a Unix agent.
            bat "mvn test -f testing/pom.xml"
            // To run Maven on a Windows agent, use
            //bat "mvn -Dmaven.test.failure.ignore=true clean package"
         }
         post {
            // If Maven was able to run the tests, even if some of the test
            // failed, record the test results and archive the jar file.
               always{
                archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
                junit "**/target/surefire-reports/*.xml"
               }
         }
      }
   }
}
