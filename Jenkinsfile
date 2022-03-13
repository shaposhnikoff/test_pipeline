  
pipeline {
    agent any
    
    options {
    ansiColor('xterm')
    }

    environment {
       ANSIBLE_CONFIG=".ansible.cfg"
    }

    stages {
        stage('Generate AMI for Jenkins Slave') {
            steps {
                git url: "https://github.com/shaposhnikoff/test_pipeline.git",
                    branch: $parameter1
                sh '''
                    		    
		    ami_base=$parameter1
                    echo $parameter1
		    echo $parameter2
		    echo $parameter3
		    packer build -on-error abort -machine-readable jenkins.json | tee build.log
                '''
            }
        }
    }

}

