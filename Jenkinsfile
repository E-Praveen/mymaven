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
        sh 'scp /home/ubuntu/.jenkins/workspace/scriptedpipeline1/webapp/target/webapp.war ubuntu@172.31.21.48:/var/lib/tomcat9/webapps/testingapp'
    }
    stage('ContinuousTesting')
    {
        git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
        sh 'java -jar /home/ubuntu/.jenkins/workspace/scriptedpipeline1/testing.jar'
    }
    stage('ContinuousDelivery')
    {
        input message: 'Need approval from the Delivery Manager', submitter: 'surya'
        sh 'scp /home/ubuntu/.jenkins/workspace/scriptedpipeline1/webapp/target/webapp.war ubuntu@172.31.22.177:/var/lib/tomcat9/webapps/prodapp1.war'
    }
}
