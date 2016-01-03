# JeedomSynologyDSM5.2
Installation de Jeedom sur un NAS Synology DSM 5.2

**Sources :**
* http://www.domopi.eu/installation-de-jeedom-sur-un-nas-synology/

Étapes:
==
Installation de Debian chroot
-
### Déclaration de la source SynoCommunity
Rajoutez la source pour obtenir le paquet debian chroot. Pour cela, allez dans le Centre de Paquets Synology, puis dans Paramètres, Sources de paquets. 
Cliquez sur Ajouter et renseignez comme suit :
nom : SynoCommunity
emplacement : http://packages.synocommunity.com/

### Installation du paquet debian chroot
Dans le Centre de Paquets Synology, dans la section communauté, cherchez le paquet Debian Chroot (avec un logo en spirale rose) et installez-le. Cela prend quelques minutes. 
Maintenant, toujours dans le Centre de Paquets Synology, allez dans les paquets installés, cliquez sur le paque Debian Chroot et Lancez-le.

Installation des drivers
-
* Connexion ssh au NAS
ssh root@IPDUNAS -p PORTUTILISE (22 par defaut)
(le mot de passe du compte root est le même que le mot de passe du compte admin dans DSM)

    
    cd /tmp
    
    wget https://raw.githubusercontent.com/CharlyPoppins/JeedomSynologyDSM5.2/master/install_drivers_alias.sh
    
    chmod 777 install_drivers_alias.sh
    
    ./install_drivers_alias.sh
    
    rm install_drivers_alias.sh
    

Vous devez ensuite impérativement redémarrer votre Nas Synology avant de continuer dans l'installation de Jeedom.

Partage du dossier de la debian
-
Allez dans le Panneau de configuration de DSM, dans l'onglet Dossier Partagé. Créez un nouveau dossier partagé que vous appelerez debian et donnez les droits en lecture/écriture à votre utilisateur.

Installation de Jeedom
-
Connectez-vous en ssh, toujours en root, sur votre Nas Synology.

Si vous avez bien respecté les étapes précédentes, en tapant `debian`, vous devriez vous retrouver dans la Debian. Un warning sur les locales peut s'afficher, normal à cette étape, nous allons les configurer par la suite.


    cd /home
    
    wget --no-check-certificate https://raw.githubusercontent.com/CharlyPoppins/JeedomSynologyDSM5.2/master/install_syno.sh
    
    chmod 777 install_syno.sh
    
    ./install_syno.sh
    
    rm install_syno.sh
    
L'installation dure environ 15 minutes et vous demandera de saisir quelques réponses à certaines questions.

Pour toutes les questions où vous devez répondre par Y (Yes) ou N (No), tapez Y.

Vous aurez également plusieurs écrans bleus pour vous demander de configurer certains paramètres :

Le premier concerne les locales : choisissez en.US UTF8 et fr.FR UTF8 en appuyant sur la touche Espace pour mettre une étoile (*) devant chacune des 2 lignes. Appuyez sur la touche Entrée pour valider.
Il vous sera ensuite demandé la Default locale : sélectionnez fr.FR UTF8 et appuyez sur la touche Entrée pour valider.
Ensuite vient le choix du Timezone : Choisissez Europe, puis Paris.
La prochaine question qui vous sera demandée sera si vous voulez installez jeedom et écraser nginx sur la chroot. Répondez par l'affirmative, oui/yes.

Il sera ensuite nécessaire de saisir un mot de passe pour mysql et de le resaisir pour confirmation (choisissez-en un et retenez-le).

L'installation continue et vous demandera à un moment le mot de passe mysql (celui que vous avez choisis juste avant).

Monitoring de Jeedom depuis DSM
-
Dans DSM, cliquez sur l'icône Debian Chroot, cliquez sur Services, puis sur Ajouter, et renseignez comme suit :

    Nom : Jeedom
    Script de lancement : /home/jeedom.sh
    Commande de statut : service jeedom status
    Voilà, vous avez définitivement fini ce tutorial !

Jeedom est maintenant accessible à partir de l'url http://@IP_DU_NAS:8088/jeedom. 
Pensez à bien configurer la section réseau dans JEEDOM.

Définition des droits root à Jeedom
-
Cette étape permettra à Jeedom d’avoir plus de droits et donc de pouvoir par exemple s’éteindre et se redémarrer, ou de gerer le réseaux par exemple.

    sudo su -
    echo "www-data ALL=(ALL) NOPASSWD: ALL" | (EDITOR="tee -a" visudo)
