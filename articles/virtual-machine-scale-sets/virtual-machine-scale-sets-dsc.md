---
title: "aaaUsing 원하는 상태 구성 된 가상 컴퓨터 크기 집합 | Microsoft Docs"
description: "가상 컴퓨터 크기 집합을 사용 하 여 Azure DSC 확장 hello로"
services: virtual-machine-scale-sets
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: c8f047b5-0e6c-4ef3-8a47-f1b284d32942
ms.service: virtual-machine-scale-sets
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 04/05/2017
ms.author: zachal
ms.openlocfilehash: a35f1ca6700aa4889978032aa512882db50d6573
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a><span data-ttu-id="2452c-103">가상 컴퓨터 크기 집합을 사용 하 여 Azure DSC 확장 hello로</span><span class="sxs-lookup"><span data-stu-id="2452c-103">Using Virtual Machine Scale Sets with hello Azure DSC Extension</span></span>
<span data-ttu-id="2452c-104">[가상 컴퓨터 크기 집합](virtual-machine-scale-sets-overview.md) hello와 함께 사용할 수 [Azure 구성 DSC (필요한 상태)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 확장 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with hello [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="2452c-105">가상 컴퓨터 크기 집합 다 수의 가상 컴퓨터 관리 고 수 탄력적으로 확장 및 축소 응답 tooload에 방식으로 toodeploy를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-105">Virtual machine scale sets provide a way toodeploy and manage large numbers of virtual machines, and can elastically scale in and out in response tooload.</span></span> <span data-ttu-id="2452c-106">DSC는은 때문에 hello 프로덕션 소프트웨어 실행 되 고 온라인으로 사용 되는 tooconfigure hello Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-106">DSC is used tooconfigure hello VMs as they come online so they are running hello production software.</span></span>

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="2452c-107">TooVirtual 컴퓨터 및 가상 컴퓨터 크기 집합 배포의 차이점</span><span class="sxs-lookup"><span data-stu-id="2452c-107">Differences between deploying tooVirtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="2452c-108">가상 컴퓨터 크기 집합에 대 한 기본 서식 파일 구조 hello 단일 VM 간에 약간 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-108">hello underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="2452c-109">특히, 단일 VM hello "virtualMachines" 노드 아래에 확장을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-109">Specifically, a single VM deploys extensions under hello "virtualMachines" node.</span></span> <span data-ttu-id="2452c-110">없는 "extensions" 유형의 항목 DSC toohello 서식 파일은 추가 하는 위치</span><span class="sxs-lookup"><span data-stu-id="2452c-110">There is an entry of type "extensions" where DSC is added toohello template</span></span>

```
"resources": [
          {
              "name": "Microsoft.Powershell.DSC",
              "type": "extensions",
              "location": "[resourceGroup().location]",
              "apiVersion": "2015-06-15",
              "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "tags": {
                  "displayName": "dscExtension"
              },
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": false,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "DscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }
          }
      ]
```

<span data-ttu-id="2452c-111">가상 컴퓨터 크기 조정 설정 노드 "extensionProfile" 특성 "VirtualMachineProfile" hello로 "속성" 섹션을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-111">A virtual machine scale set node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="2452c-112">"extensions" 아래에 DSC가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-112">DSC is added under "extensions"</span></span>

```
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": false,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
```

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="2452c-113">가상 컴퓨터 확장 집합의 동작</span><span class="sxs-lookup"><span data-stu-id="2452c-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="2452c-114">가상 컴퓨터 크기 집합에 대 한 hello 동작은 단일 VM에 대 한 동일한 toohello 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-114">hello behavior for a virtual machine scale set is identical toohello behavior for a single VM.</span></span> <span data-ttu-id="2452c-115">새 VM이 만들어지면 DSC 확장 hello로 자동으로 구축 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-115">When a new VM is created, it is automatically provisioned with hello DSC extension.</span></span> <span data-ttu-id="2452c-116">최신 버전의 hello WMF hello 확장에 필요한 경우 온라인 상태로 만들기 전에 hello VM 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-116">If a newer version of hello WMF is required by hello extension, hello VM reboots before coming online.</span></span> <span data-ttu-id="2452c-117">온라인 상태 이면 되 면 hello DSC 구성.zip을 다운로드 하 고 hello VM에서 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-117">Once it is online, it downloads hello DSC configuration .zip and provision it on hello VM.</span></span> <span data-ttu-id="2452c-118">자세한 내용은에서 확인할 수 있습니다 [Azure DSC 확장 개요 hello](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-118">More details can be found in [hello Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2452c-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2452c-119">Next steps</span></span>
<span data-ttu-id="2452c-120">Hello 검사 [hello DSC 확장에 대 한 Azure Resource Manager 템플릿](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-120">Examine hello [Azure Resource Manager template for hello DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="2452c-121">자세한 내용은 방법 hello [DSC 확장 자격 증명을 안전 하 게 처리](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-121">Learn how hello [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="2452c-122">Hello Azure DSC 확장 처리기에 대 한 자세한 내용은 참조 하십시오. [소개 toohello Azure 필요한 상태 구성 확장 처리기](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-122">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="2452c-123">PowerShell DSC에 대 한 자세한 내용은 [hello PowerShell 설명서 센터를 방문](https://msdn.microsoft.com/powershell/dsc/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="2452c-123">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

