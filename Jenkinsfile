pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                echo 'In C or Java, we can compile our program in this step'
                echo 'In Python, we can build our package here or skip this step'
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                echo 'Test Step: We run testing tool like pytest here'

                # Ejecutar en bash para que funcione 'source'
                bash -c "source /var/jenkins_home/miniconda3/etc/profile.d/conda.sh && conda activate mlip_env && pytest tests/ --junitxml=report.xml"
                '''
            }
        }
        stage('Report') {
            steps {
                junit 'report.xml'
            }
        }
        stage('Deploy') {
            steps {
                echo 'In this step, we deploy our project'
                echo 'Depending on the context, we may publish the project artifact or upload pickle files'
            }
        }
    }
}
