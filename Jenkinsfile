pipeline {
    agent any
    
     triggers {
        pollSCM ''
    }

    stages {

        stage('Checkout') {
            steps {
               echo 'pulling BBBRCCL and Promotion from Git Hub'
                 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'aec0f0bb-36a4-44bd-9bd4-21f118b01f2b', url: 'https://github.com/Vasanthkumar1821/promotionManagement.git']]])
                echo 'Success...'
            }
        }

        stage('Deploy') {
       tools {
                jdk "ibmjdk"
	       jdk "MavenHome"
            }
            steps {
           		bat 'java -version'
                echo 'Running sample Ant...'
                bat 'ant war' 

 			fileOperations([fileCopyOperation(excludes: '', flattenFiles: false, includes: 'BBBRCCL.war', targetLocation: 'C:/IBM/wlp/usr/servers/odm81000/dropins')])
            }
        }
	}
}
