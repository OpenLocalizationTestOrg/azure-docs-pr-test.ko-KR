---
title: "aaaResource Manager 및 클래식 배포 | Microsoft Docs"
description: "Hello hello 리소스 관리자 배포 모델 및 hello 클래식 (또는 서비스 관리) 간의 차이점 배포 모델에 설명 합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7ae0ffa3-c8da-4151-bdcc-8f4f69290fb4
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: tomfitz
ms.openlocfilehash: fbf1959991b100547a459bf88a29c0afbc8592e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-vs-classic-deployment-understand-deployment-models-and-hello-state-of-your-resources"></a>Azure 리소스 관리자 및 클래식 배포: 배포 모델을 이해 하 고 리소스 상태를 hello
이 항목에서는 Azure Resource Manager 및 클래식 배포 모델, 리소스 hello 상태에 대 한 설명 및 리소스를 하나 또는 다른 hello로 배포 된 이유입니다. 리소스 관리자 hello 및 클래식 배포 모델 배포 및 관리 Azure 솔루션의 두 가지 방법으로 나타냅니다. 서로 다른 두 API 집합을 통해을 사용 하 고 배포 된 hello 리소스에는 중요 한 차이점이 포함 될 수 있습니다. hello 두 모델이 완전히 서로 호환 되지 않습니다. 이 항목에서는 이러한 차이점을 설명합니다.

toosimplify hello 배포 및 리소스 관리에는 모든 새 리소스에 대 한 리소스 관리자를 사용 하는 것이 좋습니다. 가능하면 기존 리소스도 Resource Manager를 통해 다시 배포하는 것이 좋습니다.

새 tooResource 관리자 인 경우 hello에 정의 된 toofirst 검토 hello 용어 [Azure 리소스 관리자 개요](resource-group-overview.md)합니다.

## <a name="history-of-hello-deployment-models"></a>Hello 배포 모델의 기록
Azure는 원래만 hello 클래식 배포 모델을 제공 합니다. 이 모델에서는 각 리소스 존재 하지 독립적으로; 방법이 함께 toogroup 관련 리소스입니다. 솔루션 또는 응용 프로그램을 구성 하는 리소스를 추적 하 고 기억 toomanage toomanually 사용 했던 대신는 조정 된 방식으로 해당 합니다. 솔루션 toodeploy tooeither hello 클래식 포털을 통해 개별적으로 각 리소스를 만들거나 hello 올바른 순서로 모든 hello 리소스를 배포 하는 스크립트를 만들 했습니다. 솔루션 toodelete 했습니다 toodelete 각 리소스 개별적으로. 관련 리소스에 대한 액세스 제어 정책을 쉽게 적용 및 업데이트할 수 없었습니다. 마지막으로 리소스를 모니터링 하 고 대금 청구를 관리 하는 데 도움이 되는 용어를 사용 하 여 태그 tooresources toolabel을 적용 하지 못했습니다.

2014 년 Azure 리소스 그룹의 hello 개념 추가 리소스 관리자를 도입 했습니다. 리소스 그룹은 공통 수명 주기를 공유하는 리소스의 컨테이너입니다. hello 리소스 관리자 배포 모델에는 여러 가지 이점을 제공합니다.

* 배포, 관리 하 고 이러한 서비스를 개별적으로 처리 하지 않고 그룹에서 솔루션에 대 한 모든 hello 서비스를 모니터링할 수 있습니다.
* 수명 주기 내내 솔루션을 반복적으로 배포하며 안심하고 일관된 상태로 리소스를 배포할 수 있습니다.
* 리소스 그룹에 대 한 액세스 제어 tooall 리소스를 적용할 수 있습니다 및 새 리소스를 추가 toohello 리소스 그룹에 자동으로 해당 정책이 적용 됩니다.
* 태그를 적용할 수 tooresources toologically 구독에서 모든 hello 리소스를 구성 합니다.
* 솔루션에 대 한 개체 JSON (JavaScript Notation) toodefine hello 인프라를 사용할 수 있습니다. hello JSON 파일 리소스 관리자 템플릿을 라고 합니다.
* Hello 올바른 순서로 배포 되므로 리소스 간의 종속성을 hello를 정의할 수 있습니다.

리소스 관리자 요소가 추가 될 때 모든 리소스는 toodefault 리소스 그룹은 이전의 추가 되었습니다. 이제는 클래식 배포를 통해 리소스를 만들면 배포에서 해당 리소스 그룹을 지정 하지 않은 경우에 hello 리소스가 해당 서비스에 대 한 기본 리소스 그룹 내에서 자동으로 생성 됩니다. 그러나 리소스 그룹 내에 있는 것은 아닙니다 hello 리소스 변환 된 toohello 리소스 관리자 모델 되었음을 합니다. 각 서비스 hello hello 다음 섹션의 두 가지 배포 모델을 처리 하는 방법을 살펴보겠습니다. 

## <a name="understand-support-for-hello-models"></a>Hello 모델에 대 한 지원 이해
리소스에 대 한 배포 모델 toouse 어떤를 결정할 때는 세 가지 시나리오 toobe 알고 있습니다.

1. hello 서비스 리소스 관리자를 지원 하 고 하나의 형식만 제공 합니다.
2. hello 서비스 리소스 관리자를 지원 하지만 ¸ ¦ á ¦-리소스 관리자 기본입니다. 이 시나리오는 toovirtual 컴퓨터, 저장소 계정 및 가상 네트워크에만 적용 됩니다.
3. hello 서비스 리소스 관리자를 지원 하지 않습니다.

toodiscover 서비스 리소스 관리자를 지원 하는지 여부를 참조 [리소스 공급자 및 형식](resource-manager-supported-services.md)합니다.

Toouse hello 서비스 리소스 관리자를 지원 하지 않는 경우 클래식 배포를 사용 하 여 계속 해야 합니다.

Hello 서비스에서 리소스 관리자를 지원 하면 및 **않습니다** 가상 컴퓨터, 저장소 계정 또는 가상 네트워크를 복잡 한 문제 없이 리소스 관리자를 사용할 수 있습니다.

가상 컴퓨터, 저장소 계정 및 가상 네트워크를 통해 클래식 배포 hello 리소스를 만든 경우 계속 해야 toooperate에 클래식 작업을 통해. Hello 가상 컴퓨터, 저장소 계정 또는 가상 네트워크를 만든 경우 리소스 관리자 배포를 통해 리소스 관리자 작업을 사용 하 여를 계속 해야 합니다. 이러한 차이는 구독에서 Resource Manager 및 클래식 배포를 통해 만든 리소스가 혼합되는 경우에는 혼동을 줄 수 있습니다. 리소스의 이러한 조합은 hello 리소스 지원 하지 않기 때문에 예기치 않은 결과 만들 수 hello 이와 동일한 작업을 합니다.

경우에 따라 리소스 관리자 명령 클래식 배포를 통해 만든 리소스에 대 한 정보를 검색할 수 또는 클래식 리소스만 tooanother 리소스 그룹을 이동 하는 등 관리 작업을 수행할 수 있습니다. 하지만 이러한 경우 hello 종류가 리소스 관리자 작업을 지원 하는지 hello 인상을 지정 하지 않아야 합니다. 예를 들어 클래식 배포로 만든 가상 컴퓨터가 포함된 리소스 그룹이 있다고 가정합니다. Hello 다음 리소스 관리자 PowerShell 명령을 실행 하면:

```powershell
Get-AzureRmResource -ResourceGroupName ExampleGroup -ResourceType Microsoft.ClassicCompute/virtualMachines
```

Hello 가상 컴퓨터를 반환합니다.

```powershell
Name              : ExampleClassicVM
ResourceId        : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.ClassicCompute/virtualMachines/ExampleClassicVM
ResourceName      : ExampleClassicVM
ResourceType      : Microsoft.ClassicCompute/virtualMachines
ResourceGroupName : ExampleGroup
Location          : westus
SubscriptionId    : {guid}
```

그러나 리소스 관리자 cmdlet을 hello **Get AzureRmVM** 리소스 관리자를 통해 배포 된 가상 컴퓨터만 반환 합니다. hello 다음 명령을 반환 하지 않습니다 클래식 배포를 통해 만든 hello 가상 컴퓨터.

```powershell
Get-AzureRmVM -ResourceGroupName ExampleGroup
```

리소스 관리자를 통해 만든 리소스만이 태그를 지원합니다. 태그 tooclassic 리소스를 적용할 수 없습니다.

## <a name="resource-manager-characteristics"></a>리소스 관리자 특성
두 hello 이해 toohelp 모델, 리소스 관리자 유형의 hello 특징을 검토해 보겠습니다.

* Hello를 통해 만들어진 [Azure 포털](https://portal.azure.com/)합니다.
  
     ![Azure portal](./media/resource-manager-deployment-model/portal.png)
  
     계산, 저장소 및 네트워킹 리소스에 대 한 리소스 관리자 또는 기본 배포를 사용 하 여 hello 선택할을 수 있습니다. **리소스 관리자**를 선택합니다.
  
     ![리소스 관리자 배포](./media/resource-manager-deployment-model/select-resource-manager.png)
* Hello Azure PowerShell cmdlet의 hello 리소스 관리자 버전으로 만들어졌습니다. 이 명령은 hello 형식을 *동사 AzureRmNoun*합니다.

  ```powershell
  New-AzureRmResourceGroupDeployment
  ```

* Hello를 통해 만들어진 [Azure 리소스 관리자 REST API](https://docs.microsoft.com/rest/api/resources/) REST 작업에 대 한 합니다.
* Hello에서 실행 하는 Azure CLI 명령을 통해 만든 **arm** 모드입니다.
  
  ```azurecli
  azure config mode arm
  azure group deployment create
  ```

* hello 리소스 종류는 **(클래식)** hello 이름에서입니다. hello 다음 그림에 나와 hello 종류로 **저장소 계정**합니다.
  
    ![웹앱](./media/resource-manager-deployment-model/resource-manager-type.png)

## <a name="classic-deployment-characteristics"></a>클래식 배포 특성
또한 hello 서비스 관리 모델으로 hello 클래식 배포 모델을 알고 있습니다.

Hello 클래식 배포 모델 공유 hello 특성 뒤에 생성 된 리소스:

* Hello를 통해 만들어진 [클래식 포털](https://manage.windowsazure.com)
  
     ![클래식 포털](./media/resource-manager-deployment-model/classic-portal.png)
  
     또는 Azure 포털 hello 하 고 지정한 **클래식** 배포 (계산, 저장소, 네트워킹).
  
     ![클래식 배포](./media/resource-manager-deployment-model/select-classic.png)
* Hello 서비스 관리 버전의 hello Azure PowerShell cmdlet 통해 만들어집니다. 이러한 명령 이름에는 hello 형식 *동사 AzureNoun*합니다.

  ```powershell
  New-AzureVM
  ```

* Hello를 통해 만들어진 [서비스 관리 REST API](https://msdn.microsoft.com/library/azure/ee460799.aspx) REST 작업에 대 한 합니다.
* **asm** 모드에서 실행되는 Azure CLI 명령을 통해 생성되었습니다.

  ```azurecli
  azure config mode asm
  azure vm create
  ```
   
* hello 리소스 형식 포함 **(클래식)** hello 이름에서입니다. hello 다음 그림에 나와 hello 종류로 **저장소 계정 (클래식)**합니다.
  
    ![클래식 유형](./media/resource-manager-deployment-model/classic-type.png)

클래식 배포를 통해 생성 된 hello Azure 포털 toomanage 리소스를 사용할 수 있습니다.

## <a name="changes-for-compute-network-and-storage"></a>계산, 네트워크 및 저장소에 대한 변경
hello 다음 다이어그램에서는 리소스 관리자를 통해 배포 된 계산, 네트워크 및 저장소 리소스

![Resource Manager 아키텍처](./media/resource-manager-deployment-model/arm_arch3.png)

참고 hello hello 리소스 간의 관계를 따라:

* 리소스 그룹 내의 모든 hello 리소스가 없습니다.
* hello 가상 컴퓨터 구성 요소를 해당 디스크에서 blob 저장소 (필수) hello 저장소 리소스 공급자 toostore에 정의 된 특정 저장소 계정에 따라 달라 집니다.
* hello 가상 컴퓨터 (필수) hello 네트워크 리소스 공급자 및 가용성 집합 hello 계산 리소스 공급자에 정의 된 (선택 사항)에 정의 된 특정 NIC를 참조 합니다.
* hello NIC 참조 hello 가상 컴퓨터의 IP 주소 (필수), (필수), hello 가상 컴퓨터 및 네트워크 보안 그룹 (선택 사항) tooa hello 가상 네트워크의 서브넷을 hello에 할당 합니다.
* 가상 네트워크 내에서 hello 서브넷 네트워크 보안 그룹 (선택 사항)을 참조합니다.
* hello 부하 분산 장치 인스턴스 hello (선택 사항) 가상 컴퓨터의 NIC를 포함 하는 IP 주소의 hello 백 엔드 풀을 참조 하 고 부하 분산 장치 공개 또는 개인 IP 주소를 (선택 사항)를 참조 합니다.

다음은 hello 구성 요소 및 클래식 배포에 대 한 관계입니다.

![클래식 아키텍처](./media/resource-manager-deployment-model/arm_arch1.png)

가상 컴퓨터를 호스트 하기 위한 hello 클래식 솔루션에 포함 됩니다.

* 가상 컴퓨터 호스팅(계산)을 위한 컨테이너 역할을 하는 데 필요한 클라우드 서비스. 가상 컴퓨터는 NIC(네트워크 인터페이스 카드) 및 Azure에서 할당된 IP 주소와 함께 자동으로 제공됩니다. 또한 hello 클라우드 서비스에서는 외부 부하 분산 장치 인스턴스는 공용 IP 주소, 기본 끝점 tooallow 원격 데스크톱 및 원격 PowerShell 트래픽 Windows 기반 가상 컴퓨터에 대 한 캡슐화 된 트래픽과 SSH (보안 셸)에 대 한 Linux ± â 가상 컴퓨터입니다.
* 저장소, 임시 및 추가 데이터 디스크 (저장소) hello 운영 체제를 포함 하 여 가상 컴퓨터에 대 한 Vhd를 hello 필요한 저장소 계정입니다.
* 서브넷된 구조를 만들 고 hello는 hello에 가상 컴퓨터가 위치한 서브넷을 지정할 수 있는 추가 컨테이너 역할을 하는 선택적 가상 네트워크 (네트워크).

다음 표에서 hello 계산, 네트워크 및 저장소 리소스 공급자 상호 작용 하는 방법에 대 한 변경 내용을 설명 합니다.

| 항목 | 클래식 | 리소스 관리자 |
| --- | --- | --- |
| 가상 컴퓨터용 클라우드 서비스 |클라우드 서비스에서 가용성 hello 플랫폼 및 부하 분산에서 필요한 hello 가상 컴퓨터를 보관 하기 위한 컨테이너입니다. |클라우드 서비스는 더 이상 hello 새 모델을 사용 하 여 가상 컴퓨터를 만드는 데 필요한 개체입니다. |
| 가상 네트워크 |가상 네트워크 hello 가상 컴퓨터에 대 한 선택 사항입니다. 포함 하는 경우 hello 가상 네트워크와 리소스 관리자를 배포할 수 없습니다. |가상 컴퓨터에 Resource Manager에서 배포한 가상 네트워크가 필요합니다. |
| 저장소 계정 |hello 가상 컴퓨터 hello 운영 체제, 임시 및 추가 데이터 디스크에 대 한 hello Vhd를 저장 하는 저장소 계정이 필요 합니다. |hello 가상 컴퓨터에서 blob 저장소의 디스크를 저장소 계정 toostore 필요합니다. |
| 가용성 집합 |가용성 toohello 플랫폼을 구성 하 여 지정 된 hello 가상 컴퓨터에서 동일한 "AvailabilitySetName" hello 합니다. hello 최대 장애 도메인 수는 2입니다. |가용성 집합은 Microsoft.Compute 공급자가 표시하는 리소스입니다. 고가용성을 요구 하는 가상 컴퓨터는 hello 가용성 집합에 포함 되어야 합니다. hello 최대 개수가 오류 도메인은 이제 3입니다. |
| 선호도 그룹 |선호도 그룹은 가상 네트워크를 만드는 데 필요했습니다. 그러나 지역 가상 네트워크의 hello 도입으로 사용 하는 필요 하지 않습니다 더 이상. |toosimplify, hello 선호도 그룹 개념 hello Azure 리소스 관리자를 통해 노출 된 Api에에서 존재 하지 않습니다. |
| 부하 분산 |클라우드 서비스를 만들지 hello 배포 된 가상 컴퓨터에 대 한 암시적 부하 분산을 제공 합니다. |hello 부하 분산 장치는 hello Microsoft.Network 공급자가 제공 하는 리소스입니다. hello에 필요한 toobe 부하 분산 된 가상 컴퓨터의 주 네트워크 인터페이스만 hello hello 부하 분산 장치를 참조 해야 합니다. 부하 분산 장치는 내부 또는 외부에 있을 수 있습니다. 부하 분산 장치 인스턴스 hello (선택 사항) 가상 컴퓨터의 NIC를 포함 하는 IP 주소의 hello 백 엔드 풀을 참조 하 고 부하 분산 장치 공개 또는 개인 IP 주소를 (선택 사항)를 참조 합니다. [자세한 정보](../virtual-network/resource-groups-networking.md) |
| 가상 IP 주소 |클라우드 서비스 VM을 tooa 클라우드 서비스를 추가 하는 경우 기본 VIP을 (가상 IP 주소)를 가져옵니다. hello 가상 IP 주소는 hello 암시적 부하 분산 장치와 관련 된 hello 주소입니다. |공용 IP 주소는 hello Microsoft.Network 공급자가 제공 하는 리소스입니다. 공용 IP 주소는 고정(예약된) 또는 동적일 수 있습니다. 부하 분산 장치 tooa 동적 공용 Ip은 할당할 수 있습니다. 보안 그룹을 사용하여 공용 IP의 보안을 유지할 수 있습니다. |
| 예약된 IP 주소 |Azure와 hello IP 주소는 클라우드 서비스 tooensure와 팀 멤버는 연결의 IP 주소를 예약할 수 있습니다. |공용 IP 주소를 만들 수 있습니다 "정적" 모드에서 제안을 hello "예약 된 IP 주소"와 동일한 기능입니다. 고정 공용 Ip만 할당할 수 tooa 부하 분산 장치 지금 바로 합니다. |
| VM당 PIP(공용 IP 주소) |공용 IP 주소 연결된 tooa VM에 직접 될 수도 있습니다. |공용 IP 주소는 hello Microsoft.Network 공급자가 제공 하는 리소스입니다. 공용 IP 주소는 고정(예약된) 또는 동적일 수 있습니다. 그러나 동적 공용 Ip만 할당 된 tooa 네트워크 인터페이스 tooget VM 당 공용 IP를 지금 바로 수 있습니다. |
| 끝점 |가상 컴퓨터 toobe에 구성 된 입력된 끝점 필요한 toobe 특정 포트에 대 한 연결을 엽니다. 입력된 끝점을 설정 하 여 수행 toovirtual 컴퓨터를 연결 하는 hello 일반 모드 중 하나입니다. |부하 분산 장치 인바운드 NAT 규칙을 구성할 수 있습니다 tooachieve hello 동일한 기능 toohello Vm을 연결 하기 위한 특정 포트의 끝점을 사용 하도록 설정 합니다. |
| DNS 이름 |클라우드 서비스는 전역적으로 고유한 암시적 DNS 이름을 가져옵니다. 예: `mycoffeeshop.cloudapp.net` |DNS 이름은 공용 IP 주소 리소스에 지정할 수 있는 선택적 매개 변수입니다. hello FQDN은 다음 예제 hello 형식- `<domainlabel>.<region>.cloudapp.azure.com`합니다. |
| 네트워크 인터페이스 |기본 및 보조 네트워크 인터페이스와 해당 속성이 가상 컴퓨터의 네트워크 구성으로 정의되었습니다. |네트워크 인터페이스는 Microsoft.Network 공급자가 표시하는 리소스입니다. 네트워크 인터페이스가 아니므로 hello의 hello 수명 주기 tooa 가상 컴퓨터를 연결 합니다. Hello 가상 컴퓨터의 할당 된 IP 주소 (필수), (필수), hello 가상 컴퓨터 및 네트워크 보안 그룹 (선택 사항) tooa hello 가상 네트워크의 서브넷을 hello 참조 합니다. |

다양 한 배포 모델에서 가상 네트워크에 연결 하는 방법에 대 한 toolearn 참조 [hello 포털의 다양 한 배포 모델에서 가상 네트워크를 연결할](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md)합니다.

## <a name="migrate-from-classic-tooresource-manager"></a>클래식 tooResource 관리자에서 마이그레이션
준비 toomigrate 모르는 경우 클래식 배포 tooResource 관리자 배포에서에서 리소스를 참조 하세요.

1. [클래식 tooAzure 리소스 관리자에서에서 마이그레이션 플랫폼 지원에 기술 심층 분석](../virtual-machines/windows/migration-classic-resource-manager-deep-dive.md)
2. [플랫폼이는 클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 지원](../virtual-machines/windows/migration-classic-resource-manager-overview.md)
3. [Azure PowerShell을 사용 하 여 IaaS 리소스 클래식 tooAzure 리소스 관리자에서 마이그레이션](../virtual-machines/windows/migration-classic-resource-manager-ps.md)
4. [Azure CLI를 사용 하 여 IaaS 리소스 클래식 tooAzure 리소스 관리자에서 마이그레이션](../virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md)

## <a name="frequently-asked-questions"></a>질문과 대답
**Azure 리소스 관리자 toodeploy 클래식 배포를 사용 하 여 만든 가상 네트워크에서 사용 하 여 가상 컴퓨터를 만들 수 있습니까?**

이 기능은 지원되지 않습니다. 클래식 배포를 사용 하 여 만든 가상 네트워크에 Azure 리소스 관리자 toodeploy 가상 컴퓨터를 사용할 수 없습니다.

**에서 만들 수 있나요 hello를 사용 하 여 가상 컴퓨터를 Azure 리소스 관리자 hello Azure 서비스 관리 Api를 사용 하 여 만들어진 사용자 이미지?**

이 기능은 지원되지 않습니다. 그러나 hello 서비스 관리 Api를 사용 하 여 만든 저장소 계정에서 hello VHD 파일을 복사 하 고 Azure 리소스 관리자를 통해 만든 tooa 새 계정을 추가할 수 있습니다.

**내 구독에 대 한 hello 할당량에 미치는 영향을 hello 이란?**

hello 가상 컴퓨터, 가상 네트워크 및 hello Azure 리소스 관리자를 통해 생성 된 저장소 계정에 대 한 hello 할당량의 다른 할당량과와에서 구분 됩니다. 각 구독 가져옵니다 할당량 toocreate hello 리소스를 사용 하 여 hello 새로운 Api입니다. 자세한 내용은 hello 추가 할당량에 대 한 [여기](../azure-subscription-service-limits.md)합니다.

**계속 toouse 가상 컴퓨터, 가상 네트워크 및 hello 리소스 관리자 Api를 통해 저장소 계정 구축에 대 한 자동화 된 스크립트 합니까?**

모든 hello 자동화 및 스크립트를 빌드 했으므로 toowork hello 기존 가상 컴퓨터, hello Azure 서비스 관리 모드에서 만든 가상 네트워크를 계속 합니다. 그러나 hello 스크립트가 toobe 업데이트 toouse hello hello hello 리소스 관리자 모드를 통해 동일한 리소스를 만들기 위한 새 스키마를 보유 합니다.

**Azure 리소스 관리자 템플릿 예제는 어디서 찾을 수 있습니까?**

[Azure Resource Manager 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/)에서 포괄적인 시작 템플릿 집합을 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계
* 가상 컴퓨터, 저장소 계정 및 가상 네트워크에서 참조를 정의 하는 템플릿의 hello 작성을 통해 toowalk [리소스 관리자 템플릿 연습](resource-manager-template-walkthrough.md)합니다.
* 서식 파일을 배포 하기 위한 toosee hello 명령을 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.

