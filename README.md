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
##  4. Observation dans MobSF

###  Logcat Stream (Runtime Logs)
- Visualisation des logs Android en temps réel
- Filtrage avec :

