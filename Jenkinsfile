node{
	stage('SCM Checkout'){
		git branch: 'slacknotification', url: 'https://github.com/prabhatpankaj/devopsprojects.git'
	}
	stage('Compile-Package'){
		def mvnHome = tool name: 'mymaven', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
	stage('Deploy to Tomcat'){
		sshagent(['tomcat-dev']) {
		sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@18.234.96.135:/opt/tomcat9/webapps/'
		}
	}
	stage('Slack Notification'){
	slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#jenkinslab', color: '#439FE0', message: 'New Build deployed', teamDomain: 'intelycore8', tokenCredentialId: 'secret-slack'
	}

}
