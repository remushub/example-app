node {
	def app
	
	stage('Clone repository') {
		checkout scm
	}
	
	stage('Build image') {
		app = docker.build('remushub/example-app')
	}
	
	stage('Test') {
		app.inside {
			sh 'npm test'
		}
		timeout(time: 1, unit: 'HOURS') {
			input 'upload to Docker Hub?'
		}
	}
	
	
	stage('Push image') {
		docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
			app.push('latest')
		}
	}
}