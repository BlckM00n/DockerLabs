
# DockerLabs - Trust Walkthrough

[![DockerLabs](https://img.shields.io/badge/DockerLabs-Trust-blue)](https://dockerlabs.es)
[![Difficulty](https://img.shields.io/badge/Difficulty-Fácil-green)]()
[![Techniques](https://img.shields.io/badge/Techniques-SSH%20Bruteforce%20%7C%20Sudo%20Abuse-red)]()

---

# 📌 Descripción

Máquina de dificultad **Fácil** donde explotamos un archivo PHP oculto, realizamos fuerza bruta al servicio SSH y abusamos de permisos sudo sobre el binario `vim` para escalar privilegios a root.

---

# 📡 Reconocimiento

## Escaneo de puertos

nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn <IP> -oG allPorts

![Nmap](Trust_nmap.png)

---

## Enumeración web

### Fuzzing con Gobuster

gobuster dir -u http://<IP> -w <WORDLIST> -x php,html,txt -t 20

![Gobuster](Gobuster_trust.png)

---

## Análisis con curl

curl http://<IP>

![Curl](Curl_trust.png)

---

# 🔐 Ataque SSH

hydra -l mario -P <WORDLIST> ssh://<IP> -t 4

![Hydra](Hydra_trust.png)

---

## Acceso SSH

ssh mario@<IP>

![SSH](Ssh_trust.png)

---

# 🧗 Escalada de privilegios

## Enumeración sudo

sudo -l

📸 Captura: [AQUI_SUDO]

---

## Escalada a root

whoami  
id  

![Root](Root_trust.png)

---

# 📋 Resumen

| Paso | Herramienta | Resultado |
|---|---|---|
| Nmap | Escaneo | Puertos 22/80 |
| Gobuster | Fuzzing web | Descubrimiento |
| Curl | Enumeración | Usuario |
| Hydra | Brute force | Credenciales |
| SSH | Acceso | mario |
| sudo -l | Priv esc | vim permitido |
| Vim | Root | acceso total |

---

# 🧠 Notas

- Enumerar siempre antes de explotar
- Revisar web primero
- Validar wordlists
- Revisar sudo antes de escalar
