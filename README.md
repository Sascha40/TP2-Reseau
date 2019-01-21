# TP2-Reseau
Ce tp est entièrement réalisé sous le système macOs.

## I. Exploration locale en solo


### 1. Affichage d'informations sur la pile TCP/IP locale


---
**Affichez les infos des cartes réseau sur mac :**

Sur mac, on ouvre bash et on tape la commande `ifconfig`

| NOM         | Carte Réseau Sans Fil           | Binaire|
| ------------- |-------------|----------------|
| Masque de sous-réseau      | 0xfffffc00 ou 255.255.252.0 | 11111111.11111111.11111100.00000000|
| Adresse MAC      | f0:18:98:46:5c:b2 ||
| Adresse IP (IPv4) | 10.33.3.253 (préféré)      |00001010.00100001.00000011.11111101|


| NOM         | Carte Ethernet Ethernet |
| ------------- |-------------|
| Adresse MAC      | 10-65-30-74-17-F0      |
| Adresse IP      | il n'y en a pas car c'est relié à un port RJ45|


Adresse de réseau de la carte WiFi : `10.33.0.0`

Adresse de broadcast de la carte WiFi : `10.33.3.255/22` =>  00001010.00100001.00000011.11111111

![alt text]( https://github.com/Sascha40/TP2-Reseau/blob/master/images/Capture%20d’écran%202019-01-21%20à%2011.53.13.png "capture")
