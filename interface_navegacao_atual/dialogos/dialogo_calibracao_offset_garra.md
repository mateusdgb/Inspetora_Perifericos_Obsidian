# Diálogo: Calibração de Offset da Garra

## Objetivo

Calibrar o **offset entre a garra e o centro da câmera fiducial**.

---

## O que significa offset

**Offset** é uma diferença de posição entre dois referenciais.

Nesta tela, o offset representa a diferença entre:

- o ponto central visto pela câmera fiducial
- o ponto real da garra que efetivamente pega a peça

Em outras palavras:

> a câmera enxerga um ponto, mas a garra não está exatamente nesse mesmo ponto.  
> O offset mede essa diferença.

---

## Por que isso é importante

Sem essa calibração, o sistema pode:

- enxergar corretamente a peça
- mas mover a garra para o lugar errado

Essa calibração é essencial para:
- alinhar visão e pega
- transformar coordenadas da câmera em coordenadas da garra
- reduzir erro mecânico de captura

---

## Elementos observados

### Instruções na tela
A própria tela orienta um fluxo parecido com:

1. usar os controles JOG para mover a garra esquerda até um ponto visível
2. capturar esse ponto
3. repetir com a garra direita no mesmo ponto
4. mover o centro da câmera fiducial para o mesmo ponto
5. calcular e salvar

---

### Preview da Câmera
Mostra a imagem da câmera fiducial com cruz central.

### Campo `Câmera Fiducial`
Permite escolher qual índice de câmera será usado.

### Botão de ligar vídeo
Inicia o preview da câmera.

---

### Painel de Controles JOG XYZ
Permite movimentar:
- X
- Y
- Z
- garra abrir/fechar

Também mostra coordenadas atuais:
- X
- Y
- Z

---

### Seção `Pontos de Calibração`

Campos observados:

1. **Garra Esquerda**
2. **Garra Direita**
3. **Centro Câmera**

Cada um representa um ponto capturado na máquina para o mesmo ponto físico de referência.

Botões:
- capturar Garra Esquerda
- capturar Garra Direita
- capturar Centro Câmera

---

### Seção `Cálculos`

Campos observados:

- **Centro da Garra**
- **Centro da Câmera**
- **Offset (ΔX, ΔY, ΔZ)**

---

## Significado dos campos

### Garra Esquerda
Posição da máquina quando a garra esquerda está alinhada sobre o ponto de referência.

### Garra Direita
Posição da máquina quando a garra direita está alinhada sobre o mesmo ponto de referência.

### Centro da Garra
Provavelmente calculado a partir da média entre os pontos das duas garras.

### Centro da Câmera
Posição da máquina quando o centro da câmera fiducial está alinhado com o mesmo ponto.

### Offset (ΔX, ΔY, ΔZ)
Diferença entre o centro da garra e o centro da câmera.

Exemplo:
- ΔX = diferença no eixo X
- ΔY = diferença no eixo Y
- ΔZ = diferença no eixo Z

---

## Interpretação matemática

Uma hipótese coerente é:

1. calcular o centro da garra pela média entre Garra Esquerda e Garra Direita
2. calcular o offset como:

```text
Offset = Centro da Garra - Centro da Câmera
```

## Ações relacionadas

- [[acao_abrir_calibracao_offset_garra|Abrir Calibração de Offset da Garra]]
- [[interface_navegacao/acoes/acao_capturar_offset_garra|Capturar Ponto de Offset da Garra]]
- [[interface_navegacao/acoes/acao_calcular_salvar_offset|Calcular e Salvar Offset]]

## Fluxo relacionado

- [[interface_navegacao/fluxos/fluxo_calibracao_offset_garra|Fluxo Calibração de Offset da Garra]]
