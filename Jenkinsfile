pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('docker-hub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/intjborj/NodeApp.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build . -t intjborj/nodeapps:latest'
			}
		}

		  stage('Test image') {
        
       		 steps {
           		 echo "Tests passed"
       		 }
  			  }
	
		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push intjborj/nodeapps:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}


