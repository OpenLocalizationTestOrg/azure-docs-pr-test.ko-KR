---
title: "Linux Vm에 대 한 점수 aaaCompute 벤치 마크 | Microsoft Docs"
description: "Linux를 실행하는 Azure VM에 대한 CoreMark 계산 벤치마크 점수를 비교합니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 93e812c1-79dd-40c5-b97b-aa79f5cd7d76
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cynthn
ms.openlocfilehash: b2c1ca5fbd80cea030ac2cc22156c4e9444c6726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="compute-benchmark-scores-for-linux-vms"></a>Linux VM에 대한 벤치마크 점수 계산
hello CoreMark 벤치 마크 점수 표시 다음 Azure의 Ubuntu 실행 되는 성능 우선 VM 목록에 대해 성능을 계산 합니다. [Windows Vm](../windows/compute-benchmark-scores.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에 대해 계산 벤치마크 점수를 사용할 수도 있습니다.

## <a name="a-series---compute-intensive"></a>A 시리즈-계산 집약적
| 크기 | vCPU | NUMA 노드 | CPU | 실행 | 반복 수/초 | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8 |8 |1 |Intel Xeon CPU E5-2670 0 @ 2.6 GHz |179 |110,294 |554 |
| Standard_A9 |16 |2 |Intel Xeon CPU E5-2670 0 @ 2.6 GHz |189 |210,816 |2,126 |
| Standard_A10 |8 |1 |Intel Xeon CPU E5-2670 0 @ 2.6 GHz |188 |110,025 |1,045 |
| Standard_A11 |16 |2 |Intel Xeon CPU E5-2670 0 @ 2.6 GHz |188 |210,727 |2,073 |

## <a name="dv2-series"></a>Dv2 시리즈
| 크기 | vCPU | NUMA 노드 | CPU | 실행 | 반복 수/초 | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_D1_v2 |1 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |140 |14,852 |780 |
| Standard_D2_v2 |2 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |133 |29,467 |1,863 |
| Standard_D3_v2 |4 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |139 |56,205 |1,167 |
| Standard_D4_v2 |8 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |126 |108,543 |3,446 |
| Standard_D5_v2 |16 |2 |Intel Xeon E5-2673 v3 @ 2.4 GHz |126 |205,332 |9,998 |
| Standard_D11_v2 |2 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |125 |28,598 |1,510 |
| Standard_D12_v2 |4 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |131 |55,673 |1,418 |
| Standard_D13_v2 |8 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |140 |107,986 |3,089 |
| Standard_D14_v2 |16 |2 |Intel Xeon E5-2673 v3 @ 2.4 GHz |140 |208,186 |8,839 |
| Standard_D15_v2 |20 |2 |Intel Xeon E5-2673 v3 @ 2.4 GHz |28 |268,560 |4,667 |

## <a name="f-series"></a>F 시리즈
| 크기 | vCPU | NUMA 노드 | CPU | 실행 | 반복 수/초 | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_F1 |1 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |154 |15,602 |787 |
| Standard_F2 |2 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |126 |29,519 |1,233 |
| Standard_F4 |4 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |147 |58,709 |1,227 |
| Standard_F8 |8 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |224 |112,772 |3,006 |
| Standard_F16 |16 |2 |Intel Xeon E5-2673 v3 @ 2.4 GHz |42 |218,571 |5,113 |

## <a name="g-series"></a>G 시리즈
| 크기 | vCPU | NUMA 노드 | CPU | 실행 | 반복 수/초 | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_G1 |2 |1 |Intel Xeon E5-2698B v3 @ 2 GHz |83 |31,310 |2,891 |
| Standard_G2 |4 |1 |Intel Xeon E5-2698B v3 @ 2 GHz |84 |60,112 |3,537 |
| Standard_G3 |8 |1 |Intel Xeon E5-2698B v3 @ 2 GHz |84 |107,522 |4,537 |
| Standard_G4 |16 |1 |Intel Xeon E5-2698B v3 @ 2 GHz |83 |195,116 |5,024 |
| Standard_G5 |32 |2 |Intel Xeon E5-2698B v3 @ 2 GHz |84 |360,329 |14,212 |

## <a name="gs-series"></a>GS 시리즈
| 크기 | vCPU | NUMA 노드 | CPU | 실행 | 반복 수/초 | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_GS1 |2 |1 |Intel Xeon E5-2698B v3 @ 2 GHz |84 |28,613 |1,884 |
| Standard_GS2 |4 |1 |Intel Xeon E5-2698B v3 @ 2 GHz |83 |54,348 |3,474 |
| Standard_GS3 |8 |1 |Intel Xeon E5-2698B v3 @ 2 GHz |83 |104,564 |1,834 |
| Standard_GS4 |16 |1 |Intel Xeon E5-2698B v3 @ 2 GHz |84 |194,111 |4,735 |
| Standard_GS5 |32 |2 |Intel Xeon E5-2698B v3 @ 2 GHz |84 |357,396 |16,228 |

## <a name="h-series"></a>H 시리즈
| 크기 | vCPU | NUMA 노드 | CPU | 실행 | 반복 수/초 | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_H8 |8 |1 |Intel Xeon E5-2667 v3 @ 3.2 GHz |28 |140,782 |2,512 |
| Standard_H16 |16 |2 |Intel Xeon E5-2667 v3 @ 3.2 GHz |35 |275,289 |7,110 |
| Standard_H18m |8 |1 |Intel Xeon E5-2667 v3 @ 3.2 GHz |28 |139,071 |3,988 |
| Standard_H16m |16 |2 |Intel Xeon E5-2667 v3 @ 3.2 GHz |28 |275,988 |6,963 |
| Standard_H16r |16 |2 |Intel Xeon E5-2667 v3 @ 3.2 GHz |28 |273,982 |6,069 |
| Standard_H16mr |16 |2 |Intel Xeon E5-2667 v3 @ 3.2 GHz |28 |274,523 |5,698 |

## <a name="about-coremark"></a>CoreMark 정보
Linux 숫자는 Ubuntu에서 [CoreMark](http://www.eembc.org/coremark/faq.php) 를 실행하여 계산됩니다. CoreMark hello 스레드 toohello 일정 개수의 가상 Cpu 수로 구성 된 하 고 동시성 tooPThreads를 설정 합니다. hello 대상 수의 반복 예상 되는 성능 tooprovide 20 초 이상 (일반적으로 훨씬 더 긴)의 런타임에 따라 조정 되었습니다. hello 최종 점수 hello 반복 횟수를 완료 toorun hello 테스트는 데 걸린 시간 (초) hello 수로 나눈 값을 나타냅니다. 각 테스트는 각 VM에서 적어도 7번 실행되었습니다. 테스트 (제외 하 고 여러 vm에서 VM을 실행 하는 hello 날짜에에 지원 된 모든 공용 Azure 지역 hello H series_ 2015 년 10 월에에서 실행 된 합니다.

## <a name="next-steps"></a>다음 단계
* 저장 용량, 디스크 세부 정보 및 VM 크기 선택시 추가적인 고려 사항에 관한 자세한 내용은 [가상 컴퓨터의 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.
* Linux Vm에서 toorun hello CoreMark 스크립트 다운로드 hello [스크립트 팩 CoreMark](http://download.microsoft.com/download/3/0/5/305A3707-4D3A-4599-9670-AAEB423B4663/AzureCoreMarkScriptPack.zip)합니다.

