---
title: "aaaMove Azure 리소스 toonew 구독 또는 리소스 그룹이 | Microsoft Docs"
description: "Azure 리소스 관리자 toomove 리소스 tooa 새 리소스 그룹이 나 구독을 사용 합니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a>구독 또는 리소스 toonew 리소스 그룹 이동
이 항목에서는 방법을 toomove 리소스 tooeither 새 구독 또는 새 리소스 그룹 hello에 동일한 구독 합니다. Hello 포털, PowerShell, Azure CLI 또는 hello REST API toomove 리소스를 사용할 수 있습니다. 이 항목의 hello 이동 작업은 Azure 지원 담당자의 모든 지원 없이 사용할 수 있는 tooyou 합니다.

리소스를 이동할 때는 hello 소스 그룹과 hello 대상 그룹을 모두 hello 작업 동안 잠깁니다. 쓰기 및 삭제 작업 hello 이동이 완료 될 때까지 hello 리소스 그룹에서 차단 됩니다. 이 잠금에는 의미가 hello 리소스가 고정 되어 있지만 추가, 업데이트 또는 hello 리소스 그룹에 리소스를 삭제할 수 없습니다 의미 합니다. 예를 들어 SQL Server와 데이터베이스 tooa 새 리소스 그룹을 이동 하면 hello 데이터베이스를 사용 하는 응용 프로그램에 가동 중지 시간 없이 발생 합니다. 여전히 읽기 및 toohello 데이터베이스 쓰기 수입니다.

Hello 리소스의 hello 위치를 변경할 수 없습니다. Tooa 새 리소스 그룹을 이동만 리소스를 이동 합니다. hello 새 리소스 그룹의 다른 위치를 할 수 있지만 hello 리소스의 hello 위치를 변경 되지 않습니다.

> [!NOTE]
> 이 문서에서는 기존 Azure 내에서 toomove 리소스 계정 라는 메시지가 나타나지 방법을 설명 합니다. 리소스를 사용 하 여 기존 리소스와 toowork 줄이면서 (예: 종 량 제 toopre 지불에서 업그레이드)를 제공 하 여 Azure 계정 참조 하는 경우 실제로 원하는 toochange [Azure 구독 tooanother 제안을 전환](../billing/billing-how-to-switch-azure-offer.md)합니다.
>
>

## <a name="checklist-before-moving-resources"></a>리소스를 이동하기 전의 검사 목록
리소스 이동 하기 전에 몇 가지 중요 한 단계 tooperform이 있습니다. 이러한 조건을 확인하면 오류를 방지할 수 있습니다.

1. hello 원본 및 대상 구독 내에 있어야 hello 동일 [Azure Active Directory 테 넌 트](../active-directory/active-directory-howto-tenant.md)합니다. 동일한 두 구독 hello가 toocheck 테 넌 트 ID, Azure PowerShell 또는 Azure CLI를 사용 합니다.

  Azure PowerShell의 경우 다음을 사용합니다.

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  Azure CLI 2.0의 경우 다음을 사용합니다.

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  Hello에 대 한 Id 테 넌 트 하는 경우 동일한 hello, hello 구독에 대 한 toochange hello 디렉터리를 시작할 수 있습니다. hello 원본 및 대상 구독 하지 않습니다. 그러나이 옵션은 사용 가능한 tooService 관리자에 게 Microsoft 계정 (조직 계정이 아님)로 로그인 하는 합니다. tooattempt toohello 로그인 hello 디렉터리를 변경 하 고 [클래식 포털](https://manage.windowsazure.com/)를 선택 하 고 **설정**, hello 구독을 선택 하 고 있습니다. 경우 hello **디렉터리 편집** 아이콘을 사용할 수 있는 toochange 선택 hello Azure Active Directory에 연결 합니다.

  ![디렉터리 편집](./media/resource-group-move-resources/edit-directory.png)

  이 아이콘을 사용할 수 없는 경우 지원 toomove hello 리소스 tooa 새 테 넌 트에 게 문의 해야 합니다.

2. hello 서비스는 hello 기능 toomove 리소스 사용 하도록 설정 해야 합니다. 이 항목에서는 리소스 이동이 가능한 서비스와 그렇지 않은 서비스 목록을 보여 줍니다.
3. hello 대상 구독 hello 리소스 이동의 hello 리소스 공급자에 대 한 등록 되어야 합니다. 해당 hello 라는 오류가 나타나면 not, **리소스 종류에 대 한 구독이 등록 되지 않습니다**합니다. 리소스 tooa 새 구독을 이동할 때이 문제를 발생할 수 있지만 해당 리소스 종류와 해당 구독 사용 되지 않은 합니다. toolearn toocheck 등록 상태를 hello 및 리소스 공급자를 등록 하는 방법 참조 [리소스 공급자 및 형식](resource-manager-supported-services.md)합니다.

## <a name="when-toocall-support"></a>Toocall를 지 원하는 경우
이 항목에 표시 된 hello 셀프 서비스 작업을 통해 가장 많은 리소스를 이동할 수 있습니다. Hello 셀프 서비스 작업을 사용 합니다.

* Resource Manager 리소스를 이동합니다.
* 클래식 리소스 toohello에 따라 이동 [클래식 배포 제한 사항](#classic-deployment-limitations)합니다.

다음을 수행해야 할 때 지원을 호출합니다.

* 리소스 tooa 새 Azure 계정 (및 Azure Active Directory 테 넌 트)를 이동 합니다.
* 클래식 리소스를 이동 하지만 hello 제한 되는 동안 문제가 발생 합니다.

## <a name="services-that-enable-move"></a>이동을 사용하는 서비스
지금은 이동 tooboth 새 리소스 그룹 및 구독을 사용할 수 있는 서비스는 hello 다음과 같습니다.

* API 관리
* 앱 서비스 앱(웹앱) - [앱 서비스 제한](#app-service-limitations)
* Application Insights
* 자동화
* 배치
* Bing 지도
* CDN
* 클라우드 서비스 - [클래식 배포 제한 사항](#classic-deployment-limitations)
* Cognitive Services
* Content Moderator
* 데이터 카탈로그
* 데이터 팩터리
* 데이터 레이크 분석
* 데이터 레이크 저장소
* DNS
* Azure Cosmos DB
* Event Hubs
* HDInsight 클러스터 - [HDInsight 제한 사항](#hdinsight-limitations) 참조
* IoT Hub
* 키 자격 증명 모음
* 부하 분산 장치
* Logic Apps
* 기계 학습
* 미디어 서비스
* 모바일 고객 관리
* 알림 허브
* Operational Insights
* 운영 관리
* Power BI
* Redis 캐시
* 스케줄러
* 검색
* 서버 관리
* 서비스 버스
* 서비스 패브릭
* 저장소
* 저장소(클래식) - [클래식 배포 제한 사항](#classic-deployment-limitations)
* Stream Analytics - 실행 중 상태일 때는 Stream Analytics 작업을 이동할 수 없습니다.
* SQL 데이터베이스 서버-hello 데이터베이스 및 서버에에서 있어야 hello 동일한 리소스 그룹입니다. SQL Server를 이동하면 모든 해당 데이터베이스도 함께 이동합니다.
* 트래픽 관리자
* 가상 컴퓨터
* 주요 자격 증명 모음-toonew 같은 구독에서 리소스 그룹 이동에에서 저장 된 인증서로 가상 컴퓨터를 사용 하지만 구독 간 이동 사용 되지 않습니다.
* 가상 컴퓨터(클래식) - [클래식 배포 제한 사항](#classic-deployment-limitations)
* 가상 컴퓨터 확장 집합
* Virtual Networks - 현재 피어링된 Virtual Network는 VNet 피어링을 사용하지 않도록 설정할 때까지 이동할 수 없습니다. 한 번 해제, 가상 네트워크를 성공적으로 이동할 수 있는 hello 그리고 hello VNet 피어 링을 설정할 수 있습니다. 또한 가상 네트워크는 hello 가상 네트워크에 어떤 서브넷 리소스 탐색 링크로 포함 된 경우 이동된 tooa 다른 구독 일 수 없습니다. 예를 들어, Virtual Network 서브넷은 Microsoft.Cache redis 리소스가 이 서브넷에 배포된 경우 리소스 탐색 링크를 포함합니다.
* VPN 게이트웨이


## <a name="services-that-do-not-enable-move"></a>이동을 사용하지 않는 서비스
현재 사용 하지 않는 리소스를 이동 하는 hello 서비스는 같습니다.

* AD Domain Services
* AD 하이브리드 상태 관리 서비스
* Application Gateway
* Managed Disks를 포함하는 Virtual Machines의 가용성 집합
* BizTalk 서비스
* 컨테이너 서비스
* Express 경로
* DevTest Labs-toonew 같은 구독에서 리소스 그룹 이동을 사용할 수 있지만 상호 구독 이동 사용 되지 않습니다.
* Dynamics LCS
* Managed Disks에서 만든 이미지
* Managed Disks
* Managed Applications
* 복구 서비스 자격 증명 모음-하지 hello 계산, 네트워크 및 저장소 리소스 이동 연관지 않습니다 복구 서비스를 hello도 자격 증명 모음을 참조 하십시오. [복구 서비스 제한 사항](#recovery-services-limitations)합니다.
* 보안
* Managed Disks에서 만든 스냅숏
* StorSimple 장치 관리자
* Managed Disks를 포함하는 가상 컴퓨터
* 가상 네트가상 네트워크(클래식) - [클래식 배포 제한 사항](#classic-deployment-limitations)
* Marketplace 리소스에서 만든 Virtual Machines는 구독 간에 이동할 수 없습니다. 리소스 toobe hello 현재 구독에 프로 비전을 해제 하 고 hello 새 구독에 다시 배포할 필요

## <a name="app-service-limitations"></a>앱 서비스 제한
앱 서비스 앱으로 작업할 경우에는 앱 서비스 계획만 이동할 수 없습니다. 옵션은 toomove 앱 서비스 앱:

* 해당 리소스 그룹 tooa 새 리소스 그룹에 없는 응용 프로그램 서비스 리소스 hello 앱 서비스 계획 및 다른 모든 앱 서비스 리소스를 이동 합니다. 이 요구 사항은 이동 해야 하는 방법에는 응용 프로그램 서비스 리소스 hello 연결 되지 않은 앱 서비스 계획 hello로 합니다.
* Hello 앱 tooa 다른 리소스 그룹을 이동 하지만 hello 원본 리소스 그룹에 모든 앱 서비스 계획을 유지 합니다.

hello 앱 서비스 계획에서 tooreside 않아도 hello 앱 toofunction hello에 대 한 hello 응용 프로그램으로 동일한 리소스 그룹 올바르게 합니다.

예를 들어 리소스 그룹에 다음 사항이 포함된 경우:

* **plan-a**와 연결된 **web-a**
* **plan-b**와 연결된 **web-b**

옵션은 다음과 같습니다.

* **web-a**, **plan-a**, **web-b** 및 **plan-b** 이동
* **web-a** 및 **web-b** 이동
* **web-a**
* **web-b**

다른 모든 조합에는 App Service 계획 이동 시 그대로 남겨 둘 수 없는 리소스 형식(App Service 리소스 형식)을 남겨두는 것이 있습니다.

를 웹 앱의 앱 서비스 계획 보다 다른 리소스 그룹에 상주 하지만 toomove tooa 새 리소스 그룹 모두를 원하는 경우에 두 단계로 hello 이동을 수행 해야 합니다. 예:

* **web-a**가 **web-group**에 상주하는 경우
* **plan-a**가 **plan-group**에 상주하는 경우
* 원하는 **웹 a** 및 **계획 a** 에 tooreside **결합 그룹**

tooaccomplish이 이동, 순서 따르면 hello에서 두 개의 별도 이동 작업을 수행 합니다.

1. Hello 이동 **웹 a** 너무**그룹 계획**
2. 이동 **웹 a** 및 **계획 a** 너무**결합 그룹**합니다.

앱 서비스 인증서 tooa 새 리소스 그룹 또는 아무 문제 없이 구독을 이동할 수 있습니다. 그러나 웹 응용 프로그램 외부에서 구매한 toohello 앱을 업로드 하는 SSL 인증서가 포함 된 경우 이동 hello 웹 응용 프로그램 하기 전에 hello 인증서를 삭제 해야 합니다. 예를 들어 hello 다음 단계를 수행할 수 있습니다.

1. Hello 웹 앱에서 업로드 하는 hello 인증서를 삭제 합니다.
2. Hello 웹 응용 프로그램 이동
3. 웹 응용 프로그램을 toohello hello 인증서 업로드

## <a name="recovery-services-limitations"></a>Recovery Services 제한 사항
저장소, 네트워크에 대 한 이동 가능 하지 또는 계산 리소스는 Azure Site Recovery와 tooset 재해 복구를 사용 합니다.

예를 들어 온-프레미스 컴퓨터 tooa 저장소 계정 (Storage1)의 복제 설정 가정 하 고 hello 보호 된 컴퓨터 toocome를 tooAzure 장애 조치 후 가상 컴퓨터 (v m 1) (네트워크 1) tooa 가상 네트워크를 연결 합니다. 이러한 Azure 리소스가-VM1, Storage1 이동할 수 없습니다 및 네트워크 1-리소스 간에 그룹 hello 내에서 동일한 구독 또는 구독 전반에 걸쳐 있습니다.

## <a name="hdinsight-limitations"></a>HDInsight 제한 사항

HDInsight 클러스터 tooa 새 구독 또는 리소스 그룹을 이동할 수 있습니다. 그러나 구독 hello 네트워킹 리소스 (예: hello 가상 네트워크, NIC 또는 부하 분산 장치) HDInsight 클러스터를 연결 된 toohello 간에 이동할 수 없습니다. 또한 tooa 새 리소스 그룹 hello 클러스터에 대 한 연결 된 tooa 가상 컴퓨터가 있는 NIC를 이동할 수 없습니다.

HDInsight 클러스터 tooa 새 구독을 이동할 때 먼저 다른 리소스 (예: hello 저장소 계정)를 이동 합니다. 그런 다음 자체적으로 hello HDInsight 클러스터를 이동 합니다.

## <a name="classic-deployment-limitations"></a>클래식 배포 제한 사항
hello hello 클래식 모델을 통해 배포 된 리소스를 이동 하기 위한 옵션에 따라 달라 hello 리소스 tooa 새 구독 또는 구독 내에서 이동 하려는 여부.

### <a name="same-subscription"></a>동일한 구독
동일한 구독 제한에 따라 hello 적용 hello 내에서 한 리소스 그룹 tooanother 리소스 그룹에서 리소스를 이동할 때:

* 가상 네트워크(클래식)은 이동할 수 없습니다.
* Hello 클라우드 서비스와 가상 컴퓨터 (클래식)를 이동 해야 합니다.
* 클라우드 서비스 hello 이동 모든 가상 컴퓨터를 포함 하는 경우에 이동할 수 있습니다.
* 한 번에 하나의 클라우드 서비스만 이동할 수 있습니다.
* 한 번에 하나의 저장소 계정(클래식)만 이동할 수 있습니다.
* 저장소 계정 (클래식) hello에서 이동할 수 없는 가상 컴퓨터 또는 클라우드 서비스와 동일한 작업입니다.

toomove 클래식 리소스 tooa 새 리소스 그룹 내 동일한 구독 hello, hello 통해 hello 표준 이동 작업을 사용 하 여 [포털](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), 또는 [REST API](#use-rest-api)합니다. 사용 하면 리소스 관리자 리소스를 이동 하기 위한 사용 하 여 동일한 작업을 hello 합니다.

### <a name="new-subscription"></a>새 구독
Tooa 새 구독 리소스를 이동할 때는 hello 다음 제한 사항이 적용 됩니다.

* Hello에서 hello 구독에 있는 모든 클래식 리소스를 이동 해야 동일한 작업입니다.
* hello 대상 구독에 다른 모든 클래식 리소스를 사용할 수 없습니다.
* hello 이동 클래식 이동에 대 한 별도 REST API를 통해 요청할 수만 있습니다. 클래식 리소스 tooa 새 구독을 이동할 때 hello 표준 리소스 관리자 이동 명령이 작동 하지 않습니다.

toomove 클래식 리소스 tooa 새 구독을 사용 하 여 hello REST 작업을 특정 tooclassic 리소스입니다. 나머지 toouse hello 다음 단계를 수행 합니다.

1. 확인 원본 구독 hello 구독 간에에서 참여할 수 있습니다 하는 경우 이동 합니다. 다음 작업 hello를 사용 합니다.

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     Hello 요청 본문에 다음을 포함 합니다.

  ```json
  {
    "role": "source"
  }
  ```

     hello 유효성 검사 작업에 대 한 hello 응답 형식에 따라 hello 다음과 같습니다.

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. 확인은 hello 대상 구독의 구독 간에에서 참여할 수 있는 경우 이동 합니다. 다음 작업 hello를 사용 합니다.

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     Hello 요청 본문에 다음을 포함 합니다.

  ```json
  {
    "role": "target"
  }
  ```

     hello 응답 hello hello 원본 구독 유효성 검사와 동일한 형식입니다.
3. 두 구독 유효성 검사를 통과 하는 경우 모든 클래식 리소스 하나의 구독만 tooanother 구독에서 작업 하는 hello로 이동 합니다.

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    Hello 요청 본문에 다음을 포함 합니다.

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

hello 작업은 몇 분 동안 실행할 수 있습니다.

## <a name="use-portal"></a>포털 사용
toomove 리소스 이러한 리소스를 포함 하는 hello 리소스 그룹을 선택 하 고 hello 선택 **이동** 단추입니다.

![리소스 이동](./media/resource-group-move-resources/select-move.png)

Hello 리소스 tooa 새 리소스 그룹이 나 새 구독을 이동 하는 지 여부를 선택 합니다.

Hello 리소스 toomove 및 hello 대상 리소스 그룹을 선택 합니다. 이러한 리소스와 선택에 대 한 tooupdate 스크립트 할 승인 **확인**합니다. Hello 이전 단계에서 hello 편집 구독 아이콘을 선택한 경우 hello 대상 구독을 선택 해야 합니다.

![대상 선택](./media/resource-group-move-resources/select-destination.png)

**알림**, 작업이 실행 되 고 이동 하는 hello를 표시 합니다.

![이동 상태 표시](./media/resource-group-move-resources/show-status.png)

완료 되 면 hello 결과 알려 줍니다.

![이동 결과 표시](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a>PowerShell 사용
toomove 기존 리소스 tooanother 리소스 그룹이 나 hello를 사용 하 여 구독 `Move-AzureRmResource` 명령입니다.

첫 번째 예제와 hello 방법을 toomove 한 리소스 tooa 새 리소스 그룹입니다.

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

hello 방법을 예제와 두 번째 toomove 여러 리소스 tooa 새 리소스 그룹입니다.

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

toomove tooa 새 구독을 hello에 대 한 값이 포함 `DestinationSubscriptionId` 매개 변수입니다.

요청 tooconfirm toomove hello 원하는 리소스를 지정 합니다.

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a>Azure CLI 2.0 사용
toomove 기존 리소스 tooanother 리소스 그룹이 나 hello를 사용 하 여 구독 `az resource move` 명령입니다. Hello 리소스 hello 리소스 toomove의 Id를 제공 합니다. 다음 명령을 hello로 리소스 Id를 얻을 수 있습니다.

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

다음 예제는 hello toomove 저장소 tooa 새 리소스 그룹을 고려 하는 방법을 보여 줍니다. Hello에 `--ids` 매개 변수를 hello 리소스 Id toomove 공백으로 구분 된 목록을 제공 합니다.

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

toomove tooa 새 구독을 hello 제공 `--destination-subscription-id` 매개 변수입니다.

## <a name="use-azure-cli-10"></a>Azure CLI 1.0 사용
toomove 기존 리소스 tooanother 리소스 그룹이 나 hello를 사용 하 여 구독 `azure resource move` 명령입니다. Hello 리소스 hello 리소스 toomove의 Id를 제공 합니다. 다음 명령을 hello로 리소스 Id를 얻을 수 있습니다.

```azurecli
azure resource list -g sourceGroup --json
```

반환 형식에 따라 hello 됩니다.

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

다음 예제는 hello toomove 저장소 tooa 새 리소스 그룹을 고려 하는 방법을 보여 줍니다. Hello에 `-i` 매개 변수를 hello 리소스 Id toomove 쉼표로 구분 된 목록을 제공 합니다.

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

요청 tooconfirm toomove hello 원하는 리소스를 지정 합니다.

## <a name="use-rest-api"></a>REST API 사용
toomove 기존 리소스 tooanother 리소스 그룹 또는 구독을 실행 합니다.

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

Hello 요청 본문에서 hello 대상 리소스 그룹 및 리소스 toomove hello 지정 합니다. Hello 이동 REST 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [리소스 이동](https://msdn.microsoft.com/library/azure/mt218710.aspx)합니다.

## <a name="next-steps"></a>다음 단계
* 구독을 관리 하기 위한 PowerShell cmdlet에 대 한 toolearn 참조 [Azure PowerShell 사용 하 여 리소스 관리자와](powershell-azure-resource-manager.md)합니다.
* 구독을 관리 하기 위한 Azure CLI 명령에 대 한 toolearn 참조 [hello를 사용 하 여 리소스 관리자와 Azure CLI](xplat-cli-azure-resource-manager.md)합니다.
* 구독을 관리 하기 위한 포털 기능에 대 한 toolearn 참조 [hello Azure 포털 toomanage 리소스를 사용 하 여](resource-group-portal.md)합니다.
* toolearn 논리적 구성이 tooyour 리소스를 적용 하는 방법에 대 한 참조 [를 사용 하 여 태그 tooorganize 리소스](resource-group-using-tags.md)합니다.
