---
title: "Azure Resource Manager 템플릿에서 관리 디스크 사용 | Microsoft Docs"
description: "Azure Resource Manager 템플릿에서 관리 디스크를 사용하는 방법에 대한 자세한 내용"
services: storage
documentationcenter: 
author: jboeshart
manager: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/01/2017
ms.author: jaboes
ms.openlocfilehash: 4c502784a57850d6f11200e95f7432d2206e920a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="5ea21-103">Azure Resource Manager 템플릿에서 Managed Disks 사용</span><span class="sxs-lookup"><span data-stu-id="5ea21-103">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="5ea21-104">이 문서는 가상 컴퓨터를 프로비전하는 데 Azure Resource Manager 템플릿을 사용할 때 관리 및 관리되지 않는 디스크 간의 차이점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-104">This document walks through the differences between managed and unmanaged disks when using Azure Resource Manager templates to provision virtual machines.</span></span> <span data-ttu-id="5ea21-105">따라서 관리되지 않는 디스크를 사용하는 기존 템플릿을 관리 디스크로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-105">This will help you to update existing templates that are using unmanaged Disks to managed disks.</span></span> <span data-ttu-id="5ea21-106">참조를 위해 [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) 템플릿을 가이드로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-106">For reference, we are using the [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="5ea21-107">직접 비교하려는 경우 [관리 디스크](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json)를 사용하는 것과 [관리되지 않는 디스크](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json)를 사용하는 이전 버전을 사용하는 템플릿을 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-107">You can see the template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like to directly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="5ea21-108">관리되지 않는 디스크 템플릿 서식 지정</span><span class="sxs-lookup"><span data-stu-id="5ea21-108">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="5ea21-109">관리되지 않는 디스크가 배포되는 방법을 살펴보는 것으로 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-109">To begin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="5ea21-110">관리되지 않는 디스크를 만들 경우 VHD 파일을 포함하는 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-110">When creating unmanaged disks, you need a storage account to hold the VHD files.</span></span> <span data-ttu-id="5ea21-111">새 저장소 계정을 만들거나 이미 있는 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-111">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="5ea21-112">이 문서는 새 저장소 계정을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-112">This article will show you how to create a new storage account.</span></span> <span data-ttu-id="5ea21-113">이렇게 하려면 아래 표시된 것처럼 리소스 블록에 저장소 계정 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-113">To accomplish this, you need a storage account resource in the resources block as shown below.</span></span>

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="5ea21-114">가상 컴퓨터 개체 내에서 계정이 가상 컴퓨터 이전에 생성되도록 저장소 계정에 대한 종속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-114">Within the virtual machine object, we need a dependency on the storage account to ensure that it's created before the virtual machine.</span></span> <span data-ttu-id="5ea21-115">`storageProfile` 섹션 내에서 저장소 계정을 참조하고 OS 디스크 및 모든 데이터 디스크에 필요한 VHD 위치의 전체 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-115">Within the `storageProfile` section, we then specify the full URI of the VHD location, which references the storage account and is needed for the OS disk and any data disks.</span></span> 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="5ea21-116">관리 디스크 템플릿 서식 지정</span><span class="sxs-lookup"><span data-stu-id="5ea21-116">Managed disks template formatting</span></span>

<span data-ttu-id="5ea21-117">Azure Managed Disks를 사용하면 디스크가 최상위 리소스가 되며 사용자가 더 이상 저장소 계정을 만들지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-117">With Azure Managed Disks, the disk becomes a top-level resource and no longer requires a storage account to be created by the user.</span></span> <span data-ttu-id="5ea21-118">`2016-04-30-preview` API 버전에서 처음 표시되었던 관리 디스크는 모든 후속 API 버전에서 제공되며 현재 기본 디스크 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-118">Managed disks were first exposed in the `2016-04-30-preview` API version, they are available in all subsequent API versions and are now the default disk type.</span></span> <span data-ttu-id="5ea21-119">다음 섹션에서는 기본 설정과 디스크를 추가로 사용자 지정하는 방법에 대한 정보를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-119">The following sections walk through the default settings and detail how to further customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="5ea21-120">`2016-04-30-preview`와 `2017-03-30` 간에는 중요한 변경 내용이 있으므로 `2016-04-30-preview` 이상의 API 버전을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-120">It is recommended to use an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="5ea21-121">기본 관리 디스크 설정</span><span class="sxs-lookup"><span data-stu-id="5ea21-121">Default managed disk settings</span></span>

<span data-ttu-id="5ea21-122">관리 디스크를 사용하여 VM을 만들기 위해 저장소 계정 리소스를 만들지 않아도 되며 다음과 같이 가상 컴퓨터 리소스를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-122">To create a VM with managed disks, you no longer need to create the storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="5ea21-123">특히 `apiVersion`은 `2017-03-30`를 반영하며 `osDisk` 및 `dataDisks`는 VHD에 대한 특정 URI를 더 이상 참조하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-123">Specifically note that the `apiVersion` reflects `2017-03-30` and the `osDisk` and `dataDisks` no longer refer to a specific URI for the VHD.</span></span> <span data-ttu-id="5ea21-124">추가 속성을 지정하지 않고 배포할 경우 디스크는 [표준 LRS 저장소](storage-redundancy.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-124">When deploying without specifying additional properties, the disk will use [Standard LRS storage](storage-redundancy.md).</span></span> <span data-ttu-id="5ea21-125">이름을 지정하지 않으면 OS 디스크에 대해 `<VMName>_OsDisk_1_<randomstring>` 형식을, 각 데이터 디스크에 대해 `<VMName>_disk<#>_<randomstring>`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-125">If no name is specified, it takes the format of `<VMName>_OsDisk_1_<randomstring>` for the OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="5ea21-126">기본적으로 Azure Disk Encryption은 사용하지 않으며 OS 디스크에 대한 캐싱은 읽기/쓰기이고 데이터 디스크에 대한 캐싱은 없음입니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-126">By default, Azure disk encryption is disabled; caching is Read/Write for the OS disk and None for data disks.</span></span> <span data-ttu-id="5ea21-127">아래 예에서 여전히 저장소 계정 종속성이 있음을 알 수 있습니다. 이는 진단 저장소에만 해당되며 디스크 저장소에는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-127">You may notice in the example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="5ea21-128">최상위 관리 디스크 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="5ea21-128">Using a top-level managed disk resource</span></span>

<span data-ttu-id="5ea21-129">가상 컴퓨터 개체에서 디스크 구성을 지정하는 대신, 최상위 디스크 리소스를 만들고 가상 컴퓨터 만들기의 일부로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-129">As an alternative to specifying the disk configuration in the virtual machine object, you can create a top-level disk resource and attach it as part of the virtual machine creation.</span></span> <span data-ttu-id="5ea21-130">예를 들어 다음과 같이 데이터 디스크로 사용할 디스크 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-130">For example, we can create a disk resource as follows to use as a data disk.</span></span>

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

<span data-ttu-id="5ea21-131">그런 다음 VM 개체 내에서 이 디스크 개체를 참조하여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-131">Within the VM object, we can then reference this disk object to be attached.</span></span> <span data-ttu-id="5ea21-132">`managedDisk` 속성에서 만든 관리 디스크의 리소스 ID를 지정하면 VM이 생성될 때 디스크를 첨부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-132">Specifying the resource ID of the managed disk we created in the `managedDisk` property allows the attachment of the disk as the VM is created.</span></span> <span data-ttu-id="5ea21-133">위 코드에서 VM 리소스의 `apiVersion`은 `2017-03-30`으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-133">Note that the `apiVersion` for the VM resource is set to `2017-03-30`.</span></span> <span data-ttu-id="5ea21-134">또한 VM이 만들어지기 전에 리소스가 만들어졌는지 확인하는 디스크 리소스에 대한 종속성도 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-134">Also note that we've created a dependency on the disk resource to ensure it's successfully created before VM creation.</span></span> 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="5ea21-135">관리 디스크를 사용하여 VM에서 관리 가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="5ea21-135">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="5ea21-136">관리 디스크를 사용하여 VM에서 관리 가용성 집합을 만들려면 `sku` 개체를 가용성 집합 리소스에 추가하고 `name` 속성을 `Aligned`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-136">To create managed availability sets with VMs using managed disks, add the `sku` object to the availability set resource and set the `name` property to `Aligned`.</span></span> <span data-ttu-id="5ea21-137">이렇게 하면 각 VM에 대한 디스크가 단일 실패 지점을 피할 만큼 서로 충분히 격리됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-137">This ensures that the disks for each VM are sufficiently isolated from each other to avoid single points of failure.</span></span> <span data-ttu-id="5ea21-138">또한 가용성 집합 리소스의 `apiVersion`도 `2017-03-30`으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-138">Also note that the `apiVersion` for the availability set resource is set to `2017-03-30`.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="5ea21-139">추가 시나리오 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="5ea21-139">Additional scenarios and customizations</span></span>

<span data-ttu-id="5ea21-140">REST API 사양에 대한 전체 정보를 찾으려면 [관리 디스크 REST API 설명서 만들기](/rest/api/manageddisks/disks/disks-create-or-update)를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="5ea21-140">To find full information on the REST API specifications, please review the [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="5ea21-141">추가 시나리오는 물론 템플릿 배포를 통해 API에 전송할 수 있는 허용되는 값 및 기본값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea21-141">You will find additional scenarios, as well as default and acceptable values that can be submitted to the API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5ea21-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ea21-142">Next steps</span></span>

* <span data-ttu-id="5ea21-143">관리 디스크를 사용하는 전체 템플릿은 다음 Azure 빠른 시작 리포지토리 링크를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="5ea21-143">For full templates that use managed disks visit the following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="5ea21-144">관리 디스크가 있는 Windows VM</span><span class="sxs-lookup"><span data-stu-id="5ea21-144">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="5ea21-145">관리 디스크가 있는 Linux VM</span><span class="sxs-lookup"><span data-stu-id="5ea21-145">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="5ea21-146">관리 디스크 템플릿의 전체 목록</span><span class="sxs-lookup"><span data-stu-id="5ea21-146">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="5ea21-147">관리 디스크에 대해 자세히 알아보려면 [Azure Managed Disks 개요](storage-managed-disks-overview.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ea21-147">Visit the [Azure Managed Disks Overview](storage-managed-disks-overview.md) document to learn more about managed disks.</span></span>
* <span data-ttu-id="5ea21-148">[Microsoft.Compute/virtualMachines 템플릿 참조](/templates/microsoft.compute/virtualmachines) 문서를 방문하여 가상 컴퓨터 리소스에 대한 템플릿 참조 설명서를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="5ea21-148">Review the template reference documentation for virtual machine resources by visiting the [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="5ea21-149">[Microsoft.Compute/disks 템플릿 참조](/templates/microsoft.compute/disks) 문서를 방문하여 디스크 리소스에 대한 템플릿 참조 설명서를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="5ea21-149">Review the template reference documentation for disk resources by visiting the [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
