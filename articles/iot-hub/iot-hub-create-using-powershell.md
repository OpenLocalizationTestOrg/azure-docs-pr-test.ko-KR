---
title: "PowerShell cmdlet을 사용하여 Azure IoT Hub 만들기 | Microsoft Docs"
description: "PowerShell cmdlet을 사용하여 IoT Hub를 만드는 방법입니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 02227adeb8a9a7463506efa44ddc2977f8aae65a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-new-azurermiothub-cmdlet"></a><span data-ttu-id="ec0b6-103">New-AzureRmIotHub cmdlet을 사용하여 IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="ec0b6-103">Create an IoT hub using the New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="ec0b6-104">소개</span><span class="sxs-lookup"><span data-stu-id="ec0b6-104">Introduction</span></span>

<span data-ttu-id="ec0b6-105">Azure PowerShell cmdlet을 사용하여 Azure IoT Hub를 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-105">You can use Azure PowerShell cmdlets to create and manage Azure IoT hubs.</span></span> <span data-ttu-id="ec0b6-106">이 자습서에서는 PowerShell로 IoT Hub를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-106">This tutorial shows you how to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="ec0b6-107">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델, 즉 [Azure Resource Manager 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md) 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ec0b6-108">이 문서에서는 Azure Resource Manager 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-108">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="ec0b6-109">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="ec0b6-110">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-110">An active Azure account.</span></span> <br/><span data-ttu-id="ec0b6-111">계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="ec0b6-112">[Azure PowerShell cmdlet][lnk-powershell-install]</span><span class="sxs-lookup"><span data-stu-id="ec0b6-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="ec0b6-113">Azure 구독에 연결</span><span class="sxs-lookup"><span data-stu-id="ec0b6-113">Connect to your Azure subscription</span></span>
<span data-ttu-id="ec0b6-114">PowerShell 명령 프롬프트에서 다음 명령을 입력하여 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="ec0b6-115">Azure 구독이 여러 개 있는 경우 Azure에 로그인하면 자격 증명과 연결된 모든 Azure 구독에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="ec0b6-116">다음 명령을 사용하여 사용할 수 있는 Azure 구독을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="ec0b6-117">다음 명령을 사용하여 IoT Hub를 만드는 명령을 실행하는 데 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="ec0b6-118">이전 명령의 출력에서 구독 이름 또는 ID를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="ec0b6-119">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ec0b6-119">Create resource group</span></span>

<span data-ttu-id="ec0b6-120">IoT Hub를 배포할 리소스 그룹이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-120">You need a resource group to deploy an IoT hub.</span></span> <span data-ttu-id="ec0b6-121">기존 리소스 그룹을 사용하거나 리소스 그룹을 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="ec0b6-122">다음 명령을 사용하여 IoT Hub를 배포할 수 있는 위치를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-122">You can use the following command to discover the locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="ec0b6-123">IoT Hub가 지원되는 위치 중 하나에서 IoT Hub에 대한 리소스 그룹을 만들려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-123">To create a resource group for your IoT hub in one of the supported locations for IoT Hub, use the following command.</span></span> <span data-ttu-id="ec0b6-124">이 예에서는 **미국 동부** 지역에 **MyIoTRG1**이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-124">This example creates a resource group called **MyIoTRG1** in the **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="ec0b6-125">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="ec0b6-125">Create an IoT hub</span></span>

<span data-ttu-id="ec0b6-126">이전 단계에서 만든 리소스 그룹에 IoT Hub를 만들려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-126">To create an IoT hub in the resource group you created in the previous step, use the following command.</span></span> <span data-ttu-id="ec0b6-127">이 예제에서는 **미국 동부** 지역에 **MyTestIoTHub**라는 **S1** 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-127">This example creates an **S1** hub called **MyTestIoTHub** in the **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="ec0b6-128">IoT Hub의 이름은 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-128">The name of the IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="ec0b6-129">다음 명령을 사용하여 구독에 있는 모든 IoT Hub를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-129">You can list all the IoT hubs in your subscription using the following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="ec0b6-130">이전 예제에서는 대금이 청구되는 S1 표준 IoT Hub를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-130">The previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="ec0b6-131">다음 명령을 사용하여 IoT Hub를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-131">You can delete the IoT hub using the following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="ec0b6-132">또는 다음 명령을 사용하여 리소스 그룹과 리소스 그룹이 포함된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-132">Alternatively, you can remove a resource group and all the resources it contains using the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="ec0b6-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec0b6-133">Next steps</span></span>

<span data-ttu-id="ec0b6-134">이제 PowerShell cmdlet을 사용하여 IoT Hub를 배포했으면 구체적인 내용을 알아볼 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want to explore further:</span></span>

* <span data-ttu-id="ec0b6-135">[IoT Hub로 작업하기 위한 다른 PowerShell cmdlet][lnk-iothub-cmdlets]을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="ec0b6-136">[IoT Hub 리소스 공급자 REST API][lnk-rest-api]의 기능을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-136">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="ec0b6-137">IoT Hub를 개발하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-137">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="ec0b6-138">[C SDK 소개][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="ec0b6-138">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="ec0b6-139">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="ec0b6-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="ec0b6-140">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec0b6-140">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ec0b6-141">[IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="ec0b6-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
