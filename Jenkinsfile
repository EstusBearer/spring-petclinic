pipeline {
    agent any

    tools {
        maven 'M3.8.1'
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
                sh 'mvn clean package'
            }
        }
        
        stage('Code Coverage') {
            steps {
                sh 'mvn org.jacoco:jacoco-maven-plugin:prepare-agent install'
                sh 'mvn org.jacoco:jacoco-maven-plugin:report'
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
