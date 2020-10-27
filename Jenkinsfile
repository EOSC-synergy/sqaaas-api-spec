@Library(['github.com/indigo-dc/jenkins-pipeline-library@fix/detached_head']) _

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
                    // branch 'master'
                    branch 'prototype/1.0'
                }
            }
            steps {
                script {
                    projectConfig = pipelineConfig(
                        './.sqa/config_docs.yml',
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
