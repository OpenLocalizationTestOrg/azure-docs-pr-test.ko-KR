---
title: "Azure에서 Windows Vm에서 정책 사용 하 여 aaaEnforce 보안 | Microsoft Docs"
description: "어떻게 tooapply 정책 tooan Azure 리소스 관리자 Windows 가상 컴퓨터"
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
ms.openlocfilehash: b31c8a03ecf8eed6a929f97fe4146ea14364404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toowindows-vms-with-azure-resource-manager"></a><span data-ttu-id="1e60c-103">정책을 tooWindows Azure 리소스 관리자와 Vm을 적용</span><span class="sxs-lookup"><span data-stu-id="1e60c-103">Apply policies tooWindows VMs with Azure Resource Manager</span></span>
<span data-ttu-id="1e60c-104">정책을 사용 하면 조직의 다양 한 규칙 및 hello 엔터프라이즈 전체에서 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-104">By using policies, an organization can enforce various conventions and rules throughout hello enterprise.</span></span> <span data-ttu-id="1e60c-105">원하는 hello 동작의 적용 hello 조직의 toohello 성공에 기여 하는 동안 위험을 완화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-105">Enforcement of hello desired behavior can help mitigate risk while contributing toohello success of hello organization.</span></span> <span data-ttu-id="1e60c-106">이 문서에서는 조직의 가상 컴퓨터에 대 한 Azure 리소스 관리자 정책 toodefine hello 원하는 동작을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-106">In this article, we describe how you can use Azure Resource Manager policies toodefine hello desired behavior for your organization’s Virtual Machines.</span></span>

<span data-ttu-id="1e60c-107">참조는 소개 toopolicies [toomanage 리소스 사용 정책 및 액세스 제어](../../azure-resource-manager/resource-manager-policy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-107">For an introduction toopolicies, see [Use Policy toomanage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="1e60c-108">허용되는 Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="1e60c-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="1e60c-109">조직에 대 한 가상 컴퓨터 응용 프로그램 호환 되는지 tooensure, 운영 체제를 허용 하는 hello를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-109">tooensure that virtual machines for your organization are compatible with an application, you can restrict hello permitted operating systems.</span></span> <span data-ttu-id="1e60c-110">다음 예에서는 정책 hello에서 만든 Windows Server 2012 R2 Datacenter 가상 컴퓨터 toobe만 허용:</span><span class="sxs-lookup"><span data-stu-id="1e60c-110">In hello following policy example, you allow only Windows Server 2012 R2 Datacenter Virtual Machines toobe created:</span></span>

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

<span data-ttu-id="1e60c-111">모든 Windows Server Datacenter 이미지 정책 tooallow 앞 와일드 카드 toomodify hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-111">Use a wild card toomodify hello preceding policy tooallow any Windows Server Datacenter image:</span></span>

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

<span data-ttu-id="1e60c-112">모든 Windows Server 2012 R2 Datacenter 또는 더 높은 이미지 정책 tooallow 앞 anyOf toomodify hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-112">Use anyOf toomodify hello preceding policy tooallow any Windows Server 2012 R2 Datacenter or higher image:</span></span>

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

<span data-ttu-id="1e60c-113">정책 필드에 대한 자세한 내용은 [정책 별칭](../../azure-resource-manager/resource-manager-policy.md#aliases)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e60c-113">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="1e60c-114">관리 디스크</span><span class="sxs-lookup"><span data-stu-id="1e60c-114">Managed disks</span></span>

<span data-ttu-id="1e60c-115">toorequire hello 사용 하 여 관리 되는 디스크의 다음 정책을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="1e60c-115">toorequire hello use of managed disks, use hello following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="1e60c-116">Virtual Machines에 대한 이미지 </span><span class="sxs-lookup"><span data-stu-id="1e60c-116">Images for Virtual Machines</span></span>

<span data-ttu-id="1e60c-117">보안상의 이유로 승인된 사용자 지정 이미지만 환경에 배포하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-117">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="1e60c-118">Hello 승인 된 이미지를 포함 하는 hello 리소스 그룹 또는 hello 특정 승인 된 이미지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-118">You can specify either hello resource group that contains hello approved images, or hello specific approved images.</span></span>

<span data-ttu-id="1e60c-119">다음 예제는 hello 승인 된 리소스 그룹에서 이미지를이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-119">hello following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="1e60c-120">hello 다음 예제에서는 지정 승인 hello 이미지 Id:</span><span class="sxs-lookup"><span data-stu-id="1e60c-120">hello following example specifies hello approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="1e60c-121">가상 컴퓨터 확장 </span><span class="sxs-lookup"><span data-stu-id="1e60c-121">Virtual Machine extensions</span></span>

<span data-ttu-id="1e60c-122">특정 유형의 확장 tooforbid 사용을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-122">You may want tooforbid usage of certain types of extensions.</span></span> <span data-ttu-id="1e60c-123">예를 들어 한 확장이 특정 사용자 지정 가상 컴퓨터 이미지와 호환되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-123">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="1e60c-124">hello 방법을 예제와 다음 tooblock 특정 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-124">hello following example shows how tooblock a specific extension.</span></span> <span data-ttu-id="1e60c-125">게시자 및 유형별로 toodetermine 어떤 확장 tooblock을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-125">It uses publisher and type toodetermine which extension tooblock.</span></span>

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


## <a name="azure-hybrid-use-benefit"></a><span data-ttu-id="1e60c-126">AHUB(Azure Hybrid Use Benefit)</span><span class="sxs-lookup"><span data-stu-id="1e60c-126">Azure Hybrid Use Benefit</span></span>

<span data-ttu-id="1e60c-127">온-프레미스 라이선스를 사용 하는 경우에 가상 컴퓨터에 hello 사용료를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-127">When you have an on-premise license, you can save hello license fee on your virtual machines.</span></span> <span data-ttu-id="1e60c-128">Hello 라이선스가 없는 hello 옵션 금지 하지도 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-128">When you don't have hello license, you should forbid hello option.</span></span> <span data-ttu-id="1e60c-129">hello 정책에 따라 Azure 하이브리드 사용 혜택 (AHUB)의 사용을 금지:</span><span class="sxs-lookup"><span data-stu-id="1e60c-129">hello following policy forbids usage of Azure Hybrid Use Benefit (AHUB):</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1e60c-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e60c-130">Next steps</span></span>
* <span data-ttu-id="1e60c-131">한 정책 규칙 (에서처럼 앞 예제는 hello)를 정의한 후 toocreate hello 정책 정의 필요 하 고 tooa 범위 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-131">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="1e60c-132">구독, 리소스 그룹 또는 리소스 hello 범위 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-132">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="1e60c-133">hello 포털을 통해 tooassign 정책 참조 [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](../../azure-resource-manager/resource-manager-policy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-133">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="1e60c-134">REST API, PowerShell 또는 Azure CLI를 통해 tooassign 정책을 참조 [지정 하 고 스크립트를 통해 정책을 관리할](../../azure-resource-manager/resource-manager-policy-create-assign.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-134">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="1e60c-135">소개 tooresource 정책에 대 한 참조 [리소스 정책 개요](../../azure-resource-manager/resource-manager-policy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-135">For an introduction tooresource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="1e60c-136">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](../../azure-resource-manager/resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e60c-136">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
