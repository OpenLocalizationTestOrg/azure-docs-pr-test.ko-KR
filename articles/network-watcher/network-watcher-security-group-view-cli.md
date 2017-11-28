---
title: "Azure 네트워크 감시자 보안 그룹 보기-Azure CLI 2.0을 통한 aaaAnalyze 네트워크 보안 | Microsoft Docs"
description: "이 문서는 어떻게 Azure CLI 2.0 toouse tooanalyze a 가상 컴퓨터 보안 보안 그룹을 설명 합니다."
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
ms.openlocfilehash: 31a4cd628f54d7548f495251fd275f099e79a060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a><span data-ttu-id="2c8d5-103">Azure CLI 2.0을 사용하는 보안 그룹 보기에서 가상 컴퓨터 보안 분석</span><span class="sxs-lookup"><span data-stu-id="2c8d5-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2c8d5-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c8d5-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="2c8d5-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2c8d5-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="2c8d5-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2c8d5-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="2c8d5-107">REST API</span><span class="sxs-lookup"><span data-stu-id="2c8d5-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="2c8d5-108">보안 그룹 보기 구성 하 고 효과적인 네트워크 보안 규칙을 적용된 tooa 가상 컴퓨터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="2c8d5-109">이 기능은 유용 tooaudit은 네트워크 보안 그룹 진단 및 VM tooensure 트래픽이에 구성 되어 있는 규칙은 올바르게 허용 또는 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="2c8d5-110">이 문서에서는 보여줍니다 tooretrieve hello 구성 하는 방법 및 Azure CLI를 사용 하 여 효과적인 보안 규칙 tooa 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="2c8d5-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>


<span data-ttu-id="2c8d5-111">이 문서에서는 Windows, Mac 및 Linux에 대 한 사용 하지 않는 hello 리소스 관리 배포 모델, Azure CLI 2.0에 대 한 우리의 차세대 CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="2c8d5-112">이 문서의 단계를 tooperform hello, 너무 필요한[Mac, Linux 및 Windows Azure CLI ()에 대 한 hello Azure 명령줄 인터페이스 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2c8d5-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="2c8d5-113">Before you begin</span></span>

<span data-ttu-id="2c8d5-114">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="2c8d5-115">시나리오</span><span class="sxs-lookup"><span data-stu-id="2c8d5-115">Scenario</span></span>

<span data-ttu-id="2c8d5-116">이 문서에서 다루는 hello 시나리오를 구성 하는 hello 및 지정된 된 가상 컴퓨터에 대 한 효과적인 보안 규칙 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="2c8d5-117">VM 확인</span><span class="sxs-lookup"><span data-stu-id="2c8d5-117">Get a VM</span></span>

<span data-ttu-id="2c8d5-118">가상 컴퓨터는 필요한 toorun hello `vm list` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="2c8d5-119">hello 다음 명령은 나열 리소스 그룹의 hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-119">hello following command lists hello virtual machines in a resource group:</span></span>

```azurecli
az vm list -resource-group resourceGroupName
```

<span data-ttu-id="2c8d5-120">Hello 가상 컴퓨터를 알게 되 면 hello를 사용할 수 있습니다 `vm show` cmdlet tooget 상대방이 리소스 Id:</span><span class="sxs-lookup"><span data-stu-id="2c8d5-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="2c8d5-121">보안 그룹 보기 검색</span><span class="sxs-lookup"><span data-stu-id="2c8d5-121">Retrieve security group view</span></span>

<span data-ttu-id="2c8d5-122">hello 다음 단계 tooretrieve hello 보안 그룹 뷰 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-122">hello next step is tooretrieve hello security group view result.</span></span>

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-hello-results"></a><span data-ttu-id="2c8d5-123">Hello 결과 보기</span><span class="sxs-lookup"><span data-stu-id="2c8d5-123">Viewing hello results</span></span>

<span data-ttu-id="2c8d5-124">hello 다음 예제는 반환 된 hello 결과의 축약된 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-124">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="2c8d5-125">hello 결과 표시 모든 hello 효과적이 고 적용 된 보안 규칙의 그룹에 세분화 hello 가상 컴퓨터에서 **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, 및  **EffectiveSecurityRules**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-125">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
      "resourceGroup": "{resourceGroupName}",
      "securityRuleAssociations": {
        "defaultSecurityRules": [
          {
            "access": "Allow",
            "description": "Allow inbound traffic from all VMs in VNET",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "*",
            "direction": "Inbound",
            "etag": null,
            "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups//providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/AllowVnetInBound",
            "name": "AllowVnetInBound",
            "priority": 65000,
            "protocol": "*",
            "provisioningState": "Succeeded",
            "resourceGroup": "",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "*"
          }...
        ],
        "effectiveSecurityRules": [
          {
            "access": "Deny",
            "destinationAddressPrefix": "*",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": null,
            "expandedSourceAddressPrefix": null,
            "name": "DefaultOutboundDenyAll",
            "priority": 65500,
            "protocol": "All",
            "sourceAddressPrefix": "*",
            "sourcePortRange": "0-65535"
          },
          {
            "access": "Allow",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "expandedSourceAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "name": "DefaultRule_AllowVnetOutBound",
            "priority": 65000,
            "protocol": "All",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "0-65535"
          },...
        ],
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "resourceGroup": "{resourceGroupName}",
          "securityRules": [
            {
              "access": "Allow",
              "description": null,
              "destinationAddressPrefix": "*",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "etag": "W/\"efb606c1-2d54-475a-ab20-da3f80393577\"",
              "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "name": "default-allow-rdp",
              "priority": 1000,
              "protocol": "TCP",
              "provisioningState": "Succeeded",
              "resourceGroup": "{resourceGroupName}",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          ]
        },
        "subnetAssociation": null
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="2c8d5-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c8d5-126">Next steps</span></span>

<span data-ttu-id="2c8d5-127">방문 [감사 보안 그룹 NSG (네트워크)와 네트워크 감시자](network-watcher-nsg-auditing-powershell.md) toolearn 방법을 네트워크 보안 그룹의 tooautomate 유효성 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="2c8d5-128">Hello 보안 규칙을 방문 하 여 적용 된 tooyour 네트워크 리소스에 대 한 자세한 [보안 그룹, 개요 보기](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2c8d5-128">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
