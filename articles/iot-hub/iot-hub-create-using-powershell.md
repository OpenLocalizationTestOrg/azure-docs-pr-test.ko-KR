---
title: "PowerShell cmdlet을 사용 하 여 Azure IoT Hub aaaCreate | Microsoft Docs"
description: "어떻게 toouse PowerShell cmdlet toocreate IoT hub 합니다."
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
ms.openlocfilehash: 005cd8d48eb39d2e8b1bfb9ef84330d4aae4658f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a><span data-ttu-id="ef8de-103">새로 만들기-AzureRmIotHub hello cmdlet을 사용 하 여 IoT 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-103">Create an IoT hub using hello New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="ef8de-104">소개</span><span class="sxs-lookup"><span data-stu-id="ef8de-104">Introduction</span></span>

<span data-ttu-id="ef8de-105">Azure PowerShell cmdlet toocreate를 사용 하 고 Azure IoT hub를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-105">You can use Azure PowerShell cmdlets toocreate and manage Azure IoT hubs.</span></span> <span data-ttu-id="ef8de-106">이 자습서에서는 PowerShell과 함께 IoT hub toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-106">This tutorial shows you how toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="ef8de-107">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델, 즉 [Azure Resource Manager 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md) 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ef8de-108">이 문서에서는 hello Azure 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-108">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="ef8de-109">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="ef8de-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ef8de-110">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="ef8de-110">An active Azure account.</span></span> <br/><span data-ttu-id="ef8de-111">계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="ef8de-112">[Azure PowerShell cmdlet][lnk-powershell-install]</span><span class="sxs-lookup"><span data-stu-id="ef8de-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="ef8de-113">Tooyour Azure 구독 연결</span><span class="sxs-lookup"><span data-stu-id="ef8de-113">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="ef8de-114">PowerShell 명령 프롬프트에 hello 명령 toosign tooyour Azure 구독에서에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="ef8de-115">TooAzure 로그인 여러 Azure 구독이 있는 경우 tooall 액세스 부여 hello 자격 증명으로 연결 된 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="ef8de-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="ef8de-116">다음 명령을 toolist hello 있습니다 사용할 수 있는 Azure 구독 toouse hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="ef8de-117">다음 명령은 tooselect 구독 toouse toorun hello 명령을 toocreate IoT 허브를 지정 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="ef8de-118">Hello 이전 명령의 hello 출력에서 hello 구독 이름 또는 ID를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="ef8de-119">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ef8de-119">Create resource group</span></span>

<span data-ttu-id="ef8de-120">리소스 그룹 toodeploy IoT hub 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-120">You need a resource group toodeploy an IoT hub.</span></span> <span data-ttu-id="ef8de-121">기존 리소스 그룹을 사용하거나 리소스 그룹을 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="ef8de-122">다음 명령은 toodiscover hello 위치 IoT hub를 배포할 수 있는 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-122">You can use hello following command toodiscover hello locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="ef8de-123">IoT 허브를 hello 중 하나에 대 한 리소스 그룹 toocreate IoT 허브, 다음 명령을 사용 하 여 hello에 대 한 위치를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-123">toocreate a resource group for your IoT hub in one of hello supported locations for IoT Hub, use hello following command.</span></span> <span data-ttu-id="ef8de-124">이 예에서는 라는 리소스 그룹을 만든 **MyIoTRG1** hello에 **미국 동부** 영역:</span><span class="sxs-lookup"><span data-stu-id="ef8de-124">This example creates a resource group called **MyIoTRG1** in hello **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="ef8de-125">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="ef8de-125">Create an IoT hub</span></span>

<span data-ttu-id="ef8de-126">다음 명령을 사용 하 여 hello hello 이전 단계에서 만든 hello 리소스 그룹에서 IoT hub toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-126">toocreate an IoT hub in hello resource group you created in hello previous step, use hello following command.</span></span> <span data-ttu-id="ef8de-127">이 예제에서는 만듭니다는 **S1** 호출할 허브 **MyTestIoTHub** hello에 **미국 동부** 영역:</span><span class="sxs-lookup"><span data-stu-id="ef8de-127">This example creates an **S1** hub called **MyTestIoTHub** in hello **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="ef8de-128">hello IoT 허브의 hello 이름은 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-128">hello name of hello IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="ef8de-129">다음 명령을 hello를 사용 하 여 구독에서 모든 hello IoT 허브를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-129">You can list all hello IoT hubs in your subscription using hello following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="ef8de-130">청구는 S1 표준 IoT Hub를 추가 하는 hello 이전 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-130">hello previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="ef8de-131">다음 명령을 hello를 사용 하 여 hello IoT 허브를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-131">You can delete hello IoT hub using hello following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="ef8de-132">또는, 리소스 그룹을 제거할 수 있습니다 하 고 모든 hello hello 다음 명령을 사용 하 여 포함 된 리소스:</span><span class="sxs-lookup"><span data-stu-id="ef8de-132">Alternatively, you can remove a resource group and all hello resources it contains using hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="ef8de-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef8de-133">Next steps</span></span>

<span data-ttu-id="ef8de-134">이제 PowerShell cmdlet을 사용 하 여 IoT hub를 배포한 tooexplore 더 이상 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want tooexplore further:</span></span>

* <span data-ttu-id="ef8de-135">[IoT Hub로 작업하기 위한 다른 PowerShell cmdlet][lnk-iothub-cmdlets]을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="ef8de-136">Hello의 hello 기능에 대 한 읽기 [IoT 허브 리소스 공급자 REST API][lnk-rest-api]합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8de-136">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="ef8de-137">IoT 허브에 대 한 개발에 대 한 더 toolearn hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ef8de-137">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="ef8de-138">[소개 tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="ef8de-138">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="ef8de-139">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="ef8de-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="ef8de-140">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ef8de-140">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ef8de-141">[IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="ef8de-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
