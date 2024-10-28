pipeline {
    agent {
        label 'ubuntu-latest'
    }
    environment {
        PACKAGIST_USERNAME = credentials('PACKAGIST_USERNAME')
        PACKAGIST_TOKEN = credentials('PACKAGIST_TOKEN')
        GITHUB_REPOSITORY = 'your-github-repo-path'
    }
    stages {
        stage('Run Only on Tag') {
            when {
                expression {
                    return env.BRANCH_NAME ==~ /^rls_\d+\.\d+\.\d+$/  
                }
            }
            steps {
                echo "Running on tag: $env.BRANCH_NAME"
            }
            stages {
                stage('Pre-check for Environment Variables') {
                    steps {
                        script {
                            if (!env.PACKAGIST_USERNAME || !env.PACKAGIST_TOKEN) {
                                error("Error: PACKAGIST_USERNAME or PACKAGIST_TOKEN is not defined")
                            }
                            echo "All necessary environment variables are defined."
                        }
                    }
                }
                stage('Checkout Code') {
                    steps {
                        checkout scm
                    }
                }
                stage('Update Packagist Package') {
                    steps {
                        sh '''
                            curl -XPOST -H 'content-type:application/json' \
                            "https://packagist.org/api/update-package?username=${PACKAGIST_USERNAME}&apiToken=${PACKAGIST_TOKEN}" \
                            -d '{"repository":{"url":"https://github.com/${GITHUB_REPOSITORY}"}}'
                        '''
                    }
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
