@Library('sharedlib')_
pipeline   {
    agent any
    tools {
        maven 'Maven3'
    }
    stages   {
        //stage('Clone the project from git')   {
            //steps   {
                //git credentialsId: 'git_cred', url: 'https://github.com/biswanathsubudhi/maven_work.git'
            //}
        //}
        
        stage('Build it using Maven')   {
            steps   {
                sh 'mvn clean package'
            }
        }
        
        stage('Deploy to Tomcat')   {
            steps   {
                deploytotomcat('tomcat','ec2-user','172.31.46.209')
            }
        }
        
        stage('Upload to Nenxus')   {
            steps   {
                nexusArtifactUploader artifacts: [[artifactId: 'myweb', classifier: '', 
                file: 'target/myweb.war', 
                type: 'war']], 
                credentialsId: '7891fac7-9335-4a65-a49f-c5ee9af0d2f1', 
                groupId: 'in.javahome', 
                nexusUrl: '65.0.81.107:8081', 
                nexusVersion: 'nexus3', protocol: 'http', 
                repository: 'sample-release', 
                version: '0.0.2-SNAPSHOT'
            }
        }
    }
}
