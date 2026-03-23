# Fluxo: Configuração CLP

```mermaid
flowchart TD

A[Menu Configurações] --> B[Conexão CLP]
B --> C[Preencher IP Porta Timeout]
C --> D[Testar Comunicação]
D --> E{Comunicação OK?}
E -->|Não| F[Exibir erro no log]
E -->|Sim| G[Conectar]
G --> H[Atualizar status]
H --> I[Salvar configuração]