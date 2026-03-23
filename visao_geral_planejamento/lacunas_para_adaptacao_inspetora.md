# Lacunas para Adaptação da Inspetora

## Objetivo

Registrar as principais diferenças entre o projeto de software existente e a configuração real desejada para a Inspetora de Periféricos.

---

## 1. Garra

### Situação atual

O projeto possui base para controle de ciclo e até documentação da garra, mas na máquina atual a automação completa da garra ainda não está finalizada no CLP.

### Necessidade

- integrar abertura/fechamento ao CLP
- integrar ajuste ao tamanho da placa
- validar sensores e estados da garra
- documentar sequência de captura e soltura

---

## 2. Limites reais dos eixos

### Situação atual

O software já possui limites configuráveis e regiões de segurança, mas os testes mostraram que os valores ainda não refletem corretamente a máquina física.

### Necessidade

- recalibrar limites de X, Y e Z
- revisar homing
- revisar zonas proibidas
- revisar distâncias seguras até vidro e câmeras

---

## 3. Layout de bandejas

### Situação atual

O sistema já suporta cadastro de bandejas, mas o arranjo físico final da máquina ainda precisa ser consolidado.

### Necessidade

- definir posição exata da bandeja de entrada
- definir posição da bandeja de aprovadas
- definir posição da bandeja de reprovadas
- definir alcance real da garra

---

## 4. Fluxo automático completo

### Situação atual

Há base de ciclo automático, mas o uso real na inspetora ainda precisa ser validado ponta a ponta.

### Necessidade

- validar ciclo completo com hardware real
- validar retomada de ciclo
- validar deposição correta por resultado
- validar integração entre movimento, captura e inspeção

---

## 5. Parametrização do programa para placas reais

### Situação atual

O sistema de programas já existe.

### Necessidade

- cadastrar programas reais de placas de notebook
- mapear componentes por câmera
- definir critérios de aprovação
- organizar referências reais

---

## Documentos Relacionados

- [[visão_geral|Visão Geral]]
- [[arquitetura_sistema|Arquitetura do Sistema]]
- [[visão_computacional|Visão Computacional]]
- [[lógica_clp|Lógica do CLP]]
- [[bandejas_e_regioes_seguranca|Bandejas e Regiões de Segurança]]