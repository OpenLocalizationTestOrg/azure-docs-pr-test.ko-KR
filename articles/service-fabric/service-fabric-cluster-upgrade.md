---
title: "Azure 서비스 패브릭 클러스터 aaaUpgrade | Microsoft Docs"
description: "클러스터 업데이트 모드를 업그레이드 하는 인증서, OS 패치를 수행 하는 응용 프로그램 포트 추가 설정을 포함 하는 서비스 패브릭 클러스터를 실행 하는 구성 및/또는 hello 서비스 패브릭 코드를 업그레이드 하 한 등. 수 있을 경우 hello 업그레이드를 수행 하 시겠습니까?"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 15190ace-31ed-491f-a54b-b5ff61e718db
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/10/2017
ms.author: chackdan
ms.openlocfilehash: 94ac3833ec0810f79de06ecb50f254028fa90408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a>Azure Service Fabric 클러스터 업그레이드
> [!div class="op_single_selector"]
> * [Azure 클러스터](service-fabric-cluster-upgrade.md)
> * [독립 실행형 클러스터](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

모든 최신 시스템에 대 한 업그레이드 기능에 대 한 디자인은 제품의 핵심 tooachieving 장기 success입니다. Azure 서비스 패브릭 클러스터는 개인이 소유하지만 Microsoft에서 부분적으로 관리하는 리소스입니다. 이 문서는 자동으로 관리되는 것과 스스로 구성할 수 있는 것을 설명합니다.

## <a name="controlling-hello-fabric-version-that-runs-on-your-cluster"></a>클러스터에서 실행 되는 hello 패브릭 버전 제어
Microsoft에서 릴리스되는 하거나 클러스터 toobe에서 원하는 패브릭 지원 되는 버전을 선택할 수 업그레이드 클러스터 tooreceive 자동 패브릭을 설정할 수 있습니다.

이렇게 하려면 hello 포털 또는 리소스 관리자 생성 hello 시 또는 나중에 라이브 클러스터를 사용 하 여 hello "upgradeMode" 클러스터 구성 설정 

> [!NOTE]
> 항상 지원 되는 패브릭 버전을 실행 하 여 클러스터 tookeep 있는지를 확인 합니다. 수정한 서비스 패브릭의 새 버전의 hello 릴리스 필요 없이 업데이트가 발표, hello 이전 버전 지원 종료 최소 해당 날짜 로부터 60 일 후 표시 되어 있습니다. hello hello 새 릴리스 발표 됩니다 [hello 서비스 패브릭 팀 블로그에](https://blogs.msdn.microsoft.com/azureservicefabric/)합니다. hello 새 릴리스 하는 toochoose 사용할 수 있습니다. 
> 
> 

14 일 hello 릴리스 이전 toohello 만료 클러스터 실행 중인에서 경고 성능 상태에 클러스터를 추가 하는 상태 이벤트가 생성 됩니다. hello 클러스터 tooa 패브릭 지원 되는 버전 업그레이드 될 때까지 경고 상태로 유지 됩니다.

### <a name="setting-hello-upgrade-mode-via-portal"></a>포털을 통해 hello 업그레이드 모드 설정
Hello 클러스터 tooautomatic 또는 수동 hello 클러스터를 만들 때 설정할 수 있습니다.

![Create_Manualmode][Create_Manualmode]

라이브 클러스터에 있는 경우 수동 hello를 사용 하 여 환경을 관리할 또는 hello 클러스터 tooautomatic를 설정할 수 있습니다. 

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-portal"></a>Tooa tooManual 모드 포털을 통해 설정 된 클러스터에 새 버전을 업그레이드 합니다.
tooupgrade tooa 새 버전으로 toodo 있으면 hello 드롭다운에서 hello 사용 가능한 버전을 선택 하 고 저장 합니다. hello Fabric 업그레이드 자동으로 시작을 가져옵니다. hello 클러스터 상태 정책 (노드 상태 및 hello 상태 hello 클러스터에서 실행 중인 응용 프로그램을 hello 모두의 조합)를 준수 tooduring hello 업그레이드 합니다.

Hello 클러스터 상태 정책을 충족 되지 않으면 hello 업그레이드가 롤백됩니다. 이 문서 tooread 방법에 자세한 아래로 스크롤하여 tooset 사용자 지정 상태 정책입니다. 

Hello 롤백이 발생 하는 hello 문제를 해결 한 후 tooinitiate hello 업그레이드를 다시 여 필요한 이전과 동일한 단계를 다음 hello 합니다.

![Manage_Automaticmode][Manage_Automaticmode]

### <a name="setting-hello-upgrade-mode-via-a-resource-manager-template"></a>리소스 관리자 템플릿을 통해 hello 업그레이드 모드 설정
Hello "upgradeMode" 구성 toohello Microsoft.ServiceFabric/clusters 리소스 정의의 hello 집합 hello "clusterCodeVersion" tooone 아래와 같이 지원 되는 패브릭 버전 및 다음 hello 서식 파일을 배포 및 추가 합니다. "수동" 또는 "자동" hello "upgradeMode"에 대 한 유효한 값은

![ARMUpgradeMode][ARMUpgradeMode]

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-a-resource-manager-template"></a>리소스 관리자 템플릿을 통해 tooManual 모드 설정 되어 있는 클러스터 tooa 새 버전을 업그레이드 합니다.
Hello 클러스터 tooupgrade tooa 새 버전으로 수동 모드일 때 clusterCodeVersion"hello" tooa 지원 되는 버전을 변경 하 고 배포 합니다. hello 템플릿의 hello 배포 hello Fabric 업그레이드의 작동 가져옵니다 시작 자동으로. hello 클러스터 상태 정책 (노드 상태 및 hello 상태 hello 클러스터에서 실행 중인 응용 프로그램을 hello 모두의 조합)를 준수 tooduring hello 업그레이드 합니다.

Hello 클러스터 상태 정책을 충족 되지 않으면 hello 업그레이드가 롤백됩니다. 이 문서 tooread 방법에 자세한 아래로 스크롤하여 tooset 사용자 지정 상태 정책입니다. 

Hello 롤백이 발생 하는 hello 문제를 해결 한 후 tooinitiate hello 업그레이드를 다시 여 필요한 이전과 동일한 단계를 다음 hello 합니다.

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a>지정된 구독의 모든 환경에 대해 사용 가능한 모든 버전 목록 가져오기
실행 명령에 따라 hello 및 출력 유사한 toothis을 얻어야 합니다.

"supportExpiryUtc"는 지정된 릴리스가 만료되거나 이미 만료되었음을 알려 줍니다. hello 최신 릴리스는 없습니다는 유효한 날짜-의 해당 값이 "9999-12-31T23:59:59.9999999", 방금 hello 만료 날짜가 아직 설정 되지 않았음을 의미 합니다.

```REST
GET https://<endpoint>/subscriptions/{{subscriptionId}}/providers/Microsoft.ServiceFabric/locations/{{location}}/clusterVersions?api-version=2016-09-01

Example: https://management.azure.com/subscriptions/1857f442-3bce-4b96-ad95-627f76437a67/providers/Microsoft.ServiceFabric/locations/eastus/clusterVersions?api-version=2016-09-01

Output:
{
                  "value": [
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/5.0.1427.9490",
                      "name": "5.0.1427.9490",
                      "type": "Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.0.1427.9490",
                        "supportExpiryUtc": "2016-11-26T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.0.1427.9490",
                      "name": "5.1.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.1.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.4.1427.9490",
                      "name": "4.4.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "4.4.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Linux"
                      }
                    }
                  ]
                }


```

## <a name="fabric-upgrade-behavior-when-hello-cluster-upgrade-mode-is-automatic"></a>Fabric 업그레이드 동작 hello 클러스터 업그레이드 모드는 자동 하는 경우
Microsoft는 hello 패브릭 코드 및 Azure 클러스터에서 실행 되는 구성을 유지 관리 합니다. 모니터링 되는 자동 업그레이드 toohello 소프트웨어에는 필요에 따라 수행합니다. 이러한 업그레이드는 코드, 구성 또는 둘 모두가 될 수 있습니다. 응용 프로그램의 성능이 영향 없음이나 toothese 업그레이드 때문에 미치는 영향을 최소화 하 고 있는지 toomake, 단계를 수행 하는 hello에서 hello 업그레이드 수행:

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a>1단계: 모든 클러스터 상태 정책을 사용하여 업그레이드 수행
이 단계 동안 hello 업그레이드 한 번에 하나의 업그레이드 도메인을 계속 하 고 hello 클러스터에서 실행 중이 던 hello 응용 프로그램은 toorun 가동 중지 시간 없이 계속 합니다. hello 클러스터 상태 정책 (노드 상태 및 hello 상태 hello 클러스터에서 실행 중인 응용 프로그램을 hello 모두의 조합)를 준수 tooduring hello 업그레이드 합니다.

Hello 클러스터 상태 정책을 충족 되지 않으면 hello 업그레이드가 롤백됩니다. 다음 전자 메일 구독 hello toohello 소유자를 전송 됩니다. hello 다음 정보를 포함 하는 hello 전자 메일:

* 놓았습니다 tooroll 다시 클러스터 업그레이드는 알림입니다.
* 권장 수정 작업(있는 경우).
* 2 단계 실행 될 때까지 (n) 일 hello 수입니다.

인프라 이유로 잘못 되었습니다 업그레이드 하는 경우를 몇 번 더 업그레이드 동일 tooexecute hello를 시도 합니다. Hello 후 tooPhase 2를 계속 진행 n 일 hello 날짜 hello 전자 메일에서 전송 되었습니다.

Hello 클러스터 상태 정책을 충족 되 면 hello 업그레이드를 성공한 것으로 간주 하 고 완료로 표시 합니다. 이 단계에서는 hello 초기 업그레이드 또는 업그레이드 트리거하는지 hello 중 하나는 동안 발생할 수 있습니다. 성공적 실행에 대한 전자 메일 확인은 없습니다. 이 tooavoid 전송 하면 너무 많은 전자 메일-전자 메일을 보내 예외 toonormal으로 이해 되어야 합니다. 응용 프로그램 가용성에 영향을 주지 않고 대부분의 클러스터 업그레이드 toosucceed hello 라고 생각 됩니다.

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a>2단계: 기본 상태 정책만을 사용하여 업그레이드 수행
이 단계에서는 hello 상태 정책은 hello hello 업그레이드의 hello 시작 부분에서 문제가 있는 응용 프로그램 수 hello hello 업그레이드 프로세스의 소요 시간은 hello에 대해 동일 하 게 유지 되도록 하는 방식으로 설정 됩니다. 1 단계에서와 같이 hello 2 단계를 업그레이드 한 번에 하나의 업그레이드 도메인을 계속 하 고 hello 클러스터에서 실행 중이 던 hello 응용 프로그램이 중단 시간 없이 toorun를 계속 합니다. hello 클러스터 상태 정책 (노드 상태 및 hello 상태 hello 클러스터에서 실행 중인 응용 프로그램을 hello 모두의 조합) 준수 toofor hello 업그레이드 기간에 hello 됩니다.

Hello 클러스터 상태 정책 적용 충족 되지 않는 경우 hello 업그레이드가 롤백됩니다. 다음 전자 메일 구독 hello toohello 소유자를 전송 됩니다. hello 다음 정보를 포함 하는 hello 전자 메일:

* 놓았습니다 tooroll 다시 클러스터 업그레이드는 알림입니다.
* 권장 수정 작업(있는 경우).
* 3 단계를 실행 될 때까지 (n) 일 hello 수입니다.

인프라 이유로 잘못 되었습니다 업그레이드 하는 경우를 몇 번 더 업그레이드 동일 tooexecute hello를 시도 합니다. 미리 알림 전자 메일은 n일이 끝나기 몇 일 전에 전송됩니다. Hello 후 tooPhase 3를 계속 진행 n 일 hello 날짜 hello 전자 메일에서 전송 되었습니다. म ध ा ड 2 단계에서에서 hello 전자 메일을 심각 하 게 수행 해야 하 고 수정 작업을 수행 해야 합니다.

Hello 클러스터 상태 정책을 충족 되 면 hello 업그레이드를 성공한 것으로 간주 하 고 완료로 표시 합니다. 이 단계에서는 hello 초기 업그레이드 또는 업그레이드 트리거하는지 hello 중 하나는 동안 발생할 수 있습니다. 성공적 실행에 대한 전자 메일 확인은 없습니다.

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a>3단계: 까다로운 상태 정책을 사용하여 업그레이드 수행
이 단계에서는 이러한 상태 정책은 hello 응용 프로그램의 hello 상태 보다는 hello 업그레이드가 완료 맞춰진 합니다. 이 단계에서 매우 적은 클러스터 업그레이드가 끝납니다. 클러스터 toothis 단계를 가져오는 경우 응용 프로그램이 비정상 상태가 되 및 가용성을 손실 가능성이 있습니다.

비슷한 toohello 다른 두 단계 3 단계 업그레이드 한 번에 하나의 업그레이드 도메인을 진행 합니다.

Hello 클러스터 상태 정책을 충족 되지 않으면 hello 업그레이드가 롤백됩니다. 인프라 이유로 잘못 되었습니다 업그레이드 하는 경우를 몇 번 더 업그레이드 동일 tooexecute hello를 시도 합니다. 그 후 hello 클러스터 고정 된 지원 및 업그레이드 더 이상 수신할 수 있도록 합니다.

이 정보로 전자 메일 작업을 수행해 hello 함께 toohello 구독 소유자에 전송 됩니다. 3 단계 실패 했습니다 상태로 모든 클러스터 tooget을 예상 되지 않는 것입니다.

Hello 클러스터 상태 정책을 충족 되 면 hello 업그레이드를 성공한 것으로 간주 하 고 완료로 표시 합니다. 이 단계에서는 hello 초기 업그레이드 또는 업그레이드 트리거하는지 hello 중 하나는 동안 발생할 수 있습니다. 성공적 실행에 대한 전자 메일 확인은 없습니다.

## <a name="cluster-configurations-that-you-control"></a>사용자가 제어하는 클러스터 구성
또한 toohello 기능 tooset hello 클러스터 업그레이드 모드, 라이브 클러스터에서 변경할 수 있는 hello 구성은 다음과 같습니다.

### <a name="certificates"></a>인증서
새로 추가 하거나 hello 클러스터 및 hello 포털을 통해 클라이언트에 대 한 인증서를 쉽게 삭제할 수 있습니다. 너무 참조[대 한 자세한 지침은이 문서](service-fabric-cluster-security-update-certs-azure.md)

![Hello Azure 포털에서에서 인증서 지문을 보여 주는 스크린 샷][CertificateUpgrade]

### <a name="application-ports"></a>응용 프로그램 포트
Hello 노드 유형에 연결 된 hello 부하 분산 장치 리소스 속성을 변경 하 여 응용 프로그램 포트를 변경할 수 있습니다. Hello 포털을 사용 하거나 직접 리소스 관리자 PowerShell을 사용할 수 있습니다.

노드 형식에 있는 모든 Vm에 새 포트 tooopen 다음 hello지 않습니다.

1. 새 프로브 toohello 적절 한 부하 분산 장치를 추가 합니다.
   
    "LB-name hello 리소스 그룹 NodeTypename의" hello 부하 분산 장치 이름은 hello 포털을 사용 하 여 클러스터를 배포한 경우 각 노드 형식에 대 한 합니다. 리소스 그룹 내 에서만 고유 hello 부하 분산 장치 이름이 있으므로 검색 하는 특정 리소스 그룹에 것이 가장 좋습니다.
   
    ![프로브 tooa 추가 보여 주는 스크린 샷의에서 부하 분산 장치 hello 포털입니다.][AddingProbes]
2. 새 규칙 toohello 부하 분산 장치를 추가 합니다.
   
    동일한 부하 분산 장치 hello 이전 단계에서 만든 hello 프로브를 사용 하 여 새 규칙 toohello를 추가 합니다.
   
    ![Hello 포털에서 새 규칙 tooa 부하 분산 장치를 추가 합니다.][AddingLBRules]

### <a name="placement-properties"></a>배치 속성
Hello 노드 유형 각각에 대 한 응용 프로그램에서 toouse 되도록 사용자 지정 배치 속성을 추가할 수 있습니다. NodeType은 명시적으로 추가하지 않고 사용할 수 있는 기본 속성입니다.

> [!NOTE]
> 배치 제약 조건 노드 속성을 사용 하 여 hello에 대 한 자세한 내용은 방법 toodefine, 참조 toohello 섹션인 "배치 제약 조건 및 노드 속성" hello 서비스 패브릭 클러스터 리소스 관리자 문서에서 [Your 클러스터를 설명 하는 ](service-fabric-cluster-resource-manager-cluster-description.md).
> 
> 

### <a name="capacity-metrics"></a>용량 메트릭
Hello 노드 유형 각각에 대 한 응용 프로그램 tooreport 부하에서 toouse 되도록 사용자 지정 용량 메트릭을 추가할 수 있습니다. 용량 메트릭 tooreport 부하 hello 사용에 대 한 자세한 내용은에서 toohello 서비스 패브릭 클러스터 리소스 관리자 문서 참조 [Your 클러스터를 설명 하는](service-fabric-cluster-resource-manager-cluster-description.md) 및 [메트릭 및 부하](service-fabric-cluster-resource-manager-metrics.md)합니다.

### <a name="fabric-upgrade-settings---health-polices"></a>패브릭 업그레이드 설정 - 상태 정책
패브릭 업그레이드에 대한 사용자 지정 상태 정책을 지정할 수 있습니다. 을 설정 했으면 클러스터 tooAutomatic fabric 업그레이드 하는 경우 이러한 정책은 hello 자동 fabric 업그레이드의 적용 된 toohello를 1 단계를 가져옵니다.
설정한 경우 수동 패브릭에 대 한 클러스터 업그레이드 되 면이 정책이 적용 될 때마다 다음 클러스터의 hello fabric 업그레이드 오프 hello 시스템 tookick 트리거 새 버전을 선택 합니다. Hello 정책을 재정의 하지 않으면 hello 기본값이 사용 됩니다.

고급 업그레이드 설정 hello를 선택 하 여 hello "fabric 업그레이드" 블레이드 hello 현재 설정을 검토 하거나 hello 사용자 지정 상태 정책을 지정할 수 있습니다. 그림에 나오는 하는 방법에는 hello를 검토 합니다. 

![사용자 지정 상태 정책 관리][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a>클러스터에 대한 패브릭 설정 사용자 지정
너무 참조[서비스 패브릭 클러스터 패브릭 설정](service-fabric-cluster-fabric-settings.md) 항목 및 방법을 사용자 지정 합니다.

### <a name="os-patches-on-hello-vms-that-make-up-hello-cluster"></a>Hello hello 클러스터를 구성 하는 Vm에 OS 패치
너무 참조[패치 오케스트레이션 응용 프로그램](service-fabric-patch-orchestration-application.md) hello 항상 사용 가능한 hello 서비스 유지 하는 오케스트레이션 방식으로 Windows 업데이트에서 클러스터 tooinstall 패치 프로그램에 배포할 수 있습니다. 

### <a name="os-upgrades-on-hello-vms-that-make-up-hello-cluster"></a>Hello hello 클러스터를 구성 하는 Vm의 OS 업그레이드
Hello 클러스터의 가상 컴퓨터 hello에 hello OS 이미지를 업그레이드 해야 하는 경우 한 번에 하나의 VM 수행 해야 있습니다. 현재 자동화 기능은 없습니다.

## <a name="next-steps"></a>다음 단계
* 자세한 내용은 방법 toocustomize 일부 hello [서비스 패브릭 클러스터 패브릭 설정](service-fabric-cluster-fabric-settings.md)
* 너무 방법에 대해 알아봅니다[클러스터를 확장 및 축소](service-fabric-cluster-scale-up-down.md)
* [응용 프로그램 업그레이드](service-fabric-application-upgrade.md)

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG
