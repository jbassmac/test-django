pipeline{
  agent any
  stages{
    stage('Checkout'){
      steps{
        git branch: 'main', url: 'https://github.com/jbassmac/test-django'
      }
    }
    stage('Build docker image'){
      steps{
        sh '''
          echo Run docker image ls
          docker image ls
      }
    }
  }
}
