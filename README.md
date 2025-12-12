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

    subgraph LAN [Réseau Interne - 192.168.56.0/24]
        Ubuntu
        Win11
    end

    
    Internet((Internet / WAN))
    Firewall[🔥 Stormshield EVA]
    Ubuntu[🐧 Ubuntu Server<br/>DNS & DHCP]
    Win11[💻 Windows 11<br/>Client]

    Internet -- Bridge (10.6.113.58) --> Firewall
    Firewall -- LAN (192.168.56.1) --> Ubuntu
    Firewall -- LAN --> Win11