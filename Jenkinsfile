node
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

stage('SendMail')
{
mail bcc: '', body: '''Build done

Regards,
Uday.''', cc: '', from: '', replyTo: '', subject: 'Build Over', to: 'uday.pati02@gmail.com'    
}
}
