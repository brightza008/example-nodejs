pipeline {
    agent any

    stages {
        
        /*stage('clean up') {
        	steps {
                cleanWs()
            }
        } */ //End stage
        
        stage('clear existing dontainer') {
        	steps {
                sh'''
                  pwd
                  hostname 
                  ifconfig
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
