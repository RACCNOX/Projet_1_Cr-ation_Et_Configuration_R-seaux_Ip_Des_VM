# 🛡️ Projet Infra & Sécurité : Virtualisation Réseau

> **Déploiement et sécurisation d'une architecture réseau virtuelle avec Stormshield**

---

## 📋 Table des Matières

1. [Présentation](#-présentation)
2. [Architecture](#-architecture)
3. [Configuration Réseau](#-configuration-réseau)
4. [Services & Infra](#-services--infra)
5. [Sécurité & Filtrage](#-sécurité--filtrage)
6. [Tests & Validation](#-tests--validation)
7. [Technologies](#-technologies)

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
    %% Noeuds du haut (WAN & Firewall)
    Internet((Internet / WAN<br/>IP: 10.6.113.58))
    Firewall[🔥 Stormshield EVA<br/>Passerelle]

    %% Zone du bas (LAN)
    subgraph LAN_ZONE [Zone LAN]
        direction TB
        %% Le noeud "Network" sert de switch virtuel pour afficher l'IP du réseau clairement
        Network[<b>Réseau Interne</b><br/>192.168.56.0/24]
        
        Ubuntu[🐧 Ubuntu Server<br/>IP: 192.168.56.10]
        Win11[💻 Windows 11<br/>IP: 192.168.56.20]
    end

    %% Connexions
    Internet ===|Bridge| Firewall
    Firewall ---|GW: 192.168.56.1| Network
    
    %% Connexions depuis le Switch virtuel vers les machines
    Network --- Ubuntu
    Network --- Win11

    %% Styles
    style Firewall fill:#ff7043,stroke:#333,stroke-width:2px,color:white
    style Internet fill:#29b6f6,stroke:#333,stroke-width:2px,color:white
    style Ubuntu fill:#fff,stroke:#333,stroke-width:1px
    style Win11 fill:#fff,stroke:#333,stroke-width:1px
    
    %% Style du noeud Réseau pour qu'il ressemble à une étiquette
    style Network fill:#e1f5fe,stroke:#0277bd,stroke-width:2px,stroke-dasharray: 5 5
    style LAN_ZONE fill:#f9f9f9,stroke:#ccc,stroke-width:2px