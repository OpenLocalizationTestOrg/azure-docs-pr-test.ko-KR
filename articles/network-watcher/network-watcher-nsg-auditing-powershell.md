---
title: "Azure 네트워크 감시자 보안 그룹 보기를 사용한 aaaAutomate NSG 감사 | Microsoft Docs"
description: "이 페이지는 방법에 대해 설명 tooconfigure 네트워크 보안 그룹의 감사"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 24fc418c433fceaf55a74b7c3b0e354dc46c8729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="ddfd3-103">Azure Network Watcher 보안 그룹 보기를 사용하여 NSG 감사 자동화</span><span class="sxs-lookup"><span data-stu-id="ddfd3-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="ddfd3-104">고객은 인프라의 hello 보안 상태를 확인 하는 hello 챌린지 길어지는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-104">Customers are often faced with hello challenge of verifying hello security posture of their infrastructure.</span></span> <span data-ttu-id="ddfd3-105">이 문제는 Azure의 VM에 대해서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="ddfd3-106">유사한 보안 프로필을 적용 하는 hello 보안 그룹 NSG (네트워크) 규칙에 따라 중요 한 toohave 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-106">It is important toohave a similar security profile based on hello Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="ddfd3-107">Hello 보안 그룹 보기를 사용 하 여 VM에 NSG 규칙이 적용 되는 tooa 목록이 hello를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-107">Using hello Security Group View, you can now get hello list of rules applied tooa VM within an NSG.</span></span> <span data-ttu-id="ddfd3-108">골든 NSG 보안 프로필을 정의 및 시작한 매주 주기로 보안 그룹 보기 및 hello 출력 toohello 골든 프로 파일 비교을 보고서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare hello output toohello golden profile and create a report.</span></span> <span data-ttu-id="ddfd3-109">이러한 방식으로 식별할 수 있습니다를 쉽게 toohello 보안 프로필 규정을 준수 하지 않는 모든 hello Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-109">This way you can identify with ease all hello VMs that do not conform toohello prescribed security profile.</span></span>

<span data-ttu-id="ddfd3-110">네트워크 보안 그룹에 대해 잘 모르는 경우 [네트워크 보안 개요](../virtual-network/virtual-networks-nsg.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ddfd3-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="ddfd3-111">Before you begin</span></span>

<span data-ttu-id="ddfd3-112">알려진된 좋은 기준선 toohello 보안 그룹을 비교이 시나리오에서는 가상 컴퓨터에 대해 반환 된 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-112">In this scenario, you compare a known good baseline toohello security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="ddfd3-113">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="ddfd3-114">hello 시나리오는 또한 적합 한 가상 컴퓨터가 리소스 그룹 사용 toobe 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="ddfd3-115">시나리오</span><span class="sxs-lookup"><span data-stu-id="ddfd3-115">Scenario</span></span>

<span data-ttu-id="ddfd3-116">이 문서에서 다루는 hello 시나리오는 가상 컴퓨터에 대 한 hello 보안 그룹 보기를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-116">hello scenario covered in this article gets hello security group view for a virtual machine.</span></span>

<span data-ttu-id="ddfd3-117">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-117">In this scenario, you will:</span></span>

- <span data-ttu-id="ddfd3-118">알려진 적합한 규칙 집합 검색</span><span class="sxs-lookup"><span data-stu-id="ddfd3-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="ddfd3-119">Rest API로 가상 컴퓨터 검색</span><span class="sxs-lookup"><span data-stu-id="ddfd3-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="ddfd3-120">가상 컴퓨터에 대한 보안 그룹 보기 가져오기</span><span class="sxs-lookup"><span data-stu-id="ddfd3-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="ddfd3-121">응답 평가</span><span class="sxs-lookup"><span data-stu-id="ddfd3-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="ddfd3-122">규칙 집합 검색</span><span class="sxs-lookup"><span data-stu-id="ddfd3-122">Retrieve rule set</span></span>

<span data-ttu-id="ddfd3-123">이 예에서 hello 첫 단계는 기존 기준을 toowork를입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-123">hello first step in this example is toowork with an existing baseline.</span></span> <span data-ttu-id="ddfd3-124">hello 다음 예제는 hello를 사용 하 여 기존 네트워크 보안 그룹에서 추출 된 일부 json `Get-AzureRmNetworkSecurityGroup` hello 기준으로이 예제에 사용 되는 cmdlet입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-124">hello following example is some json extracted from an existing Network Security Group using hello `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as hello baseline for this example.</span></span>

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-toopowershell-objects"></a><span data-ttu-id="ddfd3-125">규칙 집합 tooPowerShell 개체 변환</span><span class="sxs-lookup"><span data-stu-id="ddfd3-125">Convert rule set tooPowerShell objects</span></span>

<span data-ttu-id="ddfd3-126">이 단계에서는 이전이 예제에 대 한 네트워크 보안 그룹 hello에 예상된 toobe는 hello 규칙으로 작성 된 json 파일을 읽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-126">In this step, we are reading a json file that was created earlier with hello rules that are expected toobe on hello Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="ddfd3-127">Network Watcher 검색</span><span class="sxs-lookup"><span data-stu-id="ddfd3-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="ddfd3-128">hello 다음 단계는 tooretrieve hello 네트워크 감시자 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-128">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="ddfd3-129">hello `$networkWatcher` 변수 toohello 전달 `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-129">hello `$networkWatcher` variable is passed toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="ddfd3-130">VM 확인</span><span class="sxs-lookup"><span data-stu-id="ddfd3-130">Get a VM</span></span>

<span data-ttu-id="ddfd3-131">가상 컴퓨터는 필요한 toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-131">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="ddfd3-132">다음 예제는 hello VM 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-132">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="ddfd3-133">보안 그룹 보기 검색</span><span class="sxs-lookup"><span data-stu-id="ddfd3-133">Retrieve security group view</span></span>

<span data-ttu-id="ddfd3-134">hello 다음 단계 tooretrieve hello 보안 그룹 뷰 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-134">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="ddfd3-135">이 결과 앞에 나온 비교 toohello "초기" json입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-135">This result is compared toohello "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a><span data-ttu-id="ddfd3-136">Hello 결과 분석</span><span class="sxs-lookup"><span data-stu-id="ddfd3-136">Analyzing hello results</span></span>

<span data-ttu-id="ddfd3-137">hello 응답 네트워크 인터페이스로 그룹화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-137">hello response is grouped by Network interfaces.</span></span> <span data-ttu-id="ddfd3-138">hello 다양 한 유형의 반환 되는 규칙 적용 되며 기본 보안 규칙 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-138">hello different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="ddfd3-139">hello 결과 적용 방법을, 서브넷 또는 가상 NIC에 따라 구분 추가</span><span class="sxs-lookup"><span data-stu-id="ddfd3-139">hello result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="ddfd3-140">hello 다음 PowerShell 스크립트 결과 비교 hello의 hello NSG의 보안 그룹 보기 tooan 기존 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-140">hello following PowerShell script compares hello results of hello Security Group View tooan existing output of an NSG.</span></span> <span data-ttu-id="ddfd3-141">hello 다음 예제는 hello 결과와 비교할 수는 방법의 간단한 예 `Compare-Object` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-141">hello following example is a simple example of how hello results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="ddfd3-142">다음 예제는 hello hello 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-142">hello following example is hello result.</span></span> <span data-ttu-id="ddfd3-143">Hello 첫 번째 규칙 집합에 있는 hello 규칙 2가 hello 비교에 존재 하지 않는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-143">You can see two of hello rules that were in hello first rule set were not present in hello comparison.</span></span>

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a><span data-ttu-id="ddfd3-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ddfd3-144">Next steps</span></span>

<span data-ttu-id="ddfd3-145">설정이 변경 되었을 경우 참조 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hello 네트워크 보안 그룹 및 보안 규칙을 문제가 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfd3-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are in question.</span></span>













