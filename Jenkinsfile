pipeline {
    agent { label 'default' }
    parameters {
      string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
    }
    triggers {
        cron('H 0 * * *')
    }

    stages {
        stage('write') {
            steps {
                script {
                    def content = "${params.Greeting}"
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
