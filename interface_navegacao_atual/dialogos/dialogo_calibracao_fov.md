# Diálogo: Calibração de Campo de Visão

## Objetivo

Calibrar o **campo de visão (FOV)** da câmera em diferentes alturas Z.

O objetivo é relacionar:  
- posição Z  
- largura visível em mm  
- altura visível em mm  
  
Isso ajuda o sistema a entender quanto da cena a câmera enxerga em diferentes distâncias.

---

## Conceito de FOV

FOV significa **Field of View**, ou **Campo de Visão**.

É a área que a câmera consegue enxergar.

Na prática, essa tela relaciona:

- posição Z
- largura visível em mm
- altura visível em mm

Isso permite saber quanto da cena cabe na imagem em determinada distância da câmera até o objeto.

---

## Estrutura observada

### Área explicativa
A própria tela já informa que a calibração deve ser feita em duas alturas Z diferentes.

### Colunas
- **Ponto 0 (Z baixo)**
- **Ponto 1 (Z alto)**

### Campos
Para cada ponto:

- **Posição Z (pulsos)**
- **Largura visível (mm)**
- **Altura visível (mm)**

### Botões
- **Salvar**
- **Cancelar**

---

## Significado dos campos

### Posição Z (pulsos)
Coordenada vertical do eixo Z, provavelmente expressa em pulsos internos do sistema.

### Largura visível (mm)
Largura real do mundo físico que aparece na imagem naquela altura Z.

### Altura visível (mm)
Altura real do mundo físico que aparece na imagem naquela altura Z.

---

## Interpretação funcional

Como o campo de visão muda com a distância, o sistema usa duas referências:

- uma mais próxima
- uma mais afastada

A partir disso, ele pode modelar a relação entre Z e área visível.

Isso pode ser usado para:

- conversão pixel → mm
- estimativa de escala
- precisão de inspeção
- ajuste de ROIs e medidas

---

## Fluxo de uso esperado

1. posicionar a câmera no Z baixo
2. medir área visível com padrão conhecido
3. preencher largura e altura visíveis
4. repetir no Z alto
5. salvar a calibração

---

## Pontos em aberto

- se há uma tela por câmera
- se a relação entre Z e FOV é interpolada linearmente
- onde esse FOV é usado no backend

---
## Ações relacionadas  
  
- [[acao_abrir_calibracao_fov|Abrir Calibração de FOV]]  