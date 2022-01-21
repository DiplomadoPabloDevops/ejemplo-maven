pipeline {
    agent any
    stages {
       stage('Jar') {
            steps {
                script {
                    dir('C:/Users/PCAMPOS/.jenkins/workspace/peline_multibranch_feature-nexus2/build'){
                        bat  "curl -X GET -u admin:pablo1994 http://localhost:8089/repository/nexus-test/com/devopsusach2020/DevOpsUsach2020/0.0.1/DevOpsUsach2020-0.0.1.jar -O"     
                    }
                }
            }
        }
        stage('Run') {
            steps {
                script {
                        bat  "start /min mvnw.cmd spring-boot:run &"
                }
            }
        }
	    stage('Test') {
            steps {
                script {
                        bat  'curl -X GET "http://localhost:8081/rest/mscovid/test?msg=testing"'
                }
            }
        }
	    stage('Nexus Upload') {
            steps {
		    nexusPublisher nexusInstanceId: 'nexus_test', nexusRepositoryId: 'test-repo', 
		    packages: [[$class: 'MavenPackage', 
			mavenAssetList: [[classifier: '', 
			extension: '', 
			filePath: 'C:/Users/PCAMPOS/.jenkins/workspace/peline_multibranch_feature-nexus2/build/DevOpsUsach2020-0.0.1.jar']], 
			mavenCoordinate: [artifactId: 'DevOpsUsach2020', 
			groupId: 'com.devopsusach2020', 
			packaging: 'jar', 
			version: '1.0.0']
			]]
            }
        }
    }
}
