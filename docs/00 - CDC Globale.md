# Cahier des charges global — Homelab Cloud, DevSecOps & Cybersecurity

**Version :** 1.0 — Cadrage global  
**Statut :** Document maître de référence  
**Nature :** Portfolio technique personnel, orienté architecture d'entreprise  
**Périmètre :** Trois projets GitHub interconnectés et indépendamment valorisables

---

## 1. Présentation générale

### 1.1. Contexte

Le homelab est un environnement d'expérimentation personnel destiné à reproduire, à échelle réduite, les principales problématiques rencontrées dans les infrastructures informatiques d'entreprise.

Il doit permettre de concevoir, déployer, sécuriser, automatiser, exploiter et superviser des infrastructures et des applications.

Le homelab ne constitue pas un unique projet monolithique. Il est organisé en trois projets complémentaires, chacun disposant de son propre périmètre, de ses livrables, de sa documentation et de son dépôt GitHub.

### 1.2. Finalité professionnelle

L'objectif est de construire un portfolio démontrant des compétences pertinentes pour des postes et Graduate Programs dans les domaines suivants :

- Cloud Engineering et Cloud Architecture
- Infrastructure Engineering et Platform Engineering
- DevOps, DevSecOps et GitOps
- Cloud Security et Infrastructure Security
- Security Engineering et Security Automation
- Architecture des systèmes et réseaux

Le portfolio doit démontrer non seulement la maîtrise d'outils, mais également la capacité à prendre des décisions d'architecture, expliquer des compromis, gérer des contraintes et valider techniquement les solutions.

### 1.3. Principes directeurs

1. **Architecture avant implémentation :** comprendre les concepts et les besoins avant de choisir les technologies.
2. **Infrastructure as Code :** privilégier la reproductibilité et l'automatisation.
3. **Security by Design :** intégrer la sécurité dès la conception.
4. **Documentation as Code :** versionner les architectures, procédures et décisions.
5. **Modularité :** chaque projet doit pouvoir être présenté et évalué indépendamment.
6. **Interopérabilité :** les projets doivent pouvoir partager une infrastructure et des événements.
7. **Réalisme :** appliquer des principes d'entreprise sans prétendre disposer d'un datacenter de production.
8. **Sobriété :** tenir compte des limitations matérielles et éviter les composants disproportionnés.

---

## 2. Organisation du portfolio

### 2.1. Vue d'ensemble

Le homelab comporte trois projets principaux.

| Projet | Nom | Objectif principal |
|---|---|---|
| P1 | Automated Hybrid Landing Zone | Construire l'infrastructure réseau, système et sécurité |
| P2 | DevSecOps & GitOps Software Factory | Automatiser la livraison sécurisée des applications |
| P3 | Detection-as-Code & SOAR Platform | Détecter, analyser et automatiser les réponses aux événements de sécurité |

Les trois projets représentent des couches complémentaires d'un même environnement.

### 2.2. Architecture fonctionnelle globale

```text
                  HOMELAB
                     |
       +-------------+-------------+
       |                           |
  INFRASTRUCTURE              AUTOMATISATION
       |                           |
       +--------- PROJET 1 --------+
       |  Proxmox / OPNsense       |
       |  Terraform / Ansible      |
       |  Réseaux / Sécurité       |
       +-------------+-------------+
                     |
              Hébergement
                     |
       +--------- PROJET 2 --------+
       |  Application de référence |
       |  CI/CD / DevSecOps        |
       |  Conteneurs / GitOps      |
       +-------------+-------------+
                     |
            Logs / Événements
                     |
       +--------- PROJET 3 --------+
       |  Collecte / Détection     |
       |  Detection-as-Code        |
       |  SOAR / Réponse           |
       +---------------------------+
```

Ce schéma représente les relations logiques entre les projets, et non une obligation de déployer toutes les solutions simultanément.

---

## 3. Projet 1 — Automated Hybrid Landing Zone

### 3.1. Mission

Concevoir et automatiser une infrastructure virtualisée, segmentée et sécurisée, capable d'héberger les composants des projets suivants.

Le projet doit fournir une fondation cohérente, reproductible et documentée.

### 3.2. Périmètre fonctionnel

- Virtualisation avec Proxmox VE.
- Réseaux virtuels et segmentation.
- Routage, NAT et filtrage.
- Firewall central OPNsense.
- DMZ et zones internes.
- Provisionnement automatisé avec Terraform.
- Configuration et durcissement avec Ansible.
- Initialisation des VM avec Cloud-init.
- Gestion des accès administratifs.
- Documentation des flux réseau.
- Validation de la sécurité et de la reproductibilité.

### 3.3. Technologies retenues

| Domaine | Technologie |
|---|---|
| Hyperviseur | Proxmox VE |
| Infrastructure as Code | Terraform |
| Configuration Management | Ansible |
| Firewall / routage | OPNsense |
| Initialisation | Cloud-init |
| Systèmes invités | Debian / Linux |
| Versionnement | Git / GitHub |

### 3.4. Livrables

- Architecture physique et logique.
- Plan d'adressage.
- Matrice des flux.
- Code Terraform.
- Playbooks et rôles Ansible.
- Règles de sécurité.
- Tests de connectivité et d'isolation.
- Documentation de déploiement.
- Architecture Decision Records (ADR).
- Démonstration de reproductibilité.

### 3.5. Référence

Le **CDC détaillé du Projet 1 — Version 1.0** constitue la spécification de référence de ce projet.

Le présent document maître n'a pas vocation à reproduire les détails du CDC P1.

---

## 4. Projet 2 — DevSecOps & GitOps Software Factory

### 4.1. Mission

Concevoir une chaîne de livraison logicielle automatisée, reproductible et sécurisée, allant du code source jusqu'au déploiement d'une application.

Le projet doit démontrer la capacité à construire une plateforme de livraison logicielle intégrant des contrôles de sécurité à différentes étapes.

### 4.2. Vision fonctionnelle

Le fonctionnement cible est le suivant :

```text
Développeur
    |
    v
Git Repository
    |
    v
CI Pipeline
    |
    +-- Tests
    +-- SAST
    +-- SCA
    +-- Secret Scanning
    +-- IaC Scanning
    |
    v
Build d'image
    |
    +-- Container Scanning
    +-- SBOM
    |
    v
Container Registry
    |
    v
CD / GitOps
    |
    v
Environnement applicatif
    |
    v
Monitoring / Logs
```

Cette chaîne est une architecture fonctionnelle cible. Les technologies exactes, l'ordre détaillé des contrôles et les politiques de blocage seront définis dans le CDC du Projet 2.

### 4.3. Axes à explorer

**Intégration continue**

- Git et stratégies de branches.
- Pipelines CI.
- Tests automatisés.
- Construction d'artefacts.
- Gestion des dépendances.
- Qualité et sécurité du code.

**Sécurité de la chaîne logicielle**

- SAST.
- SCA.
- Détection de secrets.
- Analyse des images de conteneurs.
- Analyse des configurations IaC.
- SBOM.
- Gestion des vulnérabilités.
- Sécurisation des secrets et identités des pipelines.
- Signature et provenance des artefacts, à étudier.

**Déploiement continu**

- Conteneurisation Docker.
- Registry d'images.
- Kubernetes, si pertinent.
- GitOps.
- Gestion des environnements.
- Rollback et stratégies de déploiement.
- Gestion des configurations et secrets.

**Exploitation**

- Logs applicatifs.
- Métriques.
- Health checks.
- Disponibilité.
- Traçabilité des déploiements.

### 4.4. Technologies candidates

Ces technologies ne constituent pas des choix définitifs.

| Fonction | Solutions à étudier |
|---|---|
| CI/CD | GitHub Actions, GitLab CI, Jenkins |
| SAST | Semgrep, SonarQube |
| SCA | Trivy, OWASP Dependency-Check |
| Secrets | Gitleaks |
| IaC Security | Checkov, Trivy |
| Container Security | Trivy |
| SBOM | Syft |
| Registry | Harbor, GitHub Container Registry |
| Orchestration | Kubernetes, K3s |
| GitOps | Argo CD, Flux |
| Monitoring | Prometheus, Grafana |
| Logs | Loki ou autre solution adaptée |

Les choix devront tenir compte des ressources disponibles, de l'intérêt pédagogique, de la maintenabilité et de la pertinence professionnelle.

### 4.5. Application de référence

Une application servira de support pour démontrer l'ensemble de la chaîne.

Elle devra être suffisamment réaliste pour justifier les tests, le packaging, le déploiement et la supervision, sans transformer le projet en exercice de développement applicatif complexe.

L'architecture exacte reste à déterminer : application simple, API avec base de données, ou application composée de plusieurs services.

### 4.6. Résultats attendus

- Pipeline automatisé de bout en bout.
- Contrôles de sécurité documentés.
- Artefacts versionnés.
- Déploiements reproductibles.
- Gestion sécurisée des identités et secrets.
- Démonstration d'un échec de contrôle bloquant un déploiement.
- Démonstration d'un déploiement réussi.
- Démonstration d'un rollback.
- Documentation des décisions et compromis.

### 4.7. Limites de ce cadrage

Le choix définitif de Kubernetes, du moteur CI/CD, du registry, des outils de sécurité et de l'application sera effectué dans le CDC détaillé P2.

---

## 5. Projet 3 — Detection-as-Code & SOAR Platform

### 5.1. Mission

Construire une plateforme permettant de collecter des événements de sécurité, de détecter des comportements suspects à l'aide de règles versionnées et d'automatiser certaines opérations d'investigation ou de réponse.

Le projet doit démontrer une approche d'ingénierie de la détection et d'automatisation de la sécurité.

Il ne doit pas se limiter à installer un SIEM et afficher des dashboards.

### 5.2. Vision fonctionnelle

```text
         SOURCES D'ÉVÉNEMENTS
                  |
       +----------+----------+
       |          |          |
    OPNsense    Linux     Projet 2
       |          |          |
       +----------+----------+
                  |
                  v
          Collecte de logs
                  |
                  v
         Normalisation / SIEM
                  |
                  v
           Detection Rules
           (Detection-as-Code)
                  |
                  v
                Alertes
                  |
                  v
          Enrichissement
                  |
                  v
            SOAR / Playbooks
                  |
          +-------+-------+
          |               |
     Notification     Réponse
```

### 5.3. Axes à explorer

**Collecte et visibilité**

- Logs Linux et authentification SSH.
- Logs OPNsense.
- Événements réseau.
- Logs applicatifs.
- Événements de sécurité CI/CD.
- Centralisation et conservation.
- Horodatage et normalisation.

**Detection Engineering**

- Règles de détection.
- Detection-as-Code.
- Sigma.
- Corrélation d'événements.
- Réduction des faux positifs.
- Tests de règles.
- Couverture MITRE ATT&CK.

**Simulation et validation**

- Génération contrôlée d'événements.
- Simulation de comportements suspects.
- Tests de déclenchement.
- Mesure de la qualité des détections.
- Documentation des scénarios.

**SOAR**

- Enrichissement d'alertes.
- Playbooks de réponse.
- Notifications.
- Gestion des validations humaines.
- Actions de confinement.
- Journalisation des actions automatisées.
- Prévention des réponses destructrices ou injustifiées.

### 5.4. Technologies candidates

| Fonction | Solutions à étudier |
|---|---|
| SIEM / XDR | Wazuh |
| Collecte | Syslog, agents, collecteurs |
| Règles portables | Sigma |
| Référentiel de détection | MITRE ATT&CK |
| Simulation | Atomic Red Team |
| Automatisation | Shuffle, StackStorm, scripts Python |
| Enrichissement | API et outils open source |
| Visualisation | Dashboards SIEM |

Ces choix ne sont pas figés. La plateforme devra être dimensionnée pour le matériel réellement disponible.

### 5.5. Scénarios envisagés

**Scénario A — Tentatives d'accès SSH**

Détecter plusieurs tentatives d'authentification échouées, déclencher une alerte et enrichir les informations de la source.

**Scénario B — Flux réseau interdit**

Observer un flux bloqué entre une zone DMZ et une zone d'administration, puis produire un événement exploitable.

**Scénario C — Activité suspecte sur un serveur**

Générer un comportement contrôlé, vérifier la remontée des événements et valider une règle de détection.

**Scénario D — Événement DevSecOps**

Exploiter un événement de sécurité issu de la Software Factory : secret détecté, vulnérabilité critique ou échec d'un contrôle de sécurité.

**Scénario E — Réponse automatisée**

À partir d'une alerte validée, déclencher un playbook de notification ou de confinement limité, réversible et auditable.

### 5.6. Résultats attendus

- Collecte multi-source.
- Détections versionnées dans Git.
- Scénarios reproductibles.
- Règles testées.
- Alertes documentées.
- Playbooks d'automatisation.
- Démonstration de réponse contrôlée.
- Indicateurs de qualité des détections.
- Documentation des limites et faux positifs.

### 5.7. Limites de ce cadrage

Le CDC P3 déterminera l'architecture précise, les outils, les scénarios prioritaires, les ressources nécessaires et les critères d'acceptation.

---

## 6. Architecture matérielle du homelab

### 6.1. PVE-01 — Infrastructure principale

**Machine :** HP ProBook 430 G5

- Processeur : Intel Core i5-8250U, 4 cœurs / 8 threads.
- RAM : 8 Go.
- SSD : 256 Go nominal.
- Hyperviseur : Proxmox VE.
- Rôle prioritaire : infrastructure réseau et services essentiels.

Composants envisagés :

- OPNsense.
- Bastion.
- Machines légères d'administration.
- Services d'infrastructure.

La RAM constitue la contrainte principale.

### 6.2. PVE-02 — Infrastructure complémentaire

**Machine :** HP ZBook 14u G6

- RAM totale : 32 Go.
- SSD : 512 Go.
- Système hôte : environnement de travail personnel.
- Proxmox secondaire : virtualisation imbriquée, à titre expérimental.

Dimensionnement initial envisagé :

- 4 vCPU.
- 8 Go de RAM.
- Environ 80 Go de stockage.

Cette infrastructure est destinée à accueillir des charges complémentaires, notamment applicatives.

**Point d'attention :** PVE-02 est une capacité expérimentale et optionnelle. Le homelab doit rester exploitable lorsque cette machine est arrêtée.

### 6.3. Évolutivité

Les ressources disponibles ne permettent pas nécessairement de faire fonctionner simultanément toutes les plateformes.

Le homelab doit donc accepter :

- L'activation des services à la demande.
- Des profils de déploiement légers.
- La destruction et la reconstruction des environnements temporaires.
- La réutilisation des ressources entre projets.
- L'externalisation ponctuelle de certaines expérimentations vers des offres cloud gratuites ou peu coûteuses, après évaluation.

L'achat de matériel supplémentaire ne constitue pas un prérequis.

---

## 7. Réseau et sécurité transverses

### 7.1. Segmentation de référence

Le Projet 1 prévoit les zones suivantes :

| VLAN | Zone | Réseau |
|---|---|---|
| 10 | DMZ | 10.10.10.0/24 |
| 20 | ADMIN | 10.10.20.0/24 |
| 30 | APP | 10.10.30.0/24 |
| 99 | MANAGEMENT | 10.10.99.0/24 |

Cette segmentation constitue la base logique initiale.

Elle pourra être étendue si un besoin réel apparaît dans P2 ou P3, après mise à jour du plan réseau et des règles de sécurité.

### 7.2. Exigences de sécurité

- Isolation des environnements.
- Filtrage explicite des communications.
- Refus par défaut des flux non autorisés.
- Administration par des chemins contrôlés.
- Authentification forte lorsque possible.
- Secrets exclus des dépôts publics.
- Permissions minimales.
- Traçabilité des accès.
- Séparation entre environnements de test et services d'administration.
- Conservation d'un accès de secours à Proxmox.

### 7.3. Sécurité des expérimentations

Les simulations offensives du Projet 3 devront être réalisées exclusivement sur des systèmes appartenant au laboratoire ou explicitement autorisés.

Les scénarios devront éviter tout impact sur le réseau extérieur, les services personnels et les équipements non concernés.

Les actions automatisées de réponse devront être limitées, vérifiables et, lorsque pertinent, réversibles.

---

## 8. Interactions entre les projets

### 8.1. Projet 1 vers Projet 2

P1 fournit :

- Réseau.
- Machines virtuelles.
- Segmentation.
- DNS et connectivité.
- Accès administratifs.
- Socle système sécurisé.
- Provisionnement reproductible.

P2 utilise ces capacités pour héberger et déployer ses composants.

### 8.2. Projet 1 vers Projet 3

P1 fournit notamment :

- Journaux du firewall.
- Événements réseau.
- Logs Linux.
- Événements d'authentification.
- Infrastructure hébergeant les collecteurs et outils de sécurité.

### 8.3. Projet 2 vers Projet 3

P2 peut fournir :

- Logs applicatifs.
- Événements de pipeline.
- Résultats d'analyses de sécurité.
- Événements de déploiement.
- Événements d'authentification et d'exécution.

P3 exploite ces sources pour développer et tester ses détections.

### 8.4. Indépendance

Chaque projet doit posséder :

- Un README autonome.
- Une documentation d'architecture.
- Ses propres prérequis.
- Ses scripts et configurations.
- Ses tests.
- Ses livrables.
- Ses limites connues.

Un recruteur doit pouvoir comprendre la valeur de P2 ou P3 sans devoir lire intégralement les autres dépôts.

---

## 9. Stratégie GitHub et documentation

### 9.1. Organisation cible

```text
GitHub Portfolio
|
+-- project-01-hybrid-landing-zone
|
+-- project-02-devsecops-gitops-factory
|
+-- project-03-detection-as-code-soar
```

Le CDC global pourra être conservé dans un espace documentaire central, avec des liens vers les trois projets.

### 9.2. Contenu documentaire minimal

Chaque projet devra présenter :

- Le problème traité.
- Les objectifs.
- Les contraintes.
- L'architecture.
- Les choix techniques.
- Les alternatives étudiées.
- Les procédures de déploiement.
- Les contrôles de sécurité.
- Les tests et preuves.
- Les difficultés rencontrées.
- Les améliorations possibles.

### 9.3. Valorisation professionnelle

Le portfolio devra privilégier les démonstrations concrètes :

- Diagrammes d'architecture.
- Extraits de code.
- Captures de tests.
- Rapports de validation.
- Exemples de pipelines.
- Démonstrations de segmentation.
- Scénarios de détection.
- Résultats mesurables.

L'objectif n'est pas de multiplier les technologies, mais de démontrer une compréhension approfondie et une mise en œuvre justifiable.

---

## 10. Architecture Cloud et transférabilité

Même si l'environnement initial repose sur Proxmox, les principes doivent être rapprochés de ceux utilisés sur AWS et Azure.

### 10.1. Correspondances conceptuelles

| Homelab | Concepts Cloud |
|---|---|
| Proxmox VM | EC2 / Azure VM |
| Réseaux virtuels | VPC / VNet |
| Segmentation | Subnets et contrôles réseau |
| OPNsense | Firewall et fonctions réseau Cloud |
| Bastion | Bastion host / services Bastion |
| Terraform | IaC Cloud |
| Ansible | Configuration Management |
| CI/CD | Pipelines Cloud |
| Registry | ECR / ACR |
| Kubernetes | EKS / AKS |
| Centralisation de logs | CloudWatch / Azure Monitor et solutions SIEM |

Ces correspondances sont conceptuelles : les modèles de responsabilité, les services managés et les mécanismes réseau diffèrent.

### 10.2. Extension Cloud envisagée

Une extension hybride ou cloud-native pourra être ajoutée ultérieurement pour démontrer :

- La connexion d'un environnement local à un cloud public.
- Le provisionnement cloud avec Terraform.
- L'utilisation d'IAM.
- La gestion des réseaux cloud.
- Le déploiement d'applications.
- L'observabilité et la sécurité cloud.

Cette extension est **optionnelle** et ne doit pas retarder les trois projets principaux.

---

## 11. Contraintes globales

### 11.1. Matériel

- RAM limitée sur PVE-01.
- Stockage limité.
- Processeurs non dédiés exclusivement au homelab.
- PVE-02 dépendant de la disponibilité du poste personnel.
- Absence de switch physique administrable.

### 11.2. Budget

Privilégier les outils gratuits, open source et les ressources déjà disponibles.

Les dépenses éventuelles devront être justifiées par un besoin pédagogique ou technique réel.

### 11.3. Complexité

Éviter les architectures inutilement distribuées.

Ne pas déployer Kubernetes, un cluster Proxmox, Ceph ou plusieurs solutions SIEM uniquement pour enrichir artificiellement la liste des technologies.

### 11.4. Disponibilité

Le homelab est un environnement d'apprentissage.

Il ne vise pas une disponibilité 24/7 ni des engagements de service de production.

### 11.5. Sécurité des données

Ne pas publier :

- Identifiants et tokens.
- Clés privées.
- Secrets applicatifs.
- Fichiers d'état Terraform contenant des informations sensibles.
- Sauvegardes contenant des secrets.
- Informations privées de l'environnement personnel.

---

## 12. Stratégie de réalisation

### Phase globale 0 — Cadrage

- Rédiger le CDC maître.
- Valider le périmètre des trois projets.
- Définir les dépendances.
- Identifier les contraintes.
- Préparer la documentation.

### Phase globale 1 — Infrastructure

Réaliser le Projet 1.

Résultat : disposer d'une fondation réseau et système sécurisée, automatisée et testée.

### Phase globale 2 — Software Factory

Réaliser le Projet 2.

Résultat : disposer d'une chaîne de livraison logicielle sécurisée et reproductible, avec une application de démonstration.

### Phase globale 3 — Detection & Response

Réaliser le Projet 3.

Résultat : disposer d'une plateforme capable d'exploiter les événements de P1 et P2 pour détecter des comportements suspects et automatiser des réponses contrôlées.

### Phase globale 4 — Intégration et valorisation

- Vérifier les interactions entre projets.
- Réaliser des scénarios transverses.
- Finaliser la documentation.
- Produire des diagrammes et démonstrations.
- Préparer des présentations techniques et des explications adaptées aux entretiens.

Les projets peuvent être développés de façon incrémentale. Leur ordre ne constitue pas une obligation de terminer intégralement chaque projet avant d'étudier le suivant.

---

## 13. Démonstrations transverses envisagées

### Démonstration 1 — Provisionnement sécurisé

Déployer une VM avec Terraform, appliquer son durcissement avec Ansible et vérifier ses règles de communication.

**Projets concernés :** P1.

### Démonstration 2 — Livraison logicielle sécurisée

Modifier le code de l'application, déclencher le pipeline, exécuter les contrôles de sécurité, produire une image et déployer la nouvelle version.

**Projets concernés :** P1 + P2.

### Démonstration 3 — Vulnérabilité bloquante

Introduire volontairement une faiblesse dans un environnement de test, vérifier sa détection par le pipeline et empêcher sa promotion.

**Projets concernés :** P2.

### Démonstration 4 — Détection réseau

Générer un flux interdit entre deux zones, vérifier son blocage par OPNsense et exploiter l'événement dans la plateforme de détection.

**Projets concernés :** P1 + P3.

### Démonstration 5 — Incident et réponse automatisée

Simuler un événement de sécurité contrôlé, déclencher une règle de détection, enrichir l'alerte et exécuter un playbook de réponse avec validation humaine lorsque nécessaire.

**Projets concernés :** P1 + P3, éventuellement P2.

### Démonstration 6 — Chaîne de bout en bout

```text
Terraform
    |
    v
Infrastructure
    |
    v
Ansible / Hardening
    |
    v
CI / Security Checks
    |
    v
Build / Registry
    |
    v
GitOps Deployment
    |
    v
Application
    |
    v
Logs / Detection
    |
    v
SOAR / Response
```

Cette démonstration constituera une synthèse du portfolio, sans être un prérequis à la validation individuelle de chaque projet.

---

## 14. Critères de réussite globaux

Le homelab sera considéré comme ayant atteint ses objectifs principaux lorsque :

- Les trois projets possèdent une documentation claire et autonome.
- L'infrastructure P1 est reproductible et correctement segmentée.
- La chaîne P2 exécute des contrôles de sécurité et déploie une application.
- La plateforme P3 détecte des événements reproductibles et déclenche au moins une automatisation contrôlée.
- Les interactions entre les projets sont démontrées.
- Les secrets sont correctement protégés.
- Les principaux choix d'architecture sont documentés.
- Les limites et compromis techniques sont explicitement présentés.
- Les démonstrations peuvent être expliquées et défendues en entretien.

Le succès ne dépend pas du nombre d'outils installés ni du nombre de machines virtuelles créées.

---

## 15. Idées complémentaires — Backlog non engagé

Les idées suivantes sont conservées pour ne pas être perdues. Elles ne font pas partie des obligations de la version initiale.

### Infrastructure et Cloud

- Extension AWS ou Azure.
- VPN site-to-site vers un cloud public.
- Landing Zone cloud-native.
- Infrastructure multi-environnement.
- Terraform remote state.
- Policy as Code.
- Gestion centralisée des secrets.
- PKI interne et gestion des certificats.
- Haute disponibilité expérimentale.
- Sauvegardes et tests de restauration.

### DevSecOps et Platform Engineering

- Kubernetes avancé.
- Admission controllers.
- Network Policies Kubernetes.
- OPA / Kyverno.
- Signature d'images.
- Supply-chain security.
- SLSA et provenance.
- Infrastructure GitOps.
- Golden paths / templates applicatifs.
- Developer self-service.

### Cybersecurity

- Threat Intelligence.
- Honeypot isolé.
- Threat Hunting.
- Détections MITRE ATT&CK.
- Tests automatisés des règles de détection.
- Simulation d'attaques.
- Forensics.
- Enrichissement automatisé.
- SOAR avec validation humaine.
- Mesure de couverture des détections.

### Observabilité et fiabilité

- Centralisation des métriques.
- Alerting.
- SLO / SLI.
- Distributed Tracing.
- Tests de résilience.
- Chaos Engineering contrôlé.
- Capacity Planning.

Chaque idée devra être évaluée selon sa valeur professionnelle, son coût, sa complexité et sa compatibilité avec le matériel.

---

## 16. Gestion des décisions et des évolutions

Le présent document définit la vision globale du homelab.

Les choix sont répartis en trois catégories :

**Décidé**

- Trois projets distincts et complémentaires.
- Proxmox comme fondation locale.
- Terraform et Ansible pour P1.
- OPNsense comme firewall principal.
- Sécurité intégrée dès la conception.
- Dépôts GitHub indépendants.
- Documentation et tests obligatoires.

**Orientation envisagée**

- CI/CD intégrant plusieurs contrôles de sécurité.
- Déploiement GitOps.
- Kubernetes ou distribution légère.
- Détection versionnée dans Git.
- Plateforme SIEM et automatisation SOAR.
- Intégration des événements entre projets.

**À étudier**

- Technologies définitives de P2 et P3.
- Dimensionnement des services.
- Stratégie de gestion des secrets.
- Architecture de monitoring et de logs.
- Modalités d'intégration multi-nœuds.
- Extension cloud.
- Ordre et profondeur des fonctionnalités avancées.

Une modification du CDC d'un projet ne doit entraîner une modification du CDC maître que si elle affecte la vision, les interfaces ou les contraintes globales.

---

## 17. Documents de référence

| Document | Fonction | Statut |
|---|---|---|
| CDC global du homelab | Vision et cohérence d'ensemble | V1.0 |
| CDC P1 — Hybrid Landing Zone | Architecture infrastructure détaillée | V1.0 existante |
| CDC P2 — DevSecOps & GitOps | Architecture de livraison logicielle | À rédiger |
| CDC P3 — Detection-as-Code & SOAR | Architecture de détection et réponse | À rédiger |

---

## 18. Conclusion

Le homelab doit constituer une plateforme d'apprentissage et un portfolio professionnel cohérent.

Les trois projets répondent à trois questions complémentaires :

**Projet 1 :** Comment construire et sécuriser une infrastructure ?

**Projet 2 :** Comment livrer des applications de manière automatisée et sécurisée sur cette infrastructure ?

**Projet 3 :** Comment surveiller cet environnement, détecter des activités suspectes et automatiser des réponses adaptées ?

La valeur du portfolio repose sur la capacité à expliquer et démontrer l'ensemble du cycle : **concevoir → provisionner → configurer → sécuriser → déployer → observer → détecter → répondre**.

Le CDC global conserve cette vision. Les CDC individuels définissent les moyens précis de la mettre en œuvre.