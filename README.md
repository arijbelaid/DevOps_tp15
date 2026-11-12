# TP15 : Packager une application Kubernetes (Helm & Kustomize)

Ce dépôt contient le travail du TP15 visant à packager et déployer une application Kubernetes sur un cluster K3s (du TP14) en utilisant deux approches : **Helm** et **Kustomize**.

## 🎯 Objectifs
- Consommer un chart public (podinfo).
- Écrire et structurer un chart Helm complet (templates, values, helpers).
- Gérer le cycle de vie d'une release (install, upgrade, rollback, uninstall).
- Structurer Kustomize avec une base et des overlays (dev, staging, prod).
- Comparer les deux outils et comprendre quand utiliser l'un ou l'autre.

## 📂 Structure du projet
- `chart-starter/` : Contient le chart Helm `whoami` complété (templates et TODO résolus).
- `kustomize-starter/` : Contient la base commune et les overlays (dev, staging, prod).
- `values-dev.yaml` / `values-prod.yaml` : Fichiers de surcharge pour Helm.

## 🚀 Prérequis
- Un cluster K3s fonctionnel (issu du TP14).
- `kubectl` configuré.
- `helm` installé.

## 🛠️ Ce qui a été réalisé

### Partie 1 & 2 : Helm (Chart Custom)
- Étude d'un chart public (`podinfo`).
- Complétion des TODO du chart `whoami` : boucle `range` sur les env, `readinessProbe`, Service paramétré et Ingress conditionnel (`if ingress.enabled`).
- Validation avec `helm lint` et `helm template`.

### Partie 3 : Cycle de vie Helm
- Création d'environnements distincts via `values-dev.yaml` et `values-prod.yaml`.
- Simulation d'un échec de déploiement (image inexistante) pour tester les commandes `helm history` et `helm rollback`.
- Test de l'option `--atomic` (qui annule automatiquement un upgrade échoué).

### Partie 4 : Kustomize
- Prévisualisation de la base et de l'overlay `dev` fournis.
- Création des overlays `staging` et `prod` avec des patches spécifiques (modification de la mémoire, ajout de `readinessProbe`, changement de tag d'image).
- Observation de la génération des ConfigMaps avec suffixe de hash (déclenchant des rolling updates automatiques).

## 📸 Livrables
Les captures d'écran de validation sont disponibles dans le dossier `captures/` (si applicable) :
- `helm-lint-template.png`
- `helm-history.png`
- `helm-atomic.png`
- `kustomize-envs.png`
- `kustomize-diff.png`

## ⚠️ Sécurité
Aucun secret ou identifiant n'est versionné dans ce dépôt.
