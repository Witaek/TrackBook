# Prérequis

Afin de faire fonctionner Source,  il est nécessaire de correctement configurer les drivers pour utiliser les antennes RTL-SDR correctement. On propose ici un guide afin d'effectuer correctement les installations nécessaires au bon fonctionnement de Source.

### Blacklist des pilotes

Commençons par connecter le dongle TNT à l'ordinateur.

--> La commande `dsemg` permet de vérifier que le dongle est bien connecté.

Nous allons maintenant blacklister le pilote permettant de regarder la TNT avec le dongle afin qu'il n'interfère pas dans le bon fonctionnement de notre programme.

    ~ $ cd /etc/modprobe.d
    /etc/modprobe.d $ sudo nano rtlsdr.conf

Rajoutons la ligne suivante dans le fichier rtlsdr.conf :

>blacklist dvb_usb_rtl28xxu  

Sauvegardons ensuite rtlsdr.conf.

--> La commande `lsmod` permet de vérifier si le pilote est chargé

Enfin, supprimons le pilote déjà chargé.

    ~ $ blacklist dvb_usb_rtl28xxu

### Instalation des pilotes

Commençons par installer la librairie nécessaire à l'utilisation de SoapySDR, la crate que nouis utilisons afin d'utiliser les dongles rtlsdr avec notre code RUST.

    sudo apt install libsoapysdr-dev libclang-dev llvm-dev pkg-config

On installe ensuite le pilote correspondant.

    sudo apt install soapysdr-module-rtlsdr

Enfin on installe le plugin Soapy pour RTL-SDR.

    git clone https://github.com/pothosware/SoapyRTLSDR.git
    cd SoapyRTLSDR
    mkdir build
    cd build
    cmake ..
    make
    sudo make install