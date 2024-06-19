pipeline {
    agent { label 'default' }
    parameters {
      string(name: 'Studentname', defaultValue: 'Selitckaya', description: 'What is your name?')
    }
    triggers {
        cron('H 0 * * *')
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
		sh "echo 'My UserName is $nadzeyase_USR'"
		sh "echo 'My Password is $nadzeyase_PSW'"
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
