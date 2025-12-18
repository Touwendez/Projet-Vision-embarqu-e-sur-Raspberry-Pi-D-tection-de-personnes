# Projet — Vision embarquée sur Raspberry Pi : Détection de personnes (temps réel)

Ce dépôt présente un système de **vision embarquée** déployé sur **Raspberry Pi** permettant la **détection de personnes en temps réel** à partir d’un flux caméra.  
L’objectif est d’obtenir une détection **fiable en conditions réelles**, avec une exécution **continue sous Linux** (orchestration des scripts, logs, relance) et des performances adaptées à une plateforme embarquée.

---

## Sommaire
- [Contexte](#contexte)
- [Objectifs](#objectifs)
- [Fonctionnalités](#fonctionnalités)
- [Stack](#stack)
- [Architecture](#architecture)
- [Pipeline de traitement](#pipeline-de-traitement)
- [Campagne de tests et réglages](#campagne-de-tests-et-réglages)
- [Optimisations embarquées](#optimisations-embarquées)
- [Utilisation](#utilisation)
- [Arborescence](#arborescence)
- [Résultats](#résultats)
- [Limites et améliorations](#limites-et-améliorations)
- [Aperçu visuel](#aperçu-visuel)
- [Vidéos](#vidéos)
- [Confidentialité](#confidentialité)

---

## Contexte
Dans un environnement atelier / industriel, la détection automatique de présence humaine peut servir à :
- renforcer la **sécurité** (zone d’accès, alerte, arrêt contrôlé),
- améliorer la **traçabilité** (événements horodatés),
- fournir une brique de perception pour des systèmes d’**automatisation**.

Le projet vise une solution **autonome**, capable de tourner en continu sur un **Raspberry Pi** avec une caméra (USB/CSI), en exploitant des modèles IA via **TensorFlow** ou **PyTorch**.

---

## Objectifs
- Détecter des personnes à partir d’un flux vidéo **temps réel**.
- Évaluer plusieurs modèles IA (précision / latence / FPS) et sélectionner une configuration adaptée à l’embarqué.
- Améliorer la **robustesse** par réglages (seuils, filtrage, conditions réelles).
- Garantir une exécution **stable sous Linux** (gestion caméra, orchestration, logs, relance).

---

## Fonctionnalités
- Acquisition vidéo temps réel (caméra USB/CSI)
- Pré-traitement OpenCV (resize, conversion, normalisation)
- Inférence IA (TensorFlow / PyTorch)
- Post-traitement (seuil, filtrage, suppression des doublons selon modèle)
- Overlay (bounding boxes, score, FPS) et/ou sortie logs
- Mode exécution continue : lancement, supervision, relance si crash
- Paramétrage simple via fichier de config (seuils, source vidéo, modèle)

---

## Stack
- **Python**
- **OpenCV**
- **TensorFlow**, **PyTorch**
- **Linux** (Raspberry Pi OS / Ubuntu)
- Matériel : **Raspberry Pi**, caméra USB/CSI


https://github.com/user-attachments/assets/a7fdc5fd-93c3-476b-b16a-417721183a08


https://github.com/user-attachments/assets/3d837bf3-29b5-489e-8571-d21a323329fc



---


## Architecture

```mermaid
flowchart LR
  A[Camera USB/CSI] --> B[Raspberry Pi - Linux]
  B --> C[Capture video - OpenCV]
  C --> D[Pre-traitement]
  D --> E[Inference IA - TensorFlow / PyTorch]
  E --> F[Post-traitement - seuils / filtrage]
  F --> G[Overlay + affichage]
  F --> H[Logs + evenements horodates]
  H --> I[Execution continue / supervision]
