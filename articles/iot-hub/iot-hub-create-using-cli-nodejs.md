---
title: "Azure CLI(azure.js)를 사용하여 IoT Hub 만들기 | Microsoft Docs"
description: "플랫폼 간 Azure CLI(azure.js)를 사용하여 Azure IoT hub를 만드는 방법"
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: 5e37c6c5e8625ce446ab203f19f9a8b2f1cd5a46
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-cli"></a><span data-ttu-id="49f1f-103">Azure CLI를 사용하여 IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="49f1f-103">Create an IoT hub using the Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="49f1f-104">소개</span><span class="sxs-lookup"><span data-stu-id="49f1f-104">Introduction</span></span>

<span data-ttu-id="49f1f-105">Azure CLI 2.0(azure.js)을 사용하여 Azure IoT Hub를 프로그래밍 방식으로 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-105">You can use Azure CLI (azure.js) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="49f1f-106">이 문서는 Azure CLI(azure.js)를 사용하여 IoT Hub를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-106">This article shows you how to use the Azure CLI (azure.js) to create an IoT hub.</span></span>

<span data-ttu-id="49f1f-107">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="49f1f-108">Azure CLI(azure.js) - 이 문서에 설명된 것처럼 클래식 및 리소스 관리 배포 모델용 CLI입니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-108">Azure CLI (azure.js) – the CLI for the classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="49f1f-109">[Azure CLI 2.0(az.py)](iot-hub-create-using-cli.md) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="49f1f-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - the next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="49f1f-110">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="49f1f-111">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="49f1f-111">An active Azure account.</span></span> <span data-ttu-id="49f1f-112">계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="49f1f-113">[Azure CLI 0.10.4][lnk-CLI-install] 이상</span><span class="sxs-lookup"><span data-stu-id="49f1f-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="49f1f-114">Azure CLI가 이미 설치된 경우 다음 명령을 사용하여 명령 프롬프트에서 현재 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-114">If you already have the Azure CLI installed, you can validate the current version at the command prompt with the following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="49f1f-115">Azure에는 리소스를 만들고 작업하는 [Azure Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="49f1f-116">Azure CLI는 Azure Resource Manager 모드여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-116">The Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="49f1f-117">Azure 계정 및 구독 설정</span><span class="sxs-lookup"><span data-stu-id="49f1f-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="49f1f-118">명령 프롬프트에서 다음 명령을 입력하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-118">At the command prompt, login by typing the following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="49f1f-119">제안된 웹 브라우저와 코드를 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-119">Use the suggested web browser and code to authenticate.</span></span>
1. <span data-ttu-id="49f1f-120">Azure 구독이 여러 개 있는 경우 Azure에 연결하면 자격 증명과 연결된 모든 Azure 구독에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-120">If you have multiple Azure subscriptions, connecting to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="49f1f-121">다음 명령을 사용하여 Azure 구독을 보고 기본적으로 사용되는 구독을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-121">You can view the Azure subscriptions, and identify which one is the default, using the command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="49f1f-122">나머지 명령을 실행할 구독 컨텍스트를 설정하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-122">To set the subscription context under which you want to run the rest of the commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="49f1f-123">리소스 그룹이 없으면 **exampleResourceGroup**이라는 이름의 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="49f1f-124">[Azure CLI를 사용하여 Azure 리소스 및 리소스 그룹 관리][lnk-CLI-arm] 문서는 Azure CLI를 사용하여 Azure 리소스를 관리하는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-124">The article [Use the Azure CLI to manage Azure resources and resource groups][lnk-CLI-arm] provides more information about how to use the Azure CLI to manage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="49f1f-125">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="49f1f-125">Create an IoT Hub</span></span>

<span data-ttu-id="49f1f-126">필수 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="49f1f-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="49f1f-127">**resource-group**:</span><span class="sxs-lookup"><span data-stu-id="49f1f-127">**resource-group**.</span></span> <span data-ttu-id="49f1f-128">리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-128">The resource group name.</span></span> <span data-ttu-id="49f1f-129">형식은 대/소문자를 구분하지 않는 영숫자, 밑줄 및 하이픈으로 구성되며, 길이는 1-64자입니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-129">The format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="49f1f-130">**이름**:</span><span class="sxs-lookup"><span data-stu-id="49f1f-130">**name**.</span></span> <span data-ttu-id="49f1f-131">만들려는 IoT Hub의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-131">The name of the IoT hub to be created.</span></span> <span data-ttu-id="49f1f-132">형식은 대/소문자를 구분하지 않는 영숫자, 밑줄 및 하이픈으로 구성되며, 길이는 3-50자입니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-132">The format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="49f1f-133">**location**:</span><span class="sxs-lookup"><span data-stu-id="49f1f-133">**location**.</span></span> <span data-ttu-id="49f1f-134">IoT Hub를 프로비전할 위치(Azure 지역/데이터 센터)입니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-134">The location (azure region/datacenter) to provision the IoT hub.</span></span>
* <span data-ttu-id="49f1f-135">**sku-name**:</span><span class="sxs-lookup"><span data-stu-id="49f1f-135">**sku-name**.</span></span> <span data-ttu-id="49f1f-136">sku 이름이며, [F1, S1, S2, S3] 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-136">The name of the sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="49f1f-137">최신 전체 목록은 IoT Hub 가격 책정 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49f1f-137">For the latest full list, refer to the pricing page for IoT Hub.</span></span>
* <span data-ttu-id="49f1f-138">**units**:</span><span class="sxs-lookup"><span data-stu-id="49f1f-138">**units**.</span></span> <span data-ttu-id="49f1f-139">프로비전된 단위의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-139">The number of provisioned units.</span></span> <span data-ttu-id="49f1f-140">범위: F1[1-1], S1, S2[1-200], S3[1-10].</span><span class="sxs-lookup"><span data-stu-id="49f1f-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="49f1f-141">IoT Hub 단위는 총 메시지 수와 연결하려는 장치 수를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-141">IoT Hub units are based on your total message count and the number of devices you want to connect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="49f1f-142">만들기에 사용할 수 있는 모든 매개 변수를 보려면 명령 프롬프트에서 help 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-142">To see all the parameters available for creation, you can use the help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="49f1f-143">간단한 예제: **exampleResourceGroup**이라는 리소스 그룹에 **exampleIoTHubName**이라는 IoT Hub를 만들려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-143">Quick example: To create an IoT Hub called **exampleIoTHubName** in the resource group **exampleResourceGroup**, run the following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="49f1f-144">이 Azure CLI 명령은 대금이 청구되는 S1 표준 IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="49f1f-145">다음 명령을 사용하여 IoT hub **exampleIoTHubName**을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49f1f-145">You can delete the IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="49f1f-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="49f1f-146">Next steps</span></span>

<span data-ttu-id="49f1f-147">IoT Hub를 개발하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49f1f-147">To learn more about developing for IoT Hub, see the following article:</span></span>

* <span data-ttu-id="49f1f-148">[IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="49f1f-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="49f1f-149">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49f1f-149">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="49f1f-150">[Azure Portal을 사용하여 IoT Hub 관리][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="49f1f-150">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
