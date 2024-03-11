pipeline {
    agent any

    tools {
        maven '3.9.6'
        jdk 'JDK11'
    }

    triggers {
        cron('H/10 * * * 1')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                powershell 'mvn clean package'
            }
        }

        stage('Code Coverage') {
            steps {
                powershell 'mvn org.jacoco:jacoco-maven-plugin:prepare-agent install'
                powershell 'mvn org.jacoco:jacoco-maven-plugin:report'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
            jacoco(execPattern: '**/target/jacoco.exec')
        }
    }
}
