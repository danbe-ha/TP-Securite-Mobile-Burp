# Rapport de TP : Analyse de Flux Réseau Mobile (Burp Suite)

## 1. Présentation du Lab
Ce laboratoire démontre la mise en place d'un proxy d'observation entre un **Android Emulator** et une application web de test.

* **Cible :** `testphp.vulnweb.com`
* **Outil :** Burp Suite Professional v2026.1.4
* **Configuration Proxy :** `10.0.2.2:8081`

---

## 2. Accès à la Cible
La première étape consiste à vérifier l'accessibilité du site d'entraînement depuis le navigateur de l'émulateur Android.

![Vue du site vulnérable](images/le%20site%20vulnerable.png)

---

## 3. Analyse de l'Historique (HTTP History)
Une fois la navigation effectuée, l'onglet **HTTP History** de Burp Suite permet de visualiser l'intégralité des échanges entre le mobile et le serveur. Chaque ligne représente une ressource chargée ou une action utilisateur.

![Historique des requêtes Burp](images/burp%20history.png)

---

## 4. Détails des Requêtes Interceptées

### A. Analyse de la requête GET
La requête `GET` est utilisée pour demander l'affichage de la page de connexion. On y observe les en-têtes (Headers) tels que le `User-Agent` identifiant l'émulateur.

![Détail de la requête GET](images/request%20get.png)

### B. Analyse de la requête POST (Données sensibles)
C'est la phase critique : l'envoi des identifiants. On constate que les données (`uname` et `pass`) sont transmises en **texte clair** dans le corps de la requête.

![Détail de la requête POST](images/request%20post.png)

---

## 5. Synthèse et Risques
* **Observation :** Les identifiants "Test / Test" sont interceptés sans aucun chiffrement.
* **Risque :** Attaque de type "Sniffing" ou "Man-in-the-Middle" (MitM).
* **Recommandation :** Migration immédiate vers le protocole **HTTPS** et ajout d'en-têtes de sécurité (HSTS).

---
*TP réalisé par Ali Benrioui - 2026.*