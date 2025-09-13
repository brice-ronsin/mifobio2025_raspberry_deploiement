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
  <img src="https://github.com/brice-ronsin/mifobio2025_raspberry_deploiement/blob/main/images/terminal.png" />
</p><br/> 

Tapez ensuite le code suivant ou copier/coller dans la console :

```
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev \
liblzma-dev python3-openssl
```

Editer alors le fichier .bashrc dans le dossier home/"nom que vous avez donné" (dans notre cas mifobio) <br/>
si il n’est pas visible cliquez sur voir et afficher dossier caché
Tapez ensuite les commandes suivantes : 

```
sudo nano .bashrc
```

a la fin de votre fichier rajouter ces lignes pour que pyenv puisse gérer les version et les environnements : 

```
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
```
Cliquez ensuite sur control X pour sauvegarder et redemarer la raspberry

Une fois ces dépendances installées, vous pouvez procéder à l’installation de Pyenv <br/>
en utilisant un script fourni par les mainteneurs du projet :<br/>

```
curl https://pyenv.run | bash
```
</br>
<h1 style="text-align: center;">
  <p align="center">
3) Installation par pyenv de la version python à utiliser et création de l'environement virtuel
  </p></h1>

Pyenv est un module qui vous permet de basculer aisément entre différentes versions de Python, tout en gardant votre environnement de développement propre et organisé.
Pyenv offre une variété de fonctionnalités pour gérer les versions de Python :
Installation de versions multiples : Installez et gérez facilement plusieurs versions de Python côte à côte sur votre machine.
Définition de versions globales et locales : Choisissez une version globale de Python pour l’ensemble du système, ou définissez une version spécifique pour un projet particulier avec pyenv local.
Isolation des environnements : Créez des environnements virtuels isolés avec pyenv virtualenv pour des projets

  #### 1- Installer et utiliser la version de python souhaiter en local 

Sur la raspberry ouvrir un terminal <p align="right">
  <img src="https://github.com/brice-ronsin/mifobio2025_raspberry_deploiement/blob/main/images/terminal.png" />
</p><br/> 
Taper ensuite dans le terminal la ou les version de python à installer (pour nous le python 3.9.2)

```
pyenv install 3.9.2
```
Créer ensuite un dossier TFOD de travail dans le home/"nom que vous avez donné" (dans notre cas mifobio) <br/>
dans la console se placer dans le dossier 
```
cd TFOD
```
puis spécifier la version que vous souhaitez utiliser dans ce dossier en tapant dans le terminal : 
```
pyenv local 3.9.2
```

#### 2- Création d'un environement python 

Nous allons maintenant installer avec le python 3.9.2 un environnement virtuel tflite (donner le nom ue vous souhaitez):

tapez dans le terminal : 
```
python -m venv tflite
```
Enfin activer l'environnement en écrivant dans le terminal : 
```
source tflite/bin/activate
```
Voila votre environnement est prêt à être utilisé nous pouvons donc passer au point 4 

<h1 style="text-align: center;">
  <p align="center">
4) Installation des dependances TensorFlow Lite et OpenCV
  </p></h1>

Nous allons installer TensorFlow, OpenCV et toutes les dépendances nécessaires pour ces deux paquets. 
OpenCV n'est pas nécessaire pour exécuter TensorFlow Lite, mais les scripts de détection d'objets 
l'utilisent pour récupérer des images et y dessiner les résultats de la détection.

Pour faciliter les choses, nous allons télécharger un script shell qui va télécharger et installer automatiquement tous les paquets et dépendances. 

##### 1- téléchargement du script du dossier à copier

dans le terminal tapez : 
```
wget https://raw.githubusercontent.com/brice-ronsin/mifobio2025_raspberry_deploiement/refs/heads/main/a_copier/requirements.sh
```
puis :
```
bash requirements.sh
```

#### 2- télécharger le script python pour utiliser TensorFlow avec la webcam 

nous allons télécharger un script de base déjà créer pour utiliser notre modèle sur des images  live obtenu par la webcam.
Cependant nous allons modifier ce script pour piloter nos servo moteurs
(dans le dossier à copier vous avez les deux scripts: le script de base et le script modifié)

dans le terminal tapez : 
```
wget https://raw.githubusercontent.com/brice-ronsin/mifobio2025_raspberry_deploiement/refs/heads/main/a_copier/TFLite_detection_webcam.py
```

#### 3- lancement du script dans notre epace virtuel

pour lancer enfin le script il faut au préalable avoir copier dans le dossier de travail (ici TFOD)
le modèle que vous avez sauvegarder (le dossier zippé) du Jupyter notebook  <p align="left"><a href="https://github.com/brice-ronsin/mifobio_discoscope">mifobio_discoscope</a></p><br/>

Quand tout est prêt tapez dans le terminal : 
```
python3 TFLite_detection_webcam.py --modeldir=custom_model_lite
```

 remplacer éventuellement  <a href="https://github.com/brice-ronsin/mifobio2025_raspberry_deploiement/edit/main/README.md#--3-installation-par-pyenv-de-la-version-python-%C3%A0-utiliser-et-cr%C3%A9ation-de-lenvironement-virtuel--">TFLite_detection_webcam.py</a> par le  <a href="https://github.com/brice-ronsin/mifobio2025_raspberry_deploiement/edit/main/README.md#--3-installation-par-pyenv-de-la-version-python-%C3%A0-utiliser-et-cr%C3%A9ation-de-lenvironement-virtuel--">nom du script que vous avez modifié</a></br>
 et <a href="https://github.com/brice-ronsin/mifobio2025_raspberry_deploiement/edit/main/README.md#--3-installation-par-pyenv-de-la-version-python-%C3%A0-utiliser-et-cr%C3%A9ation-de-lenvironement-virtuel--">--modeldir=custom_model_lite</a> par <a href="https://github.com/brice-ronsin/mifobio2025_raspberry_deploiement/edit/main/README.md#--3-installation-par-pyenv-de-la-version-python-%C3%A0-utiliser-et-cr%C3%A9ation-de-lenvironement-virtuel--">--modeldir="NOM du dossier contenant votre modèle et vos labels"</a>
 
