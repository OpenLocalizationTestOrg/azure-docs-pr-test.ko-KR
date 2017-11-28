---
title: "다중 NIC이 있는 개인 VM 만들기 - Azure Resource Manager 템플릿 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 다중 NIC이 있는 개인 VM을 만듭니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 85bfa264c6cf2b0586816a47b3ab72f3aee8ec96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a><span data-ttu-id="b0d27-103">템플릿을 사용하여 다중 NIC이 있는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="b0d27-103">Create a VM with multiple NICs using a template</span></span>
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="b0d27-104">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="b0d27-105">이 문서에서는 Resource Manager 배포 모델 사용을 설명하며 Microsoft에서는 대부분의 새로운 배포에 대해 [클래식 배포 모델](virtual-network-deploy-multinic-classic-ps.md) 대신 이 모델을 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="b0d27-106">다음 단계에서는 WEB 서버에 *IaaSStory*라는 리소스 그룹을, DB 서버에 *IaaSStory-BackEnd*라는 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-106">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0d27-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b0d27-107">Prerequisites</span></span>
<span data-ttu-id="b0d27-108">DB 서버를 만들려면 먼저 이 시나리오에 필요한 모든 리소스로 *IaaSStory* 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-108">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="b0d27-109">이러한 리소스를 만들려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-109">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="b0d27-110">[템플릿 페이지](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-110">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="b0d27-111">템플릿 페이지에서 **Parent resource group(부모 리소스 그룹)** 오른쪽에 있는 **Azure에 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-111">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="b0d27-112">필요한 경우 매개 변수 값을 변경한 다음 Azure Preview 포털의 단계에 따라 리소스 그룹을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-112">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0d27-113">저장소 계정 이름이 고유한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-113">Make sure your storage account names are unique.</span></span> <span data-ttu-id="b0d27-114">Azure에서 중복된 저장소 계정 이름을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-114">You cannot have duplicate storage account names in Azure.</span></span>
> 

## <a name="understand-the-deployment-template"></a><span data-ttu-id="b0d27-115">배포 템플릿 이해</span><span class="sxs-lookup"><span data-stu-id="b0d27-115">Understand the deployment template</span></span>
<span data-ttu-id="b0d27-116">이 설명서와 함께 제공된 템플릿을 배포하기 전에 먼저 그 기능을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-116">Before you deploy the template provided with this documentation, make sure you understand what it does.</span></span> <span data-ttu-id="b0d27-117">다음 단계를 통해 이 템플릿에 대해 개략적으로 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-117">The following steps provide a good overview of the template:</span></span>

1. <span data-ttu-id="b0d27-118">[템플릿 페이지](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-118">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="b0d27-119">**azuredeploy.json** 을 클릭하여 템플릿 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-119">Click **azuredeploy.json** to open the template file.</span></span>
3. <span data-ttu-id="b0d27-120">아래에 *osType* 매개 변수가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-120">Notice the *osType* parameter listed below.</span></span> <span data-ttu-id="b0d27-121">이 매개 변수는 여러 운영 체제 관련 설정과 함께 데이터베이스 서버에 사용할 VM 이미지를 선택하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-121">This parameter is used to select what VM image to use for the database server, along with multiple operating system related settings.</span></span>

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS to use for VMs: Windows or Ubuntu."
      }
    },
    ```

4. <span data-ttu-id="b0d27-122">아래로 스크롤하여 변수 목록으로 이동한 후 아래에 나온 것처럼 **dbVMSetting** 변수의 정의를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-122">Scroll down to the list of variables, and check the definition for the **dbVMSetting** variables, listed below.</span></span> <span data-ttu-id="b0d27-123">이는 **dbVMSettings** 변수에 포함된 배열 요소 중 하나를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-123">It receives one of the array elements contained in the **dbVMSettings** variable.</span></span> <span data-ttu-id="b0d27-124">소프트웨어 개발 용어에 익숙한 작업자라면 **dbVMSettings** 변수를 해시 테이블 또는 사전으로 간주해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-124">If you are familiar with software development terminology, you can view the **dbVMSettings** variable as a hash table, or a dictionary.</span></span>

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. <span data-ttu-id="b0d27-125">백 엔드에서 SQL을 실행하는 Windows VM을 배포하기로 결정하는 경우,</span><span class="sxs-lookup"><span data-stu-id="b0d27-125">Suppose you decide to deploy Windows VMs running SQL in the back-end.</span></span> <span data-ttu-id="b0d27-126">**osType**의 값은 *Windows*이고, **dbVMSetting** 변수에는 다음과 같은 요소가 포함됩니다. 이 요소는 **dbVMSettings** 변수의 첫 번째 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-126">Then the value for **osType** would be *Windows*, and the **dbVMSetting** variable would contain the element listed below, which represents the first value in the **dbVMSettings** variable.</span></span>

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. <span data-ttu-id="b0d27-127">**vmSize**에는 값 *Standard_DS3*이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-127">Notice the **vmSize** contains the value *Standard_DS3*.</span></span> <span data-ttu-id="b0d27-128">특정 VM 크기만 여러 NIC를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-128">Only certain VM sizes allow for the use of multiple NICs.</span></span> <span data-ttu-id="b0d27-129">[Windows VM 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 및 [Linux VM 크기](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 문서에서 어떤 VM 크기가 여러 NIC를 지원하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-129">You can verify which VM sizes support multiple NICs by reading the [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span></span>

7. <span data-ttu-id="b0d27-130">아래로 스크롤하여 **resources** 로 이동한 후 첫 번째 요소를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-130">Scroll down to **resources** and notice the first element.</span></span> <span data-ttu-id="b0d27-131">여기에는 저장소 계정이 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-131">It describes a storage account.</span></span> <span data-ttu-id="b0d27-132">이 저장소 계정은 각 데이터베이스 VM에서 사용하는 데이터 디스크를 유지 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-132">This storage account will be used to maintain the data disks used by each database VM.</span></span> <span data-ttu-id="b0d27-133">이 시나리오의 각 데이터베이스 VM에는 일반 저장소에 OS 디스크가 있고 SSD(프리미엄) 저장소에 두 개의 데이터 디스크가 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span></span>

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. <span data-ttu-id="b0d27-134">아래에 나열된 다음 리소스로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-134">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="b0d27-135">이 리소스는 각 데이터베이스 VM에서 데이터베이스 액세스에 사용되는 NIC를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-135">This resource represents the NIC used for database access in each database VM.</span></span> <span data-ttu-id="b0d27-136">이 리소스에서는 **copy** 함수가 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-136">Notice the use of the **copy** function in this resource.</span></span> <span data-ttu-id="b0d27-137">템플릿을 사용하면 **dbCount** 매개 변수를 기반으로 원하는 수만큼 VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-137">The template allows you to deploy as many VMs as you want, based on the **dbCount** parameter.</span></span> <span data-ttu-id="b0d27-138">따라서 데이터베이스 액세스를 위해 VM당 하나씩, 같은 수량의 NIC를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-138">Therefore you need to create the same amount of NICs for database access, one for each VM.</span></span>

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. <span data-ttu-id="b0d27-139">아래에 나열된 다음 리소스로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-139">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="b0d27-140">이 리소스는 각 데이터베이스 VM에서 관리에 사용되는 NIC를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-140">This resource represents the NIC used for management in each database VM.</span></span> <span data-ttu-id="b0d27-141">각 데이터베이스 VM에 대해 이 NIC 중 하나가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-141">Once again, you need one of these NICs for each database VM.</span></span> <span data-ttu-id="b0d27-142">아래의 **networkSecurityGroup** 요소는 RDP/SSH 액세스 권한을 이 NIC에만 허용하는 NSG를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-142">Notice the **networkSecurityGroup** element, linking an NSG that allows access to RDP/SSH to this NIC only.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. <span data-ttu-id="b0d27-143">아래에 나열된 다음 리소스로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-143">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="b0d27-144">이 리소스는 모든 데이터베이스 VM이 공유할 가용성 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-144">This resource represents an availability set to be shared by all database VMs.</span></span> <span data-ttu-id="b0d27-145">이런 방식을 통해, 유지 관리 도중에 집합에서 하나 이상의 VM이 항상 실행되도록 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-145">That way, you guarantee that there will always be one VM in the set running during maintenance.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. <span data-ttu-id="b0d27-146">아래로 스크롤하여 다음 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-146">Scroll down to the next resource.</span></span> <span data-ttu-id="b0d27-147">이 리소스는 아래에 나열된 처음 몇 줄에서 볼 수 있듯이 데이터베이스 VM을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-147">This resource represents the database VMs, as seen in the first few lines listed below.</span></span> <span data-ttu-id="b0d27-148">여기서도 **copy** 함수가 사용되어 **dbCount** 매개 변수를 기반으로 여러 VM이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-148">Notice the use of the **copy** function again, ensuring that multiple VMs are created based on the **dbCount** parameter.</span></span> <span data-ttu-id="b0d27-149">**dependsOn** 컬렉션도 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-149">Also notice the **dependsOn** collection.</span></span> <span data-ttu-id="b0d27-150">여기에는 VM을 배포하기 전에 먼저 만들어야 하는 두 개의 NIC가 가용성 집합 및 저장소 계정과 함께 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-150">It lists two NICs being necessary to be created before the VM is deployed, along with the availability set, and the storage account.</span></span>

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. <span data-ttu-id="b0d27-151">VM 리소스에서 아래로 스크롤하여 다음과 같은 **networkProfile** 요소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-151">Scroll down in the VM resource to the **networkProfile** element, as listed below.</span></span> <span data-ttu-id="b0d27-152">각 VM의 참조가 되는 두 개의 NIC가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-152">Notice that there are two NICs being reference for each VM.</span></span> <span data-ttu-id="b0d27-153">단일 VM에 대해 여러 개의 NIC를 만들 때는 NIC 중 하나의 **primary** 속성을 *true*로, 나머지의 속성을 *false*로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-153">When you create multiple NICs for a VM, you must set the **primary** property of one of the NICs to *true*, and the rest to *false*.</span></span>

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-the-arm-template-by-using-click-to-deploy"></a><span data-ttu-id="b0d27-154">클릭하여 배포하는 방식으로 ARM 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="b0d27-154">Deploy the ARM template by using click to deploy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0d27-155">아래 지침을 따르기 전에 먼저 [필수 조건](#Pre-requisites) 단계를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-155">Make sure you follow the [pre-requisites](#Pre-requisites) steps before following the instructions below.</span></span>
> 

<span data-ttu-id="b0d27-156">공용 저장소에서 사용할 수 있는 샘플 템플릿은 위에 설명된 시나리오를 생성하는 데 사용된 기본값을 포함하는 매개 변수 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-156">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="b0d27-157">클릭하여 배포하는 방식으로 이 템플릿을 배포하려면 **백 엔드 리소스 그룹(설명서 참조)** 오른쪽의 [이 링크](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)에 따라 **Azure에 배포**를 클릭하고 필요한 경우 기본 매개 변수 값을 대체하고 포털의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-157">To deploy this template using click to deploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), to the right of **Backend resource group (see documentation)** click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

<span data-ttu-id="b0d27-158">아래 그림은 배포 후 새 리소스 그룹의 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-158">The figure below shows the contents of the new resource group, after deployment.</span></span>

![백 엔드 리소스 그룹](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="b0d27-160">PowerShell을 사용하여 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="b0d27-160">Deploy the template by using PowerShell</span></span>
<span data-ttu-id="b0d27-161">PowerShell을 사용하여 다운로드한 템플릿을 배포하려면 [PowerShell 설치 및 구성](/powershell/azure/overview) 문서에 나오는 단계를 완료한 후 다음 단계를 완료하여 PowerShell을 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-161">To deploy the template you downloaded by using PowerShell, install and configure PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azure/overview) article and then complete the following steps:</span></span>

<span data-ttu-id="b0d27-162">**`New-AzureRmResourceGroup`** cmdlet을 실행하고 템플릿을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-162">Run the **`New-AzureRmResourceGroup`** cmdlet to create a resource group using the template.</span></span>

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

<span data-ttu-id="b0d27-163">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="b0d27-163">Expected output:</span></span>

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="b0d27-164">Azure CLI를 사용하여 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="b0d27-164">Deploy the template by using the Azure CLI</span></span>
<span data-ttu-id="b0d27-165">Azure CLI를 사용하여 템플릿을 배포하려면 아래 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="b0d27-165">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="b0d27-166">Azure CLI를 처음 사용하는 경우 [Azure CLI 설치 및 구성](../cli-install-nodejs.md) 을 참조하고 Azure 계정 및 구독을 선택하는 부분까지 관련 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-166">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="b0d27-167">아래와 같이 **`azure config mode`** 명령을 실행하여 리소스 관리자 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-167">Run the **`azure config mode`** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="b0d27-168">예상 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-168">The expected output follows:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="b0d27-169">[매개 변수 파일](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json)을 열고 해당 내용을 선택한 후 컴퓨터의 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-169">Open the [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it to a file in your computer.</span></span> <span data-ttu-id="b0d27-170">이 예에서는 매개 변수 파일을 *parameters.json*에 저장했습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-170">For this example, we saved the parameters file to *parameters.json*.</span></span>
4. <span data-ttu-id="b0d27-171">**`azure group deployment create`** cmdlet을 실행하여 위에서 다운로드하고 수정한 템플릿 및 매개 변수 파일을 사용해 새 VNet을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-171">Run the **`azure group deployment create`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="b0d27-172">출력 다음에 표시되는 목록은 사용되는 매개 변수를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d27-172">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    <span data-ttu-id="b0d27-173">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="b0d27-173">Expected output:</span></span>
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

