---
title: "클라우드 서비스 할당 실패 aaaTroubleshooting | Microsoft Docs"
description: "Azure에서 클라우드 서비스 배포 시 할당 실패 문제 해결"
services: azure-service-management, cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 529157eb-e4a1-4388-aa2b-09e8b923af74
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: dfd5cc4663ccc6ed1b27ca9df579182737363b0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-allocation-failure-when-you-deploy-cloud-services-in-azure"></a>Azure에서 클라우드 서비스 배포 시 할당 실패 문제 해결
## <a name="summary"></a>요약
인스턴스 tooa 클라우드 서비스를 배포 하거나 새 웹 또는 작업자 역할 인스턴스를 추가할 때 Microsoft Azure 계산 리소스를 할당 합니다. Hello Azure 구독 제한에 도달 하기 전에도 이러한 작업을 수행 하는 경우에 가끔 오류가 발생할 수 있습니다. 이 문서는 hello 원인을 hello 일반적인 할당 오류 중 일부에 대해 설명 하 고 해결할 수를 제안 합니다. 서비스의 hello 배포를 계획 하는 경우에 hello 정보 유용할 수 있습니다.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

### <a name="background--how-allocation-works"></a>배경 – 할당의 작동 원리
Azure 데이터 센터의 hello 서버 클러스터로 분할 됩니다. 여러 클러스터에서 새 클라우드 서비스 할당 요청을 시도합니다. Hello 첫 번째 인스턴스는 클라우드 서비스를 스테이징 또는 프로덕션), (에서 배포 tooa 클라우드 서비스 경우 고정 된 tooa 클러스터를 가져옵니다. Hello 클라우드 서비스에서에서 수행 될 hello 동일에 대 한 배포를 더 모든 클러스터입니다. 이 문서에서는 toothis "고정 된 tooa 클러스터"로 지칭 합니다. 아래의 다이어그램 1는 일반 할당 된 여러 개의 클러스터;에 시도의 hello 대/소문자를 보여 줍니다. 다이어그램 2는 고정 된 tooCluster 2 기존 클라우드 서비스 CS_1 여기서 hello가 있는 때문에 호스트 되는 할당의 hello 대/소문자를 보여 줍니다.

![할당 다이어그램](./media/cloud-services-allocation-failure/Allocation1.png)

### <a name="why-allocation-failure-happens"></a>할당 오류가 발생하는 이유
고정 된 tooa 클러스터 할당 요청을 사용 하는 경우 hello 사용 가능한 리소스 풀 제한 tooa 클러스터 이므로 리소스를 해제 하는 toofind 실패의 높은 가능성이 높습니다. 또한 할당 요청은 고정 된 tooa 클러스터 hello 유형의 요청한 리소스가 해당 클러스터에서 지원 되지 않습니다 되지만 hello 클러스터에는 무료 리소스 하는 경우에 요청이 실패 합니다. 아래의 다이어그램 3 고정된 할당 hello 유일한 후보 클러스터에 리소스를 해제 없기 때문에 실패 하는 hello 경우를 보여 줍니다. 다이어그램 4 hello 유일한 후보 클러스터를 지원 하지 않으므로 고정된 할당 실패 하는 hello 경우를 보여 줍니다. hello hello 클러스터에 리소스를 해제 하는 경우에 VM 크기를 요청 했습니다.

![고정된 할당 오류](./media/cloud-services-allocation-failure/Allocation2.png)

## <a name="troubleshooting-allocation-failure-for-cloud-services"></a>클라우드 서비스에 대한 할당 실패 문제 해결
### <a name="error-message"></a>오류 메시지
Hello 다음과 같은 오류 메시지가 표시 될 수 있습니다.

    "Azure operation '{operation id}' failed with code Compute.ConstrainedAllocationFailed. Details: Allocation failed; unable toosatisfy constraints in request. hello requested new service deployment is bound tooan Affinity Group, or it targets a Virtual Network, or there is an existing deployment under this hosted service. Any of these conditions constrains hello new deployment toospecific Azure resources. Please retry later or try reducing hello VM size or number of role instances. Alternatively, if possible, remove hello aforementioned constraints or try deploying tooa different region."

### <a name="common-issues"></a>일반적인 문제
다음은 발생 한 할당 요청 toobe 고정 된 tooa 단일 클러스터는 hello 일반적인 할당 시나리오입니다.

* 슬롯-tooStaging를 배포 슬롯 중 하나는 클라우드 서비스에 배포 하는 경우 다음 hello 전체 클라우드 서비스는 고정 된 tooa 특정 클러스터입니다.  이 hello 프로덕션 슬롯에 배포를 이미 있으면 다음 새 스테이징 배포 할당할 수 있습니다. 동일한 hello 프로덕션 슬롯으로 클러스터 hello에 것을 의미 합니다. Hello 클러스터 용량에 가까워졌습니다, hello 요청이 실패할 수 있습니다.
* 크기 조정-새 인스턴스가 tooan 기존 클라우드 서비스를 추가 해야에 할당할 hello 동일 클러스터 합니다.  작은 크기 조정 요청은 대부분 할당할 수 있지만 항상 가능한 것은 아닙니다. Hello 클러스터 용량에 가까워졌습니다, hello 요청이 실패할 수 있습니다.
* 선호도 그룹-hello 클라우드 서비스는 고정 된 tooan 선호도 그룹 하지 않는 한 새 배포 tooan 빈 클라우드 서비스 할당할 hello 패브릭으로 해당 지역에서 어떤 클러스터에 있습니다. Hello에 동일한 선호도 그룹을 시도 하는 배포 toohello 동일한 클러스터입니다. Hello 클러스터 용량에 가까워졌습니다, hello 요청이 실패할 수 있습니다.
* 선호도 그룹 vNet-오래 된 가상 네트워크 지역 대신 동률된 tooaffinity 그룹 였으며이 가상 네트워크에서 클라우드 서비스는 고정 된 toohello 선호도 그룹 클러스터 것. 배포 toothis 유형의 가상 네트워크는 고정 된 hello 클러스터에 시도 됩니다. Hello 클러스터 용량에 가까워졌습니다, hello 요청이 실패할 수 있습니다.

## <a name="solutions"></a>솔루션
1. 재배포 tooa 새 클라우드 서비스-이 솔루션 가능성이 toobe 성공적으로 해당 지역에서 모든 클러스터에서 hello 플랫폼 toochoose 수 있습니다.

   * Hello 작업 tooa 새 클라우드 서비스 배포  
   * Hello A 또는 CNAME 레코드 toopoint 트래픽 toohello 새 클라우드 서비스 업데이트
   * 0 트래픽이 toohello 이전 사이트, 되 면 hello 이전 클라우드 서비스를 삭제할 수 있습니다. 이 솔루션은 가동 중지 시간 없이 발생합니다.
2. 프로덕션과 스테이징 슬롯을 삭제 합니다.-이 솔루션은 기존 DNS 이름을 유지 되지만 사용 하면 가동 중지 시간 tooyour 응용 프로그램.

   * Hello 프로덕션 및 스테이징 기존 클라우드 서비스의 슬롯 hello 클라우드 서비스 비어 있도록 삭제 한 다음
   * Hello 기존 클라우드 서비스에 새 배포를 만듭니다. 이 tooallocation hello 지역에 있는 모든 클러스터에서 다시 시도 합니다. Hello 클라우드 서비스가 지원 되지 않음 동률된 tooan 선호도 그룹을 확인 합니다.
3. 예약 된 IP-이 솔루션은 유지 하면 기존 IP 주소, 되지만 사용 하면 가동 중지 시간 tooyour 응용 프로그램입니다.  

   * Powershell을 사용하여 기존 배포에 대한 ReservedIP 만들기

     ```
     New-AzureReservedIP -ReservedIPName {new reserved IP name} -Location {location} -ServiceName {existing service name}
     ```
   * 위 hello 서비스의 CSCFG에 새 ReservedIP hello 있는지 toospecify 만드는 # 2를 따릅니다.
4. 새 배포에 대한 선호도 그룹 제거 - 선호도 그룹은 더 이상 권장되지 않습니다. 새 클라우드 서비스 toodeploy 위의 # 1에 대 한 단계를 수행 합니다. 클라우드 서비스가 선호도 그룹에 없는지 확인합니다.
5. 지역 가상 네트워크-참조 tooa 변환 [어떻게 선호도 그룹 tooa 지역 가상 네트워크 (VNet)에서 toomigrate](../virtual-network/virtual-networks-migrate-to-regional-vnet.md)합니다.
