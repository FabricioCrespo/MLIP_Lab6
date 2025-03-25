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

                # Inicializar Conda (ajusta la ruta si es necesario)
                source ~/miniconda3/etc/profile.d/conda.sh

                # Activar el entorno Conda (ajusta el nombre del entorno)
                conda activate mlip_env
                
                # Ejecutar Pytest y generar un reporte en XML para Jenkins
                pytest tests/ --junitxml=report.xml

                echo 'pytest completed successfully'
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
