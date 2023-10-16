Désolé pour le retard Madame ,Jenkins n'a pas pu être installé completement que aujourd'hui.
Pipline script utilisé :
" pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Récupération du code du dépôt Git
                    checkout([$class: 'GitSCM', branches: [[name: 'main']], userRemoteConfigs: [[url: 'https://github.com/WassimB12/JenkinsBonusTask']]])
            }
        }
  stage('Send Email') {
            steps {
                script {
                    def changeLog = currentBuild.changeSets.collect { entry ->
                        entry.msg
                    }.join('\n')

                    emailext subject: "Nouveau commit dans le dépôt",
                             body: "Contenu du dernier commit :\n\n${changeLog}",
                             to: "wassim.becheikh@esprit.tn",
                             mimeType: 'text/plain'}
                }
        }
    }
 } "
