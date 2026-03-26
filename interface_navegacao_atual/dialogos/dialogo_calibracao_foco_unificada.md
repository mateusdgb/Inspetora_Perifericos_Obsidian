# Diálogo: Calibração de Foco Unificada

## Objetivo

Permitir calibrar foco e pontos de referência de múltiplas câmeras em uma única
interface.

Essa tela parece consolidar:

- preview de câmera
- movimentação via PLC
- ajuste de foco
- pontos A e B
- escopo de salvamento

---

## Estrutura geral

### Abas superiores de câmera

- `Câmera 1` = alias de `top`
- `Câmera 2` = alias de `bottom`
- `Câmera 3` = alias de `side`
- `Câmera 4` = alias de `fiducial`
- `DUPLO (1 2)` = modo combinado observado para `top` e `bottom`

### Área de preview

Mostra imagem ao vivo ou foto da câmera atual.

No modo **DUPLO (1 2)**, a tela mostra duas áreas de imagem simultaneamente.

### Botões de captura e visualização

Dependendo do modo:

- Live Top
- Foto Top
- Live Bot
- Foto Bot
- Ambas

### Painel de Controle de Movimento

Permite mover a máquina durante a calibração.

### Painel Ajuste de Foco e Pontos

Para a câmera ou câmeras atuais, exibe:

- slider de foco
- valor do foco
- botão **Ir Ponto A**
- botão **Ir Ponto B**
- status dos pontos

### Painel Salvar Calibração

- **Global (Todos)**
- **Local (Este projeto)**
- **Salvar Calibração**

---

## O que significa foco nesta tela

Aqui, "foco" pode ter dois sentidos possíveis:

1. ajuste óptico real da câmera ou lente
2. ajuste operacional ligado ao posicionamento Z ou a parâmetros associados ao
   foco percebido

A documentação futura ainda precisa confirmar qual dos dois está implementado
na tela ativa hoje.

---

## O que significam os Pontos A e B

Os pontos A e B parecem ser posições previamente cadastradas ou usadas como
referências de calibração.

Eles podem servir para:

- comparar nitidez em posições diferentes
- validar foco em regiões distintas
- reproduzir posições padrão de ajuste

---

## O que significa o modo DUPLO (1 2)

O modo DUPLO aparenta permitir calibração simultânea ou comparativa entre
`top` e `bottom`.

---

## Escopos de salvamento

### Global (Todos)

A calibração é aplicada como padrão geral da máquina ou sistema.

### Local (Este projeto)

A calibração vale apenas para o projeto atual.

---

## Fluxo de uso esperado

1. abrir o diálogo
2. selecionar a câmera desejada
3. ativar live ou capturar foto
4. mover a máquina se necessário
5. ajustar o foco
6. usar ou registrar pontos A e B
7. definir escopo de salvamento
8. salvar calibração

---

## Pontos em aberto

- se o foco é óptico real ou associado à posição
- como pontos A e B são definidos
- como o modo DUPLO é usado internamente
- qual o caminho de código atual dessa tela, já que parte da documentação
  histórica ainda usa nomes antigos
