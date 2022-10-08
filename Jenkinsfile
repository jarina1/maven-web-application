node
{
    def variable = tool name: "maven 3.8.6"
    
    stage('code from git')
    {
        git credentialsId: 'a6637bb3-d910-4ad2-be1c-e7a413417b0b', url: 'https://github.com/jarina1/maven-web-application.git'
    }
  stage('build')
    {
        sh "${variable}/bin/mvn  clean package"
    }
    stage('sonarqube report')
    {
      sh "${variable}/bin/mvn clean sonar:sonar" 
    }
    
    stage('upload artifact to nexus')
    {
        sh "${variable}/bin/mvn clean deploy"
    }
    stage('deploy app in to tomcat')
      { sshagent (['011f088b-c1bc-4d58-a060-a4e142850896'])
        {
        
         sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.109.210.73:/opt/apache-tomcat-9.0.65/webapps"
        } 

    }
    stage('Email Notifications')
    {
    emailext body: '''Build over......


   Regards,
   gori
  987654321''', subject: 'Build over', to: 'jarinadevops@gmail.com'
        
    }
}
