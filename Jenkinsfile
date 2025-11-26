pipeline{
    agent any

    stages{
        stage('scm'){
            steps{
                checkout scm
            }
        }
        stage('build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('nexus'){
            steps{
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'onlinebookstore', 
                        classifier: '', 
                        file: '/var/lib/jenkins/workspace/webapplication/target/onlinebookstore-0.0.1-SNAPSHOT.war', 
                        type: 'war'
                        ]
                    ]
                        credentialsId: 'Nexus', 
                        groupId: 'onlinebookstore', 
                        nexusUrl: '98.93.104.26:8081/', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: 'online-bookstorerepo', 
                        version: '3.81.1-01-SNAPSHOT'
            }
        }
        stage('deploy'){
            steps{
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'Tomcat', 
                        path: '', 
                        url: 'http://54.237.215.186:8080/')
                        ], 
                        contextPath: null, 
                        war: '**/*.war'
            }
        }
    }
}
