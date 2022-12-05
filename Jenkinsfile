pipeline{

    agent any

    stages{

        stage("Git checkout"){

            steps{
                git branch: 'main', 
                credentialsId: 'git', 
                url: 'https://github.com/ganeshpv7/Real-time-project.git'
            }
        }

        stage("UNIT Testing"){
            steps{
                sh 'mvn test'
            }
        }
        stage("Integration test"){
            steps{
                sh 'mvn verify -DskipUnitTest'
            }
        }
        stage("Maven build"){
            steps{
                sh 'mvn clean install'
            }
        }
        stage("Sonarqube Analysis"){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
    }
}