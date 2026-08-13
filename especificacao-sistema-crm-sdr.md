# Especificação do Sistema — CRM Comercial SDR

**Instituto Gourmet Santo André**

Especificação funcional do sistema que substitui a planilha manual atual. Reúne tudo o que foi definido sobre identificação de registros, automações, papéis por etapa, painéis de acompanhamento e regras de auditoria. Este documento é a referência para desenhar a próxima versão da planilha/sistema — não descreve como falar com o lead (isso está em `script-padrao-agendamento-sdr.md` e `script-oficial-pos-agendamento-sdr.md`), descreve como o processo deve ser registrado e medido.

## 1. Identificação por ID

Todo lead recebe um **ID único e permanente**. O ID nunca muda, mesmo que nome, telefone, responsável ou status sejam alterados.

**Formato:** `LD-AAMMDD-NNNN`
**Exemplo:** `LD-260813-0001` (lead criado em 13/08/2026, sequência 0001 do dia).

Apenas o **Lead** tem ID próprio. Agendamento, confirmação, comparecimento e resultado não são entidades separadas — são atualizações e eventos registrados sobre o mesmo Lead ID.

## 2. Origem do lead

- **Lead Novo** — vem da planilha de Marketing. Gabriela recebe essa base e distribui os contatos entre as SDRs.
- **Repique — Discador** — contato que retorna através do discador. Usa exatamente o mesmo pipeline do lead novo (tentativas, histórico, agendamento, confirmação, comparecimento, atendimento, resultado), mas fica marcado com `Origem: Repique — Discador` para permitir comparação futura no painel: **Lead Novo x Repique** (contatos realizados, agendamentos, comparecimentos, matrículas, conversão).

## 3. Tentativa de contato

### 3.1 Quem pode registrar uma tentativa

Tentativa de contato **não é ação exclusiva do SDR** — qualquer pessoa autorizada pode executar uma tentativa (ex: uma ligação de apoio feita pela Gabriela).

Regras:

- O sistema registra **automaticamente** quem executou a tentativa, data e horário. Não existe campo manual para escolher ou digitar o responsável depois.
- A tentativa fica vinculada ao mesmo Lead ID e entra no histórico cronológico.
- Se houver várias tentativas feitas por pessoas diferentes no mesmo dia, **todas permanecem registradas individualmente** — nenhuma sobrescreve a outra.
- **Quem executou uma tentativa não é necessariamente o "responsável atual" do lead.** Exemplo: Lead responsável = Sarah; tentativa feita por = Gabriela; a próxima ação continua sendo da Sarah, salvo mudança formal de responsabilidade. Isso evita que uma ligação de apoio altere a propriedade do lead sem intenção.

### 3.2 Resultado da tentativa de contato

Lista inicial de resultados disponíveis:

- Contato realizado
- Não atendeu
- Sem resposta no WhatsApp
- Pediu retorno
- Número inválido
- Sem interesse
- Agendado

Cada tentativa sempre registra: **responsável (automático) + data + horário + canal (ligação, WhatsApp etc.) + resultado.**

### 3.3 Contadores automáticos

O sistema calcula sozinho — o SDR **nunca preenche manualmente**:

- tentativas do dia;
- tentativas totais;
- última tentativa;
- último resultado;
- próxima ação.

### 3.4 Ciclo de 7 dias

Várias tentativas válidas feitas no mesmo dia contam como **apenas um dia de operação trabalhado** dentro do ciclo de 7 dias de cadência.

## 4. Agendamento

Quando o SDR consegue um agendamento, registra:

- Lead (via Lead ID);
- data da visita;
- horário da visita;
- SDR responsável;
- observação, quando necessária.

O sistema grava automaticamente a **data/hora real em que o agendamento foi criado** — esse é o dado usado para medir produtividade, não o horário da visita (ver seção 7).

Após salvar, **Gabriela recebe uma notificação automática**.

## 5. Contato pós-agendamento (Gabriela)

Ao receber a notificação, Gabriela entra em contato com o cliente para:

- parabenizar pelo agendamento;
- validar a visita;
- disponibilizar o **QR Code oficial** (é o "código de acesso" citado nos scripts de atendimento).

Gabriela registra o resultado em formato de log, ex:

> 13/08/2026 · 11:58 — Gabriela Duarte — Contato pós-agendamento realizado — QR Code disponibilizado

## 6. Confirmação da visita (Gabriela)

**Gabriela é responsável pelas confirmações nesta primeira versão** — não o SDR.

O sistema cria lembretes/ações automáticas:

- **Confirmação D-1** — um dia antes da visita.
- **Confirmação 2 horas antes** — duas horas antes do horário marcado.

Essas ações aparecem no "Meu Dia" de Gabriela.

### Resultados da confirmação

- Confirmado;
- Sem resposta;
- Cancelou;
- Solicitou reagendamento;
- Outro.

Cada contato de confirmação é um **registro individual** — nunca apaga a confirmação anterior. O histórico completo de tentativas de confirmação fica visível, não só o último status.

## 7. Como contar o agendamento

**O agendamento pertence à hora em que foi criado — nunca ao horário da visita.**

Exemplo: agendamento criado às 10h42, visita marcada para o dia seguinte às 15h → conta em **"Produção 10h–11h"** do dia em que foi criado, não em "14h–15h" do dia da visita.

Registro no histórico:

> 13/08/2026 · 10:42 — Giovanna criou agendamento — Visita marcada para 14/08/2026 · 14:00

Essa regra existe para que o indicador de produtividade não possa ser manipulado ou confundido.

## 8. Agenda do dia

Área central do sistema. Visualização simples com:

- horário;
- Lead ID;
- cliente;
- telefone;
- SDR responsável;
- status de confirmação;
- próxima ação;
- status de comparecimento;
- responsável pelo atendimento;
- resultado atual.

## 9. Atendimento presencial

Depois que o cliente comparece, entra na etapa presencial. Usuários com acesso atualizam conforme suas permissões.

**Status iniciais:**

- Aguardando atendimento;
- Em atendimento;
- Atendimento realizado;
- Não atendido.

Se o cliente **não for atendido, o motivo é obrigatório** — para diferenciar "não fechou" (foi atendido e a venda não avançou) de "compareceu, mas não foi atendido" (falha operacional da mesa, não do cliente).

### Caso registrado — 13/08/2026

Três clientes agendados pela SDR **Sara** compareceram à unidade e não foram atendidos porque a Seller escalada para o dia faltou, sem substituição definida — porque, até esta data, ainda não existe uma escala oficial de cobertura (ver `matriz-responsabilidade-comercial-sdr.md`, item 6).

**Registro correto deste caso:** Atendimento não realizado — motivo: *falta da Seller escalada, sem substituição definida*. SDR responsável pelo agendamento: Sara. Falha: operacional/cobertura, não comercial e não da SDR.

Este caso é a evidência concreta de por que:

- o motivo obrigatório em "Não atendido" existe — sem ele, essa falha de cobertura teria virado, aos olhos de quem só olha o número, uma falha da Sara;
- a escala de Recepção e de atendimento presencial precisa ser fechada com urgência, não é só um item pendente de formulário;
- a responsabilidade não recai sobre a SDR que gerou o agendamento — ela cumpriu a parte dela.

## 10. Painéis

### 10.1 Painel de conversões mensais

Funil completo, com taxa calculada automaticamente entre cada etapa:

```
Leads cadastrados
  ↓
Leads trabalhados
  ↓
Contatos realizados
  ↓
Agendamentos
  ↓
Confirmados
  ↓
Comparecimentos
  ↓
Atendimentos realizados
  ↓
Matrículas
```

### 10.2 Produção hora a hora

A ADM (Gabriela) define a meta operacional — ex: **2 agendamentos por hora por SDR**. O sistema calcula automaticamente (não é a SDR que informa "fiz 2" — o sistema conta porque existem registros reais naquele intervalo):

| Horário | SDR 1 | SDR 2 | SDR 3 | Time |
|---|---:|---:|---:|---:|
| 09h–10h | 2 | 1 | 2 | 5 |
| 10h–11h | 1 | 2 | 0 | 3 |
| 11h–12h | 2 | 2 | 1 | 5 |

**"Meu Dia" de cada SDR** mostra o próprio ritmo, sem pressão externa:

```
Hoje — Meta: 2 agendamentos/hora
09h–10h — 2/2 concluído
10h–11h — 1/2
11h–12h — em andamento

Agendamentos hoje: 7
Meta até agora: 8
Diferença: -1
```

**Tela da administradora (Gabriela)** mostra o time inteiro:

```
Produção hoje — 13/08
SDR 1 — 7 agendamentos
SDR 2 — 6
SDR 3 — 5
Total do time: 18
```

Com: produção por hora; produção acumulada; meta acumulada até aquele horário; quem está no ritmo; quem está abaixo; horas sem agendamento; quantidade total do dia.

**Alerta interno** (visível só para Gabriela, nunca vira cobrança automática repetida para a SDR):

```
Acompanhamento necessário
[SDR] registrou 1 de 2 agendamentos entre 10h e 11h.
```

Para a SDR aparece o progresso. Para Gabriela aparece o desvio. A decisão de como agir é da liderança, não do sistema.

### 10.3 Metas configuráveis (nunca fixas)

Configuráveis por Gabriela (ADM), sem depender de alteração no sistema:

- Meta de agendamento por hora;
- Meta diária por SDR (pode variar por pessoa/jornada);
- Meta mensal.

### 10.4 Dois acompanhamentos separados

- **Produção do SDR** — contato → agendamento, medido hora a hora.
- **Qualidade da agenda** — agendamento → comparecimento, medido posteriormente.

Uma pessoa pode produzir 16 agendamentos e trazer 3 comparecimentos, enquanto outra produz 12 e traz 7 — volume e qualidade não podem se misturar num único número.

### 10.5 Ranking de agendamentos

Ranking entre SDRs por volume de agendamentos.

## 11. Responsável por etapa (RACI)

Cada etapa tem um responsável próprio. **Não atribuir toda a jornada ao SDR só porque ele criou o agendamento.**

| Etapa | Responsável |
|---|---|
| Distribuição | Gabriela |
| Tentativas | Qualquer pessoa autorizada (normalmente o SDR) |
| Agendamento | SDR |
| Contato pós-agendamento | Gabriela |
| Confirmações (D-1 e 2h antes) | Gabriela |
| Comparecimento | Recepção |
| Atendimento | Pessoa autorizada |
| Resultado | Coordenadora/Seller que realizou o atendimento |

> Esta tabela substitui o exemplo simplificado que constava em `matriz-responsabilidade-comercial-sdr.md` ("Por que isso simplifica a planilha") — aquela versão foi corrigida para refletir esta.

## 12. Trilha de auditoria

**Nenhuma alteração operacional relevante pode existir sem responsável, data e horário.** Isso inclui:

- criação do lead;
- distribuição;
- mudança de responsável;
- tentativa de contato;
- resultado da ligação;
- agendamento;
- alteração de data/hora da visita;
- confirmação;
- envio de QR Code;
- cancelamento;
- reagendamento;
- comparecimento;
- não comparecimento;
- atendimento;
- resultado comercial;
- matrícula;
- observação relevante.

Se alguém corrigir um dado já preenchido, o sistema registra **quem alterou** (usuário automático) e **quando** — não é necessário guardar valor anterior/novo em formato de log descritivo separado; basta o registro do usuário e do horário da alteração.

## 13. Papéis do sistema

- **ADM** — Gabriela Duarte. Define metas (hora, dia, mês) e enxerga todos os painéis. Também cadastra/edita quem ocupa cada papel (ver abaixo).
- **SDR** — cria agendamentos e tentativas; enxerga apenas o próprio "Meu Dia".
- **Gabriela (liderança SDR)** — recebe leads do marketing, distribui, faz contato pós-agendamento, confirmações D-1 e 2h antes, acompanha produção do time.
- **Recepção** — confirma comparecimento físico do cliente na unidade. **Sem responsável definido ainda** — este é um cadastro livre: a ADM cadastra o(s) nome(s) diretamente no sistema quando definir quem exerce a função, sem precisar de alteração em documento ou script.
- **Seller/Coordenadora** — realiza o atendimento presencial e registra o resultado comercial (ver `equipe-atual.md` para quem ocupa a função hoje: Carla e Nadja).

Em geral: nenhum papel deste sistema deve ter nomes fixos em código ou em regra de negócio. A lista de pessoas por papel é sempre um cadastro editável pela ADM — `equipe-atual.md` é o retrato atual desse cadastro, não uma lista fixa.
