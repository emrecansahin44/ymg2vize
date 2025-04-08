pipeline {
    agent any // arka planda çalışması için
    environment{
        PATH = "C:\\Program Files\\Docker\\Docker\\resources\\bin;C:\\Program Files\\Git\\bin;C:\\Windows\\System32"
        IMAGE_NAME = "vmg2vize"
        CONTAINER_NAME = "ymg2vize"
    }
    triggers{
        githubPush()
    }
    stages{ 
        stage('Repoyu Klonla..'){
        steps{
            git branch: 'main' , url: 'https://github.com/emrecansahin44/ymg2vize.git'
          }
        }
        stage('Docker Image Oluştur..'){
           steps{
            echo "Docker image oluşturuluyor.."
            bat "docker build -t %IMAGE_NAME% ." 
            }
        }
        stage("Eski containerleri durdur."){
          steps{
            echo "eski containerler durduruluyor."
            bat "docker rm -f %CONTAINER_NAME% || exit 0 "
            }
        }
        stage('Yeni container oluştur.'){
            steps{
                echo "yeni container oluşturuluyor."
                bat "docker run -d --name %CONTAINER_NAME% -p 4444:80 %IMAGE_NAME%"
            }
           
        }
    }
    post {
        success {
            echo "Başarılı!"
        }
        failure {
            echo " Başarısız!"
        }
    }

}
