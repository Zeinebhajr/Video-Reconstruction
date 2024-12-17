# Video-Reconstruction
# Restructuration de Vidéos : Architecture et Choix Techniques

## Description du Projet
Ce projet vise à **restructurer des vidéos** en regroupant les images similaires tout en assurant une correspondance précise entre les frames. Pour y parvenir, une **approche hybride** a été adoptée, combinant :

- Des techniques d'extraction d'**embeddings** par réseaux neuronaux (ResNet).
- Des algorithmes de **clustering** (DBSCAN).
- Une correspondance de **points d'intérêt** robuste (SuperGlue).

### Objectifs
- **Regrouper** les images similaires en clusters.
- **Aligner** avec précision les frames appartenant au même cluster en utilisant des correspondances de points d'intérêt.

---

## Architecture du Projet

### 1. Extraction d'Embeddings avec ResNet
#### **Justification**
ResNet est utilisé pour extraire des **représentations denses (embeddings)** des images grâce à sa capacité à capturer des caractéristiques visuelles riches. Les embeddings obtenus permettent de mesurer la **similarité** entre les images.

#### **Détails**
- Chaque **frame** de la vidéo est passée à travers un modèle **ResNet** pré-entraîné.
- Une **matrice de similarité** entre embeddings est calculée pour évaluer les distances entre les images.

---

### 2. Clustering des Images avec DBSCAN
#### **Justification**
L'algorithme **DBSCAN** est choisi pour :
- Son efficacité à détecter des groupes **denses** d'images similaires.
- Sa capacité à identifier et gérer les **outliers** (images isolées).

#### **Détails**
- Les **embeddings extraits** servent d'entrée à l'algorithme DBSCAN.
- Les images sont regroupées en **clusters**, chaque cluster représentant une scène similaire.

---

### 3. Correspondance des Points avec SuperGlue
#### **Justification**
Après le clustering, une méthode de **correspondance précise** entre frames est nécessaire pour un alignement optimal. **SuperGlue** est choisi pour sa robustesse grâce à un modèle **deep learning spécialisé**.

#### **Processus**
1. SuperGlue est appliqué aux images appartenant à un même **cluster**.
2. Une **matrice de similarité** est calculée sur la base du nombre de points correspondants.
3. Cette matrice est utilisée pour **ordonner les frames** selon leur niveau de similarité.

---

## Difficultés Rencontrées

### **Limitations avec SIFT et FLANN**
Lors de la phase initiale :
- **SIFT** a été utilisé pour extraire les points clés.
- **FLANN** a servi pour le matching.

**Problème observé** :
- Résultats médiocres en termes de précision et de robustesse.
- Sensibilité aux variations d'**éclairage** ou de **perspective** entre les images.

### **Solution Approchée : Adaptation de SuperGlue**
- SuperGlue a été identifié comme une **alternative prometteuse** d'après des recherches récentes.
- Le code existant a été adapté pour surmonter les limitations de SIFT+FLANN.

---

## Résultats et Améliorations Futures

### **Résultats Actuels**
- Première tentative réussie pour intégrer **SuperGlue** et améliorer la correspondance des points.
- Les résultats sont encore **expérimentaux** mais constituent une base solide pour des améliorations.

### **Axes d'Amélioration**
- Ajuster les **hyperparamètres** de SuperGlue pour un meilleur matching.
- Explorer d'autres algorithmes de clustering comme **HDBSCAN**.
- Comparer les performances de **ResNet** avec d'autres extracteurs d'embeddings tels que **VGG** ou **EfficientNet**.
- Intégrer une **évaluation quantitative** des résultats obtenus.

---

## Conclusion
L'architecture proposée combine des techniques avancées de **deep learning** et de **clustering** pour restructurer des vidéos. Bien que des difficultés aient été rencontrées avec SIFT+FLANN, l'intégration de **SuperGlue** représente un pas vers une correspondance plus robuste des points d'intérêt.

Ce projet reste **expérimental**, avec plusieurs **axes d'amélioration** à explorer pour atteindre des résultats optimaux.

---

## Prérequis

- **Python 3.x**
- Bibliothèques principales :
  - `PyTorch`
  - `OpenCV`
  - `scikit-learn`
  - `numpy`
