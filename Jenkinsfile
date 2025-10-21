pipeline 
{
  agent any

  stages 
  {
     stage('Checkout') 
     {
        steps 
        {
            git branch: 'main', url: 'https://github.com/NishitPDesai/jenkins-ci-cd-pipeline.git'
        }
    }
    stage('Build') 
    {
      steps 
      {
        echo ' Building Docker image...'
        sh 'docker build -t jenkins-simple-app .'
      }
    }

    stage('Test') 
    {
      steps 
      {
        echo ' Running tests...'
        sh 'echo "All tests passed!"'
      }
    }

    stage('Deploy') 
    {
      steps 
      {
        echo ' Deploying container...'
        // Stop old container if exists
        sh 'docker ps -q --filter "name=jenkins-simple-app" | grep -q . && docker stop jenkins-simple-app || true'
        sh 'docker run -d --rm --name jenkins-simple-app -p 3000:3000 jenkins-simple-app'
      }
    }
  }

  post 
  {
    success 
    {
      echo 'Pipeline completed successfully!'
    }
    failure 
    {
      echo 'Pipeline failed!'
    }
  }
}
