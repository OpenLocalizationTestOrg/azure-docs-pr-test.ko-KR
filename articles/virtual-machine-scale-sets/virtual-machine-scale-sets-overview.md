---
title: "aaaAzure 가상 컴퓨터 크기 집합 개요 | Microsoft Docs"
description: "Azure Virtual Machine Scale Sets에 대해 자세히 알아보세요."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 788b2d1636e0bf4ef3fbf94aed9b3303c5fafa82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-virtual-machine-scale-sets-in-azure"></a>Azure에서 말하는 가상 컴퓨터 확장 집합이란?
가상 컴퓨터 크기 집합은 toodeploy를 사용 하 고 동일한 Vm 집합을 관리할 수 있는 한 Azure 계산 리소스입니다. 구성 된 모든 Vm이 있는 동일 hello, 확장 집합은 설계 된 toosupport true 자동 크기 조정 되며 Vm의 프로비저닝 미리 필요 합니다. 큰 계산, 빅 데이터 및 컨테이너 화 된 작업을 대상으로 하는 보다 쉽게 toobuild 대규모 서비스는.

눈금에 및 tooscale 계산 리소스를 필요로 하는 응용 프로그램에 대 한 작업은 암시적으로 장애 도메인과 업데이트 도메인에 걸쳐 분산 됩니다. 추가 소개 tooscale 설정에 대 한 참조 toohello [Azure 블로그 알림을](https://azure.microsoft.com/blog/azure-virtual-machine-scale-sets-ga/)합니다.

확장 집합에 대한 자세한 내용은 다음 비디오를 보세요.

* [Mark Russinovich의 Azure 확장 집합 설명](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)  
* [Guy Bowerman과 가상 컴퓨터 규모 집합](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

## <a name="creating-and-managing-scale-sets"></a>확장 집합 만들기 및 관리
크기 hello에 집합을 만들 수 있습니다 [Azure 포털](https://portal.azure.com) 선택 하 여 **새** 입력 하 고 **배율** hello 검색 창에서. **가상 컴퓨터 크기 집합** hello 결과에 표시 됩니다. 여기에서 필요한 hello 필드 toocustomize 채울 수 있으며 크기 집합을 배포할 수 있습니다. 옵션 tooset hello 포털에서 CPU 사용량에 따라 기본 자동 크기 조정 규칙을 갖게 됩니다.

개별 Azure Resource Manager VM처럼 JSON 템플릿 및 [REST API](https://msdn.microsoft.com/library/mt589023.aspx)를 사용하여 확장 집합을 정의하고 배포할 수 있습니다. 따라서 모든 표준 Azure Resource Manager 배포 방법을 사용할 수 있습니다. 템플릿에 대한 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하세요.

Hello에 설정 하는 가상 컴퓨터 크기에 대 한 예제 템플릿 집합을 찾을 수 있습니다 [Azure 빠른 시작 템플릿 GitHub 리포지토리](https://github.com/Azure/azure-quickstart-templates)합니다. (사용 하 여 템플릿을 찾습니다 **vmss** hello 제목에.)

Hello 퀵 스타트 서식 파일 예제를 보려면 각 템플릿에 대해 hello 추가 정보에는 "배포 tooAzure" 단추는 toohello 포털 배포 기능을 연결합니다. toodeploy hello 배율 설정, hello 단추를 클릭 hello 포털에서 필요한 모든 매개 변수를 채웁니다. 

## <a name="scaling-a-scale-set-out-and-in"></a>확장 집합 확장 및 축소
Hello를 클릭 하 여 hello Azure 포털에서에서 설정 하는 눈금의 hello 용량을 변경할 수 있습니다 **배율** 섹션 아래 **설정을**합니다. 

hello 명령줄에서 toochange 크기 집합 용량, hello를 사용 하 여 **배율** 명령을 [Azure CLI](https://github.com/Azure/azure-cli)합니다. 예를 들어이 명령은 tooset 10 개의 Vm의 크기 조정 설정 tooa 용량을 사용 합니다.

```bash
az vmss scale -g resourcegroupname -n scalesetname --new-capacity 10 
```

Vm 크기의 tooset hello 수 PowerShell을 사용 하 여 설정, hello를 사용 하 여 **업데이트 AzureRmVmss** 명령:

```PowerShell
$vmss = Get-AzureRmVmss -ResourceGroupName resourcegroupname -VMScaleSetName scalesetname  
$vmss.Sku.Capacity = 10
Update-AzureRmVmss -ResourceGroupName resourcegroupname -Name scalesetname -VirtualMachineScaleSet $vmss
```

가상 컴퓨터는 규모에 맞게 tooincrease 또는 감소 hello 수 Azure 리소스 관리자 템플릿을 사용 하 여 설정, hello 변경 **용량** 속성 및 재배포 hello 서식 파일입니다. 이 단순 하면 쉽게 toointegrate 크기 집합 Azure 자동 크기 조정 또는 toowrite 사용자 고유의 사용자 지정 크기 조정 레이어 toodefine 사용자 지정 배율이 이벤트 Azure 자동 크기 조정은 필요한 경우 지원 하지 않습니다. 

사용 하 여 Azure 리소스 관리자 템플릿 toochange hello 용량이 다시 배포 하는 hello만 포함 하는 훨씬 더 작은 템플릿을 정의할 수 있습니다 **SKU** hello 사용 하 여 속성 패킷을 용량을 업데이트 합니다. [예를 들면 다음과 같습니다](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing).

## <a name="autoscale"></a>Autoscale

Hello Azure 포털에서에서 만들 때 크기 집합 자동 크기 조정 설정을 사용 하 여 필요에 따라 구성 수 있습니다. Vm hello 수 증가 또는 평균 CPU 사용량에 따라 감소 시켜야 수 있습니다. 

Hello에서 집합 서식 파일을 조절 하는 다양 한 hello [Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates) 자동 크기 조정 설정을 정의 합니다. 또한 자동 크기 조정 설정을 tooan 기존 크기 집합을 추가할 수 있습니다. 예를 들어이 Azure PowerShell 스크립트는 CPU 기반 자동 크기 조정 tooa 크기 집합을 추가합니다.

```PowerShell

$subid = "yoursubscriptionid"
$rgname = "yourresourcegroup"
$vmssname = "yourscalesetname"
$location = "yourlocation" # e.g. southcentralus

$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Increase -ScaleActionValue 1
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator LessThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Decrease -ScaleActionValue 1
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "autoprofile1"
Add-AzureRmAutoscaleSetting -Location $location -Name "autosetting1" -ResourceGroup $rgname -TargetResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -AutoscaleProfiles $profile1
```

유효한 메트릭 tooscale의 목록에서 찾을 수 있습니다 [지원 되는 Azure 모니터로 메트릭](../monitoring-and-diagnostics/monitoring-supported-metrics.md) hello "Microsoft.Compute/virtualMachineScaleSets" 제목 아래에서 더 많은 고급 자동 크기 조정 옵션 일정 기반 자동 크기 조정 등 경고 시스템과 webhook toointegrate를 사용 하 여 사용할 수 있습니다.

## <a name="monitoring-your-scale-set"></a>확장 집합 모니터링
hello [Azure 포털](https://portal.azure.com) 목록 크기 조정 설정 하 고 해당 속성을 보여 줍니다. 또한 hello 포털 관리 작업을 지원합니다. 확장 집합과 확장 집합 내 개별 VM에서 관리 작업을 수행할 수 있습니다. 또한 hello 포털 사용자 지정 가능한 리소스 사용량 그래프를 제공합니다. 

Azure 리소스의 JSON 정의 기초가 되는 hello를 편집 하거나 toosee를 필요한 경우 사용할 수도 있습니다 [Azure 리소스 탐색기](https://resources.azure.com)합니다. 크기 집합은 hello Microsoft.Compute Azure 리소스 공급자에서 리소스입니다. 이 사이트에서 링크를 따라 hello를 확장 하 여 확인할 수 있습니다.

**구독** > **사용자의 구독** > **resourceGroups** > **공급자** > **Microsoft.Compute** > **virtualMachineScaleSets** > **사용자의 확장 집합** 등

## <a name="scale-set-scenarios"></a>확장 집합 시나리오
이 섹션에서는 몇 가지 일반적인 크기 집합 시나리오를 나열합니다. 일부 높은 수준의 Azure 서비스(예: Batch, Service Fabric, Container Service)에서 이러한 시나리오를 사용합니다.

* **RDP를 사용 하 여 또는 SSH tooconnect tooscale 설정 인스턴스**: 가상 네트워크 내부에 크기 집합 생성 및 개별 Vm 크기 집합 hello에에서는 기본적으로 공용 IP 주소를 할당 되지 않고 있습니다. 이 정책은 hello 비용을 방지 하 고 관리 오버 헤드 별도 공용 IP를 할당 주소를 계산 표에 tooall hello 노드. Vm을 설정 하는 외부 연결 tooscale 직접 필요가 경우는 눈금 집합 tooautomatically 할당 공용 IP 주소 toonew Vm을 구성할 수 있습니다. 또는 가상 네트워크에 할당 될 수 있는 공용 IP 주소 예를 들어 부하 분산 장치 및 독립 실행형 가상 컴퓨터 tooVMs 다른 리소스에서에 연결할 수 있습니다. 
* **NAT 규칙을 사용 하 여 tooVMs 연결**: 공용 IP 주소를 만들, tooa 부하 분산 장치를 할당 및는 인바운드 NAT 풀 정의할 수 있습니다. 이러한 동작은 hello hello 크기 집합의 VM에 IP 주소 tooa 포트의 포트를 매핑합니다. 예:
  
  | 원본 | 원본 포트 | 대상 | 대상 포트 |
  | --- | --- | --- | --- |
  |  공용 IP |포트 50000 |vmss\_0 |포트 22 |
  |  공용 IP |포트 50001 |vmss\_1 |포트 22 |
  |  공용 IP |포트 50002 |vmss\_2 |포트 22 |
  
   [이 예제](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-nat), NAT 규칙 정의 tooenable 크기 집합의 SSH 연결 tooevery VM은, 주소는 단일 공용 IP를 사용 하 여 합니다.
  
   [이 예제에서는](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-nat) 동일 RDP 및 Windows hello지 않습니다.
* **"Jumpbox"를 사용 하 여 tooVMs 연결**: 동일한 가상 네트워크, hello hello에 크기 집합 및 독립 실행형 VM 만드는 경우 독립 실행형 hello와 VM 크기 집합 VM 가상 hello에 정의 된 대로 해당 내부 ip 주소를 사용 하 여 다른 주소, tooone 연결할 수 있습니다 네트워크 또는 서브넷입니다. 공용 IP 주소를 만들고 toohello 독립 실행형 VM을 할당 하는 경우에 RDP 또는 SSH tooconnect toohello 독립 실행형 VM을 사용할 수 있습니다. 다음에서 연결할 수 컴퓨터 tooyour 크기 집합 인스턴스는 합니다. 본질적으로 간단한 확장 집합이 기본 구성에 공용 IP 주소를 포함하는 간단한 독립 실행형 VM보다 더 안전하다는 것을 알 수 있습니다.
  
   예를 들어 [이 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-jumpbox)은 독립 실행형 VM으로 간단한 확장 집합을 배포합니다. 
* **부하 분산 집합 인스턴스 tooscale**: 라운드 로빈 방식을 사용 하 여 Vm의 toodeliver tooa 계산 클러스터를 작업 하려는 경우 구성할 수 있습니다는 Azure 부하 분산 장치 계층 4 부하 분산 규칙으로 적절 하 게 합니다. 프로브를 정의할 수 있습니다 tooverify을 ping 하 여 응용 프로그램을 실행 하는 포트와 지정 된 프로토콜, 간격 및 요청 경로입니다. 또한 Azure [Application Gateway](https://azure.microsoft.com/services/application-gateway/)는 보다 복잡한 계층 7 부하 분산 시나리오와 함께 확장 집합을 지원합니다.
  
   [이 예제에서는](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-web-ssl) Apache 웹 서버를 실행 하며 각 VM을 수신 하는 부하 분산 장치 toobalance hello 부하를 사용 하는 확장 집합을 만듭니다. (및을 살펴보고 hello Microsoft.Network/loadBalancers 리소스 종류 및 networkProfile virtualMachineScaleSet에 extensionProfile.)

   [이 Linux 예제](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-app-gateway)와 [이 Windows 예제](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-app-gateway)는 Application Gateway를 사용합니다.  

* **확장 집합을 PaaS 클러스터 관리자에서 계산 클러스터로 배포**: 확장 집합을 차세대 작업자 역할이라고 설명하기도 합니다. 경우에 올바른 설명을 실행지 않습니다 혼동 눈금의 hello 위험 집합 기능 Azure 클라우드 서비스 기능을 통해. 어떤 의미에서 확장 집합은 진정한 작업자 역할 또는 작업자 리소스를 제공합니다. 이들은 플랫폼/런타임이 독립적이고, 사용자 지정이 가능하며 Azure Resource Manager IaaS에 통합되는 일반화된 계산 리소스입니다.
  
   Cloud Services 작업자 역할은 플랫폼/런타임 지원 면에서 제한됩니다(Windows 플랫폼 이미지에만 해당). 하지만 VIP 교환, 구성 가능한 업그레이드 설정 및 런타임/앱 배포별 설정 등의 서비스는 포함됩니다. 이러한 서비스는 크기 집합에서 *아직* 사용할 수 없지만 Azure Service Fabric 등 다른 상위 수준의 PaaS 서비스에서 제공됩니다. 크기 집합을 PaaS를 지원하는 인프라로 주목할 수 있습니다. [Service Fabric](https://azure.microsoft.com/services/service-fabric/)과 같은 PaaS 솔루션이 이 인프라에 구축됩니다.
  
   이 방식의 [이 예제](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)에서 [Azure Container Service](https://azure.microsoft.com/services/container-service/)는 크기 조정 설정에 따라 컨테이너 조정자로 클러스터를 배포합니다.

## <a name="scale-set-performance-and-scale-guidance"></a>확장 집합 성능 및 크기 조정 지침
* 소수 집합을 지원 too1, 000 Vm 합니다. 작성 하 고 사용자 지정 VM 이미지를 업로드 하는 경우 hello 제한은 100입니다. 대규모 확장 집합 사용 시 고려 사항은 [대규모 가상 컴퓨터 확장 집합과 작동](virtual-machine-scale-sets-placement-groups.md)을 참조하세요.
* Toopre 없는-Azure 저장소 계정 toouse 크기 집합을 만듭니다. 크기 조정 설정 지원 Azure 디스크 negate hello 저장소 계정당 디스크 수에 대 한 성능 문제를 관리 합니다. 자세한 내용은 [Azure 가상 컴퓨터 확장 집합 및 관리되는 디스크](virtual-machine-scale-sets-managed-disks.md)를 참조하세요.
* 보다 빠르고 예측 가능한 VM 프로비전 시간 및 향상된 I/O 성능을 위해 Azure Storage 대신 Azure Premium Storage를 사용하는 것이 좋습니다.
* hello 코어 할당량 배포 중인 hello 지역에 만들 수는 Vm의 hello 수를 제한 합니다. Azure 클라우드 서비스와 함께 사용 된 코어 높은 한도 현재 있는 경우에 계산 할당량 제한을 toocontact 고객 지원 tooincrease 할 수 있습니다. tooquery이 Azure CLI 명령을 실행 하 여 할당량: `azure vm list-usage`합니다. 또는 이 PowerShell 명령 `Get-AzureRmVMUsage`를 실행합니다.

## <a name="frequently-asked-questions-for-scale-sets"></a>크기 집합에 대한 질문과 대답
**Q.** 크기 집합에 포함할 수 있는 VM 수는 몇 개인가요?

**A.** 크기 집합 0 too1 가질 수 있습니다, 또는 플랫폼 이미지를 기반으로 한 000 Vm 0 too100 Vm 이미지를 기반으로 사용자 지정 합니다. 

**Q.** 크기 집합 내에서 데이터 디스크가 지원되나요?

**A.** 예. 크기 집합 tooall Vm hello 집합에 적용 되는 연결 된 데이터 디스크 구성을 정의할 수 있습니다. 자세한 내용은 [Azure 크기 조정 설정 및 연결된 데이터 디스크](virtual-machine-scale-sets-attached-disks.md)를 참조하세요. 데이터를 저장하는 기타 옵션은 다음과 같습니다.

* Azure 파일(SMB 공유 드라이브)
* OS 드라이브
* 임시 드라이브(Azure Storage에서 지원되지 않는 로컬 드라이브)
* Azure 데이터 서비스(예: Azure 테이블, Azure Blob)
* 외부 데이터 서비스(예: 원격 데이터베이스)

**Q.** 크기 집합을 지원하는 Azure 지역은 어디인가요?

**A.** 모든 지역에서 크기 집합을 지원합니다.

**Q.** 사용자 지정 이미지를 사용하여 크기 집합을 어떻게 만드나요?

**A.** 사용자 지정 이미지 VHD를 기반으로 Managed Disk를 만들고 크기 집합 템플릿에서 참조합니다. [예를 들면 다음과 같습니다](https://github.com/chagarw/MDPP/tree/master/101-vmss-custom-os).

**Q.** 줄이는 경우 내 크기 집합 Vm 제거 되는 20 too15에서 용량?

**A.** 가상 컴퓨터는 hello에 크기 균등 하 게 업데이트 도메인과 오류 도메인 toomaximize 가용성 집합에서 제거 됩니다. 가장 높은 Id를 먼저 제거 하는 hello로 Vm입니다.

**Q.** 경우에 어떻게 다음 15 too18에서 hello 용량 증가?

**A.** Too18 용량을 늘려야 하는 경우 3 개의 새 Vm이 생성 됩니다. 매번 hello VM 인스턴스 ID는 hello 이전 가장 높은 값 (예를 들어 20, 21, 22) 증가 합니다. VM은 장애 도메인과 업데이트 도메인에 균등하게 분배됩니다.

**Q.** 크기 집합에서 여러 확장을 사용하는 경우, 실행 순서를 강제로 적용할 수 있나요?

**A.** 직접적으로 하지만 hello customScript 확장에 대 한 스크립트는 다른 확장 toofinish 기다릴 수 있습니다. Hello 블로그 게시물에서 시퀀싱 확장에 대 한 추가 지침을 가져올 수 있습니다 [Azure VM 크기 집합의 확장 시퀀싱](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/)합니다.

**Q.** 크기 집합은 Azure 가용성 집합과 작업이 가능한가요?

**A.** 예. 확장 집합은 5개의 장애 도메인과 5개의 업데이트 도메인이 있는 암시적인 가용성 집합입니다. 배율 100 개 이상의 Vm 집합이 걸쳐 여러 *배치 그룹*, 되 가용성 집합을 동등한 toomultiple 합니다. 배치 그룹에 대한 자세한 내용은 [대규모 가상 컴퓨터 확장 집합과 작동](virtual-machine-scale-sets-placement-groups.md)을 참조하세요. Vm의 가용성 집합에에서 존재할 수 hello 동일한 가상 네트워크의 Vm 크기 집합으로 합니다. 일반적인 구성은 tooput 제어 노드 (여기 종종 고유한 구성 필요) Vm 가용성을 설정 하 고 hello 크기 집합의 데이터 노드를 배치 합니다.

Hello에 설정 하는 눈금에 대 한 자세한 답변 tooquestions 찾을 수 있습니다 [FAQ를 설정 하는 Azure 가상 컴퓨터 크기](virtual-machine-scale-sets-faq.md)합니다.
