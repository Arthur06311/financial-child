# FINANCIAL CHILD - PLANO BETA v1.0

---

## 1. VISAO GERAL DO PRODUTO

**Nome:** Financial Child
**Moeda virtual:** EKO
**Publico-alvo:** Criancas (7-14 anos) com supervisao dos pais
**Modelo de negocio:** Assinatura mensal - R$ 30,00/mes
**Proposta de valor:** Ensinar criancas a investir de forma ludica e segura, com controle total dos pais.

---

## 2. ARQUITETURA DO BETA

### Stack Tecnologica
| Camada       | Tecnologia                  |
|-------------|----------------------------|
| Frontend    | React + TypeScript          |
| Estilizacao | Tailwind CSS + Framer Motion|
| Backend     | Node.js + Express           |
| Banco       | PostgreSQL                  |
| Auth        | Firebase Auth               |
| Pagamento   | Stripe (assinatura mensal)  |
| Hospedagem  | Vercel (front) + Railway (back) |
| Tempo real  | WebSocket (Socket.io)       |

---

## 3. USUARIOS E PAPEIS

### 3.1 PAI/MAE (Admin Familiar)
- Cria a conta e paga a assinatura
- Configura o ambiente de investimento do filho
- Monitora desempenho e historico

### 3.2 CRIANCA (Investidor)
- Acessa o painel de trading simplificado
- Compra e vende EKO
- Acompanha metas e saldo

---

## 4. FUNCIONALIDADES DO BETA

### 4.1 PAINEL DO PAI (Dashboard Parental)

| # | Funcionalidade              | Descricao                                                      | Prioridade |
|---|----------------------------|----------------------------------------------------------------|------------|
| 1 | Criar conta do filho        | Nome, avatar, idade                                            | ALTA       |
| 2 | Definir saldo inicial       | Quanto a crianca comeca (ex: R$ 100 virtuais)                  | ALTA       |
| 3 | Definir preco base da EKO   | Preco inicial da moeda (ex: R$ 10,00)                          | ALTA       |
| 4 | Configurar volatilidade     | Baixa / Media / Alta - controla o quanto o preco oscila        | MEDIA      |
| 5 | Definir meta financeira     | Valor alvo que a crianca deve alcancar (ex: R$ 150)            | ALTA       |
| 6 | Historico de operacoes      | Ver todas as compras e vendas do filho                         | ALTA       |
| 7 | Pausar/Retomar simulacao    | Pausar o mercado quando quiser                                 | MEDIA      |
| 8 | Relatorio de desempenho     | Grafico simples mostrando evolucao do saldo                    | MEDIA      |
| 9 | Notificacoes                | Alerta quando o filho bate a meta                              | BAIXA      |

### 4.2 PAINEL DA CRIANCA (Trading Simplificado)

| # | Funcionalidade              | Descricao                                                      | Prioridade |
|---|----------------------------|----------------------------------------------------------------|------------|
| 1 | Grafico de preco da EKO     | Grafico em tempo real, atualiza a cada 60s                     | ALTA       |
| 2 | Indicador emoji             | Foguete quando sobe, paraquedas quando desce                   | ALTA       |
| 3 | Botao COMPRAR (verde)       | Grande, brilha quando preco < preco base (oportunidade)        | ALTA       |
| 4 | Botao VENDER (vermelho)     | Grande, brilha quando preco > preco base (lucro)               | ALTA       |
| 5 | Saldo atual                 | Mostra quanto a crianca tem em R$ virtuais                     | ALTA       |
| 6 | Quantidade de EKOs          | Mostra quantas moedas a crianca possui                         | ALTA       |
| 7 | Barra de progresso da meta  | Barra colorida que enche conforme se aproxima da meta          | ALTA       |
| 8 | Celebracao ao bater meta    | Animacao com confete e som ao atingir objetivo                 | MEDIA      |
| 9 | Historico simplificado      | Ultimas 10 operacoes com icones                                | MEDIA      |

### 4.3 MOTOR DE MERCADO (Backend)

| # | Funcionalidade              | Descricao                                                      | Prioridade |
|---|----------------------------|----------------------------------------------------------------|------------|
| 1 | Oscilacao automatica        | A cada 60s, preco muda com algoritmo controlado                | ALTA       |
| 2 | Algoritmo de volatilidade   | Variacao % baseada na config do pai (baixa/media/alta)         | ALTA       |
| 3 | Limites de seguranca        | Preco nunca vai abaixo de 10% do base nem acima de 300%        | ALTA       |
| 4 | Tendencias naturais         | Ciclos de alta e baixa para simular mercado real               | MEDIA      |
| 5 | WebSocket broadcast         | Envia preco atualizado para todos os clientes conectados       | ALTA       |

---

## 5. ALGORITMO DE OSCILACAO DA EKO (Simplificado)

```
A cada 60 segundos:
  1. Gerar variacao aleatoria baseada na volatilidade:
     - Baixa:  -2% a +2%
     - Media:  -5% a +5%
     - Alta:   -10% a +10%

  2. Aplicar tendencia (ciclos de ~5-10 min):
     - 60% do tempo: tendencia leve de alta
     - 40% do tempo: tendencia leve de baixa

  3. Aplicar limites:
     - Minimo: preco_base * 0.10
     - Maximo: preco_base * 3.00

  4. Novo preco = preco_atual + (preco_atual * variacao)
  5. Broadcast via WebSocket para todos os clientes
```

---

## 6. FLUXO DO USUARIO

### 6.1 Fluxo do Pai
```
Cadastro -> Pagamento (Stripe) -> Criar perfil do filho
   -> Definir: saldo inicial + preco base EKO + meta
   -> Dashboard: acompanhar operacoes e desempenho
```

### 6.2 Fluxo da Crianca
```
Login (com credencial criada pelo pai) -> Painel de Trading
   -> Ver grafico da EKO (atualiza a cada 60s)
   -> Decidir: COMPRAR ou VENDER
   -> Acompanhar saldo e barra de progresso
   -> Bater meta -> Celebracao!
```

---

## 7. WIREFRAMES CONCEITUAIS

### 7.1 Tela da Crianca (Mobile-first)
```
+------------------------------------------+
|  FINANCIAL CHILD          Saldo: R$120   |
+------------------------------------------+
|                                          |
|         PRECO DA EKO: R$ 12,50           |
|              (subindo)                   |
|                                          |
|     [========= GRAFICO =========]        |
|     |        /\    /\                    |
|     |   /\  /  \  /  \  /               |
|     |  /  \/    \/    \/                 |
|     +----------------------------        |
|                                          |
|  Voce tem: 5 EKOs  |  Valor: R$ 62,50   |
|                                          |
|  +----------------+  +----------------+  |
|  |                |  |                |  |
|  |    COMPRAR     |  |    VENDER      |  |
|  |                |  |                |  |
|  +----------------+  +----------------+  |
|                                          |
|  META: R$ 150                            |
|  [============------] 80%               |
|                                          |
+------------------------------------------+
```

### 7.2 Painel do Pai (Desktop)
```
+----------------------------------------------------------+
|  FINANCIAL CHILD - Painel dos Pais                       |
+----------------------------------------------------------+
|                                                          |
|  Filho: Arthur Jr.        Status: Online                 |
|                                                          |
|  +-- Configuracoes ----+  +-- Desempenho -------------+  |
|  | Saldo inicial: R$100|  | Saldo atual:    R$ 120    |  |
|  | Preco base:   R$ 10 |  | Lucro total:    R$ 20     |  |
|  | Volatilidade: Media  |  | Operacoes:      15        |  |
|  | Meta:        R$ 150  |  | Taxa acerto:    73%       |  |
|  +---------------------+  +---------------------------+  |
|                                                          |
|  +-- Historico de Operacoes -----------------------------+|
|  | 14:30  COMPROU 2 EKOs a R$ 8,50   Total: R$ 17,00   ||
|  | 14:25  VENDEU  3 EKOs a R$ 12,00  Total: R$ 36,00   ||
|  | 14:18  COMPROU 3 EKOs a R$ 7,80   Total: R$ 23,40   ||
|  +------------------------------------------------------+|
+----------------------------------------------------------+
```

---

## 8. ESTRUTURA DO BANCO DE DADOS

### Tabelas Principais

```sql
-- Pais (usuarios pagantes)
parents
  id, email, password_hash, name, phone,
  stripe_customer_id, subscription_status,
  created_at, updated_at

-- Filhos (investidores)
children
  id, parent_id, name, avatar, age,
  balance, eko_quantity,
  created_at, updated_at

-- Configuracao do mercado (por filho)
market_config
  id, child_id, base_price, volatility,
  goal_amount, is_active,
  created_at, updated_at

-- Historico de precos
price_history
  id, child_id, price, timestamp

-- Transacoes (compra/venda)
transactions
  id, child_id, type (BUY/SELL),
  quantity, price_at_time, total_value,
  created_at
```

---

## 9. REGRAS DE NEGOCIO DO BETA

| #  | Regra                                                              |
|----|-------------------------------------------------------------------|
| 1  | Crianca so pode comprar se tiver saldo suficiente                 |
| 2  | Crianca so pode vender se tiver EKOs suficientes                  |
| 3  | Cada operacao compra/vende 1 EKO por vez (simplificado no beta)   |
| 4  | Preco atualiza a cada 60 segundos automaticamente                 |
| 5  | Pai pode pausar o mercado a qualquer momento                      |
| 6  | Quando a meta e atingida, animacao de celebracao e disparada       |
| 7  | Pai pode resetar o jogo do filho (novo saldo, nova meta)          |
| 8  | Limite de 1 filho por assinatura no beta (expansivel depois)      |
| 9  | Sessao da crianca expira apos 2h de inatividade                   |
| 10 | Todos os valores sao virtuais - nenhum dinheiro real e transacionado |

---

## 10. INDICADORES VISUAIS (UX INFANTIL)

| Situacao                        | Indicador Visual                         |
|--------------------------------|------------------------------------------|
| Preco subindo                  | Foguete ao lado do valor                 |
| Preco caindo                   | Paraquedas ao lado do valor              |
| Preco abaixo do base (comprar) | Botao verde BRILHA + pulsa               |
| Preco acima do base (vender)   | Botao vermelho BRILHA + pulsa            |
| Preco estavel                  | Indicador neutro (sem emoji especial)    |
| Meta quase atingida (>90%)     | Barra de progresso pisca dourado         |
| Meta atingida                  | Explosao de confete + som de vitoria     |
| Prejuizo (saldo < inicial)     | Nenhum alerta negativo (nao assustar)    |

---

## 11. CRONOGRAMA DO BETA (8 SEMANAS)

| Semana | Entrega                                                |
|--------|-------------------------------------------------------|
| 1      | Setup do projeto + Auth (Firebase) + DB                |
| 2      | Painel do Pai: CRUD filho + configuracoes              |
| 3      | Motor de mercado + algoritmo de oscilacao + WebSocket   |
| 4      | Painel da Crianca: grafico + botoes comprar/vender      |
| 5      | Barra de progresso + celebracoes + indicadores emoji    |
| 6      | Integracao Stripe (assinatura) + fluxo de pagamento     |
| 7      | Testes + ajustes de UX + responsividade mobile          |
| 8      | Deploy + testes com usuarios reais + correcoes finais   |

---

## 12. METRICAS DE SUCESSO DO BETA

| Metrica                          | Meta do Beta           |
|---------------------------------|------------------------|
| Usuarios cadastrados             | 50 familias            |
| Retencao semanal                 | > 60%                  |
| Tempo medio de sessao (crianca)  | > 10 minutos           |
| Metas batidas por crianca/semana | > 2                    |
| NPS dos pais                     | > 8                    |
| Churn mensal                     | < 15%                  |

---

## 13. PROXIMOS PASSOS POS-BETA

- [ ] Multiplos filhos por conta
- [ ] Ranking entre irmaos/amigos
- [ ] Mais moedas virtuais (alem da EKO)
- [ ] Modo "Eventos de mercado" (simular noticias que afetam preco)
- [ ] Recompensas reais (pais definem premios ao bater metas)
- [ ] App nativo (React Native)
- [ ] Modo educacional com licoes sobre investimento
- [ ] Integracao com mesada digital

---

*Documento gerado em 21/02/2026 - Financial Child Beta v1.0*
