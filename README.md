# 🌐 Lab MPLS / VPN End-to-End

Projet de mise en œuvre, d'interconnexion et de validation d'une architecture **MPLS / VPN BGP Option A** interconnectant deux sites distants d'une entreprise (**SIEGE** et **AGENCE**) à travers un réseau d'opérateur (Backbone Service Provider).

---

## 🛠️ Spécifications & Équipements Émulés

* **Émulateur :** GNS3
* **Équipements Réseau :** Routeurs Cisco 7200 Series
* **Version IOS :** Cisco IOS v15.3 (ou équivalent 15.x)
* **Système d'exploitation client :** Windows / Linux pour la validation du trafic

---

## 📐 Architecture & Configuration du Réseau

### 1. Cœur de Réseau (Backbone Service Provider - AS 65000)
* **IGP Interne :** **OSPF (Zone 0)** assurant la connectivité IP interne entre les routeurs `SP1`, `SP2` et `SP3`.
* **Commutation de Labels :** **MPLS LDP** activé sur l'ensemble des interfaces du Backbone SP.
* **Plage Loopbacks :** 
  * `SP1` (PE 1) : `1.1.1.1/32`
  * `SP2` (P) : `2.2.2.2/32`
  * `SP3` (PE 2) : `3.3.3.3/32`
* **Multiprotocol BGP (MP-BGP) :** Session iBGP VPNv4 établie directement entre les routeurs PE (`SP1` et `SP3`).

### 2. Accès Client & Virtual Routing and Forwarding (VRF)
* **Nom de la VRF :** `CLIENT_A`
* **Route Distinguisher (RD) & Route Target (RT) :** Configuration standard pour l'isolation du trafic du client.
* **Routage PE-CE :** **EIGRP AS 100** entre le routeur `SIEGE` et `SP1`, et entre `AGENCE` et `SP3`.
* **Redistribution :** Redistribution bidirectionnelle globale entre **EIGRP 100** et **BGP 65000** sur chaque routeur PE.

---

## 📂 Structure du Dépôt

```text
.
├── tp_MPLS.gns3            # Fichier de topologie GNS3
├── demo_MPLS_VPN.mp4       # Vidéo de démonstration et validation
├── README.md               # Documentation complète du lab
└── /configs                # Configurations intégrales des équipements
    ├── SIEGE.txt
    ├── SP1.txt
    ├── SP2.txt
    ├── SP3.txt
    └── AGENCE.txt

## 📈 Validation du Lab

1. **Session MP-BGP :** Vérifiée et établie (`show ip bgp vpnv4 all summary`).
2. **Table de Routage VRF :** Routes distantes correctement apprises via BGP (`show ip route vrf CLIENT_A`).
3. **Connectivité globale :** Ping réussi à **100%** depuis le LAN SIEGE (`10.10.10.1`) vers le LAN AGENCE (`192.168.1.1`).
