@Library('shared-WP-Lib') _
pipeline {
    agent any	
	environment {		
            bucketName = "testbucket-darren"
	    stackFileName = "wp.yml"
	    awsRegion = 'us-east-1'
	    VpcId = "vpc-05d5f8515bdb0950a"
	    PSubet1 = "subnet-0331d497e6a04fb5e"
	    PSubnet2 = "subnet-0585cfd31c0f09a54"
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
				uploadFilesToS3(
					Region: "${awsRegion}",
					stackFileName: "${stackFileName}",
					workingDir: "${env.WORKSPACE}/stack_template",
					bucketName: "${bucketName}"
				)
			}
		}
	    
		stage('Deploy Stack') {                  
            steps {
				deploy_stack(
					stackName: "${stackName}",
					bucketName: "${bucketName}",
					stackFileName: "${stackFileName}",
					env: "${ENV}",
					VpcId: "${VpcId}",
					PublicSubnet1: "${PSubnet1}",
					VpcId: "${PSubnet2}"
				)
            }
        }				  
    }
}
