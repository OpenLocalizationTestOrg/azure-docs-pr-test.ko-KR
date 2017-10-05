---
title: "템플릿을 사용하여 Azure IoT Hub 만들기(PowerShell) | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 PowerShell로 IoT Hub를 만드는 방법입니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: f83fac6cffc9e58582417324a4348ca3b6220f0c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="03940-103">Azure Resource Manager 템플릿을 사용하여 IoT Hub 만들기(PowerShell)</span><span class="sxs-lookup"><span data-stu-id="03940-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="03940-104">Azure 리소스 관리자를 사용하여 Azure IoT Hub를 프로그래밍 방식으로 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-104">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="03940-105">이 자습서에서는 Azure Resource Manager 템플릿을 사용하여 PowerShell로 IoT Hub를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03940-105">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="03940-106">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델, 즉 [Azure Resource Manager 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md) 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03940-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="03940-107">이 문서에서는 Azure Resource Manager 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="03940-108">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="03940-109">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="03940-109">An active Azure account.</span></span> <br/><span data-ttu-id="03940-110">계정이 없는 경우 몇 분 내에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03940-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="03940-111">[Azure PowerShell 1.0][lnk-powershell-install] 이상.</span><span class="sxs-lookup"><span data-stu-id="03940-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="03940-112">[Azure Resource Manager로 Azure PowerShell 사용][lnk-powershell-arm] 문서에 PowerShell 및 Azure Resource Manager 템플릿을 사용하여 Azure 리소스를 만드는 방법에 대한 자세한 내용이 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03940-112">The article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how to use PowerShell and Azure Resource Manager templates to create Azure resources.</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="03940-113">Azure 구독에 연결</span><span class="sxs-lookup"><span data-stu-id="03940-113">Connect to your Azure subscription</span></span>

<span data-ttu-id="03940-114">PowerShell 명령 프롬프트에서 다음 명령을 입력하여 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="03940-115">Azure 구독이 여러 개 있는 경우 Azure에 로그인하면 자격 증명과 연결된 모든 Azure 구독에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03940-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="03940-116">다음 명령을 사용하여 사용할 수 있는 Azure 구독을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="03940-117">다음 명령을 사용하여 IoT Hub를 만드는 명령을 실행하는 데 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="03940-118">이전 명령의 출력에서 구독 이름 또는 ID를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03940-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="03940-119">다음 명령을 사용하여 IoT Hub 및 현재 지원되는 API 버전을 배포할 수 있는 위치를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03940-119">You can use the following commands to discover where you can deploy an IoT hub and the currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="03940-120">IoT Hub가 지원되는 위치 중 하나에서 다음 명령을 사용하여 IoT Hub를 포함하는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03940-120">Create a resource group to contain your IoT hub using the following command in one of the supported locations for IoT Hub.</span></span> <span data-ttu-id="03940-121">이 예에서는 **MyIoTRG1**이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03940-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-to-create-an-iot-hub"></a><span data-ttu-id="03940-122">IoT hub를 만들 템플릿 제출</span><span class="sxs-lookup"><span data-stu-id="03940-122">Submit a template to create an IoT hub</span></span>

<span data-ttu-id="03940-123">JSON 템플릿을 사용하여 리소스 그룹에 IoT hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03940-123">Use a JSON template to create an IoT hub in your resource group.</span></span> <span data-ttu-id="03940-124">Azure Resource Manager 템플릿을 사용하여 기존 IoT Hub를 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03940-124">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="03940-125">텍스트 편집기에서 새로운 표준 IoT Hub를 만드는 다음 리소스 정의를 사용하여 **template.json**이라는 Azure Resource Manager 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03940-125">Use a text editor to create an Azure Resource Manager template called **template.json** with the following resource definition to create a new standard IoT hub.</span></span> <span data-ttu-id="03940-126">이 예에서는 **미국 동부** 지역에 IoT Hub를 추가하고 이벤트 허브와 호환되는 끝점에 두 개의 소비자 그룹(**cg1** 및 **cg2**)을 만들고 **2016-02-03** API 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-126">This example adds the IoT Hub in the **East US** region, creates two consumer groups (**cg1** and **cg2**) on the Event Hub-compatible endpoint, and uses the **2016-02-03** API version.</span></span> <span data-ttu-id="03940-127">또한 이 템플릿에서 매개 변수로 IoT Hub 이름 **hubName**을 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-127">This template also expects you to pass in the IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="03940-128">IoT Hub를 지원하는 현재 위치 목록에 대해서는 [Azure 상태][lnk-status]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03940-128">For the current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. <span data-ttu-id="03940-129">로컬 컴퓨터에 Azure Resource Manager 템플릿 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-129">Save the Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="03940-130">이 예제에서는 **c:\templates** 폴더에 저장하는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="03940-131">다음 명령을 실행하여 새 IoT Hub를 배포하고, 매개 변수로 IoT Hub 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-131">Run the following command to deploy your new IoT hub, passing the name of your IoT hub as a parameter.</span></span> <span data-ttu-id="03940-132">이 예제에서는 IoT Hub 이름이 `abcmyiothub`입니다.</span><span class="sxs-lookup"><span data-stu-id="03940-132">In this example, the name of the IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="03940-133">IoT Hub의 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-133">The name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="03940-134">앞에서 만든 IoT Hub의 키가 출력에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="03940-134">The output displays the keys for the IoT hub you created.</span></span>

5. <span data-ttu-id="03940-135">응용 프로그램이 새 IoT Hub에 추가되었는지 확인하려면 [Azure Portal][lnk-azure-portal]을 방문하여 리소스 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-135">To verify your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="03940-136">또는 **Get AzureRmResource** PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-136">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="03940-137">이 예제 응용 프로그램은 대금이 청구되는 S1 표준 IoT Hub를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="03940-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="03940-138">완료되면 [Azure Portal][lnk-azure-portal] 또는 **Remove-AzureRmResource** PowerShell cmdlet을 사용하여 IoT Hub를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03940-138">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03940-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03940-139">Next steps</span></span>

<span data-ttu-id="03940-140">Azure Resource Manager 템플릿을 사용하여 PowerShell에서 IoT Hub를 배포했으므로 구체적인 내용을 알아볼 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="03940-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want to explore further:</span></span>

* <span data-ttu-id="03940-141">[IoT Hub 리소스 공급자 REST API][lnk-rest-api]의 기능을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="03940-141">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="03940-142">Azure Resource Manager의 기능에 대해 자세히 알아보려면 [Azure Resource Manager 개요][lnk-azure-rm-overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03940-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="03940-143">IoT Hub를 개발하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03940-143">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="03940-144">[C SDK 소개][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="03940-144">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="03940-145">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="03940-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="03940-146">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03940-146">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="03940-147">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="03940-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
