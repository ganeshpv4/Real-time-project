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

    }
}