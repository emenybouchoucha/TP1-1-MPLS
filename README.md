# 🌐 Lab MPLS / VPN End-to-End

Projet de mise en œuvre et de validation d'une architecture **MPLS VPN (Option A)** interconnectant deux sites clients (**SIEGE** et **AGENCE**) à travers un réseau d'opérateur (Backbone SP).

---

## 📐 Topologie & Architecture

- **Cœur de Réseau (Backbone SP) :**
  - **IGP :** OSPF (Zone 0) pour la connectivité interne entre SP1, SP2 et SP3.
  - **Commutation de labels :** MPLS LDP activé sur toutes les interfaces du cœur.
  - **Multiprotocol BGP (MP-BGP) :** Session iBGP VPNv4 établie entre les PE (**SP1** `1.1.1.1` et **SP3** `3.3.3.3`) dans l'AS 65000.

- **Accès Client (VRF & PE-CE) :**
  - **VRF :** `CLIENT_A` configurée sur SP1 et SP3.
  - **Routage PE-CE :** EIGRP AS 100.
  - **Redistribution :** Redistribution bidirectionnelle entre EIGRP 100 et BGP 65000 sur les PE.

---

## 🛠️ Contenu du Dépôt

- `/configs` : Fichiers de configuration des équipements (SIEGE, SP1, SP2, SP3, AGENCE).
- `demo_mpls_vpn.mp4` : Vidéo de démonstration et validation du lab.

---

## 📈 Validation du Lab

1. **Session MP-BGP :** Vérifiée et établie (`show ip bgp vpnv4 all summary`).
2. **Table de Routage VRF :** Routes distantes correctement apprises via BGP (`show ip route vrf CLIENT_A`).
3. **Connectivité globale :** Ping réussi à **100%** depuis le LAN SIEGE (`10.10.10.1`) vers le LAN AGENCE (`192.168.1.1`).
