pipeline {
    agent any

    tools {
        maven 'M3' // Matches the name in Jenkins Global Tool Configuration
    }

    triggers {
        cron('H/3 * * * 1') 
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package' // Use 'bat' instead of 'sh' for Windows
            }
        }

        stage('Code Coverage') {
            steps {
                bat 'mvn test jacoco:report'
            }
            post {
                success {
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
