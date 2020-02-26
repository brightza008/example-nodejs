pipeline {
    agent any
    environment { 
        PATH = "$PATH:/usr/local/bin" //define docker-compose command
    }
    stages {
        
        /*stage('clean up') {
        	steps {
                cleanWs()
            }
        } */ //End stage
        
        stage('clear existing dontainer') {
        	steps {
                sh'''
                  docker info
                  docker-compose stop
                '''

            }
        } //End stage
        
        stage('deploy docker container') {
        	steps {
                sh'''
                  docker-compose up -d
                '''
            }
        } //End stage
    }//End stages
}//End pipeline
