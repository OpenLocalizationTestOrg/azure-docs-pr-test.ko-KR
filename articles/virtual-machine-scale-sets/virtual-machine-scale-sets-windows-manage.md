---
title: "가상 컴퓨터 크기 집합의 Vm aaaManage | Microsoft Docs"
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
ms.openlocfilehash: 7d848729c0fc708bd596b61feb528cf4bf4bafd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a>가상 컴퓨터 확장 집합의 가상 컴퓨터 관리
가상 컴퓨터 크기 집합의이 문서 toomanage 가상 컴퓨터에서 hello 작업을 사용 합니다.

대부분의 가상 컴퓨터 크기 집합의 관리와 관련 된 hello 작업 필요 toomanage hello 컴퓨터의 hello 인스턴스 ID를 알아야 합니다. 사용할 수 있습니다 [Azure 리소스 탐색기](https://resources.azure.com) toofind hello 인스턴스 ID는 가상 컴퓨터 크기 집합의입니다. 또한 완료 하는 hello 작업의 리소스 탐색기 tooverify hello 상태를 사용 합니다.

참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello 최신 버전의 Azure PowerShell을 설치, 구독을 선택 하 고 tooyour 계정에 로그인 하는 방법에 대 한 정보에 대 한 합니다.

## <a name="display-information-about-a-scale-set"></a>확장 집합에 대한 정보 표시
참조 된 tooas hello 인스턴스 보기 이기도 한 크기 집합에 대 한 일반 정보를 얻을 수 있습니다. 또는 hello 크기 집합의 hello 리소스에 대 한 정보 등의 보다 구체적인 정보를 얻을 수 있습니다.

Hello 이름 또는 리소스 그룹 및 크기 조정 설정 하 고 hello 명령을 실행 하는 값을 묶은 따옴표가 hello를 바꿉니다.

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

이때 반환되는 내용은 다음과 같습니다.

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

리소스 그룹 및 확장 집합의 hello 이름의 값을 묶은 따옴표가 hello를 대체 합니다. 대체  *#*  hello 가상 컴퓨터에 대 한 tooget 정보를 가져오려면 다음를 실행 하는 hello 인스턴스 식별자:

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

이때 반환되는 내용은 다음 예제와 같습니다.

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

## <a name="start-a-virtual-machine-in-a-scale-set"></a>확장 집합의 가상 컴퓨터 시작
리소스 그룹 및 확장 집합의 hello 이름의 값을 묶은 따옴표가 hello를 대체 합니다. 대체  *#*  toostart 원하고 다음 실행 hello 가상 컴퓨터의 hello 식별자로:

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

리소스 탐색기, 알 수 있습니다는 hello hello 인스턴스 상태가 **실행**:

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

Hello-InstanceId 매개 변수를 사용 하지 않고 설정 hello 규모에 맞게 모든 hello 가상 컴퓨터를 시작할 수 있습니다.

## <a name="stop-a-virtual-machine-in-a-scale-set"></a>확장 집합의 가상 컴퓨터 중지
리소스 그룹 및 확장 집합의 hello 이름의 값을 묶은 따옴표가 hello를 대체 합니다. 대체  *#*  toostop 원하고 다음 실행 hello 가상 컴퓨터의 hello 식별자로:

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

리소스 탐색기, 알 수 있습니다는 hello hello 인스턴스 상태가 **할당 취소**:

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

가상 컴퓨터 toostop 할당을 취소 하지, hello-StayProvisioned 매개 변수를 사용 합니다. Hello hello-InstanceId 매개 변수를 사용 하지 않고 설정의 모든 hello 가상 컴퓨터를 중지할 수 있습니다.

## <a name="restart-a-virtual-machine-in-a-scale-set"></a>확장 집합의 가상 컴퓨터 다시 시작
리소스 그룹 및 hello 크기 집합의 hello 이름의 값을 묶은 따옴표가 hello를 대체 합니다. 대체  *#*  toorestart 원하고 다음 실행 hello 가상 컴퓨터의 hello 식별자로:

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Hello-InstanceId 매개 변수를 사용 하지 않고 설정 hello에서 모든 hello 가상 컴퓨터를 다시 시작할 수 있습니다.

## <a name="remove-a-virtual-machine-from-a-scale-set"></a>확장 집합에서 가상 컴퓨터 제거
리소스 그룹 및 hello 크기 집합의 hello 이름의 값을 묶은 따옴표가 hello를 대체 합니다. 대체  *#*  tooremove 원하고 다음 실행 hello 가상 컴퓨터의 hello 식별자로:  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

Hello-InstanceId 매개 변수를 사용 하지 않고 hello 가상 컴퓨터 크기 집합 한 번에 제거할 수 있습니다.

## <a name="change-hello-capacity-of-a-scale-set"></a>Hello 용량 크기 집합의 변경
추가 하거나 hello 집합의 hello 용량을 변경 하 여 가상 컴퓨터를 제거할 수 있습니다. Toochange, 집합 hello 용량 toowhat toobe, 원하는 한 다음 새 용량 hello로 hello 크기 집합을 업데이트 하려는 hello 크기 집합을 가져옵니다. 이러한 명령에 리소스 그룹 및 hello 크기 집합의 hello 이름의 값을 묶은 따옴표가 hello를 대체 합니다.

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

Hello 크기 집합에서 가상 컴퓨터를 제거 하는 경우 hello 가장 높은 id 가진 가상 컴퓨터 hello 먼저 제거 됩니다.

