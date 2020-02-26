pipeline {
    agent any
    environment { 
        PATH = "$PATH:/usr/local/bin" //define docker-compose for jenkins user 
    }
    stages {
        stage('clear existing dontainer') {
        	steps {
                sh'''
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
