pipeline {
    agent any
    options { skipDefaultCheckout() }
    stages {    
        stage ('Running on Test Environment'){
            steps{
                checkout(
                    [$class: 'GitSCM', branches: [[name: '*/master']], 
                    doGenerateSubmoduleConfigurations: false, extensions: [], 
                    submoduleCfg: [], 
                    userRemoteConfigs: [[url: 'https://github.com/jainahik/new.git']]])
                    
        
                 echo "Retriving DB credentials from AWS secret manager"
                 def test = "abhi123"
                 echo $test
                 //secret='$(/usr/local/bin/aws secretsmanager get-secret-value --secret-id mysql-test-secret --region ap-south-1 --version-stage AWSCURRENT | jq .SecretString | jq fromjson) | bash -'
                 //echo $secret
                 sh 'user="$(echo $secret | jq -r .username)"'
                 sh 'password="$(echo $secret | jq -r .password)"'
                 echo $user
                 echo $password
                    
                sh 'test build'
                echo "successfully tested"
           }
       }
    }
}
