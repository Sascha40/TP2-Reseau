# TP2-Reseau.  -- Sascha Sallès -- Mathis Bianco -- Frederic Charruyer
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
| Adresse IP (IPv4) | 10.33.3.141 |00001010.00100001.00000011.10001101|



**Nous n'avons pas de carte ethernet, donc nous n'avons pas d'adresse ethernet**


Adresse de réseau de la carte WiFi : `10.33.0.0`

Adresse de broadcast de la carte WiFi : `10.33.3.255/22` =>  00001010.00100001.00000011.11111111

**Afficher la gateway**

Dans le terminal on tape `route -n get default`, on obtient `gateway: 10.33.3.253`

---
**GUI - Trouvez comment afficher les informations sur une carte IP :**


+ Clic sur la touche option puis sur l'icône *Wifi* du bureau,
   + *Ouvrir les préférences réseau*
+ Cliquer sur *Avancé...*
+ Clic droit sur le réseau *WIFI@YNOV*
+ Cliquer sur l'onglet *TCP/IP*
---
---
**A quoi sert la gateway dans le réseau d'Ingésup ?**

Le gateway est l'adresse qui permet de communiquer avec internet.

---
**Calcul de la première et la dernière IP disponibles:**

Première adresse IP disponible est `10.33.3.1`
Dernière adresse IP disponible est `10.33.3.255`

---
---
**Nmap :**

Aprés l'installation de Nmap sur mac (qui à été fastidieuse), j'ai tapé la commande `nmap -sn -PE 10.33.0.0/22`

```
>Nmap scan report for 10.33.3.254
Host is up (0.0093s latency).
MAC Address: 94:0C:6D:84:50:C8 (Tp-link Technologies)
Nmap scan report for 10.33.3.141
Host is up.
Nmap done: 1024 IP addresses (207 hosts up) scanned in 34.91 seconds
MacBook-Pro-de-Sascha:~ saschasalles$ 
```

On remarque qu'il y a 1024 addresses IP dans le réseau.
On peux s'attribuer une adresse IP dans se réseau via l'interface graphique.

---
## II. Exploration locale en duo

Une fois les firewall désactivés on s'est connectés en RJ45.

### Cablâge

On s'est branché via RJ45 à nos adaptateur qu'on à acheté rien que pour toi 😉

---
### 3. Modification d'adresse IP


Nous avons tout deux modifié l'adresse IP de notre carte Ethernet

Adresse IP de Sascha : `10.0.0.2`

Adresse IP de Mathis : `10.0.0.3`

Masque de sous-réseau : `255.255.255.0`

**Test avec le ping :**
Statistiques Ping pour 10.0.0.3 :
```
--- 10.0.0.3 ping statistics ---
19 packets transmitted, 19 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 0.663/0.901/1.218/0.132 ms
MacBook-Pro-de-Sascha:~ saschasalles$ 
```

### 4. Utilisation d'un des deux comme gateway

Mathis à désactiver sa carte Wifi.

J'ai activé le partage internet. Mais helas sous nous ne pouvons pas acceder à la gateway de l'adaptateur RJ45.

### 5.Petit chat privé
Après 2h passé à essayer de faire la commande nc -l -p 8888, sur le mac de mathis,ainsi que celui de fred, nous n'avons réussi à faire le chat. Nous ne pouvons pas configurer l'ip 182.168.1.12 sur l'adaptateur réseau Nous ne pouvons qu'écouter mais pas envoyer de message. Nous avons essayé sur une VM Linux, évidemment cela n'a pas marché. 

### 6. WireShark
On a pas forcement tout compris de ce truc, mais je te joins un screen des connexions que j'ai filtrer, meme si je vois pas l'interet.

![alt text](https://github.com/Sascha40/TP2-Reseau/blob/master/images/Capture%20d’écran%202019-01-21%20à%2017.16.59.png)

### 7. Firewall
xxxx
---
## III. Exploration locale en duo
### DHCP

Pour savoir ça il faut aller dans Bash et taper `system_profiler SPNetworkDataType | grep "Server Identifier"` (oui on a mis beaucoup du temps à la trouver ;) )
Il nous reponds :
`Server Identifier: 10.33.3.254`

Pour ce qui est de la durée du bail nous ne parvenons pas à trouver la durée du bail dhcp sur mac. Mais il y a un onglet duration sur la commande `system_profiler SPNetworkDataType`
![alt text](https://github.com/Sascha40/TP2-Reseau/blob/master/images/Capture%20d’écran%202019-01-21%20à%2017.47.47.png)

---

**A propos du DHCP**


Nous pouvons dire que le DHCP signifie Dynamic Host Configuration Protocol (protocole de configuration automatiques des hôtes.)

Il est chargé de la configuration automatique des adresses IP d'un réseau. 
Cela évite à l'utilisateur de tout paramétrer ces IP manuellement.

---
Toujours dans notre dans le terminal, on tape la commande `sudo ipconfig set en0 DHCP`

### DNS


Avec la commande `system_profiler SPNetworkDataType`

`Serveur DNS : 10.33.10.20`
Bien que notre commande nous fourni aussi une deuxieme adresse IP du serveur DNS: la `10.33.10.7`
![alt text](https://github.com/Sascha40/TP2-Reseau/blob/master/images/Capture%20d’écran%202019-01-21%20à%2018.00.46.png)

---
---

**Nslookup**
 
lookup de google.com :

on tape dig google.com et on obtient `ANSWER SECTION: google.com. 172.217.22.142`.

lookup de ynov.com :

on tape dig ynov.com et on obtient `ANSWER SECTION: ynov.com. 217.70.184.38`.

Reverse:

Pour 78.78.21.21

Sous mac nous faisons la commande suivante `dig -x 78.78.21.21 +short`
Et on obtient `host-78-78-21-21.mobileonline.telia.com.`

Pour 92.16.54.88

Sous mac nous faisons la commande suivante `dig -x 92.16.54.88 +short`
Et on obtient `host-92-16-54-88.as13285.net.`

Intrepretation: 
C'est la même chose que pour le lookup mais dans l'autre sens. 
C'est-à-dire que `78.78.21.21` est lié au nom de domaine host-78-78-21-21.mobileonline.telia.com

### 3. Bonus

**Se renseigner sur les différences entre WiFi et câble**
Le câble a un meilleur débit que la Wifi car les pertes sont restreintes et que le signal ne peut etre altéré par les murs par exemple.

---

**explorer l'interface d'administration de votre box (chez vous) avec tout ça en tête**

C'est fait via celle de SFR pour moi . 
L'interface est accessible avec l'adresse http://192.168.0.1, 
Sur ce site il y a l'IP, la Wifi etc.

---

**sinon, elle sert à quoi la MAC si on a des IP ? => Se renseigner sur ARP**

Une adresse IP est attribuée en fonction du réseau et celle-ci peut changer. 
L'adresse MAC quant à elle, est physique en fonction de la carte réseau et ne change pas.

---

Nous ne possèdons pas de switch.

---

---



