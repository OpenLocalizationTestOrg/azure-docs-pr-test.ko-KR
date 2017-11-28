---
title: "응용 프로그램에 Azure 가상 컴퓨터 크기 집합 aaaDeploy | Microsoft Docs"
description: "Toodeploy 가상 컴퓨터 크기는 Azure 리소스 관리자 템플릿을 사용 하 여 집합에 단순 자동 크기 조정 응용 프로그램에 알아봅니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 6fccc310312cabfcdddfcbcd2d154fc5cc440417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="d904e-103">템플릿을 사용하여 자동 크기 조정 앱 배포</span><span class="sxs-lookup"><span data-stu-id="d904e-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="d904e-104">[Azure 리소스 관리자 템플릿](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) 은 훌륭한 방법 toodeploy 관련된 리소스의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="d904e-105">이 자습서를 기반 [간단한 크기 집합 배포](virtual-machine-scale-sets-mvss-start.md) toodeploy 설명에 단순 자동 크기 조정 응용 프로그램 설정 방법 Azure 리소스 관리자 템플릿을 사용 하 여에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how toodeploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="d904e-106">PowerShell, CLI 또는 hello 포털을 사용 하 여 자동 크기 조정을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-106">You can also set up autoscaling using PowerShell, CLI, or hello portal.</span></span> <span data-ttu-id="d904e-107">자세한 내용은 [크기 자동 조정 개요](virtual-machine-scale-sets-autoscale-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d904e-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="d904e-108">2개의 빠른 시작 템플릿</span><span class="sxs-lookup"><span data-stu-id="d904e-108">Two quickstart templates</span></span>
<span data-ttu-id="d904e-109">확장 집합을 배포할 때 [VM 확장](../virtual-machines/virtual-machines-windows-extensions-features.md)을 사용하여 플랫폼 이미지에 새 소프트웨어를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="d904e-110">VM 확장은 Azure Virtual Machines에 배포 후 구성 및 Automation 작업(예: 앱 배포)을 제공하는 작은 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="d904e-111">두 개의 서로 다른 예제 서식 파일에 제공 됩니다 [Azure/azure-빠른 시작-템플릿](https://github.com/Azure/azure-quickstart-templates) VM 확장을 사용 하 여 toodeploy 눈금에 자동 크기 조정 응용 프로그램을 설정 하는 방법을 보여 주는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how toodeploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="d904e-112">Linux의 Python HTTP 서버</span><span class="sxs-lookup"><span data-stu-id="d904e-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="d904e-113">hello [Linux에서 Python HTTP 서버](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) 샘플 템플릿은 Linux 크기 집합에서 실행 되는 단순 자동 크기 조정 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-113">hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="d904e-114">[Bottle](http://bottlepy.org/docs/dev/), Python 웹 프레임 워크 및 간단한 HTTP 서버 hello에 크기 집합 VM 확장 하는 사용자 지정 스크립트를 사용 하 여 각 VM에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in hello scale set using a custom script VM extension.</span></span> <span data-ttu-id="d904e-115">hello 눈금 평균 CPU 사용률은 모든 Vm에서 60% 보다 크면 고 hello 평균 CPU 사용률은 30% 보다 작은 경우 작은 규모를 눈금을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-115">hello scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when hello average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="d904e-116">또한 toohello 크기 집합 리소스에 hello *azuredeploy.json* 예제 서식 파일을 가상 네트워크, 공용 IP 주소, 부하 분산 장치 및 자동 크기 조정 설정 리소스도 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-116">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="d904e-117">템플릿에서 이러한 리소스를 만드는 방법에 대한 자세한 내용은 [자동 크기 조정 기능이 포함된 Linux 확장 집합](virtual-machine-scale-sets-linux-autoscale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d904e-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="d904e-118">Hello에 *azuredeploy.json* 템플릿, hello `extensionProfile` hello 속성 `Microsoft.Compute/virtualMachineScaleSets` 리소스는 사용자 지정 스크립트 확장을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-118">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="d904e-119">`fileUris`hello 스크립트가 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-119">`fileUris` specifies hello script(s) location.</span></span> <span data-ttu-id="d904e-120">이 경우 두 개의 파일: *workserver.py*, 간단한 HTTP 서버를 정의 하 고 *installserver.sh*, Bottle는 설치 및 시작 HTTP 서버 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts hello HTTP server.</span></span> <span data-ttu-id="d904e-121">`commandToExecute`hello 크기 집합을 배포한 후 hello 명령 toorun를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-121">`commandToExecute` specifies hello command toorun after hello scale set has been deployed.</span></span>

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "lapextension",
                "properties": {
                  "publisher": "Microsoft.Azure.Extensions",
                  "type": "CustomScript",
                  "typeHandlerVersion": "2.0",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "fileUris": [
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
                    ],
                    "commandToExecute": "bash installserver.sh"
                  }
                }
              }
            ]
          }
```

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="d904e-122">Windows의 ASP.NET MVC 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d904e-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="d904e-123">hello [Windows에서 ASP.NET MVC 응용 프로그램](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) 샘플 템플릿은 Windows 크기 집합의 IIS에서 실행 되는 간단한 ASP.NET MVC 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-123">hello [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="d904e-124">IIS 및 MVC 응용 프로그램 hello hello를 사용 하 여 배포 된 [PowerShell 필요한 상태 구성 (DSC)](virtual-machine-scale-sets-dsc.md) VM 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-124">IIS and hello MVC app are deployed using hello [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="d904e-125">hello 배율 설정 눈금 (VM 인스턴스에서 한 번에) 5 분 동안 CPU 사용률이 50% 보다 큰 경우.</span><span class="sxs-lookup"><span data-stu-id="d904e-125">hello scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="d904e-126">또한 toohello 크기 집합 리소스에 hello *azuredeploy.json* 예제 서식 파일을 가상 네트워크, 공용 IP 주소, 부하 분산 장치 및 자동 크기 조정 설정 리소스도 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-126">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="d904e-127">이 템플릿은 응용 프로그램 업그레이드도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="d904e-128">템플릿에서 이러한 리소스를 만드는 방법에 대한 자세한 내용은 [자동 크기 조정 기능이 포함된 WIndows 확장 집합](virtual-machine-scale-sets-windows-autoscale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d904e-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="d904e-129">Hello에 *azuredeploy.json* 템플릿, hello `extensionProfile` hello 속성 `Microsoft.Compute/virtualMachineScaleSets` 리소스 지정는 [원하는 상태 구성 (DSC)](virtual-machine-scale-sets-dsc.md) IIS 및 기본값을 설치 하 여 확장 프로그램 웹 배포 패키지에서 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-129">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="d904e-130">hello *IISInstall.ps1* 스크립트 hello 가상 컴퓨터에 IIS를 설치 하 고 hello에 *DSC* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-130">hello *IISInstall.ps1* script installs IIS on hello virtual machine and is found in hello *DSC* folder.</span></span>  <span data-ttu-id="d904e-131">hello MVC 웹 응용 프로그램 hello에 있으면 *WebDeploy* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-131">hello MVC web app is found in hello *WebDeploy* folder.</span></span>  <span data-ttu-id="d904e-132">hello 경로 toohello 설치 스크립트 및 웹 응용 프로그램 hello hello에 정의 되어 `powershelldscZip` 및 `webDeployPackage` hello에 대 한 매개 변수 *azuredeploy.parameters.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-132">hello paths toohello install script and hello web app are defined in hello `powershelldscZip` and `webDeployPackage` parameters in hello *azuredeploy.parameters.json* file.</span></span> 

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Powershell.DSC",
                "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.9",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('powershelldscUpdateTagVersion')]",
                  "settings": {
                    "configuration": {
                      "url": "[variables('powershelldscZipFullPath')]",
                      "script": "IISInstall.ps1",
                      "function": "InstallIIS"
                    },
                    "configurationArguments": {
                      "nodeName": "localhost",
                      "WebDeployPackagePath": "[variables('webDeployPackageFullPath')]"
                    }
                  }
                }
              }
            ]
          }
```

## <a name="deploy-hello-template"></a><span data-ttu-id="d904e-133">Hello 템플릿을 배포합니다</span><span class="sxs-lookup"><span data-stu-id="d904e-133">Deploy hello template</span></span>
<span data-ttu-id="d904e-134">가장 간단한 방법은 toodeploy hello hello [Linux에서 Python HTTP 서버](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) 또는 [Windows에서 ASP.NET MVC 응용 프로그램](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) 서식 파일은 toouse hello **tooAzure 배포** hello에 단추를 찾을 수 hello GitHub에서 추가 정보 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-134">hello simplest way toodeploy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is toouse hello **Deploy tooAzure** button found in hello in hello readme files in GitHub.</span></span>  <span data-ttu-id="d904e-135">또한 PowerShell 또는 Azure CLI toodeploy hello 예제 서식 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-135">You can also use PowerShell or Azure CLI toodeploy hello sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="d904e-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d904e-136">PowerShell</span></span>
<span data-ttu-id="d904e-137">복사 hello [Linux에서 Python HTTP 서버](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) 또는 [Windows에서 ASP.NET MVC 응용 프로그램](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) hello GitHub 리포지토리에 tooa 폴더에서 로컬 컴퓨터에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-137">Copy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from hello GitHub repo tooa folder on your local computer.</span></span>  <span data-ttu-id="d904e-138">열기 hello *azuredeploy.parameters.json* 파일 및 업데이트 hello 기본값의 hello `vmssName`, `adminUsername`, 및 `adminPassword` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-138">Open hello *azuredeploy.parameters.json* file and update hello default values of hello `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="d904e-139">PowerShell 스크립트를 너무 뒤 hello 저장*deploy.ps1* hello에 hello와 같은 폴더 *azuredeploy.json* 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-139">Save hello following PowerShell script too*deploy.ps1* in hello same folder as hello *azuredeploy.json* template.</span></span> <span data-ttu-id="d904e-140">toodeploy hello 샘플을 실행 하는 템플릿 hello *deploy.ps1* PowerShell 명령 창에서 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="d904e-140">toodeploy hello sample template run hello *deploy.ps1* script from a PowerShell command window.</span></span>

```powershell
param(
 [Parameter(Mandatory=$True)]
 [string]
 $subscriptionId,

 [Parameter(Mandatory=$True)]
 [string]
 $resourceGroupName,

 [string]
 $resourceGroupLocation,

 [Parameter(Mandatory=$True)]
 [string]
 $deploymentName,

 [string]
 $templateFilePath = "template.json",

 [string]
 $parametersFilePath = "parameters.json"
)

<#
.SYNOPSIS
    Registers RPs
#>
Function RegisterRP {
    Param(
        [string]$ResourceProviderNamespace
    )

    Write-Host "Registering resource provider '$ResourceProviderNamespace'";
    Register-AzureRmResourceProvider -ProviderNamespace $ResourceProviderNamespace;
}

#******************************************************************************
# Script body
# Execution begins here
#******************************************************************************
$ErrorActionPreference = "Stop"

# sign in
Write-Host "Logging in...";
Login-AzureRmAccount;

# select subscription
Write-Host "Selecting subscription '$subscriptionId'";
Select-AzureRmSubscription -SubscriptionID $subscriptionId;

# Register RPs
$resourceProviders = @("microsoft.compute","microsoft.insights","microsoft.network");
if($resourceProviders.length) {
    Write-Host "Registering resource providers"
    foreach($resourceProvider in $resourceProviders) {
        RegisterRP($resourceProvider);
    }
}

#Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $resourceGroupName -ErrorAction SilentlyContinue
if(!$resourceGroup)
{
    Write-Host "Resource group '$resourceGroupName' does not exist. toocreate a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start hello deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a><span data-ttu-id="d904e-141">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d904e-141">Azure CLI</span></span>
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely toocause confusing bugs when looping arrays or arguments (e.g. $@)

usage() { echo "Usage: $0 -i <subscriptionId> -g <resourceGroupName> -n <deploymentName> -l <resourceGroupLocation>" 1>&2; exit 1; }

declare subscriptionId=""
declare resourceGroupName=""
declare deploymentName=""
declare resourceGroupLocation=""

# Initialize parameters specified from command line
while getopts ":i:g:n:l:" arg; do
    case "${arg}" in
        i)
            subscriptionId=${OPTARG}
            ;;
        g)
            resourceGroupName=${OPTARG}
            ;;
        n)
            deploymentName=${OPTARG}
            ;;
        l)
            resourceGroupLocation=${OPTARG}
            ;;
        esac
done
shift $((OPTIND-1))

#Prompt for parameters is some required parameters are missing
if [[ -z "$subscriptionId" ]]; then
    echo "Subscription Id:"
    read subscriptionId
    [[ "${subscriptionId:?}" ]]
fi

if [[ -z "$resourceGroupName" ]]; then
    echo "ResourceGroupName:"
    read resourceGroupName
    [[ "${resourceGroupName:?}" ]]
fi

if [[ -z "$deploymentName" ]]; then
    echo "DeploymentName:"
    read deploymentName
fi

if [[ -z "$resourceGroupLocation" ]]; then
    echo "Enter a location below toocreate a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file toobe used
templateFilePath="template.json"

if [ ! -f "$templateFilePath" ]; then
    echo "$templateFilePath not found"
    exit 1
fi

#parameter file path
parametersFilePath="parameters.json"

if [ ! -f "$parametersFilePath" ]; then
    echo "$parametersFilePath not found"
    exit 1
fi

if [ -z "$subscriptionId" ] || [ -z "$resourceGroupName" ] || [ -z "$deploymentName" ]; then
    echo "Either one of subscriptionId, resourceGroupName, deploymentName is empty"
    usage
fi

#login tooazure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set hello default subscription id
az account set --name $subscriptionId

set +e

#Check for existing RG
az group show $resourceGroupName 1> /dev/null

if [ $? != 0 ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
    set -e
    (
        set -x
        az group create --name $resourceGroupName --location $resourceGroupLocation 1> /dev/null
    )
    else
    echo "Using existing resource group..."
fi

#Start deployment
echo "Starting deployment..."
(
    set -x
    az group deployment create --name $deploymentName --resource-group $resourceGroupName --template-file $templateFilePath --parameters $parametersFilePath
)

if [ $?  == 0 ];
 then
    echo "Template has been successfully deployed"
fi
```

## <a name="next-steps"></a><span data-ttu-id="d904e-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d904e-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
