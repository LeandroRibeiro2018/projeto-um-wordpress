pipeline {
    agent any
    environment {
        DEPLOY_PATH = 'C:\\xampp\\htdocs\\wordpress'  // Ajuste o caminho conforme necessário
        WP_USER = 'admin'   // Altere para o usuário WordPress
        WP_PASS = 'admin123*' // Altere para a senha WordPress
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Código já disponível após o checkout automático do Jenkins'
            }
        }
        stage('Testes') {
            steps {
                // Exemplo para executar testes, remova se não for necessário
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
                // Copia arquivos para o diretório do XAMPP
                bat "xcopy /E /H /Y . ${DEPLOY_PATH}"
            }
        }
        stage('WordPress Authentication') {
            steps {
                // Executa comandos WP-CLI no ambiente WordPress
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
