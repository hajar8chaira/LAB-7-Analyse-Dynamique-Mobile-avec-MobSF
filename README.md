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
