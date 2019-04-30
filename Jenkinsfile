node
{
    
    properties([
    buildDiscarder(logRotator(numToKeepStr: '5')),
    pipelineTriggers([
        pollSCM('* * * * *')
    ])
])
  
  
    def mavenHome = tool name: 'Maven-Jenkins', type: 'maven'
    
    stage ('GitHub')
    {
        git credentialsId: '12c3d3fa-f720-4fd9-9c8a-50a0ec504f16', url: 'https://github.com/mohnreddy/maven-enterprise-application.git'
    }
    
    stage ('buildMaven')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    
    stage ('SonarQubeServer')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    
    stage ('NexusArtifactory')
    {
        sh "${mavenHome}/bin/mvn deploy"
    }
    
    stage ('WildflyDeploy')
    {
        sh "cp $WORKSPACE/MavenEnterpriseApp-ear/target/*.ear /opt/wildfly-16.0.0.Final/standalone/deployments"
    }
   
    
   
    
}
