# Prérequis


## Rust 

Afin de faire fonctionner nos différents programmes (Source & Rustracker), il est nécessaire d'installer le gestionnaire de paquet rust "Cargo" ainsi que le gestionnaire des chaînes d'outils "rustup".

    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

<br/>

---
## Source
 
<p style="text-align:justify;">Afin de faire fonctionner Source,  il est nécessaire de configurer les drivers pour utiliser les dongles RTL-SDR correctement. On propose ici un guide afin d'effectuer les installations nécessaires au bon fonctionnement de Source.</p>

#### Blacklist des pilotes

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

#### Installation des pilotes

Commençons par installer la librairie nécessaire à l'utilisation de SoapySDR, le crate que nous utilisons afin d'utiliser les dongles rtlsdr avec notre code RUST.

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

<br/>

---

## Rustracker

L'installation de certaines librairies est nécessaire au bon fonctionnement du programme Rustracker.

Installons d'abord une librairie permettant d'utiliser pkg-config, un programme de gestion des librairies.

    sudo apt install pkg-config

On installe ensuite la librairie ZeroMQ que l'on utilise pour les communications tcp entre Source et Rustracker.

    sudo apt install libzmq3-dev

Enfin, on installe deux packages nécessaires à la compilation.

    sudo apt install build-essential
    sudo apt install cmake