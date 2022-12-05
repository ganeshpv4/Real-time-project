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
        stage("Quality gate status"){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, 
                    credentialsId: 'sonar-api'
                }
            }
        }
        stage("Upload jar file to nexus"){
            steps{
                script{
                    nexusArtifactUploader artifacts: 
                    [
                        [
                            artifactId: 'real-time', 
                            classifier: '', 
                            file: 'target/real-time-1.0-SNAPSHOT.jar', 
                            type: 'jar'
                            ]
                    ], 
                    credentialsId: 'nexus', 
                    groupId: 'com.example', 
                    nexusUrl: '44.203.231.49:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'demoapp-snapshot', 
                    version: '1.0-SNAPSHOT'
                }
            }
        }
    }
}