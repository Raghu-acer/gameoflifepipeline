pipeline {
    agent any
    triggers {
        cron('59 23 * * 1-5')
    }
    stages {
        stage('SCM') {
            steps {
                git 'https://github.com/wakaleo/game-of-life.git'
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
                stash name: 'warfile', includes: 'gameoflife-web/target/*.war'
            }
        }
        stage('copy to other node') {
            agent { label 'ecomm' }
            steps {
                unstash name: 'warfile'
            }
        }
    }
        post {
        always {
            mail to: 'raghudusa22@gmail.com', 
                subject: "Status of pipeline ",
                body: " has result "
        }
    }
}
