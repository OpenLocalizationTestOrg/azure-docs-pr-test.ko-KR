---
title: "Azure에서 Linux VM에 정책을 사용하여 보안 적용 | Microsoft Docs"
description: "Azure Resource Manager Linux 가상 컴퓨터에 정책을 적용하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 58eaab4fa03afc1e6a5e38bef691cce62a921ea9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="apply-policies-to-linux-vms-with-azure-resource-manager"></a><span data-ttu-id="3dde0-103">Azure Resource Manager를 사용하여 Linux VM에 정책 적용</span><span class="sxs-lookup"><span data-stu-id="3dde0-103">Apply policies to Linux VMs with Azure Resource Manager</span></span>
<span data-ttu-id="3dde0-104">조직은 정책을 사용하여 엔터프라이즈 전체에 다양한 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span></span> <span data-ttu-id="3dde0-105">원하는 동작을 적용하여 조직의 성공에 기여함과 동시에 위험을 완화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span></span> <span data-ttu-id="3dde0-106">이 문서에서는 Azure Resource Manager 정책을 사용하여 조직의 Virtual Machines에 대해 원하는 동작을 정의하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-106">In this article, we describe how you can use Azure Resource Manager policies to define the desired behavior for your organization's Virtual Machines.</span></span>

<span data-ttu-id="3dde0-107">정책에 대한 소개는 [정책을 사용하여 리소스 및 컨트롤 액세스 관리](../../azure-resource-manager/resource-manager-policy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3dde0-107">For an introduction to policies, see [Use Policy to manage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="3dde0-108">허용되는 Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="3dde0-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="3dde0-109">조직에 대한 가상 컴퓨터가 응용 프로그램과 호환되는지 확인하기 위해 허용된 운영 체제를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-109">To ensure that virtual machines for your organization are compatible with an application, you can restrict the permitted operating systems.</span></span> <span data-ttu-id="3dde0-110">다음 정책 예제에서는 Ubuntu 14.04.2-LTS Virtual Machines만 만들 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-110">In the following policy example, you allow only Ubuntu 14.04.2-LTS Virtual Machines to be created.</span></span>

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
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
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

<span data-ttu-id="3dde0-111">와일드 카드를 사용하여 모든 Ubuntu LTS 이미지를 허용하도록 이전 정책을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-111">Use a wild card to modify the preceding policy to allow any Ubuntu LTS image:</span></span> 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

<span data-ttu-id="3dde0-112">정책 필드에 대한 자세한 내용은 [정책 별칭](../../azure-resource-manager/resource-manager-policy.md#aliases)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3dde0-112">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="3dde0-113">관리 디스크</span><span class="sxs-lookup"><span data-stu-id="3dde0-113">Managed disks</span></span>

<span data-ttu-id="3dde0-114">관리 디스크 사용을 요구하려면 다음 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-114">To require the use of managed disks, use the following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="3dde0-115">Virtual Machines에 대한 이미지 </span><span class="sxs-lookup"><span data-stu-id="3dde0-115">Images for Virtual Machines</span></span>

<span data-ttu-id="3dde0-116">보안상의 이유로 승인된 사용자 지정 이미지만 환경에 배포하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-116">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="3dde0-117">승인된 이미지를 포함하는 리소스 그룹이나 특정한 승인된 이미지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-117">You can specify either the resource group that contains the approved images, or the specific approved images.</span></span>

<span data-ttu-id="3dde0-118">다음 예제에서는 승인된 리소스 그룹의 이미지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-118">The following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="3dde0-119">다음 예제에서는 승인된 이미지 ID를 명시합니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-119">The following example specifies the approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="3dde0-120">가상 컴퓨터 확장 </span><span class="sxs-lookup"><span data-stu-id="3dde0-120">Virtual Machine extensions</span></span>

<span data-ttu-id="3dde0-121">특정 유형의 확장을 사용하지 못하게 하고자 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-121">You may want to forbid usage of certain types of extensions.</span></span> <span data-ttu-id="3dde0-122">예를 들어 한 확장이 특정 사용자 지정 가상 컴퓨터 이미지와 호환되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-122">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="3dde0-123">다음 예제에서는 특정 확장을 차단하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-123">The following example shows how to block a specific extension.</span></span> <span data-ttu-id="3dde0-124">게시자 및 유형을 사용하여 차단할 확장을 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-124">It uses publisher and type to determine which extension to block.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="3dde0-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3dde0-125">Next steps</span></span>
* <span data-ttu-id="3dde0-126">앞의 예제와 표시된 바와 같이 정책 규칙을 정의한 후에는 정책 정의를 만들고 범위에 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-126">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="3dde0-127">범위는 구독, 리소스 그룹 또는 리소스일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dde0-127">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="3dde0-128">포털을 통해 정책을 할당하려면 [Azure Portal을 사용하여 리소스 정책 할당 및 관리](../../azure-resource-manager/resource-manager-policy-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3dde0-128">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="3dde0-129">REST API, PowerShell 또는 Azure CLI를 통해 정책을 할당하려면 [스크립트를 통해 정책 할당 및 관리](../../azure-resource-manager/resource-manager-policy-create-assign.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3dde0-129">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="3dde0-130">리소스 정책에 대한 소개는 [리소스 정책 개요](../../azure-resource-manager/resource-manager-policy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3dde0-130">For an introduction to resource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="3dde0-131">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](../../azure-resource-manager/resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3dde0-131">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
