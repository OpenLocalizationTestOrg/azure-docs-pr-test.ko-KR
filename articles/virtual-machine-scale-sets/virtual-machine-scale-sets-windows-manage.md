---
title: "가상 컴퓨터 확장 집합의 VM 관리 | Microsoft Docs"
description: "Azure PowerShell을 사용하여 가상 컴퓨터 확장 집합의 가상 컴퓨터를 관리합니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d35fa77a-de96-4ccd-a332-eb181d1f4273
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: d09a020b903e5f43afe03b86c675bcc1eb536cbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="4fd3f-103">가상 컴퓨터 확장 집합의 가상 컴퓨터 관리</span><span class="sxs-lookup"><span data-stu-id="4fd3f-103">Manage virtual machines in a virtual machine scale set</span></span>
<span data-ttu-id="4fd3f-104">이 문서의 작업을 사용하여 가상 컴퓨터 확장 집합에서 가상 컴퓨터를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-104">Use the tasks in this article to manage virtual machines in your virtual machine scale set.</span></span>

<span data-ttu-id="4fd3f-105">확장 집합의 가상 컴퓨터 관리와 관련된 대부분의 작업을 수행할 경우에는 관리하려는 컴퓨터의 인스턴스 ID를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-105">Most of the tasks that involve managing a virtual machine in a scale set require that you know the instance ID of the machine that you want to manage.</span></span> <span data-ttu-id="4fd3f-106">[Azure 리소스 탐색기](https://resources.azure.com) 를 사용하여 확장 집합에 있는 가상 컴퓨터의 인스턴스 ID를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-106">You can use [Azure Resource Explorer](https://resources.azure.com) to find the instance ID of a virtual machine in a scale set.</span></span> <span data-ttu-id="4fd3f-107">리소스 탐색기를 사용하여 마친 작업의 상태를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-107">You also use Resource Explorer to verify the status of the tasks that you finish.</span></span>

<span data-ttu-id="4fd3f-108">최신 버전의 Azure PowerShell 설치, 구독 선택, 자신의 계정에 로그인하는 방법에 대해서는 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-108">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>

## <a name="display-information-about-a-scale-set"></a><span data-ttu-id="4fd3f-109">확장 집합에 대한 정보 표시</span><span class="sxs-lookup"><span data-stu-id="4fd3f-109">Display information about a scale set</span></span>
<span data-ttu-id="4fd3f-110">확장 집합에 대한 일반 정보를 가져올 수 있습니다(인스턴스 보기라고도 함).</span><span class="sxs-lookup"><span data-stu-id="4fd3f-110">You can get general information about a scale set, which is also referred to as the instance view.</span></span> <span data-ttu-id="4fd3f-111">또는 확장 집합의 리소스에 대한 정보와 같이 더 구체적인 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-111">Or, you can get more specific information, such as information about the resources in the scale set.</span></span>

<span data-ttu-id="4fd3f-112">따옴표로 묶인 값을 리소스 그룹 및 확장 집합 이름으로 바꾼 후 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-112">Replace the quoted values with the name or your resource group and scale set and then run the command:</span></span>

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

<span data-ttu-id="4fd3f-113">이때 반환되는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-113">It returns something like this:</span></span>

    Id                                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/myvmss1
    Name                                        : myvmss1
    Type                                        : Microsoft.Compute/virtualMachineScaleSets
    Location                                    : centralus
    Sku                                         :
      Name                                      : Standard_A0
      Tier                                      : Standard
      Capacity                                  : 3
    UpgradePolicy                               :
      Mode                                      : Manual
    VirtualMachineProfile                       :
      OsProfile                                 :
        ComputerNamePrefix                      : vmss1
        AdminUsername                           : admin1
        WindowsConfiguration                    :
          ProvisionVMAgent                      : True
          EnableAutomaticUpdates                : True
    StorageProfile                              :
      ImageReference                            :
        Publisher                               : MicrosoftWindowsServer
        Offer                                   : WindowsServer
        Sku                                     : 2012-R2-Datacenter
        Version                                 : latest
      OsDisk                                    :
        Name                                    : vmssosdisk
        Caching                                 : ReadOnly
        CreateOption                            : FromImage
        VhdContainers[0]                        : https://astore.blob.core.windows.net/vmss
        VhdContainers[1]                        : https://gstore.blob.core.windows.net/vmss
        VhdContainers[2]                        : https://mstore.blob.core.windows.net/vmss
        VhdContainers[3]                        : https://sstore.blob.core.windows.net/vmss
        VhdContainers[4]                        : https://ystore.blob.core.windows.net/vmss
    NetworkProfile                              :
      NetworkInterfaceConfigurations[0]         :
        Name                                    : mync1
        Primary                                 : True
        IpConfigurations[0]                     :
          Name                                  : ip1
          Subnet                                :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/virtualNetworks/myvn1/subnets/mysn1
          LoadBalancerBackendAddressPools[0]    :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/backendAddressPools/bepool1
        LoadBalancerInboundNatPools[0]          :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/inboundNatPools/natpool1
    ExtensionProfile                            :
      Extensions[0]                             :
        Name                                    : Microsoft.Insights.VMDiagnosticsSettings
        Publisher                               : Microsoft.Azure.Diagnostics
        Type                                    : IaaSDiagnostics
        TypeHandlerVersion                      : 1.5
        AutoUpgradeMinorVersion                 : True
        Settings                                : {"xmlCfg":"...","storageAccount":"astore"}
    ProvisioningState                           : Succeeded

<span data-ttu-id="4fd3f-114">따옴표로 묶인 값을 리소스 그룹 및 확장 집합 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-114">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="4fd3f-115">*#*을(를) 정보를 가져올 가상 컴퓨터의 인스턴스 식별자로 바꾼 후 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-115">Replace *#* with the instance identifier of the virtual machine that you want to get information about and then run it:</span></span>

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="4fd3f-116">이때 반환되는 내용은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-116">It returns something like this example:</span></span>

    Id                            : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/
                                    virtualMachineScaleSets/myvmss1/virtualMachines/0
    Name                          : myvmss1_0
    Type                          : Microsoft.Compute/virtualMachineScaleSets/virtualMachines
    Location                      : centralus
    InstanceId                    : 0
    Sku                           :
      Name                        : Standard_A0
      Tier                        : Standard
    LatestModelApplied            : True
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : 4.0.20160617
      OsDisk                      :
        OsType                    : Windows
        Name                      : vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8
        Vhd                       :
          Uri                     : https://astore.blob.core.windows.net/vmss/vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8.vhd
        Caching                   : ReadOnly
        CreateOption              : FromImage
    OsProfile                     :
      ComputerName                : myvmss1-0
      AdminUsername               : admin1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
        EnableAutomaticUpdates    : True
    NetworkProfile                :
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/
                                    myvmss1/virtualMachines/0/networkInterfaces/mync1
    ProvisioningState             : Succeeded
    Resources[0]                  :
      Id                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachines/
                                    myvmss1_0/extensions/Microsoft.Insights.VMDiagnosticsSettings
      Name                        : Microsoft.Insights.VMDiagnosticsSettings
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Azure.Diagnostics
      VirtualMachineExtensionType : IaaSDiagnostics
      TypeHandlerVersion          : 1.5
      AutoUpgradeMinorVersion     : True
      Settings                    : {"xmlCfg":"...","storageAccount":"astore"}
      ProvisioningState           : Succeeded

## <a name="start-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="4fd3f-117">확장 집합의 가상 컴퓨터 시작</span><span class="sxs-lookup"><span data-stu-id="4fd3f-117">Start a virtual machine in a scale set</span></span>
<span data-ttu-id="4fd3f-118">따옴표로 묶인 값을 리소스 그룹 및 확장 집합 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-118">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="4fd3f-119">*#*을(를) 시작할 가상 컴퓨터의 식별자로 바꾼 후 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-119">Replace *#* with the identifier of the virtual machine that you want to start and then run it:</span></span>

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="4fd3f-120">리소스 탐색기에서 인스턴스 상태가 **실행 중**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-120">In Resource Explorer, we can see that the status of the instance is **running**:</span></span>

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T02:10:08.0730839+00:00"
      },
      {
        "code": "PowerState/running",
        "level": "Info",
        "displayStatus": "VM running"
      }
    ]

<span data-ttu-id="4fd3f-121">-InstanceId 매개 변수를 사용하지 않으면 확장 집합의 모든 가상 컴퓨터를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-121">You can start all the virtual machines in the scale set by not using the -InstanceId parameter.</span></span>

## <a name="stop-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="4fd3f-122">확장 집합의 가상 컴퓨터 중지</span><span class="sxs-lookup"><span data-stu-id="4fd3f-122">Stop a virtual machine in a scale set</span></span>
<span data-ttu-id="4fd3f-123">따옴표로 묶인 값을 리소스 그룹 및 확장 집합 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-123">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="4fd3f-124">*#*을(를) 중지할 가상 컴퓨터의 식별자로 바꾼 후 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-124">Replace *#* with the identifier of the virtual machine that you want to stop and then run it:</span></span>

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="4fd3f-125">리소스 탐색기에서 인스턴스 상태가 **할당 취소됨**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-125">In Resource Explorer, we can see that the status of the instance is **deallocated**:</span></span>

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T01:25:17.8792929+00:00"
      },
      {
        "code": "PowerState/deallocated",
        "level": "Info",
        "displayStatus": "VM deallocated"
      }
    ]

<span data-ttu-id="4fd3f-126">가상 컴퓨터를 중지하고 할당을 취소하지 않으려면 StayProvisioned 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-126">To stop a virtual machine and not deallocate it, use the -StayProvisioned parameter.</span></span> <span data-ttu-id="4fd3f-127">-InstanceId 매개 변수를 사용하지 않으면 집합의 모든 가상 컴퓨터를 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-127">You can stop all the virtual machines in the set by not using the -InstanceId parameter.</span></span>

## <a name="restart-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="4fd3f-128">확장 집합의 가상 컴퓨터 다시 시작</span><span class="sxs-lookup"><span data-stu-id="4fd3f-128">Restart a virtual machine in a scale set</span></span>
<span data-ttu-id="4fd3f-129">따옴표로 묶인 값을 리소스 그룹 및 확장 집합 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-129">Replace the quoted values with the name of your resource group and the scale set.</span></span> <span data-ttu-id="4fd3f-130">*#*을(를) 다시 시작할 가상 컴퓨터의 식별자로 바꾼 후 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-130">Replace *#* with the identifier of the virtual machine that you want to restart and then run it:</span></span>

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="4fd3f-131">-InstanceId 매개 변수를 사용하지 않으면 집합의 모든 가상 컴퓨터를 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-131">You can restart all the virtual machines in the set by not using the -InstanceId parameter.</span></span>

## <a name="remove-a-virtual-machine-from-a-scale-set"></a><span data-ttu-id="4fd3f-132">확장 집합에서 가상 컴퓨터 제거</span><span class="sxs-lookup"><span data-stu-id="4fd3f-132">Remove a virtual machine from a scale set</span></span>
<span data-ttu-id="4fd3f-133">따옴표로 묶인 값을 리소스 그룹 및 확장 집합 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-133">Replace the quoted values with the name of your resource group and the scale set.</span></span> <span data-ttu-id="4fd3f-134">*#*을(를) 다시 이동할 가상 컴퓨터의 식별자로 바꾼 후 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-134">Replace *#* with the identifier of the virtual machine that you want to remove and then run it:</span></span>  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="4fd3f-135">-InstanceId 매개 변수를 사용하지 않으면 가상 컴퓨터 확장 집합을 한 번에 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-135">You can remove the virtual machine scale set all at once by not using the -InstanceId parameter.</span></span>

## <a name="change-the-capacity-of-a-scale-set"></a><span data-ttu-id="4fd3f-136">확장 집합의 용량 변경</span><span class="sxs-lookup"><span data-stu-id="4fd3f-136">Change the capacity of a scale set</span></span>
<span data-ttu-id="4fd3f-137">집합 용량을 변경하여 가상 컴퓨터를 추가 또는 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-137">You can add or remove virtual machines by changing the capacity of the set.</span></span> <span data-ttu-id="4fd3f-138">변경할 확장 집합을 가져오고 원하는 용량을 설정한 후 확장 집합을 새 용량으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-138">Get the scale set that you want to change, set the capacity to what you want it to be, and then update the scale set with the new capacity.</span></span> <span data-ttu-id="4fd3f-139">이러한 명령에서 따옴표로 묶인 값을 리소스 그룹 및 확장 집합 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-139">In these commands, replace the quoted values with the name of your resource group and the scale set.</span></span>

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

<span data-ttu-id="4fd3f-140">확장 집합에서 가상 컴퓨터를 제거하는 경우 가장 높은 ID를 가진 가상 컴퓨터가 먼저 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fd3f-140">If you are removing virtual machines from the scale set, the virtual machines with the highest ids are removed first.</span></span>

