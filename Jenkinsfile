pipeline {
    agent any
    stages {
        stage('SCM') {
            steps {
                git 'https://github.com/Raghu-acer/gameoflifepipeline.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('post build') {
            steps {
                junit 'gameoflife-web/target/surefire-reports/*.xml'
                archiveArtifacts 'gameoflife-web/target/*.war'
            }
        }
        stage('Build') {
            steps {
                ansiblePlaybook credentialsId: 'ansible', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'host', playbook: 'playbook.yaml'
            }
        }
    }
}
