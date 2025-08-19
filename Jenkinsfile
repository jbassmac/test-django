pipeline{
  agent { label 'linux' }
  stages{
    stage('Checkout'){
      steps{
        git branch: 'main', url: 'https://github.com/jbassmac/test-django'
      }
    }
    stage("Test AWS CLI") {
        steps {
            withCredentials([[
                $class: 'AmazonWebServicesCredentialsBinding',
                credentialsId: 'smanning-aws-creds'
            ]]) {
                sh '''
                aws sts get-caller-identity --region us-east-2
                #docker build -t spadertech/django:1.1 .
                docker image ls
                #docker tag spadertech/django:1.1 690735260167.dkr.ecr.us-east-2.amazonaws.com/spadertech/django:1.1
                docker push 690735260167.dkr.ecr.us-east-2.amazonaws.com/spadertech/django:1.1
                '''
            }
        }
    }
  }
}
