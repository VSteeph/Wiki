# Kubernetes

Kubernetes permet de gérer plusieurs containers, il sert de chef d'orchestre (relancer ceux qui ont des problemes, scales, etc). Docker compose est une palier intermediaire entre Docker et Kubernetes mais Kubernetes est plus complet surtout quand on arrive en production.

## Vocabulaire:

**End-State**: L'état final à obtenir et Kubernetes essaie de l'atteindre (comme de l'IK)

**pod** : Un pod contient un container et le fait tourner. Un pod peut avoir plusieurs containers

**node port** ils sont surtout utilisés en environnement de développement, cela permet de directement d'accéder à des pods.

## Architecture

Hardware => OS => (WSL?) => Container Runtime => Kubernetes

Cela peut tourner sur plusieurs Cluster et plusieurs nodes (Ex ELK) mais pas le cas de l'exemple.
