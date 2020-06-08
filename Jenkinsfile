node {
	def app
	
	stage('Clone repository') {
		checkout scm
	}
	
	stage('Build image') {
		app = docker.build('remushub/example-app')
	}
	
	stage('Approval'){
		timeout(time: 1, unit: 'HOURS') {
			input 'upload to Docker Hub?'
		}
	}
	
	stage('Test') {
		app.inside {
			sh 'npm test'
		}
	}
	
	
	stage('Push image') {
		docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
			app.push('latest')
		}
	}
}