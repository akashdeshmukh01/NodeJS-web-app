@Library('jenkins-shared-library-examples@main') _

pipeline {
    agent any

    stages {
        stage('Fetch Terraform Output JSON') {
            steps {
                script {
                    step([
                        $class: 'CopyArtifact',
                        projectName: 'terraform-infra-pipeline',
                        filter: 'tf_outputs.json',
                        target: 'terraform-data',
                        flatten: true,
                        selector: [$class: 'StatusBuildSelector']
                    ])
                }
            }
        }

        stage('CI Pipeline') {
            steps {
                script {
                    ciPipeline(terraformOutputFile: 'terraform-data/tf_outputs.json')
                }
            }
        }
    }

    post {
        success {
            echo "CI pipeline completed successfully!"
        }
        failure {
            echo "CI pipeline failed."
        }
    }
}
