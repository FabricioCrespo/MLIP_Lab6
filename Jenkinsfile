pipeline {
    agent any

    stages {
        stage('Install wget and Anaconda') {
            steps {
                sh '''
                # Instalar wget
                apt-get update && apt-get install -y wget

                # Descargar el instalador de Anaconda
                wget https://repo.anaconda.com/archive/Anaconda3-2023.03-Linux-x86_64.sh -O ~/anaconda.sh

                # Instalar Anaconda
                bash ~/anaconda.sh -b -p $HOME/anaconda3

                # Activar conda
                source $HOME/anaconda3/etc/profile.d/conda.sh
                conda init bash
                '''
            }
        }

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

                # Usar Anaconda
                bash -c "source $HOME/anaconda3/etc/profile.d/conda.sh && conda activate mlip_env && pytest tests/ --junitxml=report.xml"
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
