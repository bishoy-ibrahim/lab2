pipeline {
    agent any

    parameters {
        string(name: 'VERSION', defaultValue: '1.0.0', description: 'Enter the app version')
        choice(name: 'ENV', choices: ['dev', 'test', 'prod'], description: 'Choose environment')
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Run tests?')
    }

    stages {
        stage('Print Parameters') {
            steps {
                echo "Version: ${params.VERSION}"
                echo "Environment: ${params.ENV}"
                echo "Run Tests: ${params.RUN_TESTS}"
            }
        }

        stage('Conditional Stage') {
            when {
                expression { return params.RUN_TESTS }
            }
            steps {
                echo "Running tests..."
                // add your test commands here
            }
        }
    }
}
