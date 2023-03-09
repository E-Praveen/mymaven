node('built-in')
{
    stage('ContinuousDownload')
    {
        git credentialsId: '035d0a68-54f2-446c-82af-c776ebc487b0', url: 'https://github.com/intelliqittrainings/maven.git'
    }
    stage('ContinuousBuild')
    {
        sh 'mvn package'
    }
    stage('ContinuousDeployment')
    {
        deploy adapters: [tomcat9(credentialsId: '035d0a68-54f2-446c-82af-c776ebc487b0', path: '', url: 'http://172.31.21.48:8080')], contextPath: 'mytestapp', war: '**/*.war'
    }
    stage('ContinuousTesting')
    {
        git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
        sh 'java -jar /home/ubuntu/.jenkins/workspace/scriptedpipeline1/testing.jar'
    }
    stage('ContinuousDelivery')
    {
        input message: 'Need approval from the Delivery Manager', submitter: 'surya'
        deploy adapters: [tomcat9(credentialsId: '035d0a68-54f2-446c-82af-c776ebc487b0', path: '', url: 'http://172.31.22.177:8080')], contextPath: 'myprodapp', war: '**/*.war'
    }
}
