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
