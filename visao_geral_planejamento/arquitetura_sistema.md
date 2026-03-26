# Arquitetura do Sistema

Resumo do estado atual:

- entrada em `inspetor_main.py`
- composition root em `CameraInspectionApp`
- persistência de programas em `services/program_manager.py`
- adaptação para runtime em `orchestrator/inspection/program_orchestrator.py`
- hardware exposto por `hardware/camera_manager.py` e `hardware/plc_controller.py`
- `HardwareTestTab` mantém o `PLCController` ativo para o restante da aplicação

Referência cruzada:

- [[../estado_atual_codigo|Estado Atual do Código]]

```mermaid
flowchart TD

A[Operador] --> B[Interface PyQt6]
B --> C[CameraInspectionApp]
C --> D[Orchestrators]
C --> E[Controllers]
C --> F[Tabs Principais]
D --> G[HardwareOrchestrator]
D --> H[InspectionOrchestrator]
H --> I[ProgramOrchestrator]
I --> J[ProgramManager]
G --> K[CameraManager]
G --> L[PLCController]
F --> M[Projeto]
F --> N[Inspeção]
F --> O[Câmera Fiducial]
K --> P[top]
K --> Q[bottom]
K --> R[side]
K --> S[fiducial]
```
