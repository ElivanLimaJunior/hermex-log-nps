# Fluxograma do processo de pós-vendas (Hermex Log)

Versão em código (Mermaid) do fluxograma desenhado no Miro. O GitHub renderiza este diagrama automaticamente. As formas com **borda vermelha** são candidatas à automação.

```mermaid
flowchart TD
    I([Início — Pedido Enviado]) --> A1(Registrar envio na planilha de handoff)
    A1 --> A2(Enviar e-mail de notificação ao pós-vendas)
    A2 --> A3(Acompanhar rastreio do transporte)
    A3 --> D1{Entrega confirmada?}
    D1 -- Não --> D1b{Prazo máximo do SLA excedido?}
    D1b -- Não --> A4(Aguardar 1 dia útil e verificar novamente)
    D1b -- Sim --> A4b(Abrir ocorrência de atraso e informar o cliente)
    A4b --> A4
    A4 --> D1
    D1 -- Sim --> A5(Confirmar entrega e registrar data de recebimento)
    A5 --> A6(Enviar pesquisa de satisfação)
    A6 --> A7(Registrar resposta NPS na planilha)
    A7 --> D2{Cliente insatisfeito? nota < 6}
    D2 -- Sim --> A8(Classificar feedback com IA)
    A8 --> A9(Notificar equipe de pós-vendas)
    A9 --> A10(Validar classificação e tratar a reclamação)
    A10 --> F([Fim — Ciclo Encerrado])
    D2 -- Não --> A11(Enviar e-mail de agradecimento ao cliente)
    A11 --> F

    classDef automacao stroke:#d32f2f,stroke-width:3px;
    class A1,A2,A4,A5,A6,A7,A8,A9,A11 automacao;
```

| Atividade automatizável | Critérios |
|---|---|
| Registrar envio na planilha de handoff | Repetitividade, Transferência entre equipes, Rastreabilidade |
| Enviar e-mail de notificação ao pós-vendas | Repetitividade, Regras claras, Transferência entre equipes, Criticidade |
| Aguardar e verificar novamente (looping) | Repetitividade, Regras claras |
| Confirmar entrega | Regras claras, Rastreabilidade |
| Enviar pesquisa de satisfação | Repetitividade, Regras claras |
| Registrar resposta NPS | Repetitividade, Transferência entre equipes, Rastreabilidade |
| Classificar feedback com IA | Repetitividade, Regras claras, Criticidade |
| Notificar equipe de pós-vendas | Transferência entre equipes, Criticidade |
| Enviar agradecimento ao cliente | Repetitividade, Regras claras |
