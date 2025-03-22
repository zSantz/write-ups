# 🏦 Write-Up - TryHackMe: Introduction to Offensive Security (Pre-Security)

**Room:** Introduction to Offensive Security
**Link:**  https://tryhackme.com/room/offensivesecurityintro
**Plataforma:** TryHackMe  
**Sistema:** Parrot OS (Lab Virtual)  
**Data:** 22/03/2025
**Player:** https://tryhackme.com/p/Elninosantz

---

## 🎯 Objetivo do Lab

O objetivo do lab é simular uma situação comum no mundo real: encontrar diretórios ocultos expostos publicamente e explorar falhas de segurança lógicas que podem permitir o acesso indevido a sistemas administrativos.

A missão principal: **Transferir $2000 da conta 2276 para a conta 8881**, explorando uma falha no sistema bancário.

---

## 📡 Etapa 1 - Reconhecimento com Gobuster

Primeiro passo foi a enumeração de diretórios usando o `gobuster`:

```bash
gobuster dir -u http://fakebank.thm -w wordlist.txt
```

image

**Diretórios encontrados:**
- `/images` → Diretório comum para arquivos estáticos.
- `/bank-transfer` → Diretório crítico, indicando possível acesso administrativo.

Acessando `http://fakebank.thm/bank-transfer`, foi encontrado uma interface de transferência bancária **sem qualquer tipo de autenticação ou controle de acesso**.

image

---


## 💸 Etapa 2 - Realizando a Transferência

Preenchi os campos do formulário da página `/bank-transfer` de acordo com o requerimento da Room:

```
From: 2276
To: 8881
Amount: 2000
```
Transferência foi executada com sucesso, sem qualquer bloqueio. Após a confirmação da transferência, voltei à página da conta e encontramos:

- Saldo atualizado com os $2000 recebidos.
- A flag final: **BANK-HACKED** 💣

image
