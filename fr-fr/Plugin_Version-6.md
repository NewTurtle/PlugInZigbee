# Explications pour passer de la version 5 à la version 6 du plugin

Pour __une nouvelle installation du plugin__, merci de suivre [la procédure d'installation](Plugin_Installation.md).

__La procédure ci-dessus est valable pour un passage de la version 5 à la version 6 du plugin pour un système fonctionnant sous Linux.__.

Les testeurs pour les autres systèmes d'exploitation sont les bienvenus !!

## Prérequis

Avant de commencer la procédure, vous devez :

* Avoir une version de DomoticZ 2021.1 au minimum.
* Être sur la branche __Stable5__ du plugin. Commande `git checkout stable5` si besoin.
* Avoir la dernière version du plugin. Commande `git pull` si besoin.

## Sauvegarde

Même si la procédure a été testé plusieurs fois, il est possible que les choses ne se passent pas comme prévus.
Il est recommandé de faire une sauvegarde complète pour pouvoir revenir en arrière si besoin.
Pensez à sauvegarder :

* DomoticZ
* Les données du Plugin
* Le système d'exploitation

## Procédure

 Ouvrir le terminal.

1. Arrêter DomoticZ. La commande est normalement :

    ``` bash
    sudo service domoticz.sh stop
    ```

1. Aller dans le répertoire du plugin. La commande est normalement :

    ``` bash
    cd domoticz/plugins/Domoticz-Zigate
    ```

1. Exécuter la commande :

    ``` bash
    git remote set-url origin https://github.com/zigbeefordomoticz/Domoticz-Zigbee
    ```

1. Exécuter la commande pour être certain d'être à jour :


    ```bash
    git pull
    ```

3. Basculer sur la version 6

    ```bash
    git checkout stable6
    ```

1. Installer les paquets Python nécessaires avec la commande :

    ``` bash
    sudo pip3 install -r requirements.txt
    ```

1. Exécuter la commande en adaptant __pi:pi__ si nécessaire au __user:group__ utilisé. Attention à bien prendre le point à la fin.

    ```bash
    sudo chown -R pi:pi .
    ```

1. Exécuter la commande :

    ```bash
    git config --add submodule.recurse true
    ```

1. Installer les librairies Python manquantes avec la commande :

    ```bash
    git submodule update --init --recursive
    ```

1. Rendre le fichier __plugin.py__ exécutable en lançant la commande :

    ```bash
    sudo chmod +x plugin.py
    ```

1. Redémarrer DomoticZ. La commande est normalement :

    ```bash
    sudo service domoticz.sh start
    ```

    Normalement, le nom du plugin dans matériel est devenu __ZigBee for DomoticZ__.

    A partir de maintenant, le terme ZiGate est remplacé par __coordinateur__, plus générique.

    Si vous avez déjà un plugin configuré avec une ZiGate comme coordinateur, vous n'avez rien à faire le plugin doit continuer à   fonctionner normalement.

## Le paramétrage

Il y a 4 modèles de coordinateurs possibles :

* ZiGate : aucune modification sur le fonctionnement du plugin existant
* ZiGate + : aucune modification sur le fonctionnement du plugin existant
* Texas Instruments ZNP : pour les nouveaux coordinateurs de marque TI
* Silicon Labs EZSP  : pour les nouveaux coordinateurs de marque Silicon Labs

## IMPORTANT Mise à jour du plugin

Le `git pull` n'est plus suffisant, il faut maintenant faire la commande `git pull --recurse-submodules`.
