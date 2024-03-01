pipeline {
    agent any

    stages {
	    stage('Sonar Analysis') {
            steps {
                echo 'Code Analyzing..'
				
            }
        }
        stage('Build') {
            steps {
				echo 'Building..'
				sh 'cd webapp && npm install && npm run build'
            }
        }
		stage('Release') {
            steps {
				script{
					echo 'Releasing....'
					def packageJSON = readJSON file: 'webapp/package.json'
					def packageJSONVersion = packageJSON.version
					echo "${packageJSONVersion}"
					sh "zip webapp/dist-${packageJSONVersion}.zip -r webapp/dist"
					sh "curl -v -u admin:password --upload-file webapp/dist-${packageJSONVersion}.zip http://3.145.95.123:8081/repository/lms/"
				}
			}
        }
        stage('Deploy') {
            steps {
				script {
					echo 'Deploying....'
                    echo "Deploying.."       
                    def packageJSON = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version
                    echo "${packageJSONVersion}"  
                    sh "curl -u admin:password -X GET \'http://3.145.95.123:8081/repository/lms/dist-${packageJSONVersion}.zip\' --output dist-'${packageJSONVersion}'.zip"
                    sh 'sudo rm -rf /var/www/html/*'
                    sh "sudo unzip -o dist-'${packageJSONVersion}'.zip"
                    sh "sudo cp -r webapp/dist/* /var/www/html"
				}

            }
        }
    }
}