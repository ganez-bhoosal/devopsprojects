node{
	stage('SCM Checkout'){
		git branch: 'smtpjenkins', url: 'https://github.com/prabhatpankaj/devopsprojects.git'
	}
	stage('Compile-Package'){
		def mvnHome = tool name: 'mymaven', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
	stage('Deploy to Tomcat'){
		sshagent(['tomcat-dev']) {
		sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@3.84.122.116:/opt/tomcat9/webapps/'
	}
	}
	stage('Slack Notification'){
	slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#jenkins', color: '#439FE0', message: 'New Build deployed', teamDomain: 'intelycore8', tokenCredentialId: 'secret-slack'
	}
	stage('Email Notification'){
	mail bcc: '', body: 'This is body', cc: '', from: 'ganez.bhoosal@gmail.com', replyTo: 'ganez.bhoosal@gmail.com', subject: 'This is Subject', to: 'prabhat@aptence.com'
	}

}

