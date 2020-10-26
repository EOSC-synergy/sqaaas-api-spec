@Library(['github.com/indigo-dc/jenkins-pipeline-library@release/2.1.0']) _

def projectConfig

pipeline {
    agent any

    stages {
        stage('OpenAPI linter') {
            steps {
                script {
                    projectConfig = pipelineConfig(
                        './.sqa/config_style.yml',
                        null,
                        null,
                        null,
                        'eoscsynergy/jpl-validator:jib-with-jpl'
                    )
                    buildStages(projectConfig)
                }
            }
            post {
                cleanup {
                    cleanWs()
                }
            }
        }
        stage('SQA baseline dynamic stages') {
            when {
                anyOf {
                    branch 'master'
                    branch 'prototype/1.0'
                }
            }
            steps {
                script {
                    projectConfig = pipelineConfig(
                        './.sqa/config.yml',
                        null,
                        null,
                        null,
                        'eoscsynergy/jpl-validator:jib-with-jpl'
                    )
                    buildStages(projectConfig)
                }
            }
            post {
                cleanup {
                    cleanWs()
                }
            }
        }
    }
}
