@Library('jenkins-shared-library-examples@main') _

pipeline {
    agent any

    stages {
        stage('Fetch Terraform Outputs') {
            steps {
                copyArtifacts(
                    projectName: 'terraform-infra-pipeline',
                    selector: lastSuccessful(),
                    filter: 'tf_outputs.json',
                    target: 'terraform-data' // store in subfolder
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
