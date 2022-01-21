pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
                script {
                        bat  "./mvnw.cmd clean compile -e"           
                }
            }
        }

        stage('Test') {
            steps {
                script {
                        bat  "./mvnw.cmd clean test -e"
                }
            }
        }
       stage('Jar') {
            steps {
                script {
                        bat  "./mvnw.cmd clean package -e"
                }
            }
        }
	stage('SonarQube analysis 2') {
            steps {
                script {
                    def scannerHome = tool 'sonar-scanner';
                    withSonarQubeEnv('sonar-scanner') {
                    bat "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ejemplo-maven2 -Dsonar.sources=src/main/java/  -Dsonar.java.binaries=build -Dsonar.projectBaseDir=C:/Users/PCAMPOS/.jenkins/workspace/peline_multibranch_feature-nexus -Dsonar.login=8e8236752890bf7bb18bc071593360e27a3d0346"
                    }
                }
            }
        }
	stage('Nexus Upload') {
            steps {
		        nexusPublisher nexusInstanceId: 'nexus_test', nexusRepositoryId: 'test-repo', 
		        packages: [[$class: 'MavenPackage', 
			    mavenAssetList: [[classifier: '', 
			    extension: '', 
			    filePath: 'C:/Users/PCAMPOS/.jenkins/workspace/peline_multibranch_feature-nexus/build/DevOpsUsach2020-0.0.1.jar']], 
			    mavenCoordinate: [artifactId: 'DevOpsUsach2020', 
			    groupId: 'com.devopsusach2020', 
			    packaging: 'jar', 
			    version: '0.0.1']
			    ]]
            }
    }
	
    }
}
