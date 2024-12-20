node { 
  // Étape de récupération du code source
  stage('SCM') {
    checkout scm
  }

  // Étape d'analyse SonarQube
  stage('SonarQube Analysis') {
    def scannerHome = tool 'SonarScanner'
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }

  // Étape de scan OWASP Dependency-Check
  stage('OWASP Dependency-Check Scan') {
    // Exécute le scan OWASP Dependency-Check
    sh 'dependency-check --project "MyProject" --scan . --format HTML --out target/dependency-check-report.html'
  }

  // Étape de construction de l'image avec Podman
  stage('Build Podman Image') {
    // Construction de l'image avec Podman (assurez-vous que Podman est installé)
    sh 'podman build -t myimage:latest .'
  }

  // Étape de déploiement
  stage('Deploy') {
    // Exemple de déploiement, cela peut être modifié selon ton environnement
    sh 'podman run -d --name mycontainer myimage:latest'
  }
}
