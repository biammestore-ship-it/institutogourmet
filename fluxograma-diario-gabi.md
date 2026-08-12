# Fluxograma Diário da Gabi — Gestão Comercial

```mermaid
flowchart TD
    A["Gabi inicia o dia"] --> B["Verificar todos os agendamentos<br/>e visitas marcadas para o dia"]

    B --> C["Confirmar as visitas<br/>antes das demais atividades"]

    C --> D{"A pessoa confirmou<br/>a visita?"}

    D -->|Sim| E["Registrar na planilha:<br/>VISITA CONFIRMADA"]

    D -->|Não respondeu| F["Registrar na planilha:<br/>AGUARDANDO CONFIRMAÇÃO"]
    F --> G["Realizar nova tentativa<br/>de confirmação"]

    D -->|Cancelou| H["Informar que o projeto<br/>se encerra hoje"]
    H --> I["Dizer que encaminhará o caso<br/>à equipe do projeto para verificar<br/>uma possível remarcação"]
    I --> J["Registrar na planilha:<br/>CANCELAMENTO E SOLICITAÇÃO<br/>DE REAGENDAMENTO"]

    E --> K["Finalizar a atualização<br/>dos agendamentos do dia"]
    G --> K
    J --> K

    K --> L["Reunir todos os leads novos"]
    L --> M["Encaminhar os leads novos<br/>para a planilha de acompanhamento"]
    M --> N["Distribuir os leads novos<br/>entre os SDRs"]

    N --> O["Selecionar os leads antigos<br/>da base que serão trabalhados"]
    O --> P["Criar uma nova planilha<br/>para utilização no discador"]
    P --> Q["Inserir na planilha do discador:<br/>nome, telefone e identificação do lead"]
    Q --> R["Distribuir a base do discador<br/>entre os SDRs"]

    R --> S["Realizar reunião rápida<br/>de início da operação"]
    S --> T["Reforçar a meta diária:<br/>2 agendamentos por hora<br/>para cada SDR"]

    T --> U["Iniciar os contatos<br/>com leads novos e leads da base"]

    U --> V{"Entraram novos leads<br/>durante o dia?"}
    V -->|Sim| W["Registrar os novos leads<br/>e distribuir entre os SDRs"]
    W --> U

    V -->|Não| X["Acompanhar produção,<br/>agendamentos e registros"]
    X --> U
```

## Ordem exata da rotina

1. Verificar os agendamentos e as visitas marcadas para o dia.
2. Confirmar todas as visitas antes de iniciar as demais atividades.
3. Registrar na planilha quem confirmou, quem não respondeu e quem cancelou.
4. Quando houver cancelamento, informar que o projeto se encerra hoje, mas que o caso será encaminhado à equipe do projeto para verificar a possibilidade de reagendamento.
5. Reunir todos os leads novos.
6. Inserir os leads novos na planilha de acompanhamento.
7. Distribuir os leads novos entre os SDRs.
8. Selecionar os leads antigos da base que serão trabalhados.
9. Preparar uma nova planilha para o discador.
10. Distribuir a base do discador entre os SDRs.
11. Fazer uma reunião rápida com o time.
12. Reforçar a meta de dois agendamentos por hora para cada SDR.
13. Abastecer os SDRs com os leads que entrarem ao longo do dia.
14. Acompanhar os agendamentos e o preenchimento das planilhas.

## Fala para cancelamento

> Entendo. Como o projeto se encerra hoje, não consigo garantir uma nova data neste momento. Vou encaminhar sua solicitação para a equipe responsável pelo projeto e verificar se existe a possibilidade de reagendamento. Assim que eu tiver um retorno, entro em contato com você.

A SDR não deve confirmar uma nova data por conta própria. Ela registra a solicitação e aguarda a autorização da responsável pelo projeto.
