---
title: "Azure Resource Manager 템플릿의 가상 컴퓨터 | Microsoft Azure"
description: "Azure Resource Manager 템플릿에서 가상 컴퓨터 리소스를 정의하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: d9b9121bc5e38396ba4def6c17f9b373c2b48056
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="1a1d9-103">Azure Resource Manager 템플릿의 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="1a1d9-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="1a1d9-104">이 문서에서는 가상 컴퓨터에 적용되는 Azure Resource Manager 템플릿의 측면을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-104">This article describes aspects of an Azure Resource Manager template that apply to virtual machines.</span></span> <span data-ttu-id="1a1d9-105">이 문서는 가상 컴퓨터를 만들기 위한 완전한 템플릿 설명하지 않습니다. 이를 위해 저장소 계정, 네트워크 인터페이스, 공용 IP 주소 및 가상 네트워크에 대한 리소스 정의가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="1a1d9-106">이러한 리소스를 함께 정의할 수 있는 방법에 대한 자세한 내용은 [Resource Manager 템플릿 연습](../../azure-resource-manager/resource-manager-template-walkthrough.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-106">For more information about how these resources can be defined together, see the [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="1a1d9-107">갤러리에 VM 리소스를 포함하는 [많은 템플릿](https://azure.microsoft.com/documentation/templates/?term=VM)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-107">There are many [templates in the gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include the VM resource.</span></span> <span data-ttu-id="1a1d9-108">템플릿에 포함될 수 있는 모든 요소가 여기에 설명되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="1a1d9-109">이 예제에서는 지정된 수의 VM을 만들기 위한 템플릿의 일반적인 리소스 섹션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

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
><span data-ttu-id="1a1d9-110">이 예제에서는 이전에 만든 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="1a1d9-111">템플릿에서 배포하여 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-111">You could create the storage account by deploying it from the template.</span></span> <span data-ttu-id="1a1d9-112">예제에서는 또한 템플릿에서 정의될 수 있는 네트워크 인터페이스 및 해당 종속 리소스에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-112">The example also relies on a network interface and its dependent resources that would be defined in the template.</span></span> <span data-ttu-id="1a1d9-113">이러한 리소스는 예제에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-113">These resources are not shown in the example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="1a1d9-114">API 버전</span><span class="sxs-lookup"><span data-stu-id="1a1d9-114">API Version</span></span>

<span data-ttu-id="1a1d9-115">템플릿을 사용하여 리소스를 배포할 때 사용할 API의 버전을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-115">When you deploy resources using a template, you have to specify a version of the API to use.</span></span> <span data-ttu-id="1a1d9-116">예제에서는 이 apiVersion 요소를 사용하여 가상 컴퓨터 리소스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-116">The example shows the virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="1a1d9-117">템플릿에서 지정하는 API의 버전은 템플릿에서 정의할 수 있는 속성에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-117">The version of the API you specify in your template affects which properties you can define in the template.</span></span> <span data-ttu-id="1a1d9-118">일반적으로 템플릿을 만들 때 최신 버전의 API를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-118">In general, you should select the most recent API version when creating templates.</span></span> <span data-ttu-id="1a1d9-119">기존 템플릿의 경우 이전 API 버전을 계속 사용할지 아니면 새 기능을 이용하도록 최신 버전에 맞게 템플릿을 업데이트할지 여하를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-119">For existing templates, you can decide whether you want to continue using an earlier API version, or update your template for the latest version to take advantage of new features.</span></span>

<span data-ttu-id="1a1d9-120">최신 API 버전을 가져오기 위해 이러한 기회를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-120">Use these opportunities for getting the latest API versions:</span></span>

- <span data-ttu-id="1a1d9-121">REST API - [모든 리소스 공급자 나열](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="1a1d9-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="1a1d9-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="1a1d9-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="1a1d9-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="1a1d9-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="1a1d9-124">매개 변수 및 변수</span><span class="sxs-lookup"><span data-stu-id="1a1d9-124">Parameters and variables</span></span>

<span data-ttu-id="1a1d9-125">[매개 변수](../../resource-group-authoring-templates.md)를 통해 실행할 때 템플릿에 대한 값을 손쉽게 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you to specify values for the template when you run it.</span></span> <span data-ttu-id="1a1d9-126">이 매개 변수 섹션은 예제에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-126">This parameters section is used in the example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="1a1d9-127">예제 템플릿을 배포할 때 각 VM에서 관리자 계정의 이름 및 암호에 대한 값과 만들 VM의 수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-127">When you deploy the example template, you enter values for the name and password of the administrator account on each VM and the number of VMs to create.</span></span> <span data-ttu-id="1a1d9-128">템플릿을 사용하여 관리되는 별도 파일에서 매개 변수 값을 지정하거나 메시지가 표시되면 값을 제공하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-128">You have the option of specifying parameter values in a separate file that's managed with the template, or providing values when prompted.</span></span>

<span data-ttu-id="1a1d9-129">[변수](../../resource-group-authoring-templates.md)를 통해 전체에 걸쳐 반복해서 사용되거나 시간에 따라 달라질 수 있는 템플릿의 값을 쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you to set up values in the template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="1a1d9-130">이 변수 섹션은 예제에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-130">This variables section is used in the example:</span></span>

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

<span data-ttu-id="1a1d9-131">예제 템플릿을 배포할 때 이전에 만든 저장소 계정의 이름 및 식별자에 대한 변수 값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-131">When you deploy the example template, variable values are used for the name and identifier of the previously created storage account.</span></span> <span data-ttu-id="1a1d9-132">변수는 진단 확장에 대한 설정을 제공하는 데에도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-132">Variables are also used to provide the settings for the diagnostic extension.</span></span> <span data-ttu-id="1a1d9-133">[Azure Resource Manager 템플릿 생성 모범 사례](../../resource-manager-template-best-practices.md)를 사용하여 템플릿에서 매개 변수 및 변수를 구성하는 방법을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-133">Use the [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) to help you decide how you want to structure the parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="1a1d9-134">리소스 루프</span><span class="sxs-lookup"><span data-stu-id="1a1d9-134">Resource loops</span></span>

<span data-ttu-id="1a1d9-135">응용 프로그램에 하나 이상의 가상 컴퓨터가 필요할 때 템플릿에서 복사 요소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="1a1d9-136">이 선택적 요소는 매개 변수로 지정한 VM의 수 만들기를 통해 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-136">This optional element loops through creating the number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="1a1d9-137">또한 예제에서 루프 인덱스는 리소스에 대한 일부 값을 지정할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-137">Also, notice in the example that the loop index is used when specifying some of the values for the resource.</span></span> <span data-ttu-id="1a1d9-138">예를 들어 3의 인스턴스 수를 입력한 경우 운영 체제 디스크의 이름은 myOSDisk1, myOSDisk2 및 myOSDisk3입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-138">For example, if you entered an instance count of three, the names of the operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="1a1d9-139">이 예제에서는 가상 컴퓨터에 대해 Managed Disks를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-139">This example uses managed disks for the virtual machines.</span></span>
>
>

<span data-ttu-id="1a1d9-140">템플릿에서 한 리소스에 대한 루프 만들기는 다른 리소스를 만들거나 액세스할 때 루프를 사용해야 한다는 점을 염두에 두십시오.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-140">Keep in mind that creating a loop for one resource in the template may require you to use the loop when creating or accessing other resources.</span></span> <span data-ttu-id="1a1d9-141">예를 들어 여러 VM은 동일한 네트워크 인터페이스를 사용할 수 없으므로 템플릿이 세 개의 VM 만들기를 통해 반복하는 경우 세 개의 네트워크 인터페이스 만들기를 통해 반복해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-141">For example, multiple VMs can’t use the same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="1a1d9-142">VM에 네트워크 인터페이스를 할당할 때 루프 인덱스는 이를 식별하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-142">When assigning a network interface to a VM, the loop index is used to identify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="1a1d9-143">종속성</span><span class="sxs-lookup"><span data-stu-id="1a1d9-143">Dependencies</span></span>

<span data-ttu-id="1a1d9-144">대부분의 리소스는 제대로 작동하기 위해 다른 리소스에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-144">Most resources depend on other resources to work correctly.</span></span> <span data-ttu-id="1a1d9-145">가상 컴퓨터는 가상 네트워크와 연결되어야 하며 이를 수행하기 위해 네트워크 인터페이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-145">Virtual machines must be associated with a virtual network and to do that it needs a network interface.</span></span> <span data-ttu-id="1a1d9-146">[dependsOn](../../resource-group-define-dependencies.md) 요소는 VM이 생성되기 전에 네트워크 인터페이스가 사용될 준비가 되었는지 확인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-146">The [dependsOn](../../resource-group-define-dependencies.md) element is used to make sure that the network interface is ready to be used before the VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="1a1d9-147">리소스 관리자는 배포되는 다른 리소스에 종속되지 않는 모든 리소스를 동시에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="1a1d9-148">불필요한 종속성을 지정하여 실수로 배포 속도를 늦출 수 있으므로 종속성을 설정할 때 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="1a1d9-149">종속성은 여러 리소스를 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="1a1d9-150">예를 들어 네트워크 인터페이스는 공용 IP 주소 및 가상 네트워크 리소스에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-150">For example, the network interface depends on the public IP address and virtual network resources.</span></span>

<span data-ttu-id="1a1d9-151">종속성이 필수인지 어떻게 알 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="1a1d9-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="1a1d9-152">템플릿에서 설정한 값을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-152">Look at the values you set in the template.</span></span> <span data-ttu-id="1a1d9-153">가상 컴퓨터 리소스 정의의 요소가 동일한 템플릿에 배포된 다른 리소스를 가리키는 경우 종속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-153">If an element in the virtual machine resource definition points to another resource that is deployed in the same template, you need a dependency.</span></span> <span data-ttu-id="1a1d9-154">예를 들어 예제 가상 컴퓨터는 네트워크 프로필을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="1a1d9-155">이 속성을 설정하려면 네트워크 인터페이스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-155">To set this property, the network interface must exist.</span></span> <span data-ttu-id="1a1d9-156">따라서 종속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="1a1d9-157">또한 하나의 리소스(자식)가 다른 리소스(부모) 내에서 정의될 때에도 종속성을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-157">You also need to set a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="1a1d9-158">예를 들어 진단 설정 및 사용자 지정 스크립트 확장 모두는 가상 컴퓨터의 자식 리소스로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-158">For example, the diagnostic settings and custom script extensions are both defined as child resources of the virtual machine.</span></span> <span data-ttu-id="1a1d9-159">가상 컴퓨터가 있을 때까지 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-159">They cannot be created until the virtual machine exists.</span></span> <span data-ttu-id="1a1d9-160">따라서 두 리소스는 가상 컴퓨터에 따라 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-160">Therefore, both resources are marked as dependent on the virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="1a1d9-161">프로필</span><span class="sxs-lookup"><span data-stu-id="1a1d9-161">Profiles</span></span>

<span data-ttu-id="1a1d9-162">몇 가지 프로필 요소는 가상 컴퓨터 리소스를 정의할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="1a1d9-163">일부는 필요하고 일부는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-163">Some are required and some are optional.</span></span> <span data-ttu-id="1a1d9-164">예를 들어 hardwareProfile, osProfile, storageProfile 및 networkProfile 요소는 필요하지만 diagnosticsProfile은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-164">For example, the hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but the diagnosticsProfile is optional.</span></span> <span data-ttu-id="1a1d9-165">이러한 프로필은 다음과 같은 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="1a1d9-166">크기</span><span class="sxs-lookup"><span data-stu-id="1a1d9-166">size</span></span>](sizes.md)
- <span data-ttu-id="1a1d9-167">[이름](/architecture/best-practices/naming-conventions) 및 자격 증명</span><span class="sxs-lookup"><span data-stu-id="1a1d9-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="1a1d9-168">디스크 및 [운영 체제 설정](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="1a1d9-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="1a1d9-169">네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="1a1d9-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="1a1d9-170">부트 진단</span><span class="sxs-lookup"><span data-stu-id="1a1d9-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="1a1d9-171">디스크 및 이미지</span><span class="sxs-lookup"><span data-stu-id="1a1d9-171">Disks and images</span></span>
   
<span data-ttu-id="1a1d9-172">Azure에서 vhd 파일은 [디스크 또는 이미지](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1a1d9-173">vhd 파일에서 운영 체제가 특정 VM이 되도록 특수화된 경우 디스크를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-173">When the operating system in a vhd file is specialized to be a specific VM, it is referred to as a disk.</span></span> <span data-ttu-id="1a1d9-174">vhd 파일에서 운영 체제가 여러 VM을 만드는 데 사용되도록 일반화된 경우 이미지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-174">When the operating system in a vhd file is generalized to be used to create many VMs, it is referred to as an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="1a1d9-175">플랫폼 이미지에서 새 가상 컴퓨터 및 새 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="1a1d9-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="1a1d9-176">VM을 만들 때 사용할 운영 체제를 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-176">When you create a VM, you must decide what operating system to use.</span></span> <span data-ttu-id="1a1d9-177">imageReference 요소는 새 VM의 운영 체제를 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-177">The imageReference element is used to define the operating system of a new VM.</span></span> <span data-ttu-id="1a1d9-178">예제는 Windows Server 운영 체제에 대한 정의를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-178">The example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="1a1d9-179">Linux 운영 체제를 만들려는 경우 이 정의를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-179">If you want to create a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="1a1d9-180">운영 체제 디스크에 대한 구성 설정은 osDisk 요소와 함께 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-180">Configuration settings for the operating system disk are assigned with the osDisk element.</span></span> <span data-ttu-id="1a1d9-181">이 예제에서는 캐싱 모드가 **ReadWrite**로 설정된 새 관리되는 디스크를 정의하며 해당 디스크는 [플랫폼 이미지](cli-ps-findimage.md)에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-181">The example defines a new managed disk with the caching mode set to **ReadWrite** and that the disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="1a1d9-182">기존 Managed Disks에서 새 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="1a1d9-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="1a1d9-183">기존 디스크에서 가상 컴퓨터를 만들려는 경우 imageReference 및 osProfile 요소를 제거하고 이러한 디스크 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-183">If you want to create virtual machines from existing disks, remove the imageReference and the osProfile elements and define these disk settings:</span></span>

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

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="1a1d9-184">관리되는 이미지에서 새 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="1a1d9-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="1a1d9-185">관리되는 이미지에서 가상 컴퓨터를 만들려는 경우 imageReference 요소를 변경하고 다음과 같은 디스크 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-185">If you want to create a virtual machine from a managed image, change the imageReference element and define these disk settings:</span></span>

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

### <a name="attach-data-disks"></a><span data-ttu-id="1a1d9-186">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="1a1d9-186">Attach data disks</span></span>

<span data-ttu-id="1a1d9-187">필요에 따라 VM에 데이터 디스크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-187">You can optionally add data disks to the VMs.</span></span> <span data-ttu-id="1a1d9-188">[디스크 수](sizes.md)는 사용하는 운영 체제 디스크의 크기에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-188">The [number of disks](sizes.md) depends on the size of operating system disk that you use.</span></span> <span data-ttu-id="1a1d9-189">Standard_DS1_v2로 설정된 VM의 크기를 사용하면 추가될 수 있는 데이터 디스크의 최대 수는 2입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-189">With the size of the VMs set to Standard_DS1_v2, the maximum number of data disks that could be added to the them is two.</span></span> <span data-ttu-id="1a1d9-190">이 예제에서는 하나의 관리되는 데이터 디스크를 각 VM에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-190">In the example, one managed data disk is being added to each VM:</span></span>

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

## <a name="extensions"></a><span data-ttu-id="1a1d9-191">확장</span><span class="sxs-lookup"><span data-stu-id="1a1d9-191">Extensions</span></span>

<span data-ttu-id="1a1d9-192">[확장](extensions-features.md)은 별도 리소스이지만 VM에 밀접하게 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied to VMs.</span></span> <span data-ttu-id="1a1d9-193">확장은 VM의 자식 리소스 또는 별도 리소스로 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-193">Extensions can be added as a child resource of the VM or as a separate resource.</span></span> <span data-ttu-id="1a1d9-194">예제는 VM에 추가되고 있는 [진단 확장](extensions-diagnostics-template.md)을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-194">The example shows the [Diagnostics Extension](extensions-diagnostics-template.md) being added to the VMs:</span></span>

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

<span data-ttu-id="1a1d9-195">이 확장 리소스는 storageName 변수 및 진단 변수를 사용하여 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-195">This extension resource uses the storageName variable and the diagnostic variables to provide values.</span></span> <span data-ttu-id="1a1d9-196">이 확장에서 수집되는 데이터를 변경하려는 경우 wadperfcounters 변수에 더 많은 성능 카운터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-196">If you want to change the data that is collected by this extension, you can add more performance counters to the wadperfcounters variable.</span></span> <span data-ttu-id="1a1d9-197">VM 디스크가 저장되는 위치가 아닌 다른 저장소 계정에 진단 데이터를 넣도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-197">You could also choose to put the diagnostics data into a different storage account than where the VM disks are stored.</span></span>

<span data-ttu-id="1a1d9-198">VM에 설치할 수 있는 많은 확장이 있지만 가장 유용한 것은 [사용자 지정 스크립트 확장](extensions-customscript.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-198">There are many extensions that you can install on a VM, but the most useful is probably the [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="1a1d9-199">예제에서 start.ps1이라는 PowerShell 스크립트는 처음 시작할 때 각 VM에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-199">In the example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

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

<span data-ttu-id="1a1d9-200">start.ps1 스크립트는 여러 구성 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-200">The start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="1a1d9-201">예를 들어 예제에서 VM에 추가되는 데이터 디스크는 초기화되지 않습니다. 사용자 지정 스크립트를 사용하여 초기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-201">For example, the data disks that are added to the VMs in the example are not initialized; you can use a custom script to initialize them.</span></span> <span data-ttu-id="1a1d9-202">수행할 여러 시작 작업이 있는 경우 start.ps1 파일을 사용하여 Azure 저장소에서 다른 PowerShell 스크립트를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-202">If you have multiple startup tasks to do, you can use the start.ps1 file to call other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="1a1d9-203">예제에서는 PowerShell을 사용하지만 사용 중인 운영 체제에서 사용할 수 있는 모든 스크립팅 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-203">The example uses PowerShell, but you can use any scripting method that is available on the operating system that you are using.</span></span>

<span data-ttu-id="1a1d9-204">포털의 확장 설정에서 설치된 확장의 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-204">You can see the status of the installed extensions from the Extensions settings in the portal:</span></span>

![확장 상태 가져오기](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="1a1d9-206">**Get-AzureRmVMExtension** PowerShell 명령, **vm extension get** Azure CLI 2.0 명령 또는 **Get extension information** REST API를 사용하여 확장 정보를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-206">You can also get extension information by using the **Get-AzureRmVMExtension** PowerShell command, the **vm extension get** Azure CLI 2.0 command, or the **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="1a1d9-207">배포</span><span class="sxs-lookup"><span data-stu-id="1a1d9-207">Deployments</span></span>

<span data-ttu-id="1a1d9-208">템플릿을 배포하는 경우 Azure는 그룹으로 배포한 리소스를 추적하고 이 배포된 그룹에 이름을 자동으로 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-208">When you deploy a template, Azure tracks the resources that you deployed as a group and automatically assigns a name to this deployed group.</span></span> <span data-ttu-id="1a1d9-209">배포의 이름은 템플릿의 이름과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-209">The name of the deployment is the same as the name of the template.</span></span>

<span data-ttu-id="1a1d9-210">배포의 리소스 상태를 알고 싶은 경우 Azure Portal에서 리소스 그룹 블레이드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-210">If you are curious about the status of resources in the deployment, you can use the Resource Group blade in the Azure portal:</span></span>

![배포 정보 가져오기](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="1a1d9-212">리소스를 만들거나 기존 리소스를 업데이트하는 데 동일한 템플릿을 사용하는 것은 문제가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-212">It’s not a problem to use the same template to create resources or to update existing resources.</span></span> <span data-ttu-id="1a1d9-213">명령을 사용하여 템플릿을 배포할 때 사용하려는 [모드](../../resource-group-template-deploy.md)를 말할 수 있는 기회가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-213">When you use commands to deploy templates, you have the opportunity to say which [mode](../../resource-group-template-deploy.md) you want to use.</span></span> <span data-ttu-id="1a1d9-214">모드는 **전체** 또는 **증분** 중 하나로 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-214">The mode can be set to either **Complete** or **Incremental**.</span></span> <span data-ttu-id="1a1d9-215">기본 값은 증분 업데이트를 수행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-215">The default is to do incremental updates.</span></span> <span data-ttu-id="1a1d9-216">리소스를 실수로 삭제할 수 있으므로 **전체** 모드를 사용할 때 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-216">Be careful when using the **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="1a1d9-217">모드를 **전체**로 설정하면 리소스 관리자는 템플릿에 없는 리소스 그룹의 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-217">When you set the mode to **Complete**, Resource Manager deletes any resources in the resource group that are not in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a1d9-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1a1d9-218">Next Steps</span></span>

- <span data-ttu-id="1a1d9-219">[Azure Resource Manager 템플릿 작성](../../resource-group-authoring-templates.md)을 사용하여 고유의 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="1a1d9-220">[Resource Manager 템플릿을 사용하여 Windows 가상 컴퓨터 만들기](ps-template.md)를 사용하여 자신이 만든 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-220">Deploy the template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="1a1d9-221">[Azure PowerShell 모듈을 사용하여 Windows VM 만들기 및 관리](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 검토하여 만든 VM을 관리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1a1d9-221">Learn how to manage the VMs that you created by reviewing [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
