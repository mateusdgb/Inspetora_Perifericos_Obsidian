# Subaba: Inspeção

## Tela

[[tela_projeto|Tela Projeto]]

### Objetivo da subaba

Permitir configurar como a inspeção será interpretada para a câmera e o
componente atual, definindo janelas, limiares e parâmetros de similaridade.

### Elementos observados

#### Painel lateral direito - Configurações de Inspeção

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

### Comportamento confirmado no código

#### Programação Rápida

Aplica configuração padrão aos componentes da câmera ativa:

- janela azul padrão
- similaridade mínima padrão de `95%`

#### Definir Janela Azul

Ativa o `BlueReferenceController` para desenhar a janela azul do componente
selecionado.

#### Adicionar Inspeção

Ativa o `InspectionRegionController` para desenhar uma nova janela de inspeção
para o componente selecionado, usando:

- `threshold`
- polaridade `Branco` ou `Preto`
- `% Mínimo`

#### Aplicar Config

Aplica `threshold`, polaridade e `% Mínimo` a todas as janelas de inspeção do
componente selecionado.

#### Threshold

Define o limiar numérico usado na configuração da inspeção.

#### Branco / Preto

Define a polaridade esperada na inspeção.

#### % Mínimo

Define o percentual mínimo exigido para a regra de inspeção.

#### Similaridade (%)

Define a similaridade mínima do componente selecionado.

#### Aplicar Similaridade

Atualiza a similaridade mínima do componente atual e, se existir janela azul,
recorta e salva a imagem de referência correspondente.

### Fluxo de uso confirmado da subaba Inspeção

1. usuário seleciona a câmera desejada
2. usuário acessa a subaba **Inspeção**
3. usuário seleciona um componente
4. define parâmetros como `threshold`, polaridade, `% mínimo` e `similaridade`
5. opcionalmente define uma janela azul
6. aplica a configuração
7. salva as alterações do programa

### Relação com o backend

Essa subaba conversa com:

- `InspectionRegionController`
- `BlueReferenceController`
- `ProgramManager`
- persistência do programa e das imagens de referência

### Pontos em aberto

- semântica completa da **Janela Azul** no comparador final de visão
- detalhes do formato persistido para todas as variações de inspeção
- limite entre comportamento já operacional e partes ainda marcadas como fase
  futura nos comentários do código
