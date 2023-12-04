pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' 
            }
        }
        stage('Unit test') {
            steps {
              sh "mvn test"       
    }
}
        stage('Code Coverage') {
            steps {
                // Run JaCoCo to collect code coverage
                jacoco(execPattern: '**/target/classes', classPattern: '**/target/classes/**/*.class')

                // Publish JaCoCo results
                jacocoReport('**/*.exec')    
    }
}
        post {
        always {
            // Publish JaCoCo coverage report
            jacocoCoverage('50') // Set the desired coverage threshold
  }
}
  }
}