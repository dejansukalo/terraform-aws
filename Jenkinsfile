pipeline {
  agent any
  environment {
    AWS_DEFAULT_REGION="eu-central-1"
  }
  stages {
    stage('Hello') {
      steps {
        withCredentials([aws(accessKeyVariable:'AWS_ACCESS_KEY_ID',credentialsId:'927112977430',secretKeyVariable:'AWS_SECRET_ACCESS_KEY')]) {
          sh '''
            aws --version
            aws ec2 describe-instances
          '''
        }
      }
    }
    stage ('provision server') {
        steps {
            withCredentials([aws(accessKeyVariable:'AWS_ACCESS_KEY_ID',credentialsId:'927112977430',secretKeyVariable:'AWS_SECRET_ACCESS_KEY')]) {
                dir('terraform') {
                    sh "terraform init"
                    sh "terraform apply -auto-approve"
                    EC2_PUBLIC_IP = sh(
                        script: "terraform output ec2_public_ip"
                    ).trim()
                }
            }
        }
    }
    stage ('deploy') {
        steps {
            script {
                sleep(time: 90, unit: "SECONDS")

            }
        }
    }
  }
}