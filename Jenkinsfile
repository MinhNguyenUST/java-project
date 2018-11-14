properties([pipelineTriggers([githubPush()])])
pipeline {
    agent any
    git url: 'https://github.com/MinhNguyenUST/java-project.git', branch: 'master'
    stage('Test') {
        sh "env"
    }

    stage('Unit Tests') {
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
    }

    stage('Build') {
        sh 'ant -f build.xml -v'
    }

    stage('Deploy') {
        sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-*.jar s3://seis665-assignment9jenkins/'
    }

    
}