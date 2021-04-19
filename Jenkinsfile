pipeline {
    agent none
    stages {
        stage('lint') {
            parallel {
                // stage('precommit') {
                //     steps {
                //         sh('python3 -m pip install --no-warn-script-location --user pre-commit')
                //         sh('python3 -m pre_commit run --all-files')
                //     }
                // }
                stage('flakehell') {
                    agent { docker { image 'docker.werally.in/rally-docker/rally-ci-python' } }
                    steps {
                        sh('python3 -m pip install --no-warn-script-location --user tox')
                        sh('python3 -m tox -e lint')
                    }
                }
            }
        }
        stage('pytest') {
            parallel {
                stage('3.8') {
                    agent { docker { image 'docker.werally.in/rally-docker/rally-ci-python:3.8.9' } }
                    steps {
                        sh('python3 -m pip install --no-warn-script-location --user tox')
                        sh('python3 -m tox -e py')
                    }
                }
                stage('3.9') {
                    agent { docker { image 'docker.werally.in/rally-docker/rally-ci-python:3.9.4' } }
                    steps {
                        sh('python3 -m pip install --no-warn-script-location --user tox')
                        sh('python3 -m tox -e py')
                    }
                }
            }
        }
    }
}