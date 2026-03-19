# Mise en place de l’émulateur Android pour MobSF

##  Objectif
Préparer un environnement Android sécurisé et compatible avec **MobSF** afin d’analyser des applications APK dans de bonnes conditions  
(émulateur rooté, sans Play Store).

---

##  Prérequis
 Les outils suivants sont installés :
- **Android Studio** (avec SDK et ADB)
- **Docker Desktop** (en cours d’exécution)
- **Git**
<p align="center"> <img src="images/0.png" width="800"> </p>

---

##  Étape 1 : Création de l’AVD 

Création d’un émulateur Android depuis **Android Studio** :
<p align="center"> <img src="images/1.png" width="800"> </p>
<p align="center"> <img src="images/2.png" width="800"> </p>
<p align="center"> <img src="images/3.png" width="800"> </p>
Résultat : un émulateur propre, sans services Google, prêt pour l’analyse de sécurité.

---


##  Étape 2 : Récupération de MobSF

Cloner le projet **MobSF** :
<p align="center"> <img src="images/4.png" width="800"> </p>
---

## Étape 3 : Lancement de l’émulateur avec MobSF:
On Utilise le script fourni par MobSF pour démarrer l’émulateur automatiquement configuré.
<p align="center"> <img src="images/5.png" width="800"> </p>
<p align="center"> <img src="images/6.png" width="800"> </p>
### Vérification:
Après le démarrage, vérifier que l’émulateur est bien détecté :
<p align="center"> <img src="images/7.png" width="800"> </p>

---

## Étape 4 : Installation et lancement de MobSF (Docker)

### Téléchargement de l’image
<p align="center"> <img src="images/8.png" width="800"> </p>

```bash
docker pull opensecurity/mobile-security-framework-mobsf:latest
```
### Lancement de MobSF:
<p align="center"> <img src="images/9.png" width="800"> </p>

### Accès à l’interface
<p align="center"> <img src="images/10.png" width="800"> </p>

### Identifiants : Username : mobsf - Password : mobsf

## Étape 5 : Téléchargement de DIVA:
<p align="center"> <img src="images/15.png" width="800"> </p



##  Étape 6 : Analyse Statique + Dynamique de DIVA

###  Objectif
Analyser l’application vulnérable **DIVA** avec **MobSF** en combinant :
- Analyse statique
- Analyse dynamique

---

## 📊 1. Analyse statique

### 🔹 Procédure
1. Accéder à l’interface de MobSF :
<p align="center"> <img src="images/11.png" width="800"> </p>
 ```
http://127.0.0.1:8000
```
2. Cliquer sur **Upload & Analyze**
3. Importer le fichier `diva.apk`
4. Attendre la fin de l’analyse

<p align="center"> <img src="images/12.png" width="800"> </p>

### Résultats observés:
- Analyse du **AndroidManifest.xml**
- Liste des **permissions**
- Extraction du **code source**
- Identification de vulnérabilités :
- Données sensibles exposées

##  2. Analyse dynamique

### Lancement
1. Dans le rapport statique → cliquer sur :
 ```
Start Dynamic Analyzer
```

2. Dans l’émulateur :
<p align="center"> <img src="images/13.png" width="800"> </p>
<p align="center"> <img src="images/14.png" width="800"> </p>
- Lancer l’application **DIVA**
- Explorer les différents challenges :
- Insecure Logging
- Hardcoded Issues
- Insecure Data Storage
- Access Control
- etc. (13 challenges)

---
#  Tests Dynamiques Réalisés

## 1️ Injection Frida (Spawn & Inject)

### Procédure
Dans MobSF :

1. Ouvrir **Dynamic Analyzer**
2. Cliquer sur : Spawn & Inject
3.  Charger le script :

### Objectif
Surveiller l’utilisation de **SharedPreferences** afin de détecter si l’application stocke des données sensibles.

---

### Test effectué

Dans l’application DIVA :

- Saisie :
 ```
username : test
password : 1234
```

Après interaction avec l’application, MobSF a généré les logs suivants :
<p align="center"> <img src="images/19.png" width="800"> </p>

Risque identifié :
Stockage potentiel de données sensibles dans le stockage local.

---

# 2️ Activity Exploration

### Objectif
Explorer les activités internes de l’application et détecter des écrans cachés ou non protégés.

### Procédure

Dans MobSF :

1. Aller dans :
```
Activity Tester
```

2. Lancer plusieurs activités de l’application.
<p align="center"> <img src="images/20.png" width="800"> </p>

### Résultat
-  Découverte de plusieurs activités internes  
-  Accès possible à certains écrans sans authentification  
- Identification de surfaces d’attaque potentielles

---

# 3️ TLS / SSL Security Test
<p align="center"> <img src="images/22.png" width="800"> </p>
### Objectif
Tester la sécurité des communications réseau de l’application.

### Procédure
```
TLS/SSL Security Tester
```
MobSF effectue automatiquement des tests de sécurité sur les connexions réseau.

---

### Vérifications effectuées

- Validation du certificat SSL
- Analyse du pinning certificat
- Détection de vulnérabilités TLS

---


# 📊 Résumé des Tests Dynamiques

| Test | Objectif | Résultat |
|------|----------|----------|
| Frida Injection | Surveiller stockage local | Détection de `SharedPreferences.putString()` |
| Activity Tester | Explorer les activités | Découverte d’écrans internes |
| TLS/SSL Tester | Vérifier la sécurité réseau | Analyse de la configuration SSL |

---


