# Diálogo: Calibração CNC

## Objetivo

Definir a conversão entre pulsos/comandos de movimento e deslocamento físico real do eixo.

Essa calibração determina os **steps por milímetro**.

---

## Conceito de Steps por Milímetro

O sistema de movimento costuma trabalhar com pulsos elétricos ou steps.

Para que a máquina saiba quanto um eixo realmente se move, é necessário converter:

- pulsos/steps
- para milímetros

Essa relação depende do conjunto mecânico e eletrônico.

---

## Estrutura observada

### Título interno

Exemplo observado:
- **Calibração de Steps/mm - Eixo X**

Isso indica que a calibração provavelmente é feita por eixo.

### Campos

- **Passos por volta (motor)**
- **Microsteps do driver**
- **Relação engrenagem (1=direto)**
- **Passo do fuso (mm/volta)**
- **Resultado**

### Botões

- botão verde para aplicar ao controlador
- **Cancelar**
- botão final para aplicar e fechar

---

## Significado de cada campo

### Passos por volta (motor)
Quantidade de passos completos necessários para o motor dar uma volta completa.

Exemplo típico:
- motor de 200 passos por volta

### Microsteps do driver
Fator de subdivisão do passo feito pelo driver do motor.

Exemplo:
- 1
- 2
- 4
- 8
- 16

Quanto maior, maior a resolução teórica do movimento.

### Relação engrenagem (1=direto)
Relação mecânica entre motor e eixo movimentado.

- `1` significa transmissão direta
- outros valores representam redução ou multiplicação mecânica

### Passo do fuso (mm/volta)
Quanto o eixo avança linearmente a cada volta completa do fuso.

Exemplo:
- 5 mm/volta

### Resultado
Mostra o valor calculado final de **steps/mm**.

---

## Fórmula conceitual

A relação geralmente segue a lógica:

`steps/mm = (passos por volta × microsteps × relação mecânica) / passo do fuso`

---

## Interpretação funcional

Essa tela ajusta o modelo matemático do movimento.

Se os valores estiverem errados:

- a máquina andará menos do que deveria
- ou mais do que deveria
- e todas as coordenadas ficarão imprecisas

---

## Fluxo de uso esperado

1. selecionar ou abrir a calibração do eixo
2. preencher:
   - passos por volta
   - microsteps
   - relação
   - passo do fuso
3. conferir o resultado calculado
4. aplicar ao controlador
5. salvar e fechar

---

## Pontos em aberto

- se existe uma tela por eixo ou seleção interna de eixo
- se o valor é gravado no CLP, em arquivo, ou em ambos
