pipeline {
  agent any

  parameters {
  string defaultValue: 'first', name: 'Release_Name'
  imageTag credentialId: 'dockerhub-pwd', defaultTag: '25', filter: '.*', image: 'krishxo/jenkins-docker', name: 'DOCKER_IMAGE', registry: 'https://registry-1.docker.io', tagOrder: 'DSC_VERSION'
}

  stages {
    stage('Pulling Docker Image') {
      steps {
        echo "Release Name = $Release_Name"
        echo "Image = $DOCKER_IMAGE" 
        echo "Image Tag = $DOCKER_IMAGE_TAG" 
      }
    }
    stage('Checkout files'){
        steps{
          checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/krish-xo/poc-8.git']]])
            }
        }

    stage('Deploying Selected Image in Helm locally'){
            steps {
              bat '''
                helm upgrade  --install %Release_Name% helm/POC8 --set image.tag=%DOCKER_IMAGE_TAG%
              '''
			}
		}
	}
}
