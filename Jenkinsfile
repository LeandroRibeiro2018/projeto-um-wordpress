pipeline {
    agent any
    
    environment {
        //GIT_URL = 'https://github.com/LeandroRibeiro2018/projeto-um-wordpress.git'
        //GIT_CREDENTIALS_ID = 'Token-Git' // ID das credenciais de autenticação Git no Jenkins
        WP_USER = 'admin'
        WP_PASSWORD = 'admin123*'
    }
    
    stages {
        stage('Clonar Repositório') {
            steps{
                script{
                git url: 'https://github.com/LeandroRibeiro2018/projeto-um-wordpress.git,
                credentialsId: 'TokenGit',
                branch: 'main'
                }
            }
        }
        
        stage('Instalar Dependências') {
            steps {
                script {
                    // Exemplo de instalação de dependências para o Wordpress (caso seja necessário)
                    sh 'composer install' // ou outro comando que você precise, dependendo da sua configuração
                }
            }
        }
        
        stage('Deploy no WordPress') {
            steps {
                script {
                    // Obter o token JWT de autenticação via API REST do WordPress
                    def response = sh(
                        script: '''
                        curl --silent --request POST \
                            --url http://localhost/wordpress/wordpress/wp-json/jwt-auth/v1/token \
                            --header 'Content-Type: application/json' \
                            --data '{"username": "${WP_USER}", "password": "${WP_PASSWORD}"}'
                        ''', 
                        returnStdout: true
                    )
                    
                    def jsonResponse = readJSON text: response
                    def WP_TOKEN = jsonResponse.token
                    
                    // Exemplo de upload de arquivos para o WordPress
                    sh '''
                    curl --request POST \
                        --url http://localhost/wordpress/wordpress/wp-json/wp/v2/media \
                        --header 'Authorization: Bearer ${WP_TOKEN}' \
                        --header 'Content-Type: multipart/form-data' \
                        --form 'file=@"caminho/para/o/arquivo.jpg"'
                    '''
                }
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline executado com sucesso!'
        }
        
        success {
            echo 'Deploy realizado com sucesso!'
        }
        
        failure {
            echo 'Ocorreu um erro durante a execução do pipeline!'
        }
    }
}
