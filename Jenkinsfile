properties([pipelineTriggers([githubPush()])])
node('linux') {
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

    stage('Report') {
        withAWS(credentials:'AWS Access Key: AKIAJ5OD2RIINNISIIBA, AWS Secret Key: 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') {
            sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins-stack'
        }
    }
}