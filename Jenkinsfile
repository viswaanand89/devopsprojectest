pipeline
{
agent {
label 'default'
}
stages {
stage('checkout') {
steps {
sh ' this is checkout stage'
checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-credentials', url: 'https://github.com/viswaanand89/devopsprojectest.git']])
}
stage('build')
{
container('docker')
{
steps {
sh '''
nohup dockerd &
docker build -f Dockerfile -t ngixn .
'''
}
}
}
stage ('image push')
{
container('docker')
{
steps{
sh '''
docker image tag nginx nginx:${BUILD_NUMBER}
'''
}
}
}
}
}
