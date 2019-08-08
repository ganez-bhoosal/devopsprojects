node{
	stage('SCM Checkout'){
		git branch: 'smtpjenkins', url: 'https://github.com/prabhatpankaj/devopsprojects.git'
	}
	stage('Compile-Package'){
		def mvnHome = tool name: 'maven', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
	stage('Deploy to Tomcat'){
		sshagent(['tomcat-dev']) {
		sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@3.84.122.116:/opt/tomcat9/webapps/'
	}
	}
	stage('Slack Notification'){
	slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#jenkins', color: '#439FE0', message: 'New Build deployed', teamDomain: 'intelycore4', tokenCredentialId: 'slack-secret'
	}
	stage('Email Notification'){
	mail bcc: '', body: 'This is body', cc: '', from: 'prabhatiitbhu@gmail.com', replyTo: 'prabhatiitbhu@gmail.com', subject: 'This is Subject', to: 'prabhat@aptence.com'
	}

}

