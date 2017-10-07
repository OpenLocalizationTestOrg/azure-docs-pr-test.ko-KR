---
title: "Azure 클라우드 서비스 컴퓨터 크기 aaaVirtual | Microsoft Docs"
description: "Azure 클라우드 서비스 웹 및 작업자 역할에 대 한 hello 다른 가상 컴퓨터 크기 (및 Id)를 나열합니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1127c23e-106a-47c1-a2e9-40e6dda640f6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 93d91a67afc352f3d18c31e0dd5cf976bf46350c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-cloud-services"></a>클라우드 서비스에 적합한 크기
이 항목에서는 hello 사용 가능한 크기 및 클라우드 서비스 역할 인스턴스 (웹 역할 및 작업자 역할)에 대 한 옵션에 설명 합니다. 또한 배포 고려 사항 toobe toouse 이러한 리소스를 계획할 때 주의 제공 합니다. 각 크기에 따라 [서비스 정의 파일](cloud-services-model-and-package.md#csdef)에 입력할 ID가 있습니다. 각 크기에 대 한 가격 hello에서 사용할 수 있는 [클라우드 서비스 가격](https://azure.microsoft.com/pricing/details/cloud-services/) 페이지.

> [!NOTE]
> toosee 관련 Azure 제한, 참조 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)
>
>

## <a name="sizes-for-web-and-worker-role-instances"></a>웹 및 작업자 역할 인스턴스에 적합한 크기
Azure에서 여러 표준 크기 toochoose가 있습니다. 이러한 크기 중 일부에 대한 고려 사항은 다음을 포함합니다.

* D 시리즈 Vm은 더 뛰어난 계산 기능과 임시 디스크 성능이 요구 하는 디자인 된 toorun 응용 프로그램. D 시리즈 Vm hello 임시 디스크에 대 한 빠른 프로세서, 더 높은 메모리 대 코어 비율, 및는 SSD (반도체 드라이브)를 제공합니다. 자세한 내용은 Azure 블로그의 hello에 hello 알림이 참조 [새 D 시리즈 가상 컴퓨터 크기](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/)합니다.
* Dv2 시리즈, 후속 toohello 원래 D 시리즈는 CPU가 더 강력한 기능입니다. hello Dv2 시리즈 CPU은 약 35 %hello 보다 더 빠르게 D 시리즈 CPU입니다. 에 기반 하는 hello 최신 세대 2.4 g h z Intel Xeon® E5-2673 v3 (Haswell) 프로세서 및 Intel 터보 증폭 기술 2.0 hello로 too3.1 g h z 위로 이동할 수 있습니다. hello Dv2 시리즈에 D 시리즈 hello으로 같은 메모리 및 디스크 구성 hello 합니다.
* G 시리즈 Vm hello 가장 많은 메모리를 제공 하 고 Intel Xeon E5 V3 제품군 프로세서가 있는 호스트에 실행 합니다.
* 다양 한 하드웨어 종류 및 프로세서에서 hello A 시리즈 Vm을 배포할 수 있습니다. hello 하드웨어에 배포 된 hello 하드웨어에 관계 없이 인스턴스를 실행 하는 hello에 대 한 toooffer 일관 된 프로세서 성능에 따라 hello 크기 제한 되었습니다. toodetermine hello 물리적 하드웨어가이 크기를 배포할 쿼리 hello 가상 하드웨어에서 hello 가상 컴퓨터 내에서.
* hello A0 크기는 과도 하 게 hello 실제 하드웨어에서 구독 합니다. 이 특정 크기에만 다른 고객 배포는 실행 중인 작업 hello 성능이 떨어질 수 있습니다. hello 상대적인 성능 주체 tooan 대략적인의 변동 15%, 예상 hello 기준으로 다음과 같습니다.

hello 가상 컴퓨터의 hello 크기 hello 가격에 영향을 줍니다. hello 크기 hello 가상 컴퓨터의 hello 처리, 메모리 및 저장소 용량을도 영향을 줍니다. 저장소 비용이 hello 저장소 계정에 사용 되는 페이지 기반 별도로 계산 됩니다. 자세한 내용은 [Cloud Services 가격 세부 정보](https://azure.microsoft.com/pricing/details/cloud-services/) 및 [Azure Storage 가격](https://azure.microsoft.com/pricing/details/storage/)을 참조하세요.

hello 다음 고려 사항에서 크기를 결정 하는 데 도움이 될 수 있습니다.

* hello A8 A11 및 H 시리즈 크기 라고 *계산 집약적인 인스턴스*합니다. 이러한 크기를 실행 하는 hello 하드웨어를 디자인 하 고 계산 집약적인에 맞게 최적화 및 네트워크 집약적 응용 프로그램, 고성능 컴퓨팅 HPC ()를 포함 하 여 클러스터 응용 프로그램, 모델링 및 시뮬레이션 합니다. hello A8 A11 시리즈 Intel Xeon E5-2670 @ 2.6 g h Z를 사용 하 고 hello H 시리즈 3.2 g h z @ Intel Xeon E5-2667 v3를 사용 합니다. 이 크기의 사용과 관련된 자세한 내용 및 고려 사항은 [고성능 계산 VM 크기](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.
* Dv2 시리즈, D 시리즈, G 시리즈는 더 빠른 CPU와 더 좋은 로컬 디스크 성능을 요구하거나 더 높은 메모리 요구량을 가진 응용 프로그램에 이상적입니다. 이들은 많은 엔터프라이즈급 응용 프로그램을 위한 강력한 조합을 제공합니다.
* 일부 hello Azure 데이터 센터에서 물리적 호스트의 수 있습니다 크기가 지원 되지 더 큰 가상 컴퓨터, 예: A5-A11 합니다. Hello 오류 메시지가 표시 될 수는 결과적으로, **실패 tooconfigure 가상 컴퓨터 {컴퓨터 이름}** 또는 **실패 toocreate 가상 컴퓨터 {컴퓨터 이름}** 는 기존 가상 컴퓨터 tooa 새 크기를 조정할 때 size; 2013 년 4 월 16 일; 이전에 만든 가상 네트워크에서 새 가상 컴퓨터 만들기 또는 새 가상 컴퓨터 tooan 기존 클라우드 서비스를 추가 합니다. 참조 [오류: "Failed tooconfigure 가상 컴퓨터"](https://social.msdn.microsoft.com/Forums/9693f56c-fcd3-4d42-850e-5e3b56c7d6be/error-failed-to-configure-virtual-machine-with-a5-a6-or-a7-vm-size?forum=WAVirtualMachinesforWindows) 각 배포 시나리오에 대 한 대안에 대 한 hello 지원 포럼에 있습니다.
* 구독은 hello 특정 크기 제품군에서 배포할 수 있는 코어 수가 제한도 될 수 있습니다. tooincrease 할당량에는 Azure 지원에 문의 합니다.

## <a name="performance-considerations"></a>성능 고려 사항
만들어져 hello Azure 계산 단위 (ACU) tooprovide Azure Sku 및 tooidentify 가능성이 가장 높은 toosatisfy 인 SKU에 따른 성능 (CPU) 계산을 비교 하는 방법의 hello 개념 성능이 필요 합니다.  ACU는 현재 100인 작은(Standard_A1) VM에서 표준화되고 다른 SKU는 모두 SKU가 표준 벤치 마크를 얼마나 빨리 실행할 수 있는지를 나타냅니다.

> [!IMPORTANT]
> hello ACU 지침일 뿐입니다. 작업에 대 한 hello 결과 달라질 수 있습니다.
>
>

<br>

| SKU 제품군 | ACU/코어 |
| --- | --- |
| [ExtraSmall](#a-series) |50 |
| [Small-ExtraLarge](#a-series) |100 |
| [A5-7](#a-series) |100 |
| [Standard_A1-8v2](#av2-series) |100 |
| [Standard_A2m-8mv2](#av2-series) |100 |
| [A8-A11](#a-series) |225* |
| [D1-14](#d-series) |160 |
| [D1-15v2](#dv2-series) |210 - 250* |
| [G1-5](#g-series) |180 - 240* |
| [H](#h-series) |290 - 300* |

으로 표시 된 ACUs는 * Intel® 터보 기술 tooincrease CPU 주기를 사용 하 고 성능 향상을 제공 합니다. hello hello 부스트 수 다 hello VM 크기, 작업 및 hello에서 실행 중인 다른 작업에 따라 동일한 호스트 합니다.

## <a name="size-tables"></a>테이블 크기 조정
hello 다음 표에서 보여 hello 크기 및 hello 용량을 제공 합니다.

* 저장소 용량 단위는 GiB(1024^3바이트) 단위로 표시됩니다. GB 단위로 측정 디스크 비교 때 (1000 ^3 바이트) toodisks GiB 단위로 측정 (1024 ^3) 기억 GiB에 지정 된 용량 숫자를 더 작은 나타날 수 있습니다. 예를 들어 1023GiB = 1098.4GB입니다.
* 디스크 처리량은 IOPS(초당 입/출력 작업 수) 및 MBps로 측정되며, MBps = 10^6바이트/초입니다.
* 데이터 디스크는 캐시된 모드 또는 캐시되지 않은 모드에서 작동할 수 있습니다. 캐시 된 데이터 디스크 작업에 대 한 hello 호스트 캐시 모드가 설정 되어 너무**ReadOnly** 또는 **ReadWrite**합니다. 캐시 되지 않은 데이터 디스크 작업에 대 한 hello 호스트 캐시 모드가 설정 되어 너무**None**합니다.
* 최대 네트워크 대역폭은 hello 최대 집계 된 대역폭 할당 한 VM 유형 마다 할당 된 것입니다. 최대 대역폭 hello hello 오른쪽 VM 유형 tooensure 적절 한 네트워크 용량을 선택 하기 위한 지침을 사용할 수를 제공 합니다. 낮음, 보통, 높음 및 매우 높은 사이 이동할 때는 hello 처리량이 적절 하 게 증가 합니다. 실제 네트워크 성능은 네트워크 및 응용 프로그램 부하, 응용 프로그램 네트워크 설정을 비롯한 여러 요인에 따라 달라집니다.

## <a name="a-series"></a>A 시리즈
| 크기            | CPU 코어 | 메모리: GiB  | 로컬 HDD: GiB       | 최대 NIC 수/네트워크 대역폭 |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| 매우 작음      | 1         | 0.768        | 20                   | 1/낮음 |
| 작음           | 1         | 1.75         | 225                  | 1/보통 |
| 중간          | 2         | 3.5 GB       | 490                  | 1/보통 |
| 큼           | 4         | 7            | 1000                 | 2/높음 |
| 매우 큼      | 8         | 14           | 2040                 | 4/높음 |
| A5              | 2         | 14           | 490                  | 1/보통 |
| A6              | 4         | 28           | 1000                 | 2/높음 |
| A7              | 8         | 56           | 2040                 | 4/높음 |

## <a name="a-series---compute-intensive-instances"></a>A-시리즈 - 계산 집약적 인스턴스
이 크기의 사용과 관련된 자세한 내용 및 고려 사항은 [고성능 계산 VM 크기](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.

| 크기            | CPU 코어 | 메모리: GiB  | 로컬 HDD: GiB       | 최대 NIC 수/네트워크 대역폭 |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| A8*             |8          | 56           | 1817                 | 2/높음 |
| A9*             |16         | 112          | 1817                 | 4/매우 높음 |
| A10             |8          | 56           | 1817                 | 2/높음 |
| A11             |16         | 112          | 1817                 | 4/매우 높음 |

\*RDMA 지원

## <a name="av2-series"></a>Av2 시리즈

| 크기            | CPU 코어 | 메모리: GiB  | 로컬 SSD: GiB       | 최대 NIC 수/네트워크 대역폭 |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_A1_v2  | 1         | 2            | 10                   | 1/보통                 |
| Standard_A2_v2  | 2         | 4            | 20                   | 2/보통                 |
| Standard_A4_v2  | 4         | 8            | 40                   | 4/높음                     |
| Standard_A8_v2  | 8         | 16           | 80                   | 8/높음                     |
| Standard_A2m_v2 | 2         | 16           | 20                   | 2/보통                 |
| Standard_A4m_v2 | 4         | 32           | 40                   | 4/높음                     |
| Standard_A8m_v2 | 8         | 64           | 80                   | 8/높음                     |


## <a name="d-series"></a>D 시리즈
| 크기            | CPU 코어 | 메모리: GiB  | 로컬 SSD: GiB       | 최대 NIC 수/네트워크 대역폭 |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_D1     | 1         | 3.5          | 50                   | 1/보통 |
| Standard_D2     | 2         | 7            | 100                  | 2/높음 |
| Standard_D3     | 4         | 14           | 200                  | 4/높음 |
| Standard_D4     | 8         | 28           | 400                  | 8/높음 |
| Standard_D11    | 2         | 14           | 100                  | 2/높음 |
| Standard_D12    | 4         | 28           | 200                  | 4/높음 |
| Standard_D13    | 8         | 56           | 400                  | 8/높음 |
| Standard_D14    | 16        | 112          | 800                  | 8/매우 높음 |

## <a name="dv2-series"></a>Dv2 시리즈
| 크기            | CPU 코어 | 메모리: GiB  | 로컬 SSD: GiB       | 최대 NIC 수/네트워크 대역폭 |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_D1_v2  | 1         | 3.5          | 50                   | 1/보통 |
| Standard_D2_v2  | 2         | 7            | 100                  | 2/높음 |
| Standard_D3_v2  | 4         | 14           | 200                  | 4/높음 |
| Standard_D4_v2  | 8         | 28           | 400                  | 8/높음 |
| Standard_D5_v2  | 16        | 56           | 800                  | 8/극히 높음 |
| Standard_D11_v2 | 2         | 14           | 100                  | 2/높음 |
| Standard_D12_v2 | 4         | 28           | 200                  | 4/높음 |
| Standard_D13_v2 | 8         | 56           | 400                  | 8/높음 |
| Standard_D14_v2 | 16        | 112          | 800                  | 8/극히 높음 |
| Standard_D15_v2 | 20        | 140          | 1,000                | 8/극히 높음 |

## <a name="g-series"></a>G 시리즈
| 크기            | CPU 코어 | 메모리: GiB  | 로컬 SSD: GiB       | 최대 NIC 수/네트워크 대역폭 |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_G1     | 2         | 28           | 384                  |1/높음 |
| Standard_G2     | 4         | 56           | 768                  |2/높음 |
| Standard_G3     | 8         | 112          | 1,536                |4/매우 높음 |
| Standard_G4     | 16        | 224          | 3,072                |8/극히 높음 |
| Standard_G5     | 32        | 448          | 6,144                |8/극히 높음 |

## <a name="h-series"></a>H 시리즈
Azure H 시리즈 가상 컴퓨터는 hello 다음 세대 고성능 컴퓨팅 Vm 분자 모델링 및 계산 유체 역학와 같은 고급 계산 요구를 목표로 합니다. 이러한 8 및 16 코어 Vm Intel Haswell E5 2667 V3 hello 프로세서 기술 DDR4 메모리 및 로컬 SSD 기반 저장소에 작성 됩니다.

또한 toohello 상당한 CPU 전원, hello H 시리즈는 FDR InfiniBand 및 몇 가지 메모리 구성 toosupport 메모리 집약적 계산 요구 사항을 사용 하 여 대기 시간이 짧은 RDMA 네트워킹에 대 한 다양 한 옵션을 제공 합니다.

| 크기            | CPU 코어 | 메모리: GiB  | 로컬 SSD: GiB       | 최대 NIC 수/네트워크 대역폭 |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_H8     | 8         | 56           | 1000                 | 8/높음 |
| Standard_H16    | 16        | 112          | 2000                 | 8/매우 높음 |
| Standard_H8m    | 8         | 112          | 1000                 | 8/높음 |
| Standard_H16m   | 16        | 224          | 2000                 | 8/매우 높음 |
| Standard_H16r*  | 16        | 112          | 2000                 | 8/매우 높음 |
| Standard_H16mr* | 16        | 224          | 2000                 | 8/매우 높음 |

\*RDMA 지원

## <a name="configure-sizes-for-cloud-services"></a>클라우드 서비스에 적합한 크기 구성
Hello에서 설명 하는 hello 서비스 모델의 일환으로 역할 인스턴스의 hello 가상 컴퓨터 크기를 지정할 수 있습니다 [서비스 정의 파일](cloud-services-model-and-package.md#csdef)합니다. hello 역할의 hello 크기 hello CPU 코어 수, hello 메모리 용량 및 인스턴스를 실행 하는 tooa 할당 되는 hello 로컬 파일 시스템 크기를 결정 합니다. 응용 프로그램의 리소스 요구 사항에 따라 hello 역할 크기를 선택 합니다.

역할 크기 toobe hello를 설정 하기 위한 예로 [Standard_D2](#general-purpose-d) 웹 역할 인스턴스에 대 한 합니다.

```xml
<WorkerRole name="Worker1" vmsize="Standard_D2">
...
</WorkerRole>
```

## <a name="changing-hello-size-of-an-existing-role"></a>기존 역할의 hello 크기 변경

작업의 변동 또는 사용할 수 있게 하는 새 VM 크기의 hello 본질적으로 toochange hello 크기인 사용자의 역할을 할 수 있습니다. toodo 하므로 (위와 같이) 서비스 정의 파일에 hello VM 크기를 변경, 사용자가 클라우드 서비스를 다시 패키지 및 배포 해야 합니다. Hello 포털 또는 PowerShell에서 직접 가능한 toochange VM 크기는 없습니다.

>[!TIP]
> 다양 한 환경에서 사용자 역할에 대 한 않음 (예: toouse 다른 VM 크기를 사용할 수 있습니다. 테스트 및 프로덕션). 한 가지 방법은 toodo이 toocreate 프로젝트에서 여러 서비스 정의 (.csdef) 파일은 다음 패키지를 만들 다른 클라우드 서비스 환경당 hello CSPack 도구를 사용 하 여 자동화 된 빌드 중 합니다. 클라우드의 hello 요소에 대해 자세히 toolearn 서비스 패키지 toocreate, 참조 및 [hello 클라우드 서비스 기능 모델을 패키지 하는 방법을?](cloud-services-model-and-package.md)
>
>

## <a name="get-a-list-of-sizes"></a>크기 목록 가져오기
PowerShell 또는 REST API tooget 크기의 목록 hello를 사용할 수 있습니다. hello REST API는 문서화 [여기](https://msdn.microsoft.com/library/azure/dn469422.aspx)합니다. hello 다음 코드는 클라우드 서비스에 대 한 현재 사용할 수 있는 모든 hello 크기를 나열 하는 PowerShell 명령입니다.

```powershell
Get-AzureRoleSize | where SupportedByWebWorkerRoles -eq $true | select InstanceSize
```

## <a name="next-steps"></a>다음 단계
* [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)에 대해 자세히 알아보세요.
* 자세한 내용은 HPC 워크로드의 [고성능 계산 VM 크기](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에 대해 자세히 알아보세요.
