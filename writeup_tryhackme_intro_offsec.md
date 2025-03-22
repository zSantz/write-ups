# 🏦 Write-Up - TryHackMe: Introduction to Offensive Security (Pre-Security)

**Room:** Introduction to Offensive Security  
**Plataforma:** TryHackMe  
**Sistema:** Parrot OS (Lab Virtual)  
**Data:** 22/03/2025

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

**Diretórios encontrados:**
- `/images` → Diretório comum para arquivos estáticos.
- `/bank-transfer` → Diretório crítico, indicando possível acesso administrativo.

---

## 🔍 Etapa 2 - Vulnerabilidade no /bank-transfer

Acessando `http://fakebank.thm/bank-transfer`, encontramos uma interface de transferência bancária **sem qualquer tipo de autenticação ou controle de acesso**.

⚠️ **Falha grave de segurança:**
- Qualquer pessoa com acesso ao sistema pode realizar transferências bancárias sem login ou verificação.
- Sistema vulnerável a abuso e manipulação de dados financeiros.

---

## 💸 Etapa 3 - Realizando a Transferência

Preenchemos os campos do formulário da página `/bank-transfer`:

```
From: 123456
To: 654321
Amount: 2000
```

Transferência foi executada com sucesso, sem qualquer bloqueio.

---

## ✅ Etapa 4 - Transferência Final e Flag Capturada

Objetivo principal da missão:
```
From: 2276
To: 8881
Amount: 2000
```

Após o envio do formulário, voltamos à página da conta e encontramos:
- Saldo atualizado com os $2000 recebidos.
- A flag final: **BANK-HACKED** 💣

---

## 🧠 Conclusão

Esse lab demonstra como **falhas de lógica de negócio** podem ser devastadoras mesmo em sistemas sem falhas técnicas aparentes.

🔑 **Lição aprendida:**  
Segurança não é só sobre firewalls e criptografia — é sobre **entender os fluxos do sistema e onde ele confia demais no usuário**.

---

**Autor:** Augusto César  
**Curso:** TryHackMe - Pre-Security Track  
**Write-Up criado com apoio do GPT 🧠💻  
