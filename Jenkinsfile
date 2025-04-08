pipeline{
    
    agent any
    
    triggers {
        githubPush()
    }
    
    environment{
        PATH = "C:\\Windows\\System32;C:/Program Files/Docker/Docker/resources/bin"
        IMAGE_NAME = "ymg-ders-test"
        CONTAINER_NAME = "nginx-test-conteyner"
    }
    
    stages{
        stage('Repo Klonla'){
            steps {
                git url:'https://github.com/Mervan34/YMGDers.git', branch: 'main'
            }
        }
        
        stage('Docker image oluştur'){
            steps{
                echo "docker image oluşturuldu"
                bat "docker build -t ${IMAGE_NAME} ."
            }
        }
        
        stage('Eski Conteyneri Durdur'){
            steps{
                echo "Eski conteyner durduruldu"
                bat "docker rm -f ${CONTAINER_NAME} ||true" 
            }
        }
        
        stage('Yeni Conteyneri Oluştur'){
            steps{
                echo "Yeni Conteyner Oluşturuldu"
                bat "docker run -d --name ${CONTAINER_NAME} -p 4444:80 ${IMAGE_NAME}"
            }
        }
        
    }
    
    post{
        success{
            echo "Yayın başarılı: http://localhost:5050"
        }
        failure{
            echo "Pipeline başarısız oldu"
        }
        
    }
    
}
