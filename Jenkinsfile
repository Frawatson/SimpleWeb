pipeline{
    agent { label 'DOABuild_project' }
	
	 tools {
        maven "maven"
    }
    
    stages{
        stage('Scm Checkout'){
            steps{
                echo 'checking out from github'
                git 'https://github.com/Frawatson/SimpleWeb.git'
            }
        }
        stage('Unit testing and Packaging'){
            steps{
                echo 'Perform Maven Build'
                sh 'mvn -Dmaven.test.failure.ignore=true clean package'
            }
        }
         stage('Deploying package'){
            steps{
                echo 'Deploying package to tomcat server'
                script {
                   sshPublisher(publishers: [sshPublisherDesc(configName: 'tomcat_server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '.', remoteDirectorySDF: false, removePrefix: 'target/', sourceFiles: 'target/demo-0.0.1-SNAPSHOT.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                }
            }
        }
        
    }
}