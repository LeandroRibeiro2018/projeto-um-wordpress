pipeline {
    agent any
    environment {
        DEPLOY_PATH = 'C:\\xampp\\htdocs\\wordpress'  // Caminho do XAMPP no Windows
        WP_USER = 'admin'
        WP_PASS = 'admin123*'
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Código já disponível após o checkout automático do Jenkins'
            }
        }
        stage('Testes') {
            steps {
                // Exemplo de execução de testes, caso existam
                bat 'phpunit --configuration phpunit.xml'
            }
        }
        stage('Build') {
            steps {
                echo 'Etapa de Build - Adicione passos de build aqui se necessário'
            }
        }
        stage('Deploy') {
            steps {
                // Deploy para o servidor local (XAMPP)
                bat "xcopy /E /H /Y . ${DEPLOY_PATH}"
            }
        }
        stage('WordPress Authentication') {
            steps {
                // Executa comandos WP-CLI no ambiente local
                bat """
                cd ${DEPLOY_PATH} && \
                wp plugin list --allow-root --user=${WP_USER} --prompt=${WP_PASS}
                """
            }
        }
    }
    post {
        success {
            echo 'Deploy realizado com sucesso!'
        }
        failure {
            echo 'Erro no deploy!'
        }
    }
}
