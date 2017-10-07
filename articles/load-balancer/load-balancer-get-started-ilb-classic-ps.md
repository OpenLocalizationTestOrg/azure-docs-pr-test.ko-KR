---
title: "aaaCreate Azure 내부 부하 분산 장치-PowerShell 클래식 | Microsoft Docs"
description: "내부 프로그램 toocreate hello 클래식 배포 모델에서 PowerShell을 사용 하 여 분산 장치를 로드 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a>PowerShell을 사용하여 내부 부하 분산 장치(클래식) 만들기 시작

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Cloud services](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.  이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 너무 방법에 대해 알아봅니다[hello 리소스 관리자 모델을 사용 하 여 이러한 단계를 수행](load-balancer-get-started-ilb-arm-ps.md)합니다.

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a>가상 컴퓨터에 대한 내부 부하 분산 장치 집합 만들기

내부 부하 분산 설정 하 고 해당 트래픽 tooit 보낼 서버 hello toocreate, toodo hello 다음을 사용할 수 있습니다.

1. 내부 부하 분산의 부하 분산 된 집합의 hello 서버에 걸쳐 분산 된 들어오는 트래픽 toobe 부하의 hello 끝점 수 있는 인스턴스를 만듭니다.
2. Hello 들어오는 트래픽을 받게 되 toohello 가상 컴퓨터를 해당 끝점을 추가 합니다.
3. 송신할 hello 트래픽 toobe 부하 분산 된 toosend 해당 트래픽을 toohello 가상 IP (VIP) 인스턴스의 주소 hello 내부 부하 분산 하는 hello 서버를 구성 합니다.

### <a name="step-1-create-an-internal-load-balancing-instance"></a>1단계: 내부 부하 분산 인스턴스 만들기

기존 클라우드 서비스 또는 지역 가상 네트워크가 배포 된 클라우드 서비스에 대 한 다음 Windows PowerShell 명령을 hello로 내부 부하 분산 인스턴스를 만들 수 있습니다.

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

hello의이 사용이 [Add-azureendpoint](https://msdn.microsoft.com/library/dn495300.aspx) hello DefaultProbe 매개 변수 집합을 사용 하 여 Windows PowerShell cmdlet. 추가 매개 변수 집합에 대한 자세한 내용은 [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx)를 참조하세요.

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a>2 단계: 끝점 toohello 내부 부하 분산 인스턴스를 추가 합니다.

다음은 예제입니다.

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a>3 단계: 구성 서버 toosend 해당 트래픽을 toohello 새로운 내부 부하 분산 끝점

진행 중인 toobe 부하 분산 된 toouse hello 새 IP 주소 (VIP hello) hello 인스턴스 내부 부하 분산의 트래픽은 hello 서버를 구성 너무 합니다. 내부 부하 분산 하는 hello 인스턴스가 수신 하는 hello 주소입니다. Toojust 대부분의 경우에서 필요한 추가 하거나 hello 내부 부하 분산 인스턴스의 VIP hello에 대 한 DNS 레코드를 수정 합니다.

Hello hello 내부 부하 분산 인스턴스를 만드는 동안 hello IP 주소를 지정한 경우 hello VIP이 이미 있습니다. 그렇지 않은 경우 명령 뒤 hello hello 프로덕션으로 VIP를 확인할 수 있습니다.

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

toouse hello 값 입력 제거 hello 이러한 명령은 < 및 >입니다. 다음은 예제입니다.

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

Hello Get AzureInternalLoadBalancer 명령의 hello 디스플레이에서 hello IP 주소 기록한 hello 필요한 변경 tooyour 서버 또는 DNS 레코드 tooensure 트래픽 toohello VIP 전송 되 게 합니다.

> [!NOTE]
> hello Microsoft Azure 플랫폼에는 다양 한 관리 시나리오에 대 한 정적, 공개적으로 라우팅 가능한 IPv4 주소를 사용합니다. hello IP 주소 168.63.129.16입니다. 이 IP 주소를 방화벽으로 차단하면 안 됩니다. 예기치 않은 동작이 발생할 수 있습니다.
> 내부 부하 분산 측면 tooAzure와 hello 부하 분산 장치 toodetermine hello 상태에서 가상 컴퓨터 부하 분산 집합에 대해 프로브를 모니터링 하 여이 IP 주소 사용 됩니다. 네트워크 보안 그룹 사용 되는 toorestrict 내부적으로 부하 분산 된 집합에 트래픽을 tooAzure 가상 컴퓨터는 되거나 적용 된 tooa 가상 네트워크 서브넷에 경우에 네트워크 보안 규칙 tooallow 트래픽을 168.63.129.16에서 추가 되어 있는지 확인 합니다.

## <a name="example-of-internal-load-balancing"></a>내부 부하 분산의 예제

toostep 2 가지의 구성 예제에 대 한 부하 분산 집합을 만드는 hello 끝 tooend 과정을 안내 합니다 참조 섹션에서는 다음 hello 합니다.

### <a name="an-internet-facing-multi-tier-application"></a>인터넷 연결 다중 계층 응용 프로그램

Tooprovide 인터넷 연결 웹 서버 집합에 대 한 부하 분산 된 데이터베이스 서비스를 사용 하는 것이 좋습니다. 두 서버 집합은 단일 Azure 클라우드 서비스에서 호스트됩니다. 웹 서버 트래픽을 tooTCP 포트 1433 hello 데이터베이스 계층의 가상 컴퓨터에 두 개의 배포 되어야 합니다. 그림 1 hello 구성을 보여 줍니다.

![Hello 데이터베이스 계층에 대 한 내부 부하 분산 된 집합](./media/load-balancer-internal-getstarted/IC736321.png)

hello 구성 hello 다음 이루어져 있습니다.

* mytestcloud hello hello 가상 컴퓨터를 호스팅하는 기존 클라우드 서비스의 이름은입니다.
* hello 두 명의 기존 데이터베이스 서버 이름은 d b 2 d b 1입니다.
* Hello 웹 계층의 웹 서버 hello 개인 IP 주소를 사용 하 여 hello 데이터베이스 계층의 toohello 데이터베이스 서버를 연결 합니다. 또 다른 옵션은 toouse hello 가상 네트워크에 대 한 사용자 고유의 DNS 하 고 수동으로 hello 내부 부하 분산 장치 집합에 대 한 A 레코드를 등록 합니다.

hello 다음 명령을 새 인스턴스를 구성 내부 부하 분산 라는 **ILBset** toohello 두 데이터베이스 서버에 해당 하는 끝점 toohello 가상 컴퓨터를 추가 합니다.

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a>내부 부하 분산 구성 제거

tooremove 인스턴스로부터 내부 부하 분산 장치, 다음 명령을 사용 하 여 hello 끝점으로 가상 컴퓨터:

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

hello 값을 제거 하는 hello toouse 이러한 명령은 입력 < 및 >입니다.

다음은 예제입니다.

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

다음 명령을 사용 하 여 hello 클라우드 서비스에서 내부 부하 분산 장치 인스턴스 tooremove:

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

이러한 명령의 toouse hello 값 입력 하 고 hello 제거 < 및 >입니다.

다음은 예제입니다.

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a>내부 부하 분산 장치 cmdlet에 대한 추가 정보

tooobtain hello 다음 Windows PowerShell 프롬프트에서 명령을 실행 합니다. 내부 부하 분산 cmdlet에 대 한 추가 정보:

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a>다음 단계

[원본 IP 선호도를 사용하여 부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)

