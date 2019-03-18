def SECRET_NAME = "mysql-test-secret"
pipeline {
    agent any
    options { skipDefaultCheckout() }
    stages {    
        stage ('Running on Test Environment'){
            steps{
                 checkout scm
                 echo "Retriving DB credentials from AWS secret manager"
                script {
                 test="abhi123"
                 sh "echo ${test}"
                 var="\$(date)"
                 sh "echo ${var}"
                }
                script {
                 sh "echo ${SECRET_NAME}"
                 username="""\$(/usr/local/bin/aws secretsmanager get-secret-value --secret-id ${SECRET_NAME} --region ap-south-1 --version-stage AWSCURRENT | jq .SecretString | jq fromjson | jq -r .username)"""
                 password="""\$(/usr/local/bin/aws secretsmanager get-secret-value --secret-id ${SECRET_NAME} --region ap-south-1 --version-stage AWSCURRENT | jq .SecretString | jq fromjson | jq -r .password)"""
                 //user="""\$(echo ${secret} | jq -r .username)"""
                 //password="""\$(echo ${secret} | jq -r .password)"""
                 sh "echo ${username}"
                 sh "echo ${password}"
                 //sh 'secret=$(/usr/local/bin/aws secretsmanager get-secret-value --secret-id mysql-test-secret --region ap-south-1 --version-stage AWSCURRENT | jq .SecretString | jq fromjson)'
                }
                 //sh """user=$(echo ${secret} | jq -r .username)"""
                 //password="$(echo ${secret} | jq -r .password)"
                 //sh "echo ${user}"
                 //sh "echo ${password}"
               
                sh 'test build'
                echo "successfully tested"
           }
       }
    }
}
