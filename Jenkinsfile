node('node1')
{
def Maven_Home= tool name: "Maven3.6.2"

stage('CheckoutCode')
{
    git branch: 'development', credentialsId: '2300bcab-7b91-49e0-9d44-c7de5b0928c3', url: 'https://github.com/udaykiranpati/maven-web-application.git'
}

stage('Build')
{
    sh "${Maven_Home}/bin/mvn clean package"
}

stage('SonarQubeReport')
{
    sh "${Maven_Home}/bin/mvn sonar:sonar"
}
stage('UploadToNexus')
{
    sh "${Maven_Home}/bin/mvn deploy"
}
    stage('DeployToTomcat')
{
        sshagent(['85f5a821-aded-41ae-b0d5-869d03f3a96c']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.145.181.247:/opt/apache-tomcat-9.0.59/webapps"
}
}

}
