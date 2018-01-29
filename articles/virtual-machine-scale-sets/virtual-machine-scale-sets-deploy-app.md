---
title: "Azure 가상 컴퓨터 확장 집합에 응용 프로그램 배포 | Microsoft Docs"
description: "Linux 및 Windows 가상 컴퓨터 인스턴스의 확장 집합에 응용 프로그램을 배포하는 방법을 알아봅니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: jeconnoc
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/13/2017
ms.author: iainfou
ms.openlocfilehash: 7e03d5e2bbdb1b3b206fa7fa455f7dce7951f02b
ms.sourcegitcommit: 3e3a5e01a5629e017de2289a6abebbb798cec736
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a>가상 컴퓨터 확장 집합에 응용 프로그램 배포
확장 집합의 VM(가상 컴퓨터) 인스턴스에서 응용 프로그램을 실행하려면 먼저 응용 프로그램 구성 요소 및 필요한 파일을 설치해야 합니다. 이 문서에서는 확장 집합의 인스턴스에 대한 사용자 지정 VM 이미지를 빌드하거나 기존 VM 인스턴스에 설치 스크립트를 자동으로 실행하는 방법을 소개합니다. 또한 확장 집합 전체에서 응용 프로그램 또는 OS 업데이트를 관리하는 방법도 알아봅니다.


## <a name="build-a-custom-vm-image"></a>사용자 지정 VM 이미지 빌드
Azure 플랫폼 이미지 중 하나를 사용하여 확장 집합에서 인스턴스를 만드는 경우 소프트웨어가 추가로 설치되거나 구성되지 않습니다. 그러나 이러한 구성 요소의 설치를 자동화할 수는 있지만 VM 인스턴스를 확장 집합에 프로비전하는 데 걸리는 시간이 늘어납니다. VM 인스턴스에 구성 변경을 많이 적용하는 경우 이러한 구성 스크립트 및 작업에는 관리 오버헤드가 있습니다.

구성 관리 및 VM 프로비전 시간을 줄이기 위해 인스턴스가 확장 집합에 프로비전되는 즉시 응용 프로그램을 실행할 준비가 된 사용자 지정 VM 이미지를 만들 수 있습니다. 확장 집합 인스턴스에 대한 사용자 지정 VM 이미지를 만드는 전체 프로세스는 다음과 같습니다.

1. 확장 집합 인스턴스에 대한 사용자 지정 VM 이미지를 빌드하려면 VM을 만들고 로그인한 다음 응용 프로그램을 설치 및 구성합니다. Packer를 사용하여 [Linux](../virtual-machines/linux/build-image-with-packer.md) 또는 [Windows](../virtual-machines/windows/build-image-with-packer.md) VM 이미지를 정의하고 빌드할 수 있습니다. 또는 다음과 같이 VM을 수동으로 만들고 구성할 수 있습니다.

    - [Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md), [Azure PowerShell](../virtual-machines/linux/quick-create-powershell.md) 또는 [포털](../virtual-machines/linux/quick-create-portal.md)을 사용하여 Linux VM을 만듭니다.
    - [Azure PowerShell](../virtual-machines/windows/quick-create-powershell.md), [Azure CLI 2.0](../virtual-machines/windows/quick-create-cli.md) 또는 [포털](../virtual-machines/windows/quick-create-portal.md)을 사용하여 Windows VM을 만듭니다.
    - [Linux](../virtual-machines/linux/mac-create-ssh-keys.md#use-the-ssh-key-pair) 또는 [Windows](../virtual-machines/windows/connect-logon.md) VM에 로그인합니다.
    - 필요한 응용 프로그램과 도구를 설치하고 구성합니다. 특정 버전의 라이브러리 또는 런타임이 필요한 경우 사용자 지정 VM 이미지를 사용하여 버전을 정의할 수 있습니다. 그리고 

2. [Azure CLI 2.0](../virtual-machines/linux/capture-image.md) 또는 [Azure PowerShell](../virtual-machines/windows/capture-image.md)을 사용하여 VM을 캡처합니다. 이 단계에서는 확장 집합에 인스턴스를 배포하는 데 사용되는 사용자 지정 VM 이미지를 만듭니다.

3. [확장 집합](virtual-machine-scale-sets-create.md)을 만들고 이전 단계에서 만든 사용자 지정 VM 이미지를 지정합니다.


## <a name="already-provisioned"></a>사용자 지정 스크립트 확장을 사용하여 앱 설치
사용자 지정 스크립트 확장은 Azure VM에서 스크립트를 다운로드하고 실행합니다. 이 확장은 배포 후 구성, 소프트웨어 설치 또는 기타 구성/관리 작업에 유용합니다. 스크립트는 Azure 저장소 또는 GitHub에서 다운로드하거나 확장 런타임에서 Azure Portal에 제공할 수 있습니다.

사용자 지정 스크립트 확장은 Azure Resource Manager 템플릿과 통합되고, Azure CLI, PowerShell, Azure Portal 또는 Azure 가상 컴퓨터 REST API를 사용하여 실행할 수도 있습니다. 

자세한 내용은 [사용자 지정 스크립트 확장 개요](../virtual-machines/windows/extensions-customscript.md)를 참조하세요.


### <a name="use-azure-powershell"></a>Azure PowerShell 사용
PowerShell에서는 해시 테이블을 사용하여 다운로드할 파일과 실행할 명령을 저장합니다. 다음 예제를 참조하세요.

- GitHub(*https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1*)에서 스크립트를 다운로드하도록 VM 인스턴스에 지시합니다.
- 설치 스크립트를 실행하도록 확장을 설정합니다(`powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1`).
- [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss)를 사용하여 확장 집합에 대한 정보를 가져옵니다.
- [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss)를 사용하여 VM 인스턴스에 확장을 적용합니다.

사용자 지정 스크립트 확장은 *myResourceGroup*이라는 리소스 그룹의 *myScaleSet* VM 인스턴스에 적용됩니다. 다음과 같이 사용자 고유의 이름을 입력합니다:

```powershell
# Define the script for your Custom Script Extension to run
$customConfig = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Get information about the scale set
$vmss = Get-AzureRmVmss `
                -ResourceGroupName "myResourceGroup" `
                -VMScaleSetName "myScaleSet"

# Add the Custom Script Extension to install IIS and configure basic website
$vmss = Add-AzureRmVmssExtension `
    -VirtualMachineScaleSet $vmss `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $customConfig

# Update the scale set and apply the Custom Script Extension to the VM instances
Update-AzureRmVmss `
    -ResourceGroupName "myResourceGroup" `
    -Name "myScaleSet" `
    -VirtualMachineScaleSet $vmss
```

확장 집합에 대한 업그레이드 정책이 *수동*이면 [Update-AzureRmVmssInstance](/powershell/module/azurerm.compute/update-azurermvmssinstance)를 사용하여 VM 인스턴스를 업데이트합니다. 이 cmdlet은 업데이트된 확장 집합 구성을 VM 인스턴스에 적용하고 응용 프로그램을 설치합니다.


### <a name="use-azure-cli-20"></a>Azure CLI 2.0 사용
Azure CLI를 통해 사용자 지정 스크립트 확장을 사용하려면 가져올 파일과 실행할 명령을 정의하는 JSON 파일을 만듭니다. 이러한 JSON 정의는 일관된 응용 프로그램 설치를 적용하기 위해 확장 집합 배포 전체에서 다시 사용할 수 있습니다.

현재 셸에서 *customConfig.json*이라는 파일을 만들고 다음 구성을 붙여넣습니다. 예를 들어 로컬 컴퓨터에 없는 Cloud Shell에서 파일을 만듭니다. 원하는 모든 편집기를 사용할 수 있습니다. `sensible-editor cloudConfig.json`를 입력하여 파일을 만들고 사용할 수 있는 편집기의 목록을 봅니다.

```json
{
  "fileUris": ["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate_nginx.sh"],
  "commandToExecute": "./automate_nginx.sh"
}
```

[az vmss extension set](/cli/azure/vmss/extension#set)를 사용하여 사용자 지정 스크립트 확장 구성을 확장 집합의 VM 인스턴스에 적용합니다. 다음 예제에서는 *customConfig.json* 구성을 *myResourceGroup*이라는 리소스 그룹의 *myScaleSet* VM 인스턴스에 적용합니다. 다음과 같이 사용자 고유의 이름을 입력합니다:

```azurecli
az vmss extension set \
    --publisher Microsoft.Azure.Extensions \
    --version 2.0 \
    --name CustomScript \
    --resource-group myResourceGroup \
    --vmss-name myScaleSet \
    --settings @customConfig.json
```

확장 집합에 대한 업그레이드 정책이 *수동*이면 [az vmss update-instances](/cli/azure/vmss#update-instances)를 사용하여 VM 인스턴스를 업데이트합니다. 이 cmdlet은 업데이트된 확장 집합 구성을 VM 인스턴스에 적용하고 응용 프로그램을 설치합니다.


## <a name="install-an-app-to-a-windows-vm-with-powershell-dsc"></a>PowerShell DSC를 사용하여 Windows VM에 앱 설치
[PowerShell DSC(Desired State Configuration)](https://msdn.microsoft.com/en-us/powershell/dsc/overview)는 대상 컴퓨터의 구성을 정의하는 관리 플랫폼입니다. DSC 구성은 컴퓨터에 설치할 항목과 호스트를 구성하는 방법을 정의합니다. LCM(로컬 구성 관리자) 엔진이 푸시된 구성에 따라 요청된 작업을 처리하는 각 대상 노드에서 실행됩니다.

PowerShell DSC 확장을 사용하면 PowerShell을 통해 확장 집합의 VM 인스턴스를 사용자 지정할 수 있습니다. 다음 예제를 참조하세요.

- GitHub(*https://github.com/iainfoulds/azure-samples/raw/master/dsc.zip*)에서 DSC 패키지를 다운로드하도록 VM 인스턴스에 지시합니다.
- 설치 스크립트를 실행하도록 확장을 설정합니다(`configure-http.ps1`).
- [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss)를 사용하여 확장 집합에 대한 정보를 가져옵니다.
- [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss)를 사용하여 VM 인스턴스에 확장을 적용합니다.

DSC 확장은 *myResourceGroup*이라는 리소스 그룹의 *myScaleSet* VM 인스턴스에 적용됩니다. 다음과 같이 사용자 고유의 이름을 입력합니다:

```powershell
# Define the script for your Desired Configuration to download and run
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/iainfoulds/azure-samples/raw/master/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Get information about the scale set
$vmss = Get-AzureRmVmss `
                -ResourceGroupName "myResourceGroup" `
                -VMScaleSetName "myScaleSet"

# Add the Desired State Configuration extension to install IIS and configure basic website
$vmss = Add-AzureRmVmssExtension `
    -VirtualMachineScaleSet $vmss `
    -Publisher Microsoft.Powershell `
    -Type DSC `
    -TypeHandlerVersion 2.24 `
    -Name "DSC" `
    -Setting $dscConfig

# Update the scale set and apply the Desired State Configuration extension to the VM instances
Update-AzureRmVmss `
    -ResourceGroupName "myResourceGroup" `
    -Name "myScaleSet"  `
    -VirtualMachineScaleSet $vmss
```

확장 집합에 대한 업그레이드 정책이 *수동*이면 [Update-AzureRmVmssInstance](/powershell/module/azurerm.compute/update-azurermvmssinstance)를 사용하여 VM 인스턴스를 업데이트합니다. 이 cmdlet은 업데이트된 확장 집합 구성을 VM 인스턴스에 적용하고 응용 프로그램을 설치합니다.


## <a name="install-an-app-to-a-linux-vm-with-cloud-init"></a>cloud-init를 사용하여 Linux VM에 앱 설치
[Cloud-init](https://cloudinit.readthedocs.io/latest/)는 처음 부팅 시 Linux VM을 사용자 지정하는 데 널리 사용되는 방법입니다. Cloud-init를 사용하여 패키지를 설치하고 파일을 쓰거나, 사용자 및 보안을 구성할 수 있습니다. 초기 부팅 프로세스 중에 cloud-init가 실행되면 구성을 적용하기 위한 추가 단계나 필요한 에이전트가 없습니다.

Cloud-init는 배포에서도 작동합니다. 예를 들어, 패키지를 설치하는 데 **apt-get install** 또는 **yum install**은 사용하지 않습니다. 대신 설치할 패키지 목록을 정의할 수 있습니다. cloud-init에서 선택한 배포판의 기본 패키지 관리 도구를 자동으로 사용합니다.

*cloud-init.txt* 예제 파일을 포함한 자세한 내용은 [cloud-init를 사용하여 Azure VM 사용자 지정](../virtual-machines/linux/using-cloud-init.md)을 참조하세요.

확장 집합을 만들고 cloud-init 파일을 사용하려면 `--custom-data` 매개 변수를 [az vmss create](/cli/azure/vmss#create) 명령에 추가하고 cloud-init 파일의 이름을 지정합니다. 다음 예제에서는 *myResourceGroup*에 *myScaleSet*라는 확장 집합을 만들고, *cloud-init.txt* 파일을 사용하여 VM 인스턴스를 구성합니다. 다음과 같이 사용자 고유의 이름을 입력합니다:

```azurecli
az vmss create \
  --resource-group myResourceGroup \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys
```


## <a name="install-applications-as-a-set-scales-out"></a>집합이 확장됨에 따라 응용 프로그램 설치
확장 집합을 사용하면 응용 프로그램을 실행하는 VM 인스턴스의 수를 늘릴 수 있습니다. 이 규모 확장 프로세스는 수동으로 시작하거나 CPU 또는 메모리 사용량과 같은 메트릭에 따라 자동으로 시작할 수 있습니다.

사용자 지정 스크립트 확장을 확장 집합에 적용한 경우 새 VM 인스턴스 각각에 응용 프로그램이 설치됩니다. 확장 집합이 미리 설치된 응용 프로그램이 있는 사용자 지정 이미지를 기반으로 하는 경우 새 VM 인스턴스 각각은 사용 가능한 상태로 배포됩니다. 

확장 집합 VM 인스턴스가 컨테이너 호스트인 경우 사용자 지정 스크립트 확장을 사용하여 필요한 컨테이너 이미지를 끌어와 실행할 수 있습니다. 사용자 지정 스크립트 확장은 Azure Container Service와 같은 오케스트레이터를 사용하여 새 VM 인스턴스를 등록할 수도 있습니다.


## <a name="deploy-application-updates"></a>응용 프로그램 업데이트 배포
응용 프로그램 코드, 라이브러리 또는 패키지를 업데이트하면 최신 응용 프로그램 상태를 확장 집합의 VM 인스턴스로 푸시할 수 있습니다. 사용자 지정 스크립트 확장을 사용하면 응용 프로그램이 업데이트되고 자동으로 배포되지는 않습니다. 업데이트된 버전 이름이 있는 설치 스크립트를 가리키는 것과 같이 사용자 지정 스크립트 구성을 변경합니다. 이전 예제에서 사용자 지정 스크립트 확장은 다음과 같이 *automate_nginx.sh*라는 스크립트를 사용합니다.

```json
{
  "fileUris": ["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate_nginx.sh"],
  "commandToExecute": "./automate_nginx.sh"
}
```

설치 스크립트가 변경되지 않는 한 응용 프로그램에 대한 모든 업데이트는 사용자 지정 스크립트 확장에 공개되지 않습니다. 한 가지 방법은 응용 프로그램 릴리스와 함께 증가하는 버전 번호를 포함하도록 하는 것입니다. 이제 사용자 지정 스크립트 확장은 다음과 같이 *automate_nginx_v2.sh*를 참조할 수 있습니다.

```json
{
  "fileUris": ["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate_nginx_v2.sh"],
  "commandToExecute": "./automate_nginx_v2.sh"
}
```

이제 사용자 지정 스크립트 확장이 VM 인스턴스에 대해 실행되어 최신 응용 프로그램 업데이트를 적용합니다.


### <a name="install-applications-with-os-updates"></a>OS 업데이트를 사용하여 응용 프로그램 설치
새 OS 릴리스를 사용할 수 있는 경우 새 사용자 지정 이미지를 사용하거나 빌드하고 확장 집합에 [OS 업그레이드를 배포](virtual-machine-scale-sets-upgrade-scale-set.md)할 수 있습니다. 각 VM 인스턴스는 지정한 최신 이미지로 업그레이드됩니다. 미리 설치된 응용 프로그램이 있는 사용자 지정 이미지, 사용자 지정 스크립트 확장 또는 PowerShell DSC를 사용하여 업그레이드를 수행할 때 응용 프로그램을 자동으로 사용할 수 있습니다. 버전 호환성 문제가 없는지 확인하기 위해 이 프로세스를 수행할 때 응용 프로그램 유지 관리를 계획해야 합니다.

미리 설치된 응용 프로그램이 있는 사용자 지정 VM 이미지를 사용하는 경우, 응용 프로그램 업데이트를 배포 파이프라인과 통합하여 새 이미지를 빌드하고 확장 집합 전체에 OS 업그레이드를 배포할 수 있습니다. 이 방법을 사용하면 파이프라인에서 최신 응용 프로그램 빌드를 선택하고, VM 이미지를 만들고 유효성을 검사한 다음, 확장 집합의 VM 인스턴스를 업그레이드할 수 있습니다. 사용자 지정 VM 이미지에서 응용 프로그램 업데이트를 빌드하고 배포하는 배포 파이프라인을 실행하려면 [Visual Studio Team Services](https://www.visualstudio.com/team-services/), [Spinnaker](https://www.spinnaker.io/) 또는 [Jenkins](https://jenkins.io/)를 사용할 수 있습니다.


## <a name="next-steps"></a>다음 단계
확장 집합에 응용 프로그램을 빌드하고 배포할 때 [확장 집합 디자인 개요](virtual-machine-scale-sets-design-overview.md)를 검토할 수 있습니다. 확장 집합을 관리하는 방법에 대한 자세한 내용은 [PowerShell을 사용하여 확장 집합 관리](virtual-machine-scale-sets-windows-manage.md)를 참조하세요.
