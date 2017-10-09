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
# <a name="apply-policies-toowindows-vms-with-azure-resource-manager"></a>정책을 tooWindows Azure 리소스 관리자와 Vm을 적용
정책을 사용 하면 조직의 다양 한 규칙 및 hello 엔터프라이즈 전체에서 규칙을 적용할 수 있습니다. 원하는 hello 동작의 적용 hello 조직의 toohello 성공에 기여 하는 동안 위험을 완화할 수 있습니다. 이 문서에서는 조직의 가상 컴퓨터에 대 한 Azure 리소스 관리자 정책 toodefine hello 원하는 동작을 사용 하는 방법을 설명 합니다.

참조는 소개 toopolicies [toomanage 리소스 사용 정책 및 액세스 제어](../../azure-resource-manager/resource-manager-policy.md)합니다.

## <a name="permitted-virtual-machines"></a>허용되는 Virtual Machines
조직에 대 한 가상 컴퓨터 응용 프로그램 호환 되는지 tooensure, 운영 체제를 허용 하는 hello를 제한할 수 있습니다. 다음 예에서는 정책 hello에서 만든 Windows Server 2012 R2 Datacenter 가상 컴퓨터 toobe만 허용:

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

모든 Windows Server Datacenter 이미지 정책 tooallow 앞 와일드 카드 toomodify hello를 사용 합니다.

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

모든 Windows Server 2012 R2 Datacenter 또는 더 높은 이미지 정책 tooallow 앞 anyOf toomodify hello를 사용 합니다.

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

정책 필드에 대한 자세한 내용은 [정책 별칭](../../azure-resource-manager/resource-manager-policy.md#aliases)을 참조하세요.

## <a name="managed-disks"></a>관리 디스크

toorequire hello 사용 하 여 관리 되는 디스크의 다음 정책을 사용 하 여 hello:

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

## <a name="images-for-virtual-machines"></a>Virtual Machines에 대한 이미지 

보안상의 이유로 승인된 사용자 지정 이미지만 환경에 배포하도록 요구할 수 있습니다. Hello 승인 된 이미지를 포함 하는 hello 리소스 그룹 또는 hello 특정 승인 된 이미지를 지정할 수 있습니다.

다음 예제는 hello 승인 된 리소스 그룹에서 이미지를이 필요 합니다.

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

hello 다음 예제에서는 지정 승인 hello 이미지 Id:

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a>가상 컴퓨터 확장 

특정 유형의 확장 tooforbid 사용을 할 수 있습니다. 예를 들어 한 확장이 특정 사용자 지정 가상 컴퓨터 이미지와 호환되지 않을 수 있습니다. hello 방법을 예제와 다음 tooblock 특정 확장 합니다. 게시자 및 유형별로 toodetermine 어떤 확장 tooblock을 사용합니다.

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


## <a name="azure-hybrid-use-benefit"></a>AHUB(Azure Hybrid Use Benefit)

온-프레미스 라이선스를 사용 하는 경우에 가상 컴퓨터에 hello 사용료를 저장할 수 있습니다. Hello 라이선스가 없는 hello 옵션 금지 하지도 해야 합니다. hello 정책에 따라 Azure 하이브리드 사용 혜택 (AHUB)의 사용을 금지:

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

## <a name="next-steps"></a>다음 단계
* 한 정책 규칙 (에서처럼 앞 예제는 hello)를 정의한 후 toocreate hello 정책 정의 필요 하 고 tooa 범위 할당 합니다. 구독, 리소스 그룹 또는 리소스 hello 범위 될 수 있습니다. hello 포털을 통해 tooassign 정책 참조 [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](../../azure-resource-manager/resource-manager-policy-portal.md)합니다. REST API, PowerShell 또는 Azure CLI를 통해 tooassign 정책을 참조 [지정 하 고 스크립트를 통해 정책을 관리할](../../azure-resource-manager/resource-manager-policy-create-assign.md)합니다.
* 소개 tooresource 정책에 대 한 참조 [리소스 정책 개요](../../azure-resource-manager/resource-manager-policy.md)합니다.
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](../../azure-resource-manager/resource-manager-subscription-governance.md)합니다.
