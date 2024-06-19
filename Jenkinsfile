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

	stage('credentials') {
          environment {
        	nadzeyase = credentials('nadzeya-se')
    	  	}
	  steps {
                sh "echo 'My github token is $nadzeyase'"
		sh "echo 'My Username is $nadzeyase_Username_USR'"
		sh "echo 'My Password is $nadzeyase_Username_PSW'"
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
