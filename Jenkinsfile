@Library('jenkins-shared-library-examples@main') _

pipeline {
    agent any

    stages {
        stage('Fetch Terraform Output JSON') {
            steps {
                copyArtifacts(
                    projectName: 'terraform-infra-pipeline',
                    selector: [$class: 'LastSuccessfulBuildSelector'],
                    filter: 'tf_outputs.json',
                    target: 'terraform-data', // Optional subfolder
                    flatten: true
                )
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
}
