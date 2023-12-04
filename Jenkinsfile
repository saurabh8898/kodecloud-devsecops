pipeline {
    agent { label 'maven' }

    stages {
        stage('Build Artifact') {
            steps {
                script {
                    // Use Maven Wrapper for clean build
                    sh "./mvnw clean"
                    
                    // Build the package (skip tests for now)
                    sh "./mvnw package -DskipTests=true"
                    
                    // Archive the JAR file
                    archiveArtifacts 'target/*.jar'
                }
            }
        }

        stage('Unit Test') {
            steps {
                script {
                    // Run Maven tests
                    sh "./mvnw test"
                }
            }
        }

        stage('Code Coverage') {
            steps {
                script {
                    // Run JaCoCo to collect code coverage
                    jacoco(execPattern: '**/target/classes', classPattern: '**/target/classes/**/*.class')

                    // Publish JaCoCo results
                    jacocoReport('**/*.exec')
                }
            }
        }
    }

    post {
        always {
            // Publish JaCoCo coverage report
            jacocoCoverage('50') // Set the desired coverage threshold
        }
    }
}
