# Diagnóstico e Testes – Aladdin eToken 64k no Windows 11

Este documento descreve os testes a serem realizados para diagnosticar problemas de reconhecimento intermitente do dispositivo **Aladdin eToken 64k** no **Windows 11**, que apresenta comportamento **aleatório ao ser inserido/removido**.

---

## 🛑 Descrição do Erro

No Windows 11, o token **Aladdin eToken 64k** nem sempre é reconhecido após ser inserido na porta USB. Esse comportamento foi identificado ao fazer o uso de drivers mais recentes.  
O problema é **intermitente**, podendo comprometer operações de autenticação, assinatura digital e gerenciamento de certificados.

---

## 🔍 Possíveis Causas (Verificar)

### 1. Problema físico no token ou porta USB ❌

- O token pode estar desgastado devido à idade.
- Testar em diferentes portas USB; se o problema persistir em todas, o token pode estar danificado.

#### | Foi feito o teste com mais de um token, todos lacrados, descartando a possibilidade de problemas físicos.|

---

### 2. Drivers/middleware desatualizados ou corrompidos

- O **SafeNet Authentication Client (SAC)** gerencia a comunicação com o token.
- Versões antigas podem ser instáveis no **Windows 11**.
- Reinstalar ou atualizar para a versão mais recente do SAC.

#### | O erro é apresentado somente em versões mais recentes como 9.0 em diante, e também foram feitos testes removendo o driver e também os arquivso de registros | É preciso fazer análises mais detalhadas em relação ao comportamento do driver no sistes ao remover e inserir o token.

---

### 3. Conflitos com o serviço Smart Card

- Serviço `Smart Card (SCardSvr)` pode travar após várias inserções/remoções.
- Reiniciar o serviço pode resolver temporariamente:

```powershell
sc stop SCardSvr && sc start SCardSvr
```

---

### 4. Gerenciamento de energia do USB

- Windows 11 pode desligar automaticamente a porta USB para economizar energia.
- Isso pode causar falha na detecção do token.
- Desativar a **USB selective suspend** nas opções de energia.

---

## 📌 Conclusão
