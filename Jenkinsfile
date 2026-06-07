pipeline{
    agent any
    parameters{
        string(
            name: 'Branch Name',
            defaultValue: 'main',
            description: 'Git branch name'
        )
        string(
            name: 'APP_VERSION',
            defaultValue: '1.0',
            description: 'Application version'
        )
    }
    environment{
        BUILD_DIR = 'target'
        ARTIFACT_NAME = 'sample-maven-app'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: "${params.BRANCH_NAME}",
                    url: 'https://github.com/tejasvijain09/parameterized-pipeline.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Unit Testing') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Code Quality Check') {
            steps {
                sh 'mvn validate'
            }
        }

        stage('Artifact Packaging') {
            steps {
                sh 'mvn package'
                echo "Version: ${params.APP_VERSION}"
                echo "Artifact: ${ARTIFACT_NAME}"
                sh "ls -l ${BUILD_DIR}"
            }
        }
    }
}