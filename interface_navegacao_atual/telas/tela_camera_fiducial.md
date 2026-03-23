# Tela: Câmera Fiducial

## Objetivo

Permitir operar a câmera fiducial e associar posições de movimento ao processo de alinhamento e captura ligado à garra.

## Elementos observados

### Navegação da tela

- Aba principal: **Câmera Fiducial**

### Área esquerda

- visualização da câmera fiducial
- estado da câmera
- botão [[acao_ligar_camera_fiducial|Ligar]]

### Área direita

#### Controles de Movimentação

- X-
- X+
- Y-
- Y+
- Z-
- Z+
- STOP
- Fechar
- Abrir
- P (pulsos)
- V (pulsos/s)
- Passo
- Contínuo
- Ir para Zero (Home)
- indicadores de posição X, Y, Z

#### Posições de Movimento

- Adicionar posição atual
- Inserir nova posição
- Editar posição
- Remover posição

#### Operação de programa

- aba/botões Salvar/Carregar
- botão [[acao_salvar_programa_fiducial|Salvar Programa]]
- botão [[acao_carregar_programa_fiducial|Carregar Programa]]
- botão Executar

## Interpretação funcional

A tela da fiducial parece funcionar como:

- tela de setup de movimentos associados à fiducial
- tela de cadastro de posições
- suporte à execução de sequência

## Pontos a confirmar depois

- diferença entre posições de movimento e posições de captura
- relação entre programa da fiducial e programa de inspeção
- o que exatamente o botão **Executar** faz
- como essas posições são consumidas no ciclo automático

## Fluxos relacionados

- [[fluxo_fiducial|Fluxo Fiducial]]
- [[acao_ligar_camera_fiducial|Ação Ligar Câmera Fiducial]]