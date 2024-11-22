pipeline {
    agent any 
    stages {
        stage('CleanUp') { 
            steps {
                script {
			 // Derruba containers em execução e remove imagens antigas
			sh 'docker-compose down --remove-orphans'
			 sh '''
				docker images -q | xargs -r docker rmi -f || true
			''' // Remove imagens não usadas
		}
            }
        }
        stage('Start Service') { 
            steps {
                script {
			// Inicia os containers usando o arquivo docker-compose.yml
			echo 'Iniciando os containers...'
			sh 'docker-compose up -d --build'
		}
            }
        }
   }

	post {
        success {
            echo 'Pipeline executado com sucesso! Todos os serviços estão no ar.'
        }
        failure {
            echo 'Pipeline falhou. Verifique os logs para mais detalhes.'
        }
    }
}
