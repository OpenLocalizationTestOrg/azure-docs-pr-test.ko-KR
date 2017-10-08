---
title: "서비스 패브릭 응용 프로그램의 aaaConfigure hello 업그레이드 | Microsoft Docs"
description: "Microsoft Visual Studio를 사용 하 여 서비스 패브릭 응용 프로그램을 업그레이드 하는 것에 대 한 tooconfigure 설정을 hello 하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a>Visual Studio에서 서비스 패브릭 응용 프로그램의 hello 업그레이드를 구성 합니다.
Azure 서비스 패브릭 용 도구 visual Studio toolocal 또는 원격 클러스터를 게시 하기 위한 업그레이드 지원을 제공 합니다. 가지 하려는 tooupgrade 응용 프로그램 tooa 새 버전 테스트 및 디버깅 하는 동안 hello 응용 프로그램을 교체 하는 대신 세 가지 시나리오가 있습니다.

* 응용 프로그램 데이터는 hello 업그레이드 동안 손실 되지 않습니다.
* 가용성 계속 남아 높은 있으므로 hello 업그레이드 중 서비스 중단 되지 않습니다는 충분 한 서비스 인스턴스 업그레이드 도메인에 분산 하는 경우.
* 업그레이드하는 동안 응용 프로그램에 대해 테스트를 실행할 수 있습니다.

## <a name="parameters-needed-tooupgrade"></a>필요한 tooupgrade 매개 변수
두 가지의 배포 형식(일반 또는 업그레이드)에서 선택할 수 있습니다. 일반 배포 업그레이드 배포 보존 하는 동안 모든 이전 배포 정보 및 hello 클러스터에서 데이터를 지웁니다. Visual Studio에서 서비스 패브릭 응용 프로그램을 업그레이드 tooprovide 응용 프로그램 업그레이드 매개 변수 및 상태 검사 정책이 필요 합니다. 도움말 매개 변수는 응용 프로그램 업그레이드 상태 검사 정책을 hello 업그레이드가 성공 했는지 확인 하는 동안 hello 업그레이드를 제어 합니다. 자세한 내용은 [서비스 패브릭 응용 프로그램 업그레이드: 업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md) 를 참조하세요.

*Monitored*, *UnmonitoredAuto* 및 *UnmonitoredManual*의 세 가지 업그레이드 모드가 있습니다.

* Hello 업그레이드 및 응용 프로그램을 자동화 하는 모니터링 된 업그레이드 상태 검사 합니다.
* UnmonitoredAuto 업그레이드 하는 자동화 hello 업그레이드 하지만 건너뜁니다 hello 응용 프로그램 상태 검사 합니다.
* Toomanually UnmonitoredManual 업그레이드를 수행 하는 경우 필요한 각 업그레이드 도메인을 업그레이드 합니다.

업그레이드 모드마다 서로 다른 매개 변수 집합이 필요합니다. 참조 [응용 프로그램 업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md) toolearn hello 사용할 수 있는 업그레이드 옵션에 대 한 자세한 합니다.

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a>Visual Studio에서 서비스 패브릭 응용 프로그램 업그레이드
Hello Visual Studio 서비스 패브릭 도구 tooupgrade 서비스 패브릭 응용 프로그램을 사용 하는 경우 지정할 수 있습니다 게시 프로세스 toobe 일반 배포 하지 않고 업그레이드 hello를 확인 하 여 **hello 응용 프로그램 업그레이드** 확인 상자입니다.

### <a name="tooconfigure-hello-upgrade-parameters"></a>tooconfigure hello 업그레이드 매개 변수
1. Hello 클릭 **설정을** 단추 다음 toohello 확인란 합니다. hello **업그레이드 매개 변수 편집** 대화 상자가 나타납니다. hello **업그레이드 매개 변수 편집** 대화 상자에서는 hello 감시, UnmonitoredAuto, 및 UnmonitoredManual 업그레이드 모드를 지원 합니다.
2. Hello 업그레이드 모드 toouse 원하고 hello 매개 변수 표에서 주소를 선택 합니다.

    각 매개 변수에는 기본값이 있습니다. 선택적 매개 변수를 hello *DefaultServiceTypeHealthPolicy* 해시 테이블 입력을 사용 합니다. 예를 들면 hello 해시 테이블에 대 한 입력된 형식이 같습니다 *DefaultServiceTypeHealthPolicy*:

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    *ServiceTypeHealthPolicyMap* hello에 해시 테이블 입력을 사용 하는 다른 선택적 매개 변수 형식에 따라 됩니다.

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    다음은 실제 예제입니다.

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. UnmonitoredManual 업그레이드 모드를 선택 하는 경우 수동으로 PowerShell 콘솔 toocontinue 시작 하며 hello 업그레이드 프로세스를 완료 합니다. 너무 참조[서비스 패브릭 응용 프로그램 업그레이드: 고급 항목](service-fabric-application-upgrade-advanced.md) toolearn 어떻게 수동 업그레이드 작동 합니다.

## <a name="upgrade-an-application-by-using-powershell"></a>PowerShell을 사용하여 응용 프로그램 업그레이드
PowerShell cmdlet tooupgrade 서비스 패브릭 응용 프로그램을 사용할 수 있습니다. 자세한 내용을 보려면 [Service Fabric 응용 프로그램 업그레이드 자습서](service-fabric-application-upgrade-tutorial.md) 및 [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx)를 참조하세요.

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a>Hello 응용 프로그램 매니페스트 파일에서 상태 검사 정책 지정
서비스 패브릭 응용 프로그램에서 모든 서비스는 hello 기본값을 재정의 하는 자체 상태 정책 매개 변수를 가질 수 있습니다. Hello 응용 프로그램 매니페스트 파일에서 이러한 매개 변수 값을 제공할 수 있습니다.

hello 다음 예제에서는 고유한 성능 tooapply hello 응용 프로그램 매니페스트에서 각 서비스에 대 한 정책을 확인 하는 방법을

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a>다음 단계
응용 프로그램을 배포하는 방법에 대한 자세한 내용은 [Azure 서비스 패브릭에서 기존 응용 프로그램 배포](service-fabric-deploy-existing-app.md)를 참조하세요.