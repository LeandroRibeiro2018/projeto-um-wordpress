pipeline {
    agent any
    stages {
        stage('Verificar Git') {
            steps {
                script {
                    // Verifica se o Git está instalado
                    def gitVersion = sh(script: 'git --version', returnStatus: true)
                    if (gitVersion != 0) {
                        error "Git não está instalado ou não foi configurado corretamente. Configure o Git nas Ferramentas Globais do Jenkins."
                    } else {
                        echo "Git está instalado e configurado corretamente."
                    }
                }
            }
        }
        
        stage('Checkout do Código') {
            steps {
                // Realiza o checkout do repositório usando as credenciais configuradas
                checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/LeandroRibeiro2018/projeto-um-wordpress.git', credentialsId: 'SUA_CREDENCIAL_ID']]
                ])
            }
        }
        
        // Demais estágios do pipeline
        stage('Build') {
            steps {
                // Coloque os passos de build aqui
            }
        }

        stage('Test') {
            steps {
                // Coloque os passos de teste aqui
            }
        }
        
        // Outros estágios do pipeline podem seguir aqui
    }
}
