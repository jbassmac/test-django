pipeline{
  agent { label 'linux' }
  stages{
    stage('Checkout'){
      steps{
        git branch: 'main', url: 'https://github.com/jbassmac/test-django'
      }
    }
    stage('Login to ECR'){
      steps{
        withAWS(region: 'us-east-2', credentials: 'smanning-aws-creds'){
          sh '''
          docker login --username smanning.aws --password $(aws ecr get-login-password --region us-east-2) 690735260167.dkr.ecr.us-east-2.amazonaws.com
          '''
        }
      }
    }
    stage('Build docker image'){
      steps{
        sh '''
          docker build -t spadertech:django .
          docker image ls
          docker tag spadertech:django 690735260167.dkr.ecr.us-east-2.amazonaws.com/spadertech:django
        '''
      }
    }
    stage('Pushing image to ECR'){
      steps{
        sh '''
        docker push 690735260167.dkr.ecr.us-east-2.amazonaws.com/spadertech:django
        '''
      }
    }
  }
}
