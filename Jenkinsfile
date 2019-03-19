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
                 secret="""\$(/usr/local/bin/aws secretsmanager get-secret-value --secret-id ${SECRET_NAME} --region ap-south-1 --version-stage AWSCURRENT | jq .SecretString | jq fromjson)"""
                 //username="""\$(/usr/local/bin/aws secretsmanager get-secret-value --secret-id ${SECRET_NAME} --region ap-south-1 --version-stage AWSCURRENT | jq .SecretString | jq fromjson | jq -r .username)"""
                 //password="""\$(/usr/local/bin/aws secretsmanager get-secret-value --secret-id ${SECRET_NAME} --region ap-south-1 --version-stage AWSCURRENT | jq .SecretString | jq fromjson | jq -r .password)"""
                 username="""\$(echo ${secret} | jq -r .username)"""
                 password="""\$(echo ${secret} | jq -r .password)"""
                 sh('#!/bin/sh -e\n' + "echo ${username}")
                 sh('#!/bin/sh -e\n' + "echo ${password}")
                }
                 sh('#!/bin/sh -e\n' + "sed -i 's/DB_USERNAME/'${user}'/g' cred_replace")
                 sh('#!/bin/sh -e\n' + "sed -i 's/DB_PASSWORD/'${password}'/g' cred_replace")
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
