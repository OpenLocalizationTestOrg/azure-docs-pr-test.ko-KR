---
title: "가상 컴퓨터 확장 집합에 필요한 상태 구성 사용 | Microsoft Docs"
description: "Azure DSC 확장에 가상 컴퓨터 확장 집합 사용"
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
ms.openlocfilehash: b61b0acf3072569ab733a13defb465c921d26187
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-virtual-machine-scale-sets-with-the-azure-dsc-extension"></a><span data-ttu-id="af682-103">Azure DSC 확장에 가상 컴퓨터 확장 집합 사용</span><span class="sxs-lookup"><span data-stu-id="af682-103">Using Virtual Machine Scale Sets with the Azure DSC Extension</span></span>
<span data-ttu-id="af682-104">[Azure DSC(필요한 상태 구성)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 확장 처리기에 [Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af682-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with the [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="af682-105">가상 컴퓨터 확장 집합은 많은 수의 가상 컴퓨터를 배포 및 관리하는 방법을 제공하며 부하에 따라 탄력적으로 확장 및 축소될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af682-105">Virtual machine scale sets provide a way to deploy and manage large numbers of virtual machines, and can elastically scale in and out in response to load.</span></span> <span data-ttu-id="af682-106">DSC는 VM이 온라인으로 전환되어 프로덕션 소프트웨어를 실행하도록 VM을 구성하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af682-106">DSC is used to configure the VMs as they come online so they are running the production software.</span></span>

## <a name="differences-between-deploying-to-virtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="af682-107">Virtual Machines 및 Virtual Machine Scale Sets에 대한 배포 간의 차이점</span><span class="sxs-lookup"><span data-stu-id="af682-107">Differences between deploying to Virtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="af682-108">가상 컴퓨터 확장 집합에 대한 기본 템플릿 구조는 단일 VM과 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="af682-108">The underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="af682-109">특히, 단일 VM은 확장을 "virtualMachines" 노드 아래에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="af682-109">Specifically, a single VM deploys extensions under the "virtualMachines" node.</span></span> <span data-ttu-id="af682-110">DSC가 템플릿에 추가된 "extensions" 유형의 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af682-110">There is an entry of type "extensions" where DSC is added to the template</span></span>

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

<span data-ttu-id="af682-111">가상 컴퓨터 확장 집합 노드에는 "VirtualMachineProfile", "extensionProfile" 특성을 포함하는 "properties" 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af682-111">A virtual machine scale set node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="af682-112">"extensions" 아래에 DSC가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="af682-112">DSC is added under "extensions"</span></span>

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="af682-113">가상 컴퓨터 확장 집합의 동작</span><span class="sxs-lookup"><span data-stu-id="af682-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="af682-114">가상 컴퓨터 확장 집합의 동작은 단일 VM의 동작과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="af682-114">The behavior for a virtual machine scale set is identical to the behavior for a single VM.</span></span> <span data-ttu-id="af682-115">새 VM을 만들 때 DSC 확장으로 자동으로 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="af682-115">When a new VM is created, it is automatically provisioned with the DSC extension.</span></span> <span data-ttu-id="af682-116">확장에 최신 버전의 WMF가 필요한 경우 확장을 온라인으로 전환하려면 VM을 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="af682-116">If a newer version of the WMF is required by the extension, the VM reboots before coming online.</span></span> <span data-ttu-id="af682-117">온라인 상태이면 DSC 구성.zip을 다운로드하고 VM에 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="af682-117">Once it is online, it downloads the DSC configuration .zip and provision it on the VM.</span></span> <span data-ttu-id="af682-118">자세한 내용은 [Azure DSC 확장 개요](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af682-118">More details can be found in [the Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="af682-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="af682-119">Next steps</span></span>
<span data-ttu-id="af682-120">[DSC 확장에 대한 Azure Resource Manager 템플릿](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="af682-120">Examine the [Azure Resource Manager template for the DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="af682-121">[DSC 확장이 자격 증명을 안전하게 처리](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="af682-121">Learn how the [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="af682-122">Azure DSC 확장 처리기에 대한 자세한 내용은 [Azure 필요한 상태 구성 확장 처리기 소개](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af682-122">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="af682-123">PowerShell DSC에 대한 자세한 내용은 [PowerShell 설명서 센터를 방문하세요](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="af682-123">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

