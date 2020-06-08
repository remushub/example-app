node {
	def app
	
	stage('Clone repository') {
		checkout scm
	}
	
	stage('Build image') {
		app = docker.build('remushub/example-app', '-p 8000:8000')
	}
	
	stage('Test') {
		app.inside {
			sh 'npm test'
			sh 'sleep 300'
		}
	}
	
	stage('Approval') {
		timeout(time: 1, unit: 'HOURS') {
			input 'Upload to Docker Hub?'
		}
	}
	
	
	stage('Push image') {
		docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
			app.push('latest')
		}
	}
}