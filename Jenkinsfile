pipeline {
    agent any

    stages {
        stage('chechout') {
            steps {
checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/abhiab1289/phpapp.git']]])
            }
        }
    

        stage('app build') {
            steps {
    sshPublisher(publishers: [sshPublisherDesc(configName: 'tomcat', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''sudo cp index.php /var/lib/docker/volumes/vol
''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'index.php')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])

            }   
        }
    

        stage('Docker build') {
            steps {
sshPublisher(publishers: [sshPublisherDesc(configName: 'tomcat', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''sudo docker build -t abrepohub/images:ubuntu .
sudo docker kill $(docker ps -q)
sudo docker rm $(docker ps -a -q)
sudo docker run -dit -p80:80 -v /var/lib/docker/volumes/vol:/var/www/html --name apache1 abrepohub/images:ubuntu
sudo docker run -dit -p81:80 -v /var/lib/docker/volumes/vol:/var/www/html --name apache2 abrepohub/images:ubuntu
sudo docker run -dit -p82:80 -v /var/lib/docker/volumes/vol:/var/www/html --name apache3 abrepohub/images:ubuntu
sudo docker image prune -a -f''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'Dockerfile')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                  }
       }
    }
}
