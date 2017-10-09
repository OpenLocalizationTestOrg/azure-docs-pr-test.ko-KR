---
title: "Azure에서 aaaWindows VM의 크기를 조정 | Microsoft Docs"
description: "Azure에서 Windows 가상 컴퓨터에 사용할 수 있는 hello 다른 크기를 나열합니다."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a>Azure에서 Windows 가상 컴퓨터에 대한 크기

이 문서는 hello 사용 가능한 크기에 설명 하 고 옵션을 hello에 대 한 Azure 가상 컴퓨터를 Windows 응용 프로그램 및 작업 toorun를 사용할 수 있습니다. 또한 이러한 리소스 toouse를 계획 하 고 있는 경우 배포 고려 사항 toobe 인식를 제공 합니다.  이 문서는 [Linux 가상 컴퓨터](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에도 적용됩니다.


| 형식                     | 크기           |    설명       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [범용](sizes-general.md)          | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7 | CPU 대 메모리 비율이 적당합니다. 테스트 및 개발, 작은 toomedium 데이터베이스 및 낮은 toomedium 트래픽이 웹 서버에 적합 합니다. |
| [Compute에 최적화](sizes-compute.md)        | Fs, F             | CPU 대 메모리 비율이 높습니다. 트래픽이 중간 정도인 웹 서버, 네트워크 어플라이언스, 일괄 처리 프로세스 및 응용 프로그램 서버에 적합합니다.        |
| [메모리에 최적화](../virtual-machines-windows-sizes-memory.md)         | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | 메모리 대 CPU 비율이 높습니다. 관계형 데이터베이스 서버, 중간 toolarge 캐시 및 메모리 내 분석에 매우 유용 합니다.                 |
| [Storage에 최적화](../virtual-machines-windows-sizes-storage.md)        | Ls                | 높은 디스크 처리량 및 IO 빅 데이터, SQL, NoSQL 데이터베이스에 적합합니다.                                                         |
| [GPU](sizes-gpu.md)            | NV, NC            | 대량의 그래픽 렌더링 및 비디오 편집에 적합한 전문 가상 컴퓨터로, 한 개 이상의 GPU를 사용할 수 있습니다.       |
| [고성능 계산](sizes-hpc.md) | H, A8-11          | Microsoft의 가장 빠르고 강력한 CPU 가상 컴퓨터로, 필요한 경우 처리량이 높은 네트워크 인터페이스(RDMA)도 제공합니다. 

<br> 

- 다양 한 크기의 hello 가격에 대 한 정보를 참조 하십시오. [가상 컴퓨터 가격](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)합니다. 
- Azure Vm에서 일반적인 제한 사항이 toosee 참조 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../../azure-subscription-service-limits.md)합니다.
- 저장소 비용이 hello 저장소 계정에 사용 되는 페이지 기반 별도로 계산 됩니다. 자세한 내용은 [Azure Storage 가격 책정](https://azure.microsoft.com/pricing/details/storage/)을 참조하세요.
- [ACU(Azure Compute 단위)](acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.



## <a name="rest-api"></a>Rest API

VM 크기에 대 한 REST API tooquery hello를 사용 하는 방법은 hello 다음을 참조 합니다.

- [크기 조정에 사용 가능한 가상 컴퓨터 크기 나열](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [구독에 사용 가능한 가상 컴퓨터 크기 나열](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [가용성 집합에서 사용 가능한 가상 컴퓨터 크기 나열](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a>ACU

[ACU(Azure Compute 단위)](acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.

## <a name="next-steps"></a>다음 단계

사용할 수 있는 hello 다른 VM 크기에 대 한 자세한 정보:
- [범용](sizes-general.md)
- [Compute에 최적화](sizes-compute.md)
- [메모리에 최적화](../virtual-machines-windows-sizes-memory.md)
- [Storage에 최적화](../virtual-machines-windows-sizes-storage.md)
- [GPU에 최적화](sizes-gpu.md)
- [고성능 계산](sizes-hpc.md)



