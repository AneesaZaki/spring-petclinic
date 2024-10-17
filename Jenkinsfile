pipeline {
    agent any
    triggers {
        cron('H/10 * * * 1') // Every 10 minutes on Mondays
    }
    stages {
        stage('Build') {
            steps {
                script {
                    
                    sh './mvnw clean package'
                }
            }
        }
        stage('Code Coverage') {
            steps {
                script {
                    // Generate Jacoco report
                    sh './mvnw jacoco:report'
                }
            }
        }
    }
    post {
        always {
            junit '**/target/surefire-reports/*.xml' 
            jacoco execPattern: '**/target/jacoco.exec', classPattern: '**/target/classes', sourcePattern: '**/src/main/java', exclusionPattern: '**/test/**'
        }
    }
}