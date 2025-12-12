# 🛡️ Projet Infra & Sécurité : Virtualisation Réseau

> **Déploiement et sécurisation d'une architecture réseau virtuelle avec Stormshield**

---

## 📋 Table des Matières

1. [Présentation](#-présentation)
2. [Architecture](#-architecture)

---

## 🎯 Présentation

Ce projet consiste en la mise en place d'une infrastructure réseau sécurisée et segmentée. L'objectif est de simuler un environnement d'entreprise réaliste comprenant une zone **LAN** (Réseau Local) et une zone **WAN** (Accès Internet), sécurisées par un pare-feu **Stormshield**.

### Points Forts
* 🔒 **Sécurité Périmétrique** : Filtrage applicatif, URL et Géolocalisation.
* 🌍 **Segmentation Réseau** : Isolation LAN/WAN via pare-feu.
* ⚙️ **Services Autonomes** : Serveur DHCP et DNS interne sous Linux Ubuntu.
* 🛡️ **NAT & Routage** : Configuration de règles de translation d'adresses pour l'accès Internet.

---

## 🏗️ Architecture

Le réseau est divisé en deux zones distinctes, orchestrées par le pare-feu.

### Topologie Logique

```mermaid
graph TD
    %% --- NOEUDS ---
    Internet((Internet / WAN))
    Firewall[🔥 Stormshield EVA]

    %% --- SOUS-GRAPHE LAN ---
    subgraph ZONE_LAN [Zone Locale]
        direction TB
        %% Étiquette réseau en tant que noeud pour être bien visible
        NetLabel(<b>Réseau Interne</b><br/>192.168.56.0/24)
        
        Ubuntu[🐧 Ubuntu Server<br/>IP: 192.168.56.10]
        Win11[💻 Windows 11<br/>IP: 192.168.56.20]
    end

    %% --- CONNEXIONS ---
    Internet ===|Bridge : 10.6.113.58| Firewall
    Firewall ---|LAN : 192.168.56.1| NetLabel
    
    %% Connexions depuis l'étiquette vers les machines
    NetLabel --- Ubuntu
    NetLabel --- Win11

    %% --- STYLES (RETOUR AUX COULEURS) ---
    
    %% Firewall : Orange avec texte BLANC
    style Firewall fill:#171717,stroke:#333,stroke-width:2px,color:white
    
    %% Internet : Bleu avec texte BLANC
    style Internet fill:#171717,stroke:#333,stroke-width:2px,color:white
    
    %% Machines : Fond blanc standard
    style Ubuntu fill:#171717,stroke:#333,stroke-width:1px
    style Win11 fill:#171717,stroke:#333,stroke-width:1px
    
    %% Étiquette réseau : Gris clair pour se différencier
    style NetLabel fill:#171717,stroke:#333,stroke-width:1px,stroke-dasharray: 5 5
    
    %% Fond de la zone LAN
    style ZONE_LAN fill:#171717,stroke:#ccc,stroke-width:2px