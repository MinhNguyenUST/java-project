properties([pipelineTriggers([githubPush()])])
pipeline {
    agent { label 'linux'}
    
    stages {
        stage('Unit Tests') {
            steps {
                sh 'ant -f test.xml -v'
                junit 'reports/result.xml'
            }
        }

        stage('Build') {
            steps {
                sh 'ant -f build.xml -v'
            }
        }

        stage('Deploy') {
            steps {
                sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-*.jar s3://seis665-assignment9jenkins/'
            }
        }

        stage('Report') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws']]) {
                    sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins-stack'
                }
            }
        }
    }
}