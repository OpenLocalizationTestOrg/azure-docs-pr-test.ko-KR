---
title: "Azure 네트워크 감시자 보안 그룹 보기-Azure CLI 1.0을 통한 aaaAnalyze 네트워크 보안 | Microsoft Docs"
description: "이 문서는 어떻게 Azure CLI 1.0 toouse tooanalyze a 가상 컴퓨터 보안 보안 그룹을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 96383a734b94d215d5b0f3d47339e46940d700b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="50cb6-103">Azure CLI 1.0을 사용하는 보안 그룹 보기에서 가상 컴퓨터 보안 분석</span><span class="sxs-lookup"><span data-stu-id="50cb6-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="50cb6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="50cb6-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="50cb6-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="50cb6-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="50cb6-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="50cb6-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="50cb6-107">REST API</span><span class="sxs-lookup"><span data-stu-id="50cb6-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="50cb6-108">보안 그룹 보기 구성 하 고 효과적인 네트워크 보안 규칙을 적용된 tooa 가상 컴퓨터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb6-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="50cb6-109">이 기능은 유용 tooaudit은 네트워크 보안 그룹 진단 및 VM tooensure 트래픽이에 구성 되어 있는 규칙은 올바르게 허용 또는 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb6-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="50cb6-110">이 문서에서는 보여줍니다 tooretrieve hello 구성 하는 방법 및 Azure CLI를 사용 하 여 효과적인 보안 규칙 tooa 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="50cb6-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>

<span data-ttu-id="50cb6-111">이 문서에서는 Windows, Mac 및 Linux에 사용할 수 있는 플랫폼 간 Azure CLI 1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb6-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="50cb6-112">Network Watcher는 현재 CLI 지원을 위한 Azure CLI 1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb6-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="50cb6-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="50cb6-113">Before you begin</span></span>

<span data-ttu-id="50cb6-114">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb6-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="50cb6-115">시나리오</span><span class="sxs-lookup"><span data-stu-id="50cb6-115">Scenario</span></span>

<span data-ttu-id="50cb6-116">이 문서에서 다루는 hello 시나리오를 구성 하는 hello 및 지정된 된 가상 컴퓨터에 대 한 효과적인 보안 규칙 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb6-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="50cb6-117">VM 확인</span><span class="sxs-lookup"><span data-stu-id="50cb6-117">Get a VM</span></span>

<span data-ttu-id="50cb6-118">가상 컴퓨터는 필요한 toorun hello `vm list` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="50cb6-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="50cb6-119">hello 다음 명령은 나열 된 리소스 그룹에에서 가상 machinese hello:</span><span class="sxs-lookup"><span data-stu-id="50cb6-119">hello following command lists hello virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="50cb6-120">Hello 가상 컴퓨터를 알게 되 면 hello를 사용할 수 있습니다 `vm show` cmdlet tooget 상대방이 리소스 Id:</span><span class="sxs-lookup"><span data-stu-id="50cb6-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="50cb6-121">보안 그룹 보기 검색</span><span class="sxs-lookup"><span data-stu-id="50cb6-121">Retrieve security group view</span></span>

<span data-ttu-id="50cb6-122">hello 다음 단계 tooretrieve hello 보안 그룹 뷰 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="50cb6-122">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="50cb6-123">추가 hello "-json" 플래그 json에서 hello 결과 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb6-123">Adding hello "--json" flag will format hello results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-hello-results"></a><span data-ttu-id="50cb6-124">Hello 결과 보기</span><span class="sxs-lookup"><span data-stu-id="50cb6-124">Viewing hello results</span></span>

<span data-ttu-id="50cb6-125">hello 다음 예제는 반환 된 hello 결과의 축약된 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb6-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="50cb6-126">hello 결과 표시 모든 hello 효과적이 고 적용 된 보안 규칙의 그룹에 세분화 hello 가상 컴퓨터에서 **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, 및  **EffectiveSecurityRules**합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb6-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="50cb6-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50cb6-127">Next steps</span></span>

<span data-ttu-id="50cb6-128">방문 [감사 보안 그룹 NSG (네트워크)와 네트워크 감시자](network-watcher-nsg-auditing-powershell.md) toolearn 방법을 네트워크 보안 그룹의 tooautomate 유효성 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb6-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="50cb6-129">Hello 보안 규칙을 방문 하 여 적용 된 tooyour 네트워크 리소스에 대 한 자세한 [보안 그룹, 개요 보기](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="50cb6-129">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
