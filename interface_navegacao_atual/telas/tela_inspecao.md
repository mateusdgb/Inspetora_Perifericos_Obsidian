# Tela: Inspeção  
  
## Objetivo  
  
Executar o processo de inspeção de placas, exibindo câmeras, programa carregado, estado do ciclo, falhas identificadas e decisão final da peça.  
  
## Elementos observados  
  
### Navegação da tela  
  
- Aba principal: **Inspeção**  
- Subabas de câmera:  
- TOP  
- BOTTOM  
- SIDE  
  
### Área esquerda  
  
#### Preview das câmeras  
  
- visualização da câmera selecionada  
- exibição de serial  
- botão **Iniciar**  
- botão **Capturar**  
  
### Área direita  
  
#### Resultado da inspeção  
  
- nome/status do programa carregado  
- indicadores de status  
- [[acao_iniciar_ciclo|Iniciar Ciclo]]  
- [[acao_parar_ciclo|Parar]]  
- [[acao_inspecionar|Inspecionar]]  
- botão **Carregar**  
- barra de progresso  
- contadores Total / OK / NOK  
  
#### Falhas identificadas  
  
- botão **Anterior**  
- botão **Próximo**  
- texto de falha atual  
- área de visualização de defeito  
- campos:  
- câmera  
- posição  
- erro  
  
#### Decisão final  
  
- [[acao_aprovar_peca|Aprovar Peça]]  
- [[acao_reprovar_peca|Reprovar Peça]]  
  
## Interpretação funcional  
  
Esta tela parece suportar dois modos:  
  
- inspeção assistida/manual  
- inspeção em ciclo automatizado  
  
## Pontos a confirmar depois  
  
- diferença exata entre **Iniciar Ciclo** e **Inspecionar**  
- se **Carregar** carrega programa, ordem ou ambos  
- critérios de habilitação de Aprovar/Reprovar  
- se a decisão final é automática, manual ou híbrida  
  
## Fluxos relacionados  
  
- [[fluxo_inspecao|Fluxo de Inspeção]]  
- [[acao_iniciar_ciclo|Ação Iniciar Ciclo]]  
- [[acao_inspecionar|Ação Inspecionar]]