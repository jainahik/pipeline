def secret = ""
def user = ""
pipeline {
    agent any
    options { skipDefaultCheckout() }
    stages {    
        stage ('Running on Test Environment'){
            steps{
                 checkout scm
                 echo "Retriving DB credentials from AWS secret manager"
                 //test = "abhi123"
                 //sh "echo ${test}"
                 //sh 'var=$(date)'
                 //sh "echo '$var'"
                script {
                 secret='''$(/usr/local/bin/aws secretsmanager get-secret-value --secret-id mysql-test-secret --region ap-south-1 --version-stage AWSCURRENT | jq .SecretString | jq fromjson)'''
                 sh "echo ${secret}"
                 //sh 'secret=$(/usr/local/bin/aws secretsmanager get-secret-value --secret-id mysql-test-secret --region ap-south-1 --version-stage AWSCURRENT | jq .SecretString | jq fromjson)'
                }
                 sh """user=$(echo ${secret} | jq -r .username)"""
                 password="$(echo ${secret} | jq -r .password)"
                 sh "echo ${user}"
                 sh "echo ${password}"
               
                sh 'test build'
                echo "successfully tested"
           }
       }
    }
}
