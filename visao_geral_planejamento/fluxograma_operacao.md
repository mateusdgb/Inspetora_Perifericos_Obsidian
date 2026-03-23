# Fluxograma de Operação da Máquina

```mermaid
flowchart TD

A[Inicialização da Máquina]

A --> B[Executar Homing dos eixos X Y Z]

B --> C[Máquina pronta]

C --> D[Operador carrega bandeja com placas]

D --> E[Operador inicia ciclo]

E --> F[Movimento até posição da placa]

F --> G[Alinhamento com câmera fiducial]

G --> H[Ajuste da garra]

H --> I[Garra captura placa]

I --> J[Elevar placa eixo Z]

J --> K[Movimentar para posição de inspeção]

K --> L[Captura de imagens]

L --> M[Processamento visão computacional]

M --> N{Periféricos corretos?}

N -->|Sim| O[Classificar como APROVADA]

N -->|Não| P[Classificar como REPROVADA]

O --> Q[Depositar em bandeja de aprovadas]

P --> R[Depositar em bandeja de reprovadas]

Q --> S[Retornar garra]

R --> S

S --> T{Ainda existem placas?}

T -->|Sim| F
T -->|Não| U[Fim do ciclo]
```

---

## Documentos Relacionados

- [[visão_geral|Visão Geral]]
- [[arquitetura_sistema|Arquitetura do Sistema]]
- [[fluxograma_segurança|Fluxograma de Segurança]]
- [[diagrama_estados|Diagrama de Estados]]
- [[lógica_clp|Lógica do CLP]]
- [[visão_computacional|Visão Computacional]]

---

## Observação

Este fluxograma descreve a sequência funcional da máquina durante o ciclo de inspeção.

As validações de proteção e intertravamento complementares devem ser consultadas em [[fluxograma_segurança]].

A implementação dos estados de controle associados a esse fluxo está descrita em [[diagrama_estados]] e [[lógica_clp]].