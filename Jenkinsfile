@Library('shared-WP-lib') _
pipeline {
    agent any
	
	environment {
            bucketName = "test-cf-bucket-1117"
	    stackFileName = "wp.yaml"
    }
	parameters { 
		string(
			name: 'ENV', 
			defaultValue: 'DEV', 
			description: 'Please insert the environment'
			)
		string(
			name: 'stackName', 
			defaultValue: 'myStack', 
			description: 'Please insert the stack name'
			)
	}	
    stages {     
		stage("Push template to S3") {
			steps {
				uploadFilesToS3(stackFileName: "${stackFileName}", workingDir: "${env.WORKSPACE}/stack_templates", bucketName: "${bucketName}")
			}
		}
		stage('Deploy Stack') {                  
                	steps {
                    		deploy_stack(stackName: "${stackName}", bucketName: "${bucketName}", stackFileName: "${stackFileName}", env: "${ENV}")
                }
            }				  
    }
}
