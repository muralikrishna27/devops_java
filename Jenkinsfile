pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/muralikrishna27/maven.git'
            }
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '9fcc54b9-3f06-46e0-81e4-514750b2f7da', path: '', url: 'http://172.31.85.244:8080')], contextPath: 'app', war: '**/*.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/muralikrishna27/devops_tester_project.git'
                
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '9fcc54b9-3f06-46e0-81e4-514750b2f7da', path: '', url: 'http://172.31.80.186:8080')], contextPath: 'prod', war: '**/*.war'
            }
        }
    }
}
