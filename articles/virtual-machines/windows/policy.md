---
title: "Azure에서 Windows VM에 정책을 사용하여 보안 적용 | Microsoft Docs"
description: "Azure Resource Manager Windows 가상 컴퓨터에 정책을 적용하는 방법"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0b71ba54-01db-43ad-9bca-8ab358ae141b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: kasing
ms.openlocfilehash: 246f5958478fd6d9afc9ba990413ab08429bd25d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="apply-policies-to-windows-vms-with-azure-resource-manager"></a><span data-ttu-id="66a3b-103">Azure Resource Manager를 사용하여 Windows VM에 정책 적용</span><span class="sxs-lookup"><span data-stu-id="66a3b-103">Apply policies to Windows VMs with Azure Resource Manager</span></span>
<span data-ttu-id="66a3b-104">조직은 정책을 사용하여 엔터프라이즈 전체에 다양한 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span></span> <span data-ttu-id="66a3b-105">원하는 동작을 적용하여 조직의 성공에 기여함과 동시에 위험을 완화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span></span> <span data-ttu-id="66a3b-106">이 문서에서는 Azure Resource Manager 정책을 사용하여 조직의 Virtual Machines에 대해 원하는 동작을 정의하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-106">In this article, we describe how you can use Azure Resource Manager policies to define the desired behavior for your organization’s Virtual Machines.</span></span>

<span data-ttu-id="66a3b-107">정책에 대한 소개는 [정책을 사용하여 리소스 및 컨트롤 액세스 관리](../../azure-resource-manager/resource-manager-policy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66a3b-107">For an introduction to policies, see [Use Policy to manage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="66a3b-108">허용되는 Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="66a3b-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="66a3b-109">조직에 대한 가상 컴퓨터가 응용 프로그램과 호환되는지 확인하기 위해 허용된 운영 체제를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-109">To ensure that virtual machines for your organization are compatible with an application, you can restrict the permitted operating systems.</span></span> <span data-ttu-id="66a3b-110">다음 정책 예제에서는 Windows Server 2012 R2 Datacenter Virtual Machines만 만드는 것을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-110">In the following policy example, you allow only Windows Server 2012 R2 Datacenter Virtual Machines to be created:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "MicrosoftWindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "WindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "2012-R2-Datacenter"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

<span data-ttu-id="66a3b-111">와일드 카드를 사용하여 모든 Windows Server Datacenter 이미지를 허용하도록 이전 정책을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-111">Use a wild card to modify the preceding policy to allow any Windows Server Datacenter image:</span></span>

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

<span data-ttu-id="66a3b-112">anyOf를 사용하여 모든 Windows Server 2012 R2 Datacenter 이상 이미지를 허용하도록 이전 정책을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-112">Use anyOf to modify the preceding policy to allow any Windows Server 2012 R2 Datacenter or higher image:</span></span>

```json
{
  "anyOf": [
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2012-R2-Datacenter*"
    },
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2016-Datacenter*"
    }
  ]
}
```

<span data-ttu-id="66a3b-113">정책 필드에 대한 자세한 내용은 [정책 별칭](../../azure-resource-manager/resource-manager-policy.md#aliases)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66a3b-113">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="66a3b-114">관리 디스크</span><span class="sxs-lookup"><span data-stu-id="66a3b-114">Managed disks</span></span>

<span data-ttu-id="66a3b-115">관리 디스크 사용을 요구하려면 다음 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-115">To require the use of managed disks, use the following policy:</span></span>

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a><span data-ttu-id="66a3b-116">Virtual Machines에 대한 이미지 </span><span class="sxs-lookup"><span data-stu-id="66a3b-116">Images for Virtual Machines</span></span>

<span data-ttu-id="66a3b-117">보안상의 이유로 승인된 사용자 지정 이미지만 환경에 배포하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-117">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="66a3b-118">승인된 이미지를 포함하는 리소스 그룹이나 특정한 승인된 이미지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-118">You can specify either the resource group that contains the approved images, or the specific approved images.</span></span>

<span data-ttu-id="66a3b-119">다음 예제에서는 승인된 리소스 그룹의 이미지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-119">The following example requires images from an approved resource group:</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

<span data-ttu-id="66a3b-120">다음 예제에서는 승인된 이미지 ID를 명시합니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-120">The following example specifies the approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="66a3b-121">가상 컴퓨터 확장 </span><span class="sxs-lookup"><span data-stu-id="66a3b-121">Virtual Machine extensions</span></span>

<span data-ttu-id="66a3b-122">특정 유형의 확장을 사용하지 못하게 하고자 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-122">You may want to forbid usage of certain types of extensions.</span></span> <span data-ttu-id="66a3b-123">예를 들어 한 확장이 특정 사용자 지정 가상 컴퓨터 이미지와 호환되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-123">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="66a3b-124">다음 예제에서는 특정 확장을 차단하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-124">The following example shows how to block a specific extension.</span></span> <span data-ttu-id="66a3b-125">게시자 및 유형을 사용하여 차단할 확장을 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-125">It uses publisher and type to determine which extension to block.</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="azure-hybrid-use-benefit"></a><span data-ttu-id="66a3b-126">AHUB(Azure Hybrid Use Benefit)</span><span class="sxs-lookup"><span data-stu-id="66a3b-126">Azure Hybrid Use Benefit</span></span>

<span data-ttu-id="66a3b-127">온-프레미스 라이선스가 있는 경우 가상 컴퓨터에서 라이선스 요금을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-127">When you have an on-premise license, you can save the license fee on your virtual machines.</span></span> <span data-ttu-id="66a3b-128">라이선스가 없는 경우 이 옵션이 금지됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-128">When you don't have the license, you should forbid the option.</span></span> <span data-ttu-id="66a3b-129">다음 정책에서는 AHUB(Azure Hybrid Use Benefit)의 사용을 금지합니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-129">The following policy forbids usage of Azure Hybrid Use Benefit (AHUB):</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in":[ "Microsoft.Compute/virtualMachines","Microsoft.Compute/VirtualMachineScaleSets"]
            },
            {
                "field": "Microsoft.Compute/licenseType",
                "exists": true
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="66a3b-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="66a3b-130">Next steps</span></span>
* <span data-ttu-id="66a3b-131">앞의 예제와 표시된 바와 같이 정책 규칙을 정의한 후에는 정책 정의를 만들고 범위에 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-131">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="66a3b-132">범위는 구독, 리소스 그룹 또는 리소스일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a3b-132">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="66a3b-133">포털을 통해 정책을 할당하려면 [Azure Portal을 사용하여 리소스 정책 할당 및 관리](../../azure-resource-manager/resource-manager-policy-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66a3b-133">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="66a3b-134">REST API, PowerShell 또는 Azure CLI를 통해 정책을 할당하려면 [스크립트를 통해 정책 할당 및 관리](../../azure-resource-manager/resource-manager-policy-create-assign.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66a3b-134">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="66a3b-135">리소스 정책에 대한 소개는 [리소스 정책 개요](../../azure-resource-manager/resource-manager-policy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66a3b-135">For an introduction to resource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="66a3b-136">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](../../azure-resource-manager/resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66a3b-136">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
