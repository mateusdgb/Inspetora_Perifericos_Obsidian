# Sistema de Visão Computacional  
  
## Visão Geral  
  
O projeto existente já possui base de inspeção por visão computacional, com captura de imagens, cadastro de regiões de inspeção, comparação com referência e consolidação do resultado.  
  
Arquivos principais observados:  
  
- `services/inspection_service.py`  
- `inspection/peripheral_comparator.py`  
- `controllers/inspection_runtime_controller.py`  
  
---  
  
## Papéis de câmera no projeto atual  
  
O projeto atual trabalha com os seguintes papéis de câmera:  
  
- `fiducial`  
- `top`  
- `bottom`  
- `side`  
  
  
---  
  
## Fluxo atual de inspeção  
  
1. O programa de inspeção é carregado.  
2. As câmeras configuradas são verificadas.  
3. Imagens são capturadas.  
4. O sistema compara as imagens capturadas com referências salvas.  
5. Cada componente pode ser avaliado por:  
- similaridade  
- janelas de inspeção  
- limiares configuráveis  
6. O resultado consolidado é emitido como aprovado ou reprovado.  
  
---  
  
## Arquivos relevantes  
  
### Serviço principal de inspeção  
  
- `services/inspection_service.py`  
  
Responsável por:  
  
- validar se o sistema está pronto  
- capturar imagens  
- coordenar a execução da inspeção  
- consolidar resultados  
  
### Comparador de imagens  
  
- `inspection/peripheral_comparator.py`  
  
Responsável por:  
  
- carregar referências  
- comparar ROIs  
- avaliar janelas de inspeção  
- calcular score de similaridade  
  
---  
  
## Documentos Relacionados  
  
- [[arquitetura_sistema|Arquitetura do Sistema]]  
- [[programas_de_inspecao|Programas de Inspeção]]  
- [[lacunas_para_adaptacao_inspetora|Lacunas para Adaptação]]  
- [[persistencia_e_rastreabilidade|Persistência e Rastreabilidade]]

## Observação

O sistema de visão computacional participa das etapas de alinhamento da garra e inspeção dos periféricos.

Seu resultado influencia diretamente a decisão descrita em [[fluxograma_operacao]] e a transição entre estados descrita em [[diagrama_estados]].