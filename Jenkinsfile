@Library('shared-WP-Lib') _
pipeline {
    agent any	
	environment {
		
            bucketName = "testbucket-darren"
	    stackFileName = "wp.yml"
		AWS_REGION = 'us-east-1'		
    }
	parameters { 
		string(
			name: 'ENV', 
			defaultValue: 'DEV', 
			description: 'Please insert the environment'
			)
		string(
			name: 'stackName', 
			defaultValue: 'myStack-darren', 
			description: 'Please insert the stack name'
			)
	}	
    stages {     
	stage("Push template to S3") {
			steps {
				uploadFilesToS3(stackFileName: "${stackFileName}", workingDir: "${env.WORKSPACE}/stack_template", bucketName: "${bucketName}")
			}
		}
	    stage("Validate Template") {
		    steps {
				def response = cfnValidate(file: "${stackFileName}")
				echo "template description: ${response.description}"
		    }
	    }
		stage('Deploy Stack') {                  
            steps {
				deploy_stack(stackName: "${stackName}", bucketName: "${bucketName}", stackFileName: "${stackFileName}", env: "${ENV}")
            }
        }				  
    }
}
