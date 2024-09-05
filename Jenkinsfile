pipeline {
    agent any
    tools {
        maven  "maven" 
    }
		stages {
			stage('checkout') {
				steps {
					git branch: 'main', url: 'https://github.com/rayalavijay27/projectweb.git'
				}
			}
			stage('Build') {
				steps {
                    sh "mvn -Dmaven.test.failure.ignore=true clean package"
				}
			}
			stage('CodeQulity') {
				steps {
					withSonarQubeEnv('My SonarQube Server') {
					sh 'mvn clean package sonar:sonar'
					}
				}
			}
			stage('deploy to prod') {
				steps {
					deploy adapters: [tomcat9(credentialsId: 'tomcat-server', path: '', url:'http://172.31.33.151:8080/')], contextPath: null, war: '**/*.war'
				}
			}
		}	
}
