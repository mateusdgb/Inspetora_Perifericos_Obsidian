# Menu: Calibrações

## Objetivo

Centralizar as ferramentas de calibração e ajuste fino da máquina inspetora.

O menu **Calibrações** reúne telas e diálogos usados para alinhar o sistema físico com o sistema lógico, garantindo que:

- os movimentos mecânicos correspondam às coordenadas esperadas
- as câmeras estejam corretamente posicionadas e parametrizadas
- a garra capture as placas com precisão
- a visão computacional opere com referências confiáveis
- os deslocamentos e velocidades sejam coerentes com a máquina real

Essas calibrações são essenciais para garantir que a Inspetora de Periféricos opere com precisão, repetibilidade e segurança.

---

## Visão geral do papel de cada calibração

### Calibração de Entrada  
Usada para encontrar o **centro da bandeja de entrada**.  
  
Essa calibração define uma posição espacial importante para o sistema saber onde começa a área útil de captura das placas.  
  
Ela é útil para:  
- posicionamento inicial  
- captura da primeira placa  
- alinhamento da bandeja no sistema  
  
---  
  
### Calibrar Offset Garra  
Usada para calcular o **deslocamento entre o ponto de visão da câmera fiducial e o ponto real de atuação da garra**.  
  
Em termos simples:  
  
- a câmera “enxerga” um ponto  
- a garra “pega” em outro ponto físico  
- o offset mede essa diferença  
  
Esse valor é essencial para:  
- alinhar captura com visão  
- transformar coordenadas visuais em coordenadas mecânicas  
- evitar erro de pega  
  
---  
  
### Calibrar CNC  
Usada para configurar a conversão entre pulsos e deslocamento físico.  
  
Ela define ou valida o cálculo de:  
  
- **steps/mm**  
- passos por milímetro  
  
Isso garante que, quando o sistema mandar mover um valor físico, a máquina realmente percorra a distância correta.  
  
---  
  
### Calibrar Foco  
Usada para configurar parâmetros de foco das câmeras.  
  
Dependendo da arquitetura, o foco pode refletir:  
- ajuste óptico  
- ajuste lógico  
- posição ideal de inspeção em diferentes contextos  
  
A tela mostra calibração por câmera e também escopo:  
- global  
- local por projeto  
  
---  
  
### Calibrar FOV  
FOV significa **Field of View** ou **Campo de Visão**.  
  
Essa calibração mede quanto da cena a câmera enxerga em milímetros, em diferentes alturas Z.  
  
Ela é importante para:  
- converter pixels em medidas físicas  
- entender quanto da peça cabe na imagem  
- ajustar inspeções conforme a distância da câmera à peça  
  
---  
  
### Pontos Fiduciais  
Usada para configurar referências visuais e espaciais da bandeja.  
  
Fiduciais são pontos de referência conhecidos, usados para:  
- alinhamento  
- correção de posição  
- validação geométrica  
- navegação assistida por câmera  
  
---  
  
### Velocidades JOG  
Usada para configurar as velocidades de deslocamento manual da máquina.  
  
JOG é o movimento manual incremental ou contínuo dos eixos e da garra.  
  
Essa tela ajusta:  
- velocidade positiva e negativa de cada eixo  
- velocidade de abrir e fechar garra
---
## Importância para a máquina  
  
Sem essas calibrações, a máquina pode apresentar problemas como:  
  
- posicionamento incorreto da garra  
- erro ao capturar placas  
- erro de alinhamento entre câmera e peça  
- inspeção em posição errada  
- movimentos excessivos ou insuficientes  
- risco maior de colisão

---
## Relação com o sistema

As calibrações afetam diretamente:

- [[tela_projeto|Tela Projeto]]
- [[tela_inspecao|Tela Inspeção]]
- [[tela_camera_fiducial|Tela Câmera Fiducial]]
- [[lógica_clp|Lógica do CLP]]
- [[visão_computacional|Visão Computacional]]

---

## Diálogos relacionados

- [[dialogo_calibracao_entrada|Diálogo Calibração de Entrada]]
- [[dialogo_calibracao_offset_garra|Diálogo Calibração Offset Garra]]
- [[dialogo_calibracao_cnc|Diálogo Calibração CNC]]
- [[dialogo_calibracao_foco_unificada|Diálogo Calibração de Foco Unificada]]
- [[dialogo_calibracao_fov|Diálogo Calibração de Campo de Visão]]
- [[dialogo_pontos_fiduciais|Diálogo Pontos Fiduciais]]
- [[dialogo_velocidades_jog|Diálogo Velocidades JOG]]

---

## Observação importante

Em calibração, a interface opera como ferramenta de **engenharia e setup**, não como tela de produção.

Por isso, a futura arquitetura ideal deve tratar essas telas como um módulo separado, com regras próprias de:

- permissão
- segurança
- persistência
- validação