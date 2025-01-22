 pipeline {
     agent any
     environment {
         DOCKER_CREDENTIALS = credentials('61a6f546-b9e9-4bc4-a0db-e6f9ce4941c4')
     }
     stages {	
         stage('Init') {
	     steps {
                 sh '''
      		#!/bin/bash
                python3 -m venv venv
                . ./venv/bin/activate
                pip install flake8
                flake8 app.py
                '''
             }
	 }
         stage('Lint') {
             steps {
                 sh 'flake8 app.py'
             }
         }
         stage('Format') {
             steps {
                 sh 'black --check app.py'
             }
         }
         stage('Build') {
             steps {
                 sh 'echo $DOCKER_CREDENTIALS_PSW | docker login -u $DOCKER_CREDENTIALS_USR --password-stdin'
                 sh 'docker build --network host -t  vojtechh12/netsoft-cicd-lab:0.0.1 .'
                 sh 'docker push vojtechh12/netsoft-cicd-lab:0.0.1'
             }
         }
     }
 }
