
pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
 stages {
     stage('Git checkout code')
  {
	steps
	{
		git branch: 'main', url: 'https://github.com/ashumesh/express.git'
         echo 'Git Check-Out Succcessfully Completed'
		 
	}
  }

        stage('Build') { 
            steps 
            { 
                script
              {
                 app = docker.build("s3-repository")
                }
            }
        }
        stage('Test') 
       {
            steps {
                 echo 'Empty'
            }
        }
        stage('deploying docker image')
  {
    steps
	{   sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 136223150925.dkr.ecr.ap-south-1.amazonaws.com'
	    sh 'docker build -t front-back-repo .'
	    sh 'docker tag front-back-repo:latest 136223150925.dkr.ecr.ap-south-1.amazonaws.com/front-back-repo:latest'
            sh 'docker push 136223150925.dkr.ecr.ap-south-1.amazonaws.com/front-back-repo:latest'
		echo "deploying docker image"
	}
  }

    }
    
}


