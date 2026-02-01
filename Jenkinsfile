//scripted-way-pipeline without slack notification
/*node
{
    // /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven-3.9.6
    def mavenHome=tool name: "maven-3.9.6"
    stage('git checkout')
    {
        git branch: 'dev', url: 'https://github.com/kkdevopsb7-7nov/maven-webapplication-project-kkfunda.git'
    }
    stage('maven compile')
    {
        //sh "mvn compile"
        sh "${mavenHome}/bin/mvn compile"
    }
    stage('Build')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('SQ Report')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('Deploy into Nexus')
    {
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage('Deploy to Tomcat') 
    {
      
      sh """

      curl -u noor:noor \
--upload-file /var/lib/jenkins/workspace/scripted-way-PL-1/target/maven-web-application.war \
"http://13.233.164.36:8080/manager/text/deploy?path=/maven-web-application&update=true"
         
        """
    }
} //node ending
*/



//scripted-way-pipeline with slack notification
/* node
{
    // /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven-3.9.6
    def mavenHome=tool name: "maven-3.9.6"

    echo "git branch Name: ${env.BRANCH_NAME}"
    echo "build number: ${env.BUILD_NUMBER}"

    try
    {

     stage('git checkout')
    {
        notifyBuild('STARTED')
        git branch: 'dev', url: 'https://github.com/kkdevopsb7-7nov/maven-webapplication-project-kkfunda.git'
    }
    stage('maven compile')
    {
        sh "${mavenHome}/bin/mvn compile"
    }
    stage('Build')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('SQ Report')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('Deploy into Nexus')
    {
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage('Deploy to Tomcat') 
    {
      
      sh """

      curl -u noor:noor \
--upload-file /var/lib/jenkins/workspace/scripted-way-PL-1/target/maven-web-application.war \
"http://3.110.215.184:8080/manager/text/deploy?path=/maven-web-application&update=true"
         
        """
    }
     


    } //try block end

    catch (e) {
   
       currentBuild.result = "FAILED"

   } finally {
    // Success or failure, always send notifications
    notifyBuild(currentBuild.result)       //function calling
   }


} //node ending
 


def notifyBuild(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESS'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESS') {
    color = 'GREEN'
    colorCode = '#27F535'
  } else {   
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary, channel: '#jio-dev')
  
}
*/
// >>>>>Declarative-Way-Pipeline without slack notification 

/*pipeline
{
	
   agent any
   tools
   {
      maven "maven-3.9.6"
   }
   stages
   {
           stage('git checkout')
           {
              steps
              {
                 git branch: 'dev', url: 'https://github.com/kkdevopsb7/maven-webapplication-project-kkfunda.git'
              }
           }
           stage('compile')
           {
              steps
              {
                 sh "mvn compile"
              }
           }
           stage('Build')
           {
             steps
             {
               sh "mvn clean package"
             }
           }
           stage('SQ REPORT')
           {
             steps
             {
                sh "mvn sonar:sonar"
             }
           }
           stage('Deploy to nexus')
           {
              steps
              {
                sh "mvn clean deploy"
              }
           }
           stage('Deploy to tomcat')
           {
              steps
              {
                 sh """

      curl -u noor:noor \
--upload-file /var/lib/jenkins/workspace/jio-Declarative-PL-dev/target/maven-web-application.war \
"http://13.127.216.234:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
              }
           }

   }  //stages ending


} //pipeline ending

*/





//jenkins 09-Dec 2025 


//10-Dec-2025>>>>>Declarative-Way-Pipeline with slack notification

/*pipeline
{
	
   agent any
   tools
   {
      maven "maven-3.9.6"
   }
   stages
   {
           stage('git checkout')
           {
              steps
              {
                 notifyBuild('STARTED') 
                 git branch: 'dev', url: 'https://github.com/kkdevopsb7-7nov/maven-webapplication-project-kkfunda.git'
              }
           }
           stage('compile')
           {
              steps
              {
                 sh "mvn compile"
              }
           }
           stage('Build')
           {
             steps
             {
               sh "mvn clean package"
             }
           }
           stage('SQ REPORT')
           {
             steps
             {
                sh "mvn sonar:sonar"
             }
           }   
           stage('Deploy to nexus')
           {
              steps
              {
                sh "mvn clean deploy"
              }
           }
           stage('Deploy to tomcat')
           {
              steps
              {
                 sh """

      curl -u noor:noor \
--upload-file /var/lib/jenkins/workspace/jio-Declarative-PL-dev/target/maven-web-application.war \
"http://13.232.14.231:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
              }
           }

   }  //stages ending

post {
  success {

    script
    {
     notifyBuild(currentBuild.result)
    }
    
  }
  failure {

  script
  {
    notifyBuild(currentBuild.result)

  }
   
  }
}



} //pipeline ending



// Notification method
def notifyBuild(String buildStatus = 'STARTED') {
    buildStatus = buildStatus ?: 'SUCCESS'

    def colorCode
    def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
    def summary = "${subject} (${env.BUILD_URL})"

    switch (buildStatus) {
        case 'STARTED':
            colorCode = '#FFFF00' // Yellow
            break
        case 'SUCCESS':
            colorCode = '#00FF00' // Green
            break
        default:
            colorCode = '#FF0000' // Red
    }

    slackSend(color: colorCode, message: summary)
} */

//upstream and downstream job uat

pipeline
{
   
   agent any
   tools
   {
      maven "maven-3.9.6"
   }
   stages
   {
           stage('git checkout')
           {
              steps
              {
                 
                 git branch: 'uat', url: 'https://github.com/kkdevopsb7-7nov/maven-webapplication-project-kkfunda.git'
              }
           }
           stage('compile')
           {
              steps
              {
                 sh "mvn compile"
              }
           }
           stage('Build')
           {
             steps
             {
               sh "mvn clean package"
             }
           }
           stage('SQ REPORT')
           {
             steps
             {
                sh "mvn sonar:sonar"
             }
           }
           stage('Deploy to nexus')
           {
              steps
              {
                sh "mvn clean deploy"
              }
           }
           stage('Deploy to tomcat')
           {
              steps
              {
                 sh """

      curl -u noor:noor \
--upload-file /var/lib/jenkins/workspace/jio-Declarative-PL-dev/target/maven-web-application.war \
"http://65.0.101.225:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
              }
           }
           

   }  //stages ending


} //pipeline ending




