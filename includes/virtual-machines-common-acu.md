



Hello Azure 계산 단위 (ACU) tooprovide Azure Sku에 따른 성능 (CPU) 계산을 비교 하는 방법의 hello 개념을 만들었습니다. 이렇게 하면 SKU가 가장 가능성이 높은 toosatisfy를 쉽게 식별할 수 성능 필요 합니다.  ACU는 현재 100인 작은(Standard_A1) VM에서 표준화되고 다른 SKU는 모두 SKU가 표준 벤치 마크를 얼마나 빨리 실행할 수 있는지를 나타냅니다. 

> [!IMPORTANT]
> hello ACU 지침일 뿐입니다.  작업에 대 한 hello 결과 달라질 수 있습니다. 
> 
> 

<br>

| SKU 제품군 | ACU \ vCPU |
| --- | --- |
| [A0](../articles/virtual-machines/windows/sizes-general.md) |50 |
| [A1-A4](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A5-A7](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A1_v2-A8_v2](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A2m_v2-A8m_v2](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A8-A11](../articles/virtual-machines/windows/sizes-hpc.md) |225* |
| [D1-D14](../articles/virtual-machines/windows/sizes-general.md) |160 |
| [D1_v2-D15_v2](../articles/virtual-machines/windows/sizes-general.md) |210 - 250* |
| [DS1-DS14](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160 |
| [DS1_v2-DS15_v2](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |210-250* |
| [D_v3](../articles/virtual-machines/virtual-machines-windows-sizes-general.md) |160-190* ** |
| [Ds_v3](../articles/virtual-machines/virtual-machines-windows-sizes-general.md) |160-190* ** |
| [E_v3](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160-190* ** |
| [Es_v3](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160-190* ** |
| [F1-F16](../articles/virtual-machines/windows/sizes-compute.md) |210-250* |
| [F1s-F16s](../articles/virtual-machines/windows/sizes-compute.md) |210-250* |
| [G1-G5](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |180 - 240* |
| [GS1-GS5](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |180 - 240* |
| [H](../articles/virtual-machines/windows/sizes-hpc.md) |290 - 300* |
| [L4s-L32s](../articles/virtual-machines/windows/sizes-storage.md) |180 - 240* |
| [M](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) | 160-180** |

으로 표시 된 ACUs는 * Intel® 터보 기술 tooincrease CPU 주기를 사용 하 고 성능 향상을 제공 합니다.  hello hello 부스트 수 다 hello VM 크기, 작업 및 hello에서 실행 중인 다른 작업에 따라 동일한 호스트 합니다.

**하이퍼 스레드 
