node('built-in') 
{
    stage('ContDownload')
    {
        git 'https://github.com/muralikrishna27/maven.git'
    }
    stage('ContBuild')
    {
        sh 'mvn package'
    }
    stage('Contdeployment')
    {
        deploy adapters: [tomcat9(credentialsId: '9fcc54b9-3f06-46e0-81e4-514750b2f7da', path: '', url: 'http://172.31.85.244:8080')], contextPath: 'testapp', war: '**/*.war'
    }
    stage('ContTesting')
    {
        git 'https://github.com/muralikrishna27/devops_tester_project.git'
        
        sh 'java -jar /var/lib/jenkins/workspace/ScriptedPipeline1/testing.jar'
    }
    stage('ContDelivery')
    {
        input message: 'Need Approval from DM!', submitter: 'sandeep'
        
        deploy adapters: [tomcat9(credentialsId: '9fcc54b9-3f06-46e0-81e4-514750b2f7da', path: '', url: 'http://172.31.80.186:8080')], contextPath: 'prodapp', war: '**/*.war'
    }
}
