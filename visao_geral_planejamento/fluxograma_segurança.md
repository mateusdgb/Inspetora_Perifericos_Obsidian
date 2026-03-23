
```mermaid
flowchart TD

A[Comando de movimento]

A --> B{Dentro do limite do eixo?}

B -->|Não| C[Cancelar movimento]

B -->|Sim| D{Zona segura?}

D -->|Não| C

D -->|Sim| E[Executar movimento]

E --> F{Sensor ativado?}

F -->|Sim| G[Parar máquina]

F -->|Não| H[Continuar operação]
```

---

## Documentos Relacionados

- [[fluxograma_operacao|Fluxograma de Operação]]
- [[diagrama_estados|Diagrama de Estados]]
- [[lógica_clp|Lógica do CLP]]
- [[lista_sensores|Lista de Sensores]]
- [[lista_atuadores|Lista de Atuadores]]

---

## Observação

As funções de segurança devem atuar em conjunto com a lógica de movimento descrita em [[lógica_clp]].

Os sensores utilizados para proteção e referência estão descritos em [[lista_sensores]].

As ações de parada e bloqueio afetam diretamente os estados descritos em [[diagrama_estados]].