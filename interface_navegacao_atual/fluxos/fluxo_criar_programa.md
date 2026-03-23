
---

# 14. Fluxo criar programa

# Fluxo: Criar Programa

```mermaid
flowchart TD

A[Tela Projeto] --> B[Clicar em Novo Programa]
B --> C[Informar nome do programa]
C --> D{Nome válido?}

D -->|Não| E[Mostrar erro]
D -->|Sim| F[Criar estrutura do programa]

F --> G[Selecionar câmera]
G --> H[Mover sistema]
H --> I[Capturar imagem]
I --> J[Definir região da placa]
J --> K[Desenhar ROI]
K --> L[Salvar alterações]
L --> M[Concluir]
```

## Ações relacionadas

- [[acao_novo_programa|Novo Programa]]
- [[acao_capturar_imagem|Capturar Imagem]]
- [[acao_definir_regiao_placa|Definir Região da Placa]]
- [[acao_desenhar_roi|Desenhar ROI]]
- [[acao_concluir_programa|Concluir]]