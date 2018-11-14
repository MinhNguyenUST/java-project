properties([pipelineTriggers([githubPush()])])
pipeline {
    agent any
    
    stages {
        stage('Test') {
            steps{
                sh "env"
            }
        }

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
                withAwsCli(defaultRegion: 'us-east-1') {
                    sh "aws s3 cp /workspace/java-pipeline/dist/rectangle-*.jar s3://seis665-assignment9jenkins/"
                }
            }
        }
    }
}