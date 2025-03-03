pipeline {
    agent any

    tools {
        maven 'M3'
    }

    triggers {
        cron('H/3 * * * 1') 
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package' 
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
