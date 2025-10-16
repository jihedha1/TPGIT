pipeline {
    // 1. Définir l'agent (la machine) sur lequel le pipeline s'exécutera
    agent any

    // 2. Déclarer les outils nécessaires (JDK et Maven)
    //    Ces noms ('JDK21', 'M2_HOME') doivent correspondre EXACTEMENT
    //    à ceux que vous avez configurés dans "Administrer Jenkins > Tools".
    tools {
        jdk 'JDK21'
        maven 'M2_HOME'
    }

    // 3. Définir les étapes (stages) du pipeline
    stages {
        // Étape 1: Récupérer le code source depuis GitHub
        stage('Checkout Source Code') {
            steps {
                echo 'Cloning the repository...'
                // Utilise l'URL de VOTRE projet
                git branch: 'master', url: 'https://github.com/jihedha1/TPGIT.git'
            }
        }

        // Étape 2: Compiler et tester le projet avec Maven
        // Maven lit le pom.xml pour savoir quoi faire.
        stage('Build with Maven' ) {
            steps {
                echo 'Building the project with Maven...'
                // La commande 'mvn' est disponible grâce à la section 'tools'
                sh 'mvn clean install'
            }
        }

        // Étape 3: Exécuter l'application (si nécessaire)
        // Cette étape n'est souvent pas faite dans un build simple,
        // mais est utile pour la démonstration.
        stage('Run Application') {
            steps {
                echo 'Running the application...'
                // Exécute le fichier .jar qui a été créé par 'mvn install'
                // Le chemin exact peut varier selon la configuration de votre pom.xml
                // sh 'java -jar target/my-app-1.0-SNAPSHOT.jar'
                
                // Pour l'instant, nous réutilisons la méthode manuelle qui fonctionne
                sh 'java -cp target/classes org.example.Main'
            }
        }
    }
    
    // 4. Actions à exécuter à la fin du pipeline (succès, échec, etc.)
    post {
        always {
            echo 'Pipeline finished.'
            // Nettoyer l'espace de travail pour le prochain build
            cleanWs()
        }
    }
}
