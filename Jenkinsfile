def buildNumber = BUILD_NUMBER
pipeline {
     
    agent any
    //for number an specific node
    /* 
    agent{
        label 'awsnode'
   }
   */

   // tools
   /*
   tools {
    nodejs 'nodejs15.30.0'
   }
*/
// Build type
/*

triggers{
   pollSCM('* * * * *') 
   cron('* * * * *')
   githubPush()
}

*/

    stages{
        stage('Cloning Git') {
            steps{
        git 'https://github.com/learningwithmainsh/Flask-Example.git'

    }
    }


stage('Building Docker Image'){
    steps{
        sh "docker build -t manishgenius/flask-example:${buildNumber} ."
    }
}
stage('Docker login and push'){

steps{
    
    withCredentials([string(credentialsId: 'Docker_hub_pwd', variable: 'DockerHubPwd')]) {
        
    // some block
    sh "docker login  -u  manishgenius -p ${DockerHubPwd}"
}
    sh " docker push manishgenius/flask-example:${buildNumber} "
}
}
stage('Deployment'){
    steps{


sshagent(['Docker_deployment_server']) 
  
   {
       //sh "ssh -o StrictHostKeyChecking=no ubuntu@13.232.59.220 'echo $HOME'"
       
    sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.13.106 docker rm -f  flask-example    || true"
    
//sh "ssh -o StrictHostKeyChecking=no ubuntu@13.232.59.220 ls"
 sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.13.106 docker run -d -p 8084:8084 --name flask-example manishgenius/flask-example:${buildNumber}  "
}

 
    }
}
}
post{
    /*
success{

emailext attachLog: true, body : '''Build Over ... Delcarative Way-success

 Regards,
 Manish,
 8765368754''', subject: 'Build Over...', to: 'mnshkmrpnd@gmail.com,manishkumarpandey144@gmail.com'
 
 /*
 emailext to: 'mnshkmrpnd@gmail.com,manishkumarpandey144@gmail.com'
          subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          body: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          replyTo: 'mnshkmrpnd@gmail.com'


}
failure{

emailext attachLog: true, body: '''Build Over.. Declarative-failed

 Regards,
 Manish,
 8765368754''', subject: 'Build Over...', to: 'mnshkmrpnd@gmail.com,manishkumarpandey144@gmail.com'
 
}


// Always when build is failed or success
always{
 emailext to: 'mnshkmrpnd@gmail.com,manishkumarpndey144@gmail.com',
          subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          body: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          replyTo: 'manishkumarpandey144@gmail.com@gmail.com'
}
*/

always{
    
    emailext attachLog: true, to: 'mnshkmrpnd@gmail.com,manishkumarpndey144@gmail.com',
             subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
             body: "Pipeline Build is over .. Build number  # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
             replyTo: 'manishkumarpandey144@gmail.com@gmail.com'
   }

}
}
