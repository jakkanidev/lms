pipeline {
    agent any

    stages {
	    stage('Sonar Analysis') {
            steps {
                echo 'Code Analyzing..'
				sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://18.190.219.36:9000/" -e SONAR_LOGIN="sqp_9e319516f4f045d62d631f5b448abeda41bb34ba"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}