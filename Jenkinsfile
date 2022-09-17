node{

def mavenhome = tool name:"maven3.8.6"


echo "jenkins url is: ${env.JENKINS_URL}"
echo "node name is: ${env.NODE_NAME}"
echo "job name is: ${env.JOB_NAME}"


stage('checkoutcode'){
git credentialsId: '50807e49-f15c-4430-9b3e-88e9eebec659', url: 'https://github.com/pm-ec/maven-web-application.git'
}
stage('build'){
sh "${mavenhome}/bin/mvn clean package"
}

stage('Executesonarqubereport'){
sh "${mavenhome}/bin/mvn clean sonar:sonar"
}
stage('uploadartifactsintoartifactrepo'){
sh "${mavenhome}/bin/mvn clean deploy"
}
stage('DeployappintoTomcatserver'){
sshagent(['c5a35e67-1b51-4d6b-970d-304a3efcf439']) {
sh "scp  -o StrictHostKeyChecking=no target/maven-web-application.war  ec2-user@172.31.46.68:/opt/apache-tomcat-9.0.65/webapps/"    
}
}
}

