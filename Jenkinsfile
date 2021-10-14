@Library('Shared') _
pipeline {
    agent any
	
	environment {
            bucketName = "test-cf-bucket-1117"
			stackFileName = "wp.yaml"
			VpcId = "vpc-05d5f8515bdb0950a"
			PubSub1 = "subnet-0331d497e6a04fb5e"
			PubSub2 = "subnet-0585cfd31c0f09a54"
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
                    deploy_stack(stackName: "${stackName}", bucketName: "${bucketName}", stackFileName: "${stackFileName}", env: "${ENV}", VpcId: "${VpcId}", PublicSubnet1: "${PubSub1}", PublicSubnet2: "${PubSub2}")
                }
            }
		
		  
    }
   }
