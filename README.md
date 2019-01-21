# TP2-Reseau
Ce tp est entièrement réalisé sous le système macOs.

## I. Exploration locale en solo


### 1. Affichage d'informations sur la pile TCP/IP locale


---
**Affichez les infos des cartes réseau sur mac :**

Sur mac, on ouvre bash et on tape la commande `ifconfig`

| NOM         | Carte Réseau Sans Fil           | Binaire|
| ------------- |-------------|----------------|
| Masque de sous-réseau      | 255.255.252.0 | 11111111.11111111.11111100.00000000|
| Adresse MAC      | 20-16-B9-E9-7D-E8      ||
| Adresse IP (IPv4) | 10.33.2.92 (préféré)      | 00001010.00100001.00000010.01011100 |


| NOM         | Carte Ethernet Ethernet |
| ------------- |-------------|
| Adresse MAC      | 10-65-30-74-17-F0      |
| Adresse IP      | il n'y en a pas car c'est relié à un port RJ45|


Adresse de réseau de la carte WiFi : `10.33.0.0`

Adresse de broadcast de la carte WiFi : `10.33.3.255/22` =>  00001010.00100001.00000011.11111111
