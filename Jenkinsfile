node{
	stage('SCM Checkout'){
        git branch: 'wartomcat', url: 'https://github.com/ganez-bhoosal/devopsprojects.git'	}
	stage('Compile-Package'){
		def mvnHome = tool name: 'mymaven', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
	stage('Deploy to Tomcat'){
		sshagent(['tomcat-dev']) {
		sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@54.158.99.218:/opt/tomcat9/webapps/'
	}
	}
}
