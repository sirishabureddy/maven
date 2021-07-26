pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git '  https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '4513fc33-e7e3-426f-997f-681354563c4e', path: '', url: 'http://172.31.5.118:8080')], contextPath: 'apptest', war: '**/*.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git '  https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/NewDeclarationPipeline/testing.jar'
            }
        }
    }
    post
    {
        success
        {
            
                deploy adapters: [tomcat9(credentialsId: '4513fc33-e7e3-426f-997f-681354563c4e', path: '', url: 'http://172.31.4.139:8080')], contextPath: 'appprod', war: '**/*.war'
        }
        failure
        {
            mail bcc: '', body: 'Jenkins is failing in CI stages', cc: '', from: '', replyTo: '', subject: 'ci Failed', to: 'sirisha.bureddy@gmail.com'
        }
    }
}
