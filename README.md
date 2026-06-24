# 🔐 Lab 03 — GRE sobre IPSec + IKEv1

**Estudiante:** Enmanuel Feliz Soto | **Matrícula:** 2025-1402  
**Institución:** Instituto Tecnológico de Las Américas (ITLA)  
**Curso:** Seguridad en Redes | **Sección:** 5 - Lunes  
**Docente:** Jonathan Esteban Rondón Corniel

---

## 📋 Descripción

Combina la flexibilidad de GRE (multiprotocolo, multicast) con la seguridad de IPSec. El túnel GRE es protegido mediante IPSec profile.

| Campo | Valor |
|-------|-------|
| **Tipo de VPN** | Site-to-Site |
| **Protocolo** | IKEv1 + IPSec ESP-AES256-SHA256 + GRE |
| **Mecanismo** | Túnel GRE encapsulado en IPSec (tunnel protection) |
| **Routing** | Rutas estáticas sobre Tunnel0 GRE |
| **Pre-shared Key** | `Cisco2025-1402-GRE!` |

---

## 🗺️ Topología

> 📸 <img width="1191" height="647" alt="Captura de pantalla 2026-06-24 120545" src="https://github.com/user-attachments/assets/ff86a133-aefb-41d7-bdd0-2c092fba26e2" />


<!-- Coloca aquí el screenshot de PNetLab con la topología del Lab 03 -->

**Entorno:** PNetLab — Cisco IOL  
**Peers:** R1-S1 (20.25.3.2) ↔ R4-S2 (20.25.3.6)

### Tabla de Direccionamiento

| Router | Rol | IP WAN | Interfaz WAN | IP LAN | Interfaz LAN |
|--------|-----|--------|--------------|--------|--------------|
| ISP | ENLACE / INTERMEDIARIO | 20.25.1.2 | Ethernet0/0 | -- | -- |
| R3 | Peer 1 / INICIADOR | 20.25.2.6 | Ethernet0/0 | 30.30.30.1/24 | Ethernet0/1 |

### ISP

| **Interfaz ISP** | **IP** | **Descripción** | | **Rol** |
|-------------|-----|-------------|-------------|---------|
| Ethernet0/0 | 20.25.1.1/30 | Link to R1-S1 | | **RESPONDEDOR** |

### Dirección Túnel
| Endpoint | IP Tunnel |
|----------|-----------|
| R3 Tunnel0 | 14.2.10.1/30 |
| ISP Tunnel0 | 14.2.10.2/30 |

---

## ⚙️ Configuración

El script completo de configuración se encuentra en:  
📄 [`EnmanuelFelizSoto_2025-1402_GRE_sobre_IPSec_IKEv1_P3.txt`](./EnmanuelFelizSoto_2025-1402_GRE_sobre_IPSec_IKEv1_P3.txt)

### Parámetros IKE/IPSec

| Parámetro | Valor |
|-----------|-------|
| Encryption | AES-256 |
| Hash/Integrity | SHA-256 |
| DH Group | 14 (2048-bit) |
| SA Lifetime (IKE) | 86400 s (24h) |
| SA Lifetime (IPSec) | 3600 s (1h) |
| PFS | Group 14 |
| Auth Method | Pre-Shared Key |

---

## ▶️ Procedimiento de Ejecución

### 1. Cargar configuración en PNetLab
```
# Aplicar configuración en cada dispositivo en el orden:
# 1. ISP → 2. R1-S1 → 3. R4-S2 → 4. R2/Server
```

### 2. Verificar la VPN

```
show crypto ipsec sa
```
```
show interface Tunnel0
```
```
show ip interface brief
```

### 3. Prueba de conectividad
```
ping 14.2.10.1 source 14.2.10.2 o 30.30.30.10
```

---

## 📸 Capturas de Verificación

> 📸 <img width="624" height="84" alt="image" src="https://github.com/user-attachments/assets/0cc70112-fbfe-4774-b77d-029fc1ceb154" />

<!-- Captura mostrando el estado QM_IDLE / ESTABLISHED -->

> 📸 <img width="562" height="335" alt="image" src="https://github.com/user-attachments/assets/fa22c4f8-2167-4648-93ba-946fb06a2a82" />


<!-- Captura mostrando pkts encaps/decaps incrementando -->

> 📸 <img width="633" height="452" alt="image" src="https://github.com/user-attachments/assets/1f0483a3-a557-4648-93e1-edf82b90afa9" />


<!-- Captura del ping source 30.30.30.10 -->

---

## 🔍 Análisis y Comparativa

### Ventajas de este tipo de VPN
- Ver documentación técnica en el informe PDF

### Diferencias con otros labs
- Ver tabla comparativa en el README principal

---

## 📎 Recursos

| Recurso | Enlace |
|---------|--------|
| Repositorio Principal | [Enmafs/NetSec](https://github.com/Enmafs/NetSec) |
| Script de configuración | [`EnmanuelFelizSoto_2025-1402_GRE_sobre_IPSec_IKEv1_P3.txt`](./EnmanuelFelizSoto_2025-1402_GRE_sobre_IPSec_IKEv1_P3.txt) |
| Video demostración | 🎬 [Aquí](https://youtu.be/VRtaDZReCvE) |

---

> ⚠️ *Laboratorio realizado en entorno controlado (PNetLab). Fines exclusivamente académicos.*
