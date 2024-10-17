pipeline {
    agent any
    triggers {
        cron('H/10 * * * 1') // Every 10 minutes on Mondays
    }
    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'  
            }
        }
        stage('Code Coverage') {
            steps {
                bat 'mvn jacoco:report'  
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
