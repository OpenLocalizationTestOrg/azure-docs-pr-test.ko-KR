---
title: "클러스터에 대 한 Azure 부하 분산 장치 규칙 aaaCreate"
description: "Azure 서비스 패브릭 클러스터에 대 한 Azure 부하 분산 장치 tooopen 포트를 구성 합니다."
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a>Service Fabric 클러스터에 대한 포트 열기

hello 부하 분산 장치에 배포 된 Azure 서비스 패브릭 클러스터 노드에서 실행 되는 트래픽 tooyour 응용 프로그램을 지시 합니다. 사용자 앱 toouse 다른 포트를 변경 하면 해야 해당 포트를 노출 (또는 다른 포트로 라우팅할) hello Azure 부하 분산 장치에에서 있습니다.

서비스 패브릭 클러스터 tooAzure 프로그램을 배포할 때 부하 분산 장치에 자동으로 만들어진 합니다. 부하 분산 장치가 없는 경우 [인터넷 연결 부하 분산 장치 구성](..\load-balancer\load-balancer-get-started-internet-portal.md)을 참조하세요.

## <a name="configure-service-fabric"></a>Service Fabric 구성

서비스 패브릭 응용 프로그램 **ServiceManifest.xml** 응용 프로그램에 toouse hello 끝점을 정의 하는 구성 파일입니다. Hello 부하 분산 장치에 업데이트 된 tooexpose 해당 (또는 다른)이 있어야 hello 구성 파일에 대 한 업데이트 된 toodefine 끝점을 수행한 후 포트입니다. Toocreate 서비스 패브릭 끝점 hello 하는 방법에 대 한 자세한 내용은 참조 하십시오. [끝점 설정](service-fabric-service-manifest-resources.md)합니다.

## <a name="create-a-load-balancer-rule"></a>부하 분산 장치 규칙 만들기

부하 분산 장치 규칙 인터넷 연결 포트를 열리고 응용 프로그램에서 사용 하는 트래픽 toohello 내부 노드 포트를 전달 합니다. 부하 분산 장치가 없는 경우 [인터넷 연결 부하 분산 장치 구성](..\load-balancer\load-balancer-get-started-internet-portal.md)을 참조하세요.

다음 정보는 toocollect hello 해야 toocreate 부하 분산 장치 규칙:

- 부하 분산 장치 이름
- 리소스 그룹의 hello 부하 분산 장치 및 서비스 패브릭 클러스터입니다.
- 외부 포트
- 내부 포트

## <a name="azure-cli"></a>Azure CLI
>[!NOTE]
>Toodetermine hello hello 부하 분산 장치의 이름으로 필요한 경우이 명령은 tooquickly get 모든 부하 분산 장치 및 연결 된 hello 리소스 그룹의 목록을 사용 합니다.
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

단 하나의 명령 toocreate hello로 부하 분산 장치 규칙 **Azure CLI**합니다. 하기만 하면 tooknow hello 부하 분산 장치 및 리소스 그룹 toocreate 새 규칙의 이름을 모두 hello 됩니다.

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

hello Azure CLI 명령을 hello 표 다음에 설명 되어 있는 몇 가지 매개 변수가 있습니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `--backend-port`  | hello 포트 hello 서비스 패브릭 응용 프로그램을 수신 대기 합니다. |
| `--frontend-port` | hello 포트 hello 부하 분산 장치 노출 하는 외부 연결에 대 한 합니다. |
| `-lb-name` | hello의 hello 이름 부하 분산 장치 toochange 합니다. |
| `-g`       | hello 부하 분산 장치 및 서비스 패브릭 클러스터를 모두 있는 hello 리소스 그룹입니다. |
| `-n`       | hello hello 규칙의 이름을 선택 합니다. |


>[!NOTE]
>Toocreate hello Azure CLI로 부하 분산 장치를 확인 하려면 어떻게 대 한 자세한 내용은 [hello Azure CLI를 사용 하 여 부하 분산 장치 만들기](..\load-balancer\load-balancer-get-started-internet-arm-cli.md)합니다.

## <a name="powershell"></a>PowerShell

>[!NOTE]
>Toodetermine hello hello 부하 분산 장치의 이름으로 필요한 경우이 명령은 tooquickly get 모든 부하 분산 장치 및 관련된 리소스 그룹의 목록을 사용 합니다.
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

PowerShell은 Azure CLI hello 보다 좀 더 복잡 합니다. 개념적으로 hello 단계 toocreate 다음 규칙을 수행 합니다.

1. Azure의 hello 부하 분산 장치를 가져옵니다.
2. 규칙을 만듭니다.
3. Hello 규칙 toohello 부하 분산 장치를 추가 합니다.
4. Hello 부하 분산 장치를 업데이트 합니다.

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

Hello에 대 한 `New-AzureRmLoadBalancerRuleConfig` 명령을 hello `-FrontendPort` 나타냅니다 hello 포트 hello 부하 분산 장치의 외부 연결 및 hello에 대 한 노출 `-BackendPort` 나타냅니다 hello 포트 hello 서비스 패브릭 응용 프로그램을 수신 대기 합니다.

>[!NOTE]
>Toocreate powershell을 부하 분산 장치를 확인 하려면 어떻게 대 한 자세한 내용은 [PowerShell을 사용 하 여 부하 분산 장치 만들기](..\load-balancer\load-balancer-get-started-internet-arm-ps.md)합니다.

