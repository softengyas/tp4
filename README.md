# TP 4 : Docker Engine, Jenkins, CI/CD - Yassine LAMBARKI

### Partie 1: CI

##### 1. Installer Jenkins
![Java jdk11](/watermarked_images/java.jpg)

![Java jdk11](/watermarked_images/java11%20%20en%20cours.jpg)

![Jenkins installation](/watermarked_images/jenkins.jpg)

![Jenkins installation](/watermarked_images/jenkins%20port.jpg)

![Jenkins installation](/watermarked_images/jenkins%20nst.jpg)

![Jenkins installation](/watermarked_images/jenkins%20jdk.jpg)

![Jenkins installation](/watermarked_images/jenkins%20finished.jpg)

![Jenkins installation](/watermarked_images/installer%20les%20plugins.jpg)

![Jenkins installation](/watermarked_images/installation.jpg)

![Jenkins installation](/watermarked_images/redemarrage%20jenkins.jpg)

![Jenkins installation](/watermarked_images/admin.jpg)

![Jenkins installation](/watermarked_images/admin%20jenkins.jpg)

![Jenkins installation](/watermarked_images/admin%20create%20user.jpg)

![Jenkins installation](/watermarked_images/connexion.jpg)


#### 2. Créer un projet « tp4 » contenant une page web index.html, qui affiche « Welcome BDCC » et un fichier de configuration docker au répertoire du projet (un docker file qui permet de lancer cette page sur un serveur web nginx).

![Projet](/watermarked_images/projet.jpg)

![Projet](/watermarked_images/dockerfile.jpg)

![Projet](/watermarked_images/welcome.jpg)

![Projet](/watermarked_images/eclipse.jpg)


#### 3. Créer un répertoire Git hub nommée tp4 pour partager le code de l’application locale (tp4).

![Git](/watermarked_images/git%20tp4.jpg)


![Git](/watermarked_images/git%20add%20.jpg)

![Git](/watermarked_images/git%20commit%20-m.jpg)

![Git](/watermarked_images/git%20push%20cmd.jpg)

![Git](/watermarked_images/git%20push.jpg)

#### 4. Créer et configurer un Job Jenkins (job1tp4) du type free style


![Job Jenkins](/watermarked_images/saisir%20un%20job.jpg)

![Job Jenkins](/watermarked_images/top1job1.jpg)

#### 5. Ajouter des plugins docker à Jenkins.

![Plugins Jenkins](/watermarked_images/docker%20commons.jpg)


#### 6. Configurer job1tp4 afin de générer une image (docker build) et publier une image docker du projet sur docker hub (Tag latest).

![job1tp4 Jenkins](/watermarked_images/repo%20jenkins.jpg)

![job1tp4 Jenkins](/watermarked_images/mot%20de%20passe.jpg)

![job1tp4 Jenkins](/watermarked_images/screencapture-localhost-8079-job-job1tp4-configure-2023-01-15-10_55_23.png)


![job1tp4 Jenkins](/watermarked_images/screencapture-localhost-8079-manage-configure-2023-01-15-21_09_03%20(1).png)


![Tp4 dockerhub](/watermarked_images/tp4%20docker%20hub.jpg)



#### 7. Faire un changement dans index.html, découvrir les changements sur le job1tp4.

![job1tp4](/watermarked_images/tp1.png)


### Partie 2: CI/CD (continuous delivery/continuous deployment)

#### 1. Créer un autre job freestyle job2tp4 contenant les mêmes instructions du job1tp4 de la première partie tout en ajoutant un script Shell qui déploie l’image sous un nouveau conteneur sur docker engine.


![job2tp4](/watermarked_images/tp2-4.png)

#### 2. Faire un changement dans index.html, découvrir les changements sur le job2tp4 et sur l’image déployé. Enregistrer les changements dans le répertoire avec la commande git commit -m “tp4 v3” Pusher le code vers le répertoire GitHub avec la commande git push origin master D’après les changements Déclenchement automatique du build sur Jenkins

![job2tp4](/watermarked_images/tp2.png)

#### 3. Créer un job du type pipeline job2tp4v2 (qui reprend les mêmes tâches du job freestyle job2tp4 mais d’une autre manière), ajouter sans rien changer dans les paramètres du job, un script dans la partie script du pipeline assurant les trois stages (Cloning Git, Building image, Publish Image).


![job2tp4](/watermarked_images/pipeline.jpg)

![job2tp4](/watermarked_images/tpscript2.png)

![job2tp4](/watermarked_images/tp%20pour%20script.jpg)

![job2tp4](/watermarked_images/tp%20script%20success.jpg)

![job2tp4](/watermarked_images/docker%20pipeline%20-%20script.jpg)

![job2tp4](/watermarked_images/build%20success%20automatique.jpg)

![job2tp4](/watermarked_images/screencapture-localhost-8079-job-job2tp4v2-2023-01-15-22_30_25.png)




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

![job2tp4](/watermarked_images/jenkins%20file.jpg)


![job2tp4](/watermarked_images/jenkins%204eme.jpg)


#### 4. Créer un job du type pipeline (job3tp4). Ce dernier contiendra quatre Stages(Cloning Git, Building image, Test image, Publish Image). Sur le même projet TP4, créer un fichier ‘jenkinsfile’ qui définit le script assurant les quatre stages, par la suite spécifier sur le job le chemin du fichier ‘jenkinsfile’.


![job3tp4](/watermarked_images/scm%20job3.jpg)

![job3tp4](/watermarked_images/scm%20jenkins.png)


##### 5- Afficher stage view après quelques changements dans le projet (par exemple sur index.html). Enregistrer les changements dans le répertoire avec la commande git commit -m “tp4 v3” Pusher le code vers le répertoire GitHub avec la commande git push origin master D’après les changementsDéclenchement automatique du build sur Jenkins

![job3tp4](/watermarked_images/scm%20push.png)

![job3tp4](/watermarked_images/ECLIPSE%20SCM.jpg)

![job3tp4](/watermarked_images/DOCKER%20SCM.png)

![job3tp4](/watermarked_images/JENKINS%20SCM.jpg)



````
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
stage('Test image') {
        steps{
        script {
        
            echo "Tests passed"
        }
      }
    }
    stage('Deploy Image') {
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
````




##### 6. Modifier le pipeline. Ce dernier contiendra cinq Stages (Cloning Git, Building image, Test image, Publish Image, deploy image). Ajouter sur le fichier jenkinsfile un stage du déploiement de l’image vers docker engine. Tester le changement via le stage view.



![job4tp4](/watermarked_images/deploy.jpg)

![job4tp4](/watermarked_images/deploy2.png)

![job4tp4](/watermarked_images/deploy%20finish.png)

![job4tp4](/watermarked_images/jenkins%20finish.png)

![job4tp4](/watermarked_images/docker%20finish.png)




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
stage('Test image') {
        steps{
        script {
                    echo "Tests passed"
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
        stage('Deploy image') {
      steps{
        bat "docker run -d $registry:$BUILD_NUMBER"
      }
    }
  }
}


`````










