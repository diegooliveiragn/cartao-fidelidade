[README.md](https://github.com/user-attachments/files/25508989/README.md)
# 🫓 EmpaDinhas — Sistema de Gestão e Fidelidade

> Plataforma digital completa para gestão de clientes, estoque, financeiro e marketing de uma marca artesanal de empadas. Desenvolvido para operar 100% no navegador, sem necessidade de servidor próprio.

---

## 📱 Telas do Sistema

### `cliente.html` — App do Cliente
Interface voltada para o cliente final, acessível pelo celular.

- **Cardápio do dia** — visualiza empadas disponíveis, preços e combos em tempo real
- **Pedido via WhatsApp** — seleciona itens e envia pedido formatado direto para a Dinha
- **Cartão Fidelidade Digital** — acompanha selos acumulados (a cada 10, ganha 1 grátis)
- **Cadastro com bloqueio de duplicidade** — por telefone e e-mail
- **Mensagem da próxima fornada** — banner dinâmico atualizado pelo admin

### `admin.html` — Painel Administrativo
Interface de gestão, protegida por senha, para uso interno.

| Aba | Funcionalidade |
|-----|---------------|
| 📊 Dashboard | KPIs, top compradores, mapa de bairros, gráficos de engajamento |
| 👥 Clientes | Lista completa com busca, filtro por bairro e carimbo de selos |
| 🔔 Alertas | Aniversariantes, inativos e entregas pendentes |
| 📅 Calendário | Feriados nacionais, datas de CE/Fortaleza e insights de marketing por data |
| 📦 Estoque | Cadastro de sabores, controle de quantidade e combos por fornada |
| 💰 Financeiro | Entradas, saídas, lucro em tempo real e gráfico mensal |
| 📲 Disparos | CRM com segmentação de clientes e disparo via WhatsApp |

---

## 🔧 Configuração

### 1. Firebase Realtime Database

O projeto usa o Firebase como banco de dados em tempo real. As credenciais já estão embutidas nos arquivos HTML.

**Estrutura do banco:**

```
empadinhas-fidelidade (raiz)
├── clients/
│   └── {id}/
│       ├── name, phone, email, gender, birthdate
│       ├── city, neighborhood, street
│       ├── source, flavor, qty
│       ├── stamps, totalRedeemed, pendingDelivery
│       └── createdAt, lastStampAt
├── menu/
│   ├── sabores/
│   │   └── {id}/ → name, emoji, price, qty
│   └── combos/
│       └── {id}/ → name, emoji, desc, price
├── financeiro/
│   ├── entradas/
│   │   └── {id}/ → desc, valor, date, cat
│   └── saidas/
│       └── {id}/ → desc, valor, date, cat
└── settings/
    ├── whatsappDinha   → número do WhatsApp (ex: "5585912345678")
    └── fornadaMsg      → mensagem da próxima fornada para os clientes
```

### 2. Número do WhatsApp

Adicione o número da Dinha diretamente no Firebase:

```
settings/
  whatsappDinha: "5585912345678"
```

> **Formato:** código do país (55) + DDD + número, sem espaços ou símbolos.

Alternativamente, edite a constante no `cliente.html`:
```js
const DINHA_WHATSAPP = '5585912345678'; // ← substituir pelo número real
```

### 3. Senha do Admin

A senha de acesso ao painel está definida no `admin.html`:
```js
const ADMIN_PASS = "empadinhas2025";
```
Altere para uma senha de sua preferência antes de publicar.

### 4. Regras do Firebase

As regras atuais permitem leitura e escrita pública. Para produção, considere restringir:

```json
{
  "rules": {
    "clients": {
      ".read": true,
      ".write": true
    },
    "menu": {
      ".read": true,
      ".write": true
    },
    "financeiro": {
      ".read": false,
      ".write": false
    },
    "settings": {
      ".read": true,
      ".write": true
    }
  }
}
```

---

## 🚀 Deploy

O projeto é hospedado no **Netlify** com deploy automático via GitHub.

**Fluxo:**
```
Editar arquivos → Commit no GitHub → Netlify publica automaticamente
```

**Links em produção:**
- Cliente: `https://fidelidade-empadinhas.netlify.app/cliente.html`
- Admin: `https://fidelidade-empadinhas.netlify.app/admin.html`

---

## 📦 Tecnologias

| Tecnologia | Uso |
|-----------|-----|
| HTML / CSS / JS puro | Interface completa sem frameworks |
| Firebase Realtime Database | Banco de dados em tempo real |
| Chart.js | Gráficos do dashboard e financeiro |
| WhatsApp API (wa.me) | Disparo de mensagens e pedidos |
| Netlify | Hospedagem e deploy contínuo |
| GitHub | Controle de versão |

---

## 📲 Funcionalidades detalhadas

### Cartão Fidelidade
- A cada 10 empadas compradas (carimbos), o cliente ganha a 11ª grátis
- Carimbos são adicionados manualmente pelo admin
- Quando completa, o card muda de estado e aguarda confirmação de entrega
- Após entrega confirmada, o cartão é zerado e novo ciclo começa

### Calendário de Datas
- Feriados nacionais brasileiros
- Feriados estaduais do Ceará e municipais de Fortaleza
- Datas comemorativas relevantes para o negócio
- Pop-up de insight ao clicar em cada data com sugestão de produto e copy de marketing

### Sistema de Disparos (CRM)
- Segmentação por: toda a base, inativos, ativos, aniversariantes, próximos do grátis, bairro
- 5 templates de mensagem prontos (fornada, saudade, aniversário, fidelidade, promoção)
- Personalização automática com `{nome}` do cliente
- Disparo individual ou em massa via WhatsApp

### Controle de Estoque
- Cadastro de sabores com emoji, preço e quantidade
- Badges visuais: OK / POUCO / ESGOTADO
- Ajuste rápido de quantidade com botões + e −
- Combos personalizados com descrição e preço
- Tudo reflete em tempo real na tela do cliente

### Financeiro
- Registro de entradas (vendas) e saídas (ingredientes, embalagens, outros)
- KPIs em tempo real: receita, custo e lucro com margem percentual
- Filtro por período: semana, mês ou tudo
- Gráfico de barras: receita vs custos dos últimos 6 meses

---

## 👤 Sobre o Projeto

Desenvolvido para a **EmpaDinhas**, marca artesanal de empadas de Fortaleza-CE. O sistema nasceu como um cartão fidelidade digital e evoluiu para uma plataforma completa de gestão para microempresas do setor alimentício.

---

*Feito com 💜 e muito 🫓*
