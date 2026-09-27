# v1 — Monólito com I/O bloqueante

## O que é
Pipeline de processamento de pedidos onde cada etapa (verificar estoque,
cobrar pagamento, enviar e-mail, atualizar estoque) é uma chamada **síncrona**
que bloqueia a thread até responder. Os pedidos são processados **um de
cada vez**, em sequência.

## Como rodar
```bash
python main.py
```

Durante a execucao, o terminal atualiza uma barra de progresso a cada etapa
concluida do pedido atual.

## O gargalo
Cada pedido leva ~1.4s de I/O simulado. Como não há concorrência entre
pedidos, o tempo total escala linearmente com N:

```
tempo_total ≈ N × 1.4s
```

Para 10 pedidos, isso são ~14 segundos, mesmo que as etapas de pedidos
diferentes não dependam umas das outras — o gargalo é puramente
arquitetural (falta de concorrência), não de capacidade real do sistema.
