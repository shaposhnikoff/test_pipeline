  
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
                git url: "git@github.com:knockrentals/ami_builder.git",
                    branch: "jenkins_slave"
                sh '''
                    cd jenkins_slave_ami_ubuntu
		    
		    ami_base=`aws ssm get-parameters --names \
		    /aws/service/canonical/ubuntu/server/20.04/stable/current/amd64/hvm/ebs-gp2/ami-id \
		    --region us-east-1 --query 'Parameters[0].Value' --output text`
                    packer build -on-error abort -machine-readable jenkins.json | tee build.log
                '''
            }
        }
    }

}

