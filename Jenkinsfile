pipeline {
    agent any
    triggers {
        cron('H * * * 1-5')
    }
    stages {
        stage('SCM') {
            steps {
                git 'https://github.com/wakaleo/game-of-life.git'
            }
        }
        stage('Build') {
            steps {
                 withSonarQubeEnv('SONAR') {
                    sh script: 'mvn clean package sonar:sonar'

                }
            }
        }
        stage('post build') {
            steps {
                junit 'gameoflife-web/target/surefire-reports/*.xml'
                archiveArtifacts 'gameoflife-web/target/*.war'
            }
        }
    }
}
