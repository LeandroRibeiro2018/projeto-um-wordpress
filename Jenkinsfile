pipeline {
    agent any
    
    environment {
        GIT_URL = 'https://github.com/LeandroRibeiro2018/projeto-um-wordpress'
        GIT_CREDENTIALS_ID = 'Token-Git'  // ID das credenciais de autenticação Git no Jenkins
        WP_USER = 'admin'
        WP_PASSWORD = 'admin123*'
    }
    
    stages {
        stage('Clonar Repositório') {
            steps {
                script {
                    // Clonando o repositório Git com autenticação via Token
                    git credentialsId: GIT_CREDENTIALS_ID, url: GIT_URL
                }
            }
        }
        
        stage('Instalar Dependências') {
            steps {
                script {
                    // Exemplo de instalação de dependências para o Wordpress (caso seja necessário)
                    // Comandos de instalação para o WordPress ou outros pacotes podem ser executados aqui
                    sh 'composer install'  // ou outro comando que você precise, dependendo da sua configuração
                }
            }
        }
        
        stage('Deploy no WordPress') {
            steps {
                script {
                    // Aqui você pode adicionar comandos para fazer o deploy ou configurar o WordPress
                    // Exemplo de envio de comandos HTTP para login ou configuração do WordPress
                    // Aqui você pode usar o `curl` ou alguma outra ferramenta para interagir com a API do WordPress
                    
                    // Exemplo de login via API REST ou qualquer outro comando de deploy:
                    sh '''
                    curl --request POST \
                         --url http://seu-servidor-wordpress/wp-json/jwt-auth/v1/token \
                         --header 'Content-Type: application/json' \
                         --data '{"username": "${WP_USER}", "password": "${WP_PASSWORD}"}'
                    '''
                }
            }
        }
    }
    
    post {
        always {
            // Aqui você pode adicionar comandos para limpar ou realizar outras ações após a execução
            echo 'Pipeline executado com sucesso!'
        }
        
        success {
            // Mensagem caso o pipeline seja bem-sucedido
            echo 'Deploy realizado com sucesso!'
        }
        
        failure {
            // Mensagem caso o pipeline falhe
            echo 'Ocorreu um erro durante a execução do pipeline!'
        }
    }
}
