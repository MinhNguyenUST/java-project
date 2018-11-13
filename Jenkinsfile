properties([pipelineTriggers([githubPush()])])
node('linux') {
    git url: 'https://github.com/MinhNguyenUST/java-project.git', branch: 'master'
    stage('Test') {
        sh "env"
    }
}