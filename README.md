# TP 4 : Docker Engine, Jenkins, CI/CD - Yassine LAMBARKI

### Partie 1: CI

##### 1. Installer Jenkins
![Java jdk11](/images/java.jpg)

![Java jdk11](/images/java11%20%20en%20cours.jpg)

![Jenkins installation](/images/jenkins.jpg)

![Jenkins installation](/images/jenkins%20port.jpg)

![Jenkins installation](/images/jenkins%20nst.jpg)

![Jenkins installation](/images/jenkins%20jdk.jpg)

![Jenkins installation](/images/jenkins%20finished.jpg)

![Jenkins installation](/images/installer%20les%20plugins.jpg)

![Jenkins installation](/images/installation.jpg)

![Jenkins installation](/images/redemarrage%20jenkins.jpg)

![Jenkins installation](/images/admin.jpg)

![Jenkins installation](/images/admin%20jenkins.jpg)

![Jenkins installation](/images/admin%20create%20user.jpg)

![Jenkins installation](/images/connexion.jpg)


#### 2. Créer un projet « tp4 » contenant une page web index.html, qui affiche « Welcome BDCC » et un fichier de configuration docker au répertoire du projet (un docker file qui permet de lancer cette page sur un serveur web nginx).

![Projet](/images/projet.jpg)

![Projet](/images/dockerfile.jpg)

![Projet](/images/welcome.jpg)

![Projet](/images/eclipse.jpg)


#### 3. Créer un répertoire Git hub nommée tp4 pour partager le code de l’application locale (tp4).

![Git](/images/git%20tp4.jpg)


![Git](/images/git%20add%20.jpg)

![Git](/images/git%20commit%20-m.jpg)

![Git](/images/git%20push%20cmd.jpg)

![Git](/images/git%20push.jpg)

#### 4. Créer et configurer un Job Jenkins (job1tp4) du type free style


![Job Jenkins](/images/saisir%20un%20job.jpg)

![Job Jenkins](/images/top1job1.jpg)

#### 5. Ajouter des plugins docker à Jenkins.

![Plugins Jenkins](/images/docker%20commons.jpg)


#### 6. Configurer job1tp4 afin de générer une image (docker build) et publier une image docker du projet sur docker hub (Tag latest).

![job1tp4 Jenkins](/images/repo%20jenkins.jpg)

![job1tp4 Jenkins](/images/mot%20de%20passe.jpg)

![job1tp4 Jenkins](/images/screencapture-localhost-8079-job-job1tp4-configure-2023-01-15-10_55_23.png)


![job1tp4 Jenkins](/images/screencapture-localhost-8079-manage-configure-2023-01-15-21_09_03%20(1).png)


![Tp4 dockerhub](/images/tp4%20docker%20hub.jpg)



#### 7. Faire un changement dans index.html, découvrir les changements sur le job1tp4.

![job1tp4](/images/tp1.png)


### Partie 2: CI/CD (continuous delivery/continuous deployment)

#### 1. Créer un autre job freestyle job2tp4 contenant les mêmes instructions du job1tp4 de la première partie tout en ajoutant un script Shell qui déploie l’image sous un nouveau conteneur sur docker engine.


![job2tp4](/images/tp2-4.png)

#### 2. Faire un changement dans index.html, découvrir les changements sur le job2tp4 et sur l’image déployé. Enregistrer les changements dans le répertoire avec la commande git commit -m “tp4 v3” Pusher le code vers le répertoire GitHub avec la commande git push origin master D’après les changements Déclenchement automatique du build sur Jenkins

![job2tp4](/images/tp2.png)

#### 3. Créer un job du type pipeline job2tp4v2 (qui reprend les mêmes tâches du job freestyle job2tp4 mais d’une autre manière), ajouter sans rien changer dans les paramètres du job, un script dans la partie script du pipeline assurant les trois stages (Cloning Git, Building image, Publish Image).

![job2tp4](/images/build%20success%20automatique.jpg)

![job2tp4](/images/pipeline.jpg)

![job2tp4](/images/screencapture-localhost-8079-job-job2tp4v2-2023-01-15-22_30_25.png)


`````
pipeline {
  environment {
    registry = "softengyas/tp4devops"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/softengyas/tp4'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Publish Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
  }
}


`````

![job2tp4](/images/jenkins%20file.jpg)

![job2tp4](/images/screencapture-localhost-8079-job-job2tp4v2-2023-01-15-22_30_25.png)

![job2tp4](/images/jenkins%204eme.jpg)










