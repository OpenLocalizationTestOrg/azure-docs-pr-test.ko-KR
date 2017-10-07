---
title: "Azure Resource Manager 템플릿에 aaaVirtual 컴퓨터 | Microsoft Azure"
description: "Hello 가상 컴퓨터 리소스는 Azure Resource Manager 템플릿에 정의 된 방법에 대해 자세히 알아보기"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="d6309-103">Azure Resource Manager 템플릿의 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="d6309-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="d6309-104">이 문서에서는 toovirtual 컴퓨터에 적용 되는 Azure 리소스 관리자 템플릿의 측면을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-104">This article describes aspects of an Azure Resource Manager template that apply toovirtual machines.</span></span> <span data-ttu-id="d6309-105">이 문서는 가상 컴퓨터를 만들기 위한 완전한 템플릿 설명하지 않습니다. 이를 위해 저장소 계정, 네트워크 인터페이스, 공용 IP 주소 및 가상 네트워크에 대한 리소스 정의가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="d6309-106">이러한 리소스를 함께 정의할 수 있는 방법을 하는 방법에 대 한 자세한 내용은 참조 hello [리소스 관리자 템플릿 연습](../../azure-resource-manager/resource-manager-template-walkthrough.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-106">For more information about how these resources can be defined together, see hello [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="d6309-107">여러 [hello 갤러리에 템플릿](https://azure.microsoft.com/documentation/templates/?term=VM) hello VM 리소스를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-107">There are many [templates in hello gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include hello VM resource.</span></span> <span data-ttu-id="d6309-108">템플릿에 포함될 수 있는 모든 요소가 여기에 설명되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="d6309-109">이 예제에서는 지정된 수의 VM을 만들기 위한 템플릿의 일반적인 리소스 섹션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
><span data-ttu-id="d6309-110">이 예제에서는 이전에 만든 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="d6309-111">Hello 서식 파일에서 배포 하 여 hello 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-111">You could create hello storage account by deploying it from hello template.</span></span> <span data-ttu-id="d6309-112">hello 예제 hello 서식 파일에 정의한 해당 종속 리소스와 네트워크 인터페이스에도 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-112">hello example also relies on a network interface and its dependent resources that would be defined in hello template.</span></span> <span data-ttu-id="d6309-113">이러한 리소스 hello 예제에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-113">These resources are not shown in hello example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="d6309-114">API 버전</span><span class="sxs-lookup"><span data-stu-id="d6309-114">API Version</span></span>

<span data-ttu-id="d6309-115">서식 파일을 사용 하 여 리소스를 배포할 때 버전 hello API toouse의 toospecify가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-115">When you deploy resources using a template, you have toospecify a version of hello API toouse.</span></span> <span data-ttu-id="d6309-116">hello 예제가 apiVersion 요소를 사용 하 여 hello 가상 컴퓨터 리소스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-116">hello example shows hello virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="d6309-117">hello 버전의 hello 서식 파일에 지정 된 API hello 서식 파일에서 정의할 수 있는 속성에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-117">hello version of hello API you specify in your template affects which properties you can define in hello template.</span></span> <span data-ttu-id="d6309-118">일반적으로 템플릿을 만들 때 hello 최신 API 버전을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-118">In general, you should select hello most recent API version when creating templates.</span></span> <span data-ttu-id="d6309-119">기존 서식 파일에 대 한 toocontinue 이전 API 버전을 사용 하 여 원하는 하거나 hello 최신 버전 tootake 새 기능 활용에 대 한 서식 파일을 업데이트 하면 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-119">For existing templates, you can decide whether you want toocontinue using an earlier API version, or update your template for hello latest version tootake advantage of new features.</span></span>

<span data-ttu-id="d6309-120">Hello 최신 API 버전을 가져오기 위한 이러한 기회를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-120">Use these opportunities for getting hello latest API versions:</span></span>

- <span data-ttu-id="d6309-121">REST API - [모든 리소스 공급자 나열](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="d6309-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="d6309-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="d6309-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="d6309-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="d6309-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="d6309-124">매개 변수 및 변수</span><span class="sxs-lookup"><span data-stu-id="d6309-124">Parameters and variables</span></span>

<span data-ttu-id="d6309-125">[매개 변수](../../resource-group-authoring-templates.md) 간편 하 게 하면 toospecify 값 hello 서식 파일을 실행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you toospecify values for hello template when you run it.</span></span> <span data-ttu-id="d6309-126">이 매개 변수 섹션 hello 예제에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-126">This parameters section is used in hello example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="d6309-127">Hello 예제 서식 파일을 배포 하는 경우 값을 입력 hello 이름과 hello 관리자 계정의 암호 Vm toocreate 각 VM 및 hello 수에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-127">When you deploy hello example template, you enter values for hello name and password of hello administrator account on each VM and hello number of VMs toocreate.</span></span> <span data-ttu-id="d6309-128">Hello 템플릿을 사용 하 여 관리 되는 별도 파일에 매개 변수 값 지정 또는 메시지가 표시 되 면 값을 제공 하는 hello 선택할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-128">You have hello option of specifying parameter values in a separate file that's managed with hello template, or providing values when prompted.</span></span>

<span data-ttu-id="d6309-129">[변수](../../resource-group-authoring-templates.md) 간편 하 게 하면 tooset 값 전체에 걸쳐 반복 해 서 사용 되는 또는 시간이 지나면서 달라질 수 있는 hello 서식 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you tooset up values in hello template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="d6309-130">이 변수 섹션 hello 예제에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-130">This variables section is used in hello example:</span></span>

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

<span data-ttu-id="d6309-131">Hello 예제 서식 파일을 배포 하는 경우 변수 값은 hello 이름 및 식별자의 hello 이전에 만든 저장소 계정에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-131">When you deploy hello example template, variable values are used for hello name and identifier of hello previously created storage account.</span></span> <span data-ttu-id="d6309-132">변수는 hello 진단 확장에 대 한 사용 되는 tooprovide hello 설정도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-132">Variables are also used tooprovide hello settings for hello diagnostic extension.</span></span> <span data-ttu-id="d6309-133">사용 하 여 hello [Azure 리소스 관리자 템플릿 만들기에 대 한 유용한](../../resource-manager-template-best-practices.md) toohelp 용도 toostructure hello 매개 변수 및 변수 서식 파일에서 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-133">Use hello [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) toohelp you decide how you want toostructure hello parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="d6309-134">리소스 루프</span><span class="sxs-lookup"><span data-stu-id="d6309-134">Resource loops</span></span>

<span data-ttu-id="d6309-135">응용 프로그램에 하나 이상의 가상 컴퓨터가 필요할 때 템플릿에서 복사 요소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="d6309-136">이 선택적 요소는 매개 변수로 지정 하는 Vm의 hello 많이 만들지 반복:</span><span class="sxs-lookup"><span data-stu-id="d6309-136">This optional element loops through creating hello number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="d6309-137">또한 루프 인덱스 hello hello 예에서는 hello 리소스에 대 한 값을 hello 중 일부를 지정할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-137">Also, notice in hello example that hello loop index is used when specifying some of hello values for hello resource.</span></span> <span data-ttu-id="d6309-138">예를 들어 3 개 hello 형태의 hello 운영 체제 디스크의 인스턴스 수를 입력 한 경우 myOSDisk1, myOSDisk2, 및 myOSDisk3 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-138">For example, if you entered an instance count of three, hello names of hello operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="d6309-139">이 예제에서는 hello 가상 컴퓨터에 대 한 관리 되는 디스크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-139">This example uses managed disks for hello virtual machines.</span></span>
>
>

<span data-ttu-id="d6309-140">필요할 수 있는 hello 서식 파일의 한 리소스에 대 한 루프를 만드는 있습니다 toouse hello 루프를 만들거나 다른 리소스에 액세스할 때 염두에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-140">Keep in mind that creating a loop for one resource in hello template may require you toouse hello loop when creating or accessing other resources.</span></span> <span data-ttu-id="d6309-141">예를 들어 여러 Vm hello 3 개의 네트워크 인터페이스를 만드는 과정 루프도 해야 하는 세 개의 Vm을 만드는 과정 서식 파일에 반복 되므로 동일한 네트워크 인터페이스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-141">For example, multiple VMs can’t use hello same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="d6309-142">Hello 루프 인덱스에 사용 되는 tooidentify는 네트워크 인터페이스 tooa VM에 할당할 때 해당:</span><span class="sxs-lookup"><span data-stu-id="d6309-142">When assigning a network interface tooa VM, hello loop index is used tooidentify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="d6309-143">종속성</span><span class="sxs-lookup"><span data-stu-id="d6309-143">Dependencies</span></span>

<span data-ttu-id="d6309-144">대부분의 리소스는 다른 리소스 toowork에 올바르게 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-144">Most resources depend on other resources toowork correctly.</span></span> <span data-ttu-id="d6309-145">가상 컴퓨터 네트워크 인터페이스 필요 함을 toodo 가상 네트워크와 연결 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-145">Virtual machines must be associated with a virtual network and toodo that it needs a network interface.</span></span> <span data-ttu-id="d6309-146">hello [dependsOn](../../resource-group-define-dependencies.md) 요소는 사용 되는 toomake 해당 hello 네트워크 인터페이스는 hello Vm 생성 되기 전에 사용 준비 toobe 있는지:</span><span class="sxs-lookup"><span data-stu-id="d6309-146">hello [dependsOn](../../resource-group-define-dependencies.md) element is used toomake sure that hello network interface is ready toobe used before hello VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="d6309-147">리소스 관리자는 배포되는 다른 리소스에 종속되지 않는 모든 리소스를 동시에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="d6309-148">불필요한 종속성을 지정하여 실수로 배포 속도를 늦출 수 있으므로 종속성을 설정할 때 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="d6309-149">종속성은 여러 리소스를 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="d6309-150">예를 들어 hello 네트워크 인터페이스 hello 공용 IP 주소와 가상 네트워크 리소스에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-150">For example, hello network interface depends on hello public IP address and virtual network resources.</span></span>

<span data-ttu-id="d6309-151">종속성이 필수인지 어떻게 알 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="d6309-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="d6309-152">Hello 서식 파일에 설정 된 hello 값 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-152">Look at hello values you set in hello template.</span></span> <span data-ttu-id="d6309-153">Hello 가상 컴퓨터 리소스 정의에서 요소는 tooanother 리소스 hello에 배포 된 경우 동일한 템플릿을 종속성 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-153">If an element in hello virtual machine resource definition points tooanother resource that is deployed in hello same template, you need a dependency.</span></span> <span data-ttu-id="d6309-154">예를 들어 예제 가상 컴퓨터는 네트워크 프로필을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="d6309-155">tooset이이 속성을 hello 네트워크 인터페이스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-155">tooset this property, hello network interface must exist.</span></span> <span data-ttu-id="d6309-156">따라서 종속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="d6309-157">하나의 리소스 (자식) 다른 리소스 (부모) 내에 정의 된 경우 tooset 종속성을 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-157">You also need tooset a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="d6309-158">예를 들어 hello 진단 설정 및 사용자 지정 스크립트 확장 둘 다 정의 된 hello 가상 컴퓨터의 자식 리소스 그룹으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-158">For example, hello diagnostic settings and custom script extensions are both defined as child resources of hello virtual machine.</span></span> <span data-ttu-id="d6309-159">Hello 가상 컴퓨터가 둘 때까지 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-159">They cannot be created until hello virtual machine exists.</span></span> <span data-ttu-id="d6309-160">따라서 두 리소스가 hello 가상 컴퓨터에 종속으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-160">Therefore, both resources are marked as dependent on hello virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="d6309-161">프로필</span><span class="sxs-lookup"><span data-stu-id="d6309-161">Profiles</span></span>

<span data-ttu-id="d6309-162">몇 가지 프로필 요소는 가상 컴퓨터 리소스를 정의할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="d6309-163">일부는 필요하고 일부는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-163">Some are required and some are optional.</span></span> <span data-ttu-id="d6309-164">예를 들어 hello hardwareProfile, osProfile, storageProfile, 및 networkProfile 요소는 필수 이지만 hello diagnosticsProfile은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-164">For example, hello hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but hello diagnosticsProfile is optional.</span></span> <span data-ttu-id="d6309-165">이러한 프로필은 다음과 같은 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="d6309-166">크기</span><span class="sxs-lookup"><span data-stu-id="d6309-166">size</span></span>](sizes.md)
- <span data-ttu-id="d6309-167">[이름](/architecture/best-practices/naming-conventions) 및 자격 증명</span><span class="sxs-lookup"><span data-stu-id="d6309-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="d6309-168">디스크 및 [운영 체제 설정](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="d6309-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="d6309-169">네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="d6309-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="d6309-170">부트 진단</span><span class="sxs-lookup"><span data-stu-id="d6309-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="d6309-171">디스크 및 이미지</span><span class="sxs-lookup"><span data-stu-id="d6309-171">Disks and images</span></span>
   
<span data-ttu-id="d6309-172">Azure에서 vhd 파일은 [디스크 또는 이미지](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="d6309-173">Vhd 파일에 hello 운영 체제가 특수 toobe가 특정 VM 인 경우 참조 된 tooas 디스크 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-173">When hello operating system in a vhd file is specialized toobe a specific VM, it is referred tooas a disk.</span></span> <span data-ttu-id="d6309-174">Hello 운영 체제 vhd 파일에 일반화 된 toobe toocreate 많은 Vm을 사용할 경우 참조 tooas 이미지는.</span><span class="sxs-lookup"><span data-stu-id="d6309-174">When hello operating system in a vhd file is generalized toobe used toocreate many VMs, it is referred tooas an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="d6309-175">플랫폼 이미지에서 새 가상 컴퓨터 및 새 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="d6309-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="d6309-176">VM을 만들 때 어떤 운영 체제 toouse를 결정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-176">When you create a VM, you must decide what operating system toouse.</span></span> <span data-ttu-id="d6309-177">hello imageReference 요소는 새 VM의 사용 되는 toodefine hello 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-177">hello imageReference element is used toodefine hello operating system of a new VM.</span></span> <span data-ttu-id="d6309-178">hello 예제는 Windows Server 운영 체제에 대 한 정의 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-178">hello example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="d6309-179">Linux 운영 체제 toocreate 하려는 경우에이 정의 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-179">If you want toocreate a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="d6309-180">Hello 운영 체제 디스크에 대 한 구성 설정은 hello osDisk 요소가 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-180">Configuration settings for hello operating system disk are assigned with hello osDisk element.</span></span> <span data-ttu-id="d6309-181">hello 예제에서는 새 관리 되는 디스크를 정의 너무 모드 집합 캐싱 hello**ReadWrite** 에 해당 하는 hello 디스크에서 만들어지는 [플랫폼 이미지](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="d6309-181">hello example defines a new managed disk with hello caching mode set too**ReadWrite** and that hello disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="d6309-182">기존 Managed Disks에서 새 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="d6309-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="d6309-183">기존 디스크 로부터 toocreate 가상 컴퓨터를 hello imageReference 및 hello osProfile 요소를 제거 하 고 이러한 디스크 설정을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-183">If you want toocreate virtual machines from existing disks, remove hello imageReference and hello osProfile elements and define these disk settings:</span></span>

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="d6309-184">관리되는 이미지에서 새 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="d6309-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="d6309-185">Toocreate 하려는 경우 관리 되는 이미지에서 가상 컴퓨터 hello imageReference 요소를 변경 하 고 이러한 디스크 설정을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-185">If you want toocreate a virtual machine from a managed image, change hello imageReference element and define these disk settings:</span></span>

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a><span data-ttu-id="d6309-186">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="d6309-186">Attach data disks</span></span>

<span data-ttu-id="d6309-187">필요에 따라 데이터 디스크 toohello Vm을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-187">You can optionally add data disks toohello VMs.</span></span> <span data-ttu-id="d6309-188">hello [디스크 번호](sizes.md) 있습니다를 사용 하는 운영 체제 디스크의 hello 크기에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-188">hello [number of disks](sizes.md) depends on hello size of operating system disk that you use.</span></span> <span data-ttu-id="d6309-189">Hello로 hello Vm의 크기는 tooStandard_DS1_v2, hello에는 두 toohello 추가 될 수 있는 데이터 디스크의 최대 수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-189">With hello size of hello VMs set tooStandard_DS1_v2, hello maximum number of data disks that could be added toohello them is two.</span></span> <span data-ttu-id="d6309-190">Hello 예제에서는 하나의 관리 되는 데이터 디스크가 추가 되 tooeach VM:</span><span class="sxs-lookup"><span data-stu-id="d6309-190">In hello example, one managed data disk is being added tooeach VM:</span></span>

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a><span data-ttu-id="d6309-191">확장</span><span class="sxs-lookup"><span data-stu-id="d6309-191">Extensions</span></span>

<span data-ttu-id="d6309-192">하지만 [확장](extensions-features.md) 별도 리소스에서 밀접 하 게 동률된 tooVMs 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied tooVMs.</span></span> <span data-ttu-id="d6309-193">Hello VM의 자식 리소스 또는 별도 리소스 확장을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-193">Extensions can be added as a child resource of hello VM or as a separate resource.</span></span> <span data-ttu-id="d6309-194">hello 예제 hello [진단 확장](extensions-diagnostics-template.md) toohello Vm 추가:</span><span class="sxs-lookup"><span data-stu-id="d6309-194">hello example shows hello [Diagnostics Extension](extensions-diagnostics-template.md) being added toohello VMs:</span></span>

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

<span data-ttu-id="d6309-195">이 확장 리소스 hello storageName 변수 및 hello 진단 변수 tooprovide 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-195">This extension resource uses hello storageName variable and hello diagnostic variables tooprovide values.</span></span> <span data-ttu-id="d6309-196">이 확장 프로그램에서 수집 되는 toochange hello 데이터를 원하는 경우에 더 많은 성능 카운터 toohello wadperfcounters 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-196">If you want toochange hello data that is collected by this extension, you can add more performance counters toohello wadperfcounters variable.</span></span> <span data-ttu-id="d6309-197">또한 hello VM 디스크 저장 되는 다른 저장소 계정에 tooput hello 진단 데이터를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-197">You could also choose tooput hello diagnostics data into a different storage account than where hello VM disks are stored.</span></span>

<span data-ttu-id="d6309-198">VM에 설치할 수 있는 다양 한 확장 프로그램 있지만 가장 유용한 hello hello 되었을 [사용자 지정 스크립트 확장](extensions-customscript.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-198">There are many extensions that you can install on a VM, but hello most useful is probably hello [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="d6309-199">처음 시작할 때 hello 예제에서는 start.ps1 라는 PowerShell 스크립트 각 VM에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-199">In hello example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

<span data-ttu-id="d6309-200">hello start.ps1 스크립트는 여러 가지 구성 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-200">hello start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="d6309-201">예를 들어 hello 예제에서 toohello Vm에 추가 된 hello 데이터 디스크는 초기화 되지 않은; 사용자 지정 스크립트 tooinitialize를 사용할 수 있습니다 이러한.</span><span class="sxs-lookup"><span data-stu-id="d6309-201">For example, hello data disks that are added toohello VMs in hello example are not initialized; you can use a custom script tooinitialize them.</span></span> <span data-ttu-id="d6309-202">여러 시작 작업이 toodo를 설정한 경우 사용할 수 있습니다 hello start.ps1 파일 toocall 다른 PowerShell 스크립트에서 Azure 저장소.</span><span class="sxs-lookup"><span data-stu-id="d6309-202">If you have multiple startup tasks toodo, you can use hello start.ps1 file toocall other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="d6309-203">PowerShell을 사용 하 여 hello 예제 있지만 사용 중인 hello 운영 체제에서 사용할 수 있는 모든 스크립팅 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-203">hello example uses PowerShell, but you can use any scripting method that is available on hello operating system that you are using.</span></span>

<span data-ttu-id="d6309-204">Hello 포털의 hello 확장 설정의 hello 설치 확장 hello 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-204">You can see hello status of hello installed extensions from hello Extensions settings in hello portal:</span></span>

![확장 상태 가져오기](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="d6309-206">Hello를 사용 하 여 확장 정보를 가져올 수도 있습니다 **Get AzureRmVMExtension** PowerShell 명령을 hello **vm 확장 get** Azure CLI 2.0 명령 또는 hello **확장 정보 가져오기 ** REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-206">You can also get extension information by using hello **Get-AzureRmVMExtension** PowerShell command, hello **vm extension get** Azure CLI 2.0 command, or hello **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="d6309-207">배포</span><span class="sxs-lookup"><span data-stu-id="d6309-207">Deployments</span></span>

<span data-ttu-id="d6309-208">서식 파일을 Azure 트랙 hello 리소스 그룹으로 이동 하 고 자동으로 배포를 배포 하는 경우 이름 toothis 배포 그룹을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-208">When you deploy a template, Azure tracks hello resources that you deployed as a group and automatically assigns a name toothis deployed group.</span></span> <span data-ttu-id="d6309-209">hello 배포의 hello 이름 hello 템플릿의 hello 이름과 달라 서 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-209">hello name of hello deployment is hello same as hello name of hello template.</span></span>

<span data-ttu-id="d6309-210">인 경우 hello 상태 hello 배포의 리소스에 대 한 자세한 내용을 보려면 hello 리소스 그룹 블레이드 hello Azure 포털에서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-210">If you are curious about hello status of resources in hello deployment, you can use hello Resource Group blade in hello Azure portal:</span></span>

![배포 정보 가져오기](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="d6309-212">문제가 toouse 아니므로 동일한 템플릿 toocreate 리소스나 tooupdate 기존 리소스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-212">It’s not a problem toouse hello same template toocreate resources or tooupdate existing resources.</span></span> <span data-ttu-id="d6309-213">Hello 기회 toosay 있는 명령을 toodeploy 템플릿을 사용 하는 경우는 [모드](../../resource-group-template-deploy.md) toouse 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-213">When you use commands toodeploy templates, you have hello opportunity toosay which [mode](../../resource-group-template-deploy.md) you want toouse.</span></span> <span data-ttu-id="d6309-214">hello 모드를 설정할 수 있습니다 tooeither **완료** 또는 **증분**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-214">hello mode can be set tooeither **Complete** or **Incremental**.</span></span> <span data-ttu-id="d6309-215">hello 기본값은 toodo 증분 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-215">hello default is toodo incremental updates.</span></span> <span data-ttu-id="d6309-216">Hello를 사용할 때는 주의 해야 **완료** 모드 이므로 리소스를 실수로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-216">Be careful when using hello **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="d6309-217">너무 hello 모드를 설정 하면**완료**, 리소스 관리자 hello 서식 파일에 없는 hello 리소스 그룹에 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-217">When you set hello mode too**Complete**, Resource Manager deletes any resources in hello resource group that are not in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6309-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d6309-218">Next Steps</span></span>

- <span data-ttu-id="d6309-219">[Azure Resource Manager 템플릿 작성](../../resource-group-authoring-templates.md)을 사용하여 고유의 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="d6309-220">Hello 템플릿을 사용 하 여 만든 배포 [리소스 관리자 템플릿을 사용 하 여 Windows 가상 컴퓨터를 만들](ps-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-220">Deploy hello template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="d6309-221">어떻게 toomanage hello를 검토 하 여 만든 Vm에 알아봅니다 [만들기 hello Azure PowerShell 모듈을 사용 하 여 Windows Vm을 관리 하 고](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6309-221">Learn how toomanage hello VMs that you created by reviewing [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
