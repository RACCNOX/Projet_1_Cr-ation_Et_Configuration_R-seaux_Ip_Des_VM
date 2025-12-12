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
    %% Noeuds du haut
    Internet((Internet / WAN<br/>IP: 10.6.113.58))
    Firewall[🔥 Stormshield EVA<br/>Passerelle]

    %% Zone du bas (LAN)
    subgraph LAN [Zone Réseau Interne - 192.168.56.0/24]
        direction TB
        Ubuntu[🐧 Ubuntu Server<br/>IP: 192.168.56.10]
        Win11[💻 Windows 11<br/>IP: 192.168.56.20]
    end

    %% Connexions
    Internet ===|Bridge| Firewall
    Firewall ---|LAN: 192.168.56.1| Ubuntu
    Firewall ---|LAN: 192.168.56.1| Win11

    %% Styles (Couleurs d'origine)
    style Firewall fill:#ff7043,stroke:#333,stroke-width:2px,color:white
    style Internet fill:#29b6f6,stroke:#333,stroke-width:2px,color:white
    style Ubuntu fill:#fff,stroke:#333,stroke-width:1px
    style Win11 fill:#fff,stroke:#333,stroke-width:1px
    style LAN fill:#f4f4f4,stroke:#666,stroke-width:2px,stroke-dasharray: 5 5