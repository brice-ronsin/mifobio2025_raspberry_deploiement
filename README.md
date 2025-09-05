<h1 style="text-align: center;">
  <p align="center">
Mifobio2025_raspberry_deploiement
</p></h1>
<p align="center">
  <img src="https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExcG93MmF5czhkc2d1OGsxeXpzaXE1MTd5MTlrZm5qbzZvM21razhhbyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/9jwR2KCuAf8aIANOUr/giphy.gif" alt="animated />
</p>
<p align="left"> 
    
cette page vous guidera dans l'intallation du système d'exploitation pour votre raspberry Pi (version 5 ou 4)
    et dans le déploiement de votre model obtenue en ayant effectuer toutes les étapes du dépot github :
    
 <p align="center"><a href="https://github.com/brice-ronsin/mifobio_discoscope">mifobio_discoscope</a></p><br/>
 <br/>Nous installerons le tout dans un dossier virtuel pour isoler notre travail. 
    Pour faciliter notre atelier certaines de ces actions auront dejà été réalisées 
pour notre atelier veuillez commencez au point 3. Les étapes préalables sont données qui si vous souhaitez tout refaire<br/>

<h1 style="text-align: center;">
  <p align="center">
1) Installation du système d'exploistation sur Raspberry
  </p></h1>

-allez sur le site <a href="https://www.raspberrypi.com/software/">Raspberry Pi sofware</a>
-télécharger et installer le logiciel sur votre ordinateur <br/>
-lancer le programme d'installation et inserer la carte micro SD dans votre ordinateur<br/> 

dans la nouvelle fenêtre choisir :<br/>
<p align="right">
  <img src="https://github.com/brice-ronsin/mifobio2025_raspberry_deploiement/blob/main/images/sofware_raspberry.jpg" />
</p><br/>

#### 1-le model de votre raspberry<br/>
#### 2-Le système d'exploitation (en général Raspberry Pi OS 64bit)<br/>
#### 3-le chemin de la micro SD<br/>
#### 4-cliquez sur suivant <br/>
quand tout est fini mettre la carte micro SD dans la Raspberry et la demarer. Repondre aux questions de démarage classique lors de l'installation d'un système d'exploitation (reseau, nom, mot de passe etc..)</br>

<h1 style="text-align: center;">
  <p align="center">
2) Installation de pyenv pour la création d'environement
  </p></h1>

  Sur le bureau de votre raspberry cliquez pour ouvrir le terminal (icone sur la barre de tache) <p align="right">
  <img src="https://github.com/brice-ronsin/mifobio2025_raspberry_deploiement/blob/main/images/sofware_raspberry.jpg" />
</p><br/> 

Tapez ensuite le code suivant ou copier/coller dans la console :

```
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev \
liblzma-dev python3-openssl
```

Une fois ces dépendances installées, vous pouvez procéder à l’installation de Pyenv <br/>
en utilisant un script fourni par les mainteneurs du projet :<br/>

```
curl https://pyenv.run | bash
```
