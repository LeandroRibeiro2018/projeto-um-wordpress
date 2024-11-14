pipeline {
    agent any
    environment {
        GIT_REPO = 'https://github.com/LeandroRibeiro2018/projeto-um-wordpress.git'  // Endereço do repositório GitHub
        DEPLOY_PATH = 'C:\\xampp\\htdocs\\wordpress'  // Caminho do XAMPP no Windows
        WP_USER = 'admin'
        WP_PASS = 'admin123*'
    }
    stages {
        stage('Checkout') {
            steps {
                // Clona o repositório GitHub usando o token armazenado como StringCredentials
                withCredentials([string(credentialsId: 'tokenGithub', variable: 'GITHUB_TOKEN')]) {
                    // Autentica com GitHub utilizando o token como StringCredentials
                    bat "git clone https://${GITHUB_TOKEN}@${GIT_REPO} ."
                }
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
