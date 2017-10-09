---
title: "aaaDeploy 응용 프로그램에 가상 컴퓨터 크기 집합"
description: "Azure 가상 컴퓨터 크기 집합에 확장 toodepoy 응용 프로그램을 사용 합니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a>가상 컴퓨터 확장 집합에 응용 프로그램 배포

이 문서에서는 다른 hello 시간 hello 배율로 tooinstall 소프트웨어 설정 하는 방법의 프로 비전 됩니다.

Tooreview hello를 할 수 있습니다 [디자인 개요를 설정 하는 눈금](virtual-machine-scale-sets-design-overview.md) 문서도, 가상 컴퓨터 크기 집합으로 부과 된 hello 제한의 일부에 대해 설명 합니다.

## <a name="capture-and-reuse-an-image"></a>이미지 캡처 및 재사용

눈금에 대 한 기본 이미지를 Azure tooprepare에서 설정한 가상 컴퓨터를 사용할 수 있습니다. 이 프로세스는 크기 집합에 대 한 기본 이미지 hello로 참조할 수 있는 저장소 계정에 관리 되는 디스크를 만듭니다. 

다음 단계 hello 마십시오.

1. Azure 가상 컴퓨터 만들기
   * [Linux][linux-vm-create]
   * [Windows][windows-vm-create]

2. 원격으로 가상 컴퓨터를 hello 및 hello 시스템 tooyour 원하는 대로 사용자 지정 합니다.

   원한다면 지금 응용 프로그램을 설치할 수 있습니다. 그러나는 이제 응용 프로그램을 설치 하 여 만들 수 있습니다 tooremove 해야 하기 때문에 더욱 복잡 한 응용 프로그램 업그레이드를 알고 그 첫 번째입니다. 대신, 응용 프로그램 같은 특정 런타임 또는 운영 체제 기능 할 수 있는 필수 구성 요소 단계 tooinstall이를 사용할 수 있습니다.

3. 에 대 한 hello "컴퓨터를 캡처" 자습서에 따라 [Linux] [ linux-vm-capture] 또는 [Windows][windows-vm-capture]합니다.

4. 만들기는 [가상 컴퓨터 크기 집합] [ vmss-create] hello로 URI hello 이전 단계에서 캡처된 이미지입니다.

디스크에 대한 자세한 내용은 [Managed Disks 개요](../virtual-machines/windows/managed-disks-overview.md) 및 [연결된 데이터 디스크 사용](virtual-machine-scale-sets-attached-disks.md)을 참조하세요.

## <a name="install-when-hello-scale-set-is-provisioned"></a>Hello 크기 집합 프로 비전 될 때 설치

가상 컴퓨터 확장 될 수 있습니다 tooa 가상 컴퓨터 크기 집합을 적용 합니다. 가상 컴퓨터 확장 hello 가상 컴퓨터 크기 집합으로 전체 그룹에에서 사용자 지정할 수 있습니다. 확장에 대한 자세한 내용은 [가상 컴퓨터 확장](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.

운영 체제가 Linux 기반인지 아니면 Windows 기반인지에 따라 세 가지 주요 확장을 사용할 수 있습니다.

### <a name="windows"></a>Windows

Windows 기반 운영 체제에 대 한 hello 중 하나를 사용 하 여 **사용자 정의 스크립트 v1.8** 확장명 또는 hello **PowerShell DSC** 확장 합니다.

#### <a name="custom-script"></a>Custom Script

사용자 지정 스크립트 확장 hello hello 크기 집합의 각 가상 컴퓨터 인스턴스에서 스크립트를 실행합니다. 구성 파일 또는 변수는 파일을 다운로드 한 toohello 가상 컴퓨터를 한 다음 명령을 실행을 나타냅니다. 예를 들어이 toorun 설치 관리자, 스크립트, 배치 파일에서 모든 실행 파일을 사용할 수 있습니다.

PowerShell은 hello 설정에 대 한 해시 테이블을 사용합니다. 이 예제에서는 hello 사용자 지정 스크립트 확장 toorun IIS를 설치 하는 PowerShell 스크립트를 구성 합니다.

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>사용 하 여 hello `-ProtectedSetting` 중요 한 정보가 포함 된 모든 설정에 대 한 전환 합니다.

---------


Azure CLI hello 설정에 대 한 json 파일을 사용합니다. 이 예제에서는 hello 사용자 지정 스크립트 확장 toorun IIS를 설치 하는 PowerShell 스크립트를 구성 합니다. 다음으로 json 파일 hello 저장 _settings.json_합니다.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

그런 다음 이 Azure CLI 명령을 실행합니다.

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>사용 하 여 hello `--protected-settings` 중요 한 정보가 포함 된 모든 설정에 대 한 전환 합니다.

### <a name="powershell-dsc"></a>PowerShell DSC

PowerShell DSC toocustomize hello 눈금 집합 vm 인스턴스를 사용할 수 있습니다. hello **DSC** 확장 공개한 **Microsoft.Powershell** 배포 하 고 각 가상 컴퓨터 인스턴스에서 제공 하는 hello DSC 구성을 실행 합니다. 구성 파일 또는 변수 hello 확장을 알려 줍니다 여기서 *.zip* 패키지는 이며 _스크립트 함수_ 조합 toorun 합니다.

PowerShell은 hello 설정에 대 한 해시 테이블을 사용합니다. 이 예제에서는 IIS를 설치하는 DSC 패키지를 배포합니다.

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>사용 하 여 hello `-ProtectedSetting` 중요 한 정보가 포함 된 모든 설정에 대 한 전환 합니다.

-----------

Azure CLI hello 설정에 대 한 json을 사용합니다. 이 예제에서는 IIS를 설치하는 DSC 패키지를 배포합니다. 다음으로 json 파일 hello 저장 _settings.json_합니다.

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

그런 다음 이 Azure CLI 명령을 실행합니다.

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>사용 하 여 hello `--protected-settings` 중요 한 정보가 포함 된 모든 설정에 대 한 전환 합니다.

### <a name="linux"></a>Linux

Linux 어느 hello צ ְ ײ **사용자 정의 스크립트 v2.0** 확장 또는 사용 하 여 **클라우드 init** 를 만드는 동안 합니다.

사용자 지정 스크립트는 파일 toohello 가상 컴퓨터 인스턴스를 다운로드 하 고 명령을 실행 하는 간단한 확장 합니다.

#### <a name="custom-script"></a>Custom Script

다음으로 json 파일 hello 저장 _settings.json_합니다.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

기존 가상 컴퓨터 크기 집합 확장 tooan이 Azure CLI tooadd hello를 사용 합니다. Hello 규모에 맞게 각 가상 컴퓨터 실행 hello 확장명이 자동으로 설정 합니다.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>사용 하 여 hello `--protected-settings` 중요 한 정보가 포함 된 모든 설정에 대 한 전환 합니다.

#### <a name="cloud-init"></a>Cloud-Init

클라우드 Init hello 눈금 세트를 만들 때 사용 됩니다. 첫째, 명명 된 로컬 파일을 만들 _클라우드 init.txt_ 구성 tooit 추가 합니다. 예제는 [이 gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)를 참조하세요.

사용 하 여 hello Azure CLI toocreate 소수 자릿수를 설정합니다. hello `--custom-data` 필드에서 클라우드 초기화 스크립트의 hello 파일 이름을 허용 합니다.

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a>응용 프로그램 업데이트를 관리하려면 어떻게 해야 하나요?

확장을 통해 응용 프로그램을 배포한 경우 어떤 방식으로든에서 hello 확장 정의 변경 합니다. 이러한 변경으로 인해 hello 확장 재배포 toobe tooall 가상 컴퓨터 인스턴스. 무언가 **해야** Azure가 확장 hello 표시 하지 않으려면 변경, 참조 된 파일 이름 바꾸기와 같은 hello 확장에 대 한 변경할 수 있습니다.

사용자 고유의 운영 체제 이미지에 hello 응용 프로그램을 반영 하는 경우 응용 프로그램 업데이트에 대 한 자동화 된 배포 파이프라인을 사용 합니다. 프로덕션 환경으로 설정 하는 준비 된 눈금으로 교체 신속한 아키텍처 toofacilitate 프로그램을 디자인 합니다. 이 방법의 좋은 예는 hello [Azure Spinnaker 드라이버 작업](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/)합니다.

[Packer](https://www.packer.io/) 및 [Terraform](https://www.terraform.io/) 지원 Azure 리소스 관리자도 "code" 다른 이름으로 이미지를 정의 하 고 Azure에서 빌드할 수 있도록 hello VHD 크기 집합의 사용 합니다. 그러나 사용자가 Marketplace에서 직접 조작하지 않으므로 확장/사용자 지정 스크립트가 좀 더 중요한 경우 이렇게 하면 Marketplace 이미지에 문제가 될 수 있습니다.

## <a name="what-happens-when-a-scale-set-scales-out"></a>확장 집합이 확장되면 어떻게 되나요?
하나 이상의 가상 컴퓨터 tooa 크기 집합에 추가 하면 hello 응용 프로그램은 자동으로 설치 됩니다. 예제 hello 크기 조정 설정에 정의 된 확장에 대 한 실행 새 가상 컴퓨터에 생성 될 때마다 합니다. Hello 크기 집합 사용자 지정 이미지를 기반 하는 경우 모든 새 가상 컴퓨터는 hello 원본 사용자 지정 이미지의 복사본을입니다. Hello 눈금 집합 가상 컴퓨터는 컨테이너 호스트를 시작 코드 tooload hello 컨테이너를 사용자 지정 스크립트 확장에서 할 수 있습니다. 또는 확장이 클러스터 조정자에 등록하는 Azure Container Service 같은 에이전트를 설치할 수 있습니다.


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a>업데이트 도메인 간에 OS 업데이트를 롤아웃하려면 어떻게 해야 할까요?
Tooupdate 한다고 가정 hello 가상 컴퓨터 크기를 유지 하면서 OS 이미지는 실행을 설정 합니다. PowerShell 및 Azure CLI hello hello 가상 컴퓨터 이미지를 한 번에 하나의 가상 컴퓨터를 업데이트할 수 있습니다. hello [가상 컴퓨터 크기 집합 업그레이드](./virtual-machine-scale-sets-upgrade-scale-set.md) 도 문서에 있는 가상 컴퓨터 크기 집합에서 운영 체제를 업그레이드 하는 사용 가능한 tooperform 옵션과 각 옵션의 추가 정보를 제공 합니다.

## <a name="next-steps"></a>다음 단계

* [PowerShell toomanage를 사용 하 여 크기 집합입니다.](virtual-machine-scale-sets-windows-manage.md)
* [확장 집합 템플릿 만들기](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

