pipeline {
    agent any

    stages {
        stage('Build') {
            stages {
                stage('Compile') {
                    steps {
                        echo 'Compiling...'
                        sleep 3
                    }
                }
                stage('Package') {
                    steps {
                        echo 'Packaging...'
                        sleep 3
                    }
                }
            }
        }

        stage('Registering build artifact') {
            steps {
                script {
                    echo 'Registering the metadata'
                    echo 'Another echo to make the pipeline a bit more complex'
                    def artifactOutput = registerBuildArtifactMetadata(
                        name: "h-e2e-qa-v2",
                        version: "1.0.2",
                        type: "docker",
                        url: "docker.io/hemaladev57/h-e2e-qa-v2:1.0.2",
                        digest: "a1223363706470703003461636632373839370",
                        label: "prod"
                    )
                    echo "Artifact output is: ${artifactOutput}"
                    env.ARTIFACT_ID = artifactOutput
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running Unit Tests...'
                sleep 2
            }
        }

        stage('Deploy') {
            steps {
                echo "Artifact ID : ${env.ARTIFACT_ID}"
                registerDeployedArtifactMetadata(
                    id: "${env.ARTIFACT_ID}",
                    url: "docker.io/hemaladev57/h-e2e-qa-v2:1.0.2",
                    targetEnvironment: "QA",
                    labels: "prod"
                )    
                echo 'Deploying...'
                sleep 2
            }
        }
        stage('Registering build artifact - 1') {
            steps {
                script {
                    echo 'Registering the metadata'
                    echo 'Another echo to make the pipeline a bit more complex'
                    def artifactOutput1 = registerBuildArtifactMetadata(
                        name: "h-e2e-qa-v2-1",
                        version: "1.0.2",
                        type: "docker",
                        url: "docker.io/hemaladev57/h-e2e-prod-v2-1:1.0.2",
                        digest: "ab223363706470703931101636632373832380",
                        label: "prod"
                    )
                    echo "Artifact output is: ${artifactOutput1}"
                    env.ARTIFACT_ID = artifactOutput1
                }
            }
        }

        stage('Test - 1') {
            steps {
                echo 'Running Unit Tests...'
                sleep 2
            }
        }

        stage('Deploy-1') {
            steps {
                echo "Artifact ID : ${env.ARTIFACT_ID}"
                registerDeployedArtifactMetadata(
                    id: "${env.ARTIFACT_ID}",
                    url: "docker.io/hemaladev57/h-e2e-qa-v2-1:1.0.2",
                    targetEnvironment: "Production",
                    labels: "prod"
                )    
                echo 'Deploying...'
                sleep 2
            }
        }
    }
}
