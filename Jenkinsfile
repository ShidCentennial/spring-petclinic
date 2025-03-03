pipeline {
    agent any

    // Trigger every 3 minutes on Mondays
    triggers {
        cron('H/3 * * * 1') 
    }

    stages {
        // Build stage
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        // Code Coverage stage
        stage('Code Coverage') {
            steps {
                // Generates code coverage report in target/site/jacoco/
                sh 'mvn test jacoco:report' 
            }
            post {
                success {
                    // Publish JaCoCo report (requires Jenkins JaCoCo plugin)
                    jacoco(
                        execPattern: 'target/jacoco.exec',
                        classPattern: 'target/classes',
                        sourcePattern: 'src/main/java'
                    )
                }
            }
        }
    }
}
