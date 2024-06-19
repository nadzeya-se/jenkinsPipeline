pipeline {
    agent { label 'default' }
    parameters {
      string(name: 'Studentname', defaultValue: 'Selitckaya', description: 'What is your name?')
    }
    triggers {
        cron('H 0 * * *')
    }

    environment {
        CREDENTIALS = credentials('nadzeya-se')
    }

    stages {
        stage('write') {
            steps {
                script {
                    def content = "Hello ${params.Studentname}!"
                    writeFile(file: 'result.txt', text: content)
                }
            }
        }

        stage('archive') {
            steps {
                archiveArtifacts artifacts: 'result.txt', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
