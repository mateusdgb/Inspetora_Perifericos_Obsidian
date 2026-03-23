# Subaba: Inspeção 

## Tela  
  
[[tela_projeto|Tela Projeto]]  

### Objetivo da subaba  
  
Permitir configurar como a inspeção será interpretada para a câmera e/ou item atual, definindo limiares, critérios de janela e parâmetros de similaridade.  
  
### Elementos observados  
  
#### Painel lateral direito — Configurações de Inspeção  
  
- **Programação Rápida**  
- **Definir Janela Azul**  
- **Adicionar Inspeção**  
- **Aplicar Config**  
- campo **Threshold**  
- opção de cor:  
- **Branco**  
- **Preto**  
- campo **% Mínimo**  
- campo **Similaridade (%)**  
- botão **Aplicar Similaridade**  
  
### Interpretação funcional inicial  
  
#### Programação Rápida  
Provavelmente abre ou aplica um fluxo simplificado para configurar inspeções rapidamente, talvez baseado em valores padrão ou em presets.  
  
#### Definir Janela Azul  
Indica a existência de uma região especial de inspeção, possivelmente uma janela de referência usada para detecção, alinhamento, contraste ou inspeção booleana.  
  
#### Adicionar Inspeção  
Sugere a criação de uma nova regra/configuração de inspeção dentro da câmera ou ROI atual.  
  
#### Aplicar Config  
Sugere persistir ou aplicar localmente os parâmetros definidos no painel de inspeção.  
  
#### Threshold  
Provavelmente define um limiar para binarização, segmentação ou classificação de pixels.  
  
#### Branco / Preto  
Indica o critério de polaridade da inspeção, isto é, se a análise espera predominância clara ou escura.  
  
#### % Mínimo  
Provavelmente define a porcentagem mínima de preenchimento, cobertura ou presença para considerar a inspeção válida.  
  
#### Similaridade (%)  
Provavelmente define o limiar mínimo de similaridade entre a imagem capturada e a referência esperada.  
  
#### Aplicar Similaridade  
Provavelmente aplica o parâmetro de similaridade ao item, ROI ou inspeção corrente.  
  
### Hipótese de fluxo de uso da subaba Inspeção  
  
1. usuário seleciona a câmera desejada  
2. usuário acessa a subaba **Inspeção**  
3. usuário cria ou seleciona uma inspeção  
4. define parâmetros como:  
- threshold  
- polaridade branco/preto  
- % mínimo  
- similaridade  
5. opcionalmente define uma janela azul  
6. aplica a configuração  
7. salva as alterações do programa  
  
### Relação com o backend  
  
Essa subaba provavelmente conversa com:  
  
- controller de regiões/inspeção  
- service/manager de inspeção  
- comparador de periféricos  
- persistência dos metadados do programa  
  
### Pontos em aberto  
  
Ainda precisam ser confirmados posteriormente:  
  
- o que exatamente é a **Janela Azul**  
- se os parâmetros são aplicados por:  
- câmera  
- ROI  
- componente  
- regra de inspeção  
- o que o botão **Programação Rápida** faz internamente  
- se **Adicionar Inspeção** cria:  
- uma nova regra  
- uma nova janela  
- um novo item de inspeção  
- se **Aplicar Similaridade** é redundante com **Aplicar Config** ou se atua separadamente