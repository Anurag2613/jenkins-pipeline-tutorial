pipeline {
    // 1. Specify an agent to run the pipeline
    // 'any' means Jenkins will use any available agent
    agent any

    // 2. Define parameters that the user can input when starting the build
    parameters {
        // A string parameter for the branch to build
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: 'The branch to build')
        
        // A boolean parameter to decide whether to run tests
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Run unit tests?')
        
        // A choice parameter for the deployment environment
        choice(name: 'ENVIRONMENT', choices: ['staging', 'production'], description: 'Which environment to deploy to?')
    }

    // 3. Define the stages of the pipeline
    stages {
        // Stage 1: Checkout Code
        stage('Checkout') {
            steps {
                // In a real scenario, you'd use a Git SCM step
                // For this example, we'll just print the branch name
                echo "Checking out code from branch: ${params.BRANCH_NAME}"
                // Example of a real git checkout:
                // git branch: params.BRANCH_NAME, url: 'https://github.com/your-repo/your-project.git'
            }
        }

        // Stage 2: Build the application
        stage('Build') {
            steps {
                echo "Building the application..."
                // Example of build commands
                // sh 'mvn clean install'
                // sh 'npm install'
            }
        }

        // Stage 3: Run Tests (Conditional)
        stage('Test') {
            // This stage will only run if the 'RUN_TESTS' parameter is true
            when {
                expression { params.RUN_TESTS == true }
            }
            steps {
                echo "Running tests..."
                // Example of test commands
                // sh 'mvn test'
                // sh 'npm test'
            }
        }

        // Stage 4: Deploy the application
        stage('Deploy') {
            steps {
                echo "Deploying to ${params.ENVIRONMENT} environment..."
                // You could use conditional logic here based on the environment
                script {
                    if (params.ENVIRONMENT == 'production') {
                        // Production deployment steps
                        echo "Running production deployment scripts..."
                    } else {
                        // Staging deployment steps
                        echo "Running staging deployment scripts..."
                    }
                }
            }
        }
    }

    // 4. Post-build actions
    // These actions run after all stages are completed
    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded!'
            // Example: send a notification
            // mail to: 'team@example.com',
            //      subject: "Build succeeded: ${currentBuild.fullDisplayName}",
            //      body: "Check console output at ${env.BUILD_URL}"
        }
        failure {
            echo 'Pipeline failed.'
            // Example: send an alert
            // mail to: 'alerts@example.com',
            //      subject: "Build FAILED: ${currentBuild.fullDisplayName}",
            //      body: "Build failed. Check console output at ${env.BUILD_URL}"
        }
    }
}
