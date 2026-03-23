# Diálogo: Calibração de Entrada

## Objetivo

Essa tela calibra o **centro da bandeja de entrada**.  
  
A ideia é capturar dois pontos de referência e, a partir deles, calcular um ponto central que será usado pelo sistema como posição de entrada das placas.  
  
Isso ajuda a máquina a saber **onde a bandeja está localizada no espaço físico**.  
  
Na prática, essa calibração responde à pergunta:  
  
> “Qual é o centro da região da bandeja onde a máquina deve procurar ou posicionar a captura das placas?”

---

## Estrutura da tela

### Área esquerda — Preview da câmera fiducial

Mostra a imagem da câmera fiducial com um alvo visual composto por:

- linha vertical
- linha horizontal
- ponto central

Esse alvo serve como referência para centralizar visualmente um ponto da máquina ou da bandeja.

### Botão da câmera

- **Desligar Câmera**  
  Controla o preview da câmera fiducial.

### Painel de controles de movimentação

Permite movimentar a máquina usando:

- X-
- X+
- Y-
- Y+
- Z-
- Z+
- STOP
- Abrir
- Fechar
- Passo
- Contínuo
- Ir para Zero (Home)

Também mostra as coordenadas atuais dos eixos:

- X
- Y
- Z

### Painel de captura de pontos

Possui:

- **Capturar Ponto 1**
- **Capturar Ponto 2**
- exibição das coordenadas dos pontos capturados
- exibição do **Centro**

### Ações finais

- **Calcular e Salvar**
- **Cancelar**

---

## Interpretação funcional

O usuário deve capturar dois pontos de referência na bandeja, e o sistema calcula o centro entre eles.

Esse centro passa a representar uma posição geométrica útil para:

- alinhamento inicial
- localização da bandeja
- referência de captura
- futura automação da coleta das placas

---

## O que significa “Centro da Bandeja”

É a posição central calculada a partir de dois pontos conhecidos da bandeja.

Dependendo da lógica implementada, esse centro pode servir como:

- referência absoluta
- ponto médio da área útil
- origem lógica para rotas internas da bandeja

---

## Fluxo de uso esperado

1. ligar ou manter ativa a câmera fiducial
2. mover a máquina até o primeiro ponto de referência
3. clicar em **Capturar Ponto 1**
4. mover a máquina até o segundo ponto de referência
5. clicar em **Capturar Ponto 2**
6. verificar as coordenadas capturadas
7. clicar em **Calcular e Salvar**
8. persistir o centro calculado

---

## Campos e funções

### Capturar Ponto 1 / Capturar Ponto 2
Armazenam as coordenadas atuais dos eixos no momento da captura.

### Centro
É o resultado calculado a partir dos pontos 1 e 2.

### Calcular e Salvar
Calcula o centro e grava o resultado na configuração do sistema.

### Cancelar
Fecha a calibração sem persistir alterações.

---

## Pontos em aberto

- quais pontos físicos da bandeja devem ser usados como referência
- onde exatamente o centro é persistido
- quais módulos consomem esse centro depois

---

## Ações relacionadas  
  
- [[acao_abrir_calibracao_entrada|Abrir Calibração de Entrada]]  
- [[interface_navegacao/acoes/acao_capturar_ponto_calibracao_entrada|Capturar Ponto da Calibração de Entrada]]  
- [[interface_navegacao/acoes/acao_calcular_salvar_centro_bandeja|Calcular e Salvar Centro da Bandeja]]  
  
## Fluxo relacionado  
  
- [[interface_navegacao/fluxos/fluxo_calibracao_entrada|Fluxo Calibração de Entrada]]