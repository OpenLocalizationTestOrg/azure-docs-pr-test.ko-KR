---
title: "Azure CLI (azure.js)를 사용 하 여 IoT hub aaaCreate | Microsoft Docs"
description: "어떻게 사용 하 여 Azure IoT 허브 toocreate hello 플랫폼 간 Azure CLI (azure.js)."
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
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a><span data-ttu-id="3e83e-103">Hello Azure CLI를 사용 하 여 IoT 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-103">Create an IoT hub using hello Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="3e83e-104">소개</span><span class="sxs-lookup"><span data-stu-id="3e83e-104">Introduction</span></span>

<span data-ttu-id="3e83e-105">Azure CLI (azure.js) toocreate를 사용 하 여 수 있으며, Azure IoT 허브를 프로그래밍 방식으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-105">You can use Azure CLI (azure.js) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="3e83e-106">이 문서에서는 어떻게 toouse hello Azure CLI (azure.js) toocreate IoT hub를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-106">This article shows you how toouse hello Azure CLI (azure.js) toocreate an IoT hub.</span></span>

<span data-ttu-id="3e83e-107">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="3e83e-108">Azure CLI (azure.js) – hello CLI 클래식 hello와이 문서에 설명 된 대로 리소스 관리 배포 모델에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-108">Azure CLI (azure.js) – hello CLI for hello classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="3e83e-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) -차세대 CLI hello 리소스 관리 배포 모델에 대 한 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - hello next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="3e83e-110">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="3e83e-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="3e83e-111">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="3e83e-111">An active Azure account.</span></span> <span data-ttu-id="3e83e-112">계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="3e83e-113">[Azure CLI 0.10.4][lnk-CLI-install] 이상</span><span class="sxs-lookup"><span data-stu-id="3e83e-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="3e83e-114">설치 된 Azure CLI hello 이미 있는 경우 다음 명령을 hello로 hello hello 명령 프롬프트에서 현재 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-114">If you already have hello Azure CLI installed, you can validate hello current version at hello command prompt with hello following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="3e83e-115">Azure에는 리소스를 만들고 작업하는 [Azure Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3e83e-116">hello Azure CLI Azure Resource Manager 모드에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-116">hello Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="3e83e-117">Azure 계정 및 구독 설정</span><span class="sxs-lookup"><span data-stu-id="3e83e-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="3e83e-118">Hello 명령 프롬프트에서 다음 명령을 hello를 입력 하 여 로그인:</span><span class="sxs-lookup"><span data-stu-id="3e83e-118">At hello command prompt, login by typing hello following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="3e83e-119">Hello 제안 된 웹 브라우저와 코드 tooauthenticate 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-119">Use hello suggested web browser and code tooauthenticate.</span></span>
1. <span data-ttu-id="3e83e-120">여러 Azure 구독이 있는 경우 tooAzure 연결 액세스 권한을 부여 tooall hello 자격 증명으로 연결 된 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="3e83e-120">If you have multiple Azure subscriptions, connecting tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="3e83e-121">볼 수 있습니다 hello Azure 구독 및 hello 명령을 사용 하 여 hello 기본적으로는 어떤 것을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-121">You can view hello Azure subscriptions, and identify which one is hello default, using hello command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="3e83e-122">tooset hello 구독 상황에 맞는 hello toorun hello 나머지 원하는 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-122">tooset hello subscription context under which you want toorun hello rest of hello commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="3e83e-123">리소스 그룹이 없으면 **exampleResourceGroup**이라는 이름의 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="3e83e-124">hello 문서 [hello Azure CLI toomanage Azure를 사용 하 여 리소스 및 리소스 그룹] [ lnk-CLI-arm] toouse Azure CLI toomanage Azure hello 하는 방법에 대 한 자세한 정보를 제공 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-124">hello article [Use hello Azure CLI toomanage Azure resources and resource groups][lnk-CLI-arm] provides more information about how toouse hello Azure CLI toomanage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="3e83e-125">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="3e83e-125">Create an IoT Hub</span></span>

<span data-ttu-id="3e83e-126">필수 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="3e83e-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="3e83e-127">**resource-group**:</span><span class="sxs-lookup"><span data-stu-id="3e83e-127">**resource-group**.</span></span> <span data-ttu-id="3e83e-128">hello 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-128">hello resource group name.</span></span> <span data-ttu-id="3e83e-129">hello 형식은 소문자 영숫자, 밑줄 및 하이픈, 1-64 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-129">hello format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="3e83e-130">**이름**.</span><span class="sxs-lookup"><span data-stu-id="3e83e-130">**name**.</span></span> <span data-ttu-id="3e83e-131">만든 hello IoT 허브 toobe의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-131">hello name of hello IoT hub toobe created.</span></span> <span data-ttu-id="3e83e-132">hello 형식은 소문자 영숫자, 밑줄 및 하이픈, 3-50 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-132">hello format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="3e83e-133">**location**:</span><span class="sxs-lookup"><span data-stu-id="3e83e-133">**location**.</span></span> <span data-ttu-id="3e83e-134">hello 위치 (azure 지역/데이터 센터) tooprovision hello IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-134">hello location (azure region/datacenter) tooprovision hello IoT hub.</span></span>
* <span data-ttu-id="3e83e-135">**sku-name**:</span><span class="sxs-lookup"><span data-stu-id="3e83e-135">**sku-name**.</span></span> <span data-ttu-id="3e83e-136">중 하나는 hello sku의 hello 이름: [F1, S1, S2, S3].</span><span class="sxs-lookup"><span data-stu-id="3e83e-136">hello name of hello sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="3e83e-137">최신 전체 목록을 hello toohello IoT 허브에 대 한 가격 책정 페이지를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3e83e-137">For hello latest full list, refer toohello pricing page for IoT Hub.</span></span>
* <span data-ttu-id="3e83e-138">**units**:</span><span class="sxs-lookup"><span data-stu-id="3e83e-138">**units**.</span></span> <span data-ttu-id="3e83e-139">hello 프로 비전 된 단위 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-139">hello number of provisioned units.</span></span> <span data-ttu-id="3e83e-140">범위: F1[1-1], S1, S2[1-200], S3[1-10].</span><span class="sxs-lookup"><span data-stu-id="3e83e-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="3e83e-141">IoT Hub 단위 기반 tooconnect 원하는 장치에 총 메시지 수와 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-141">IoT Hub units are based on your total message count and hello number of devices you want tooconnect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="3e83e-142">toosee 모든 hello 작성할 수 있는 매개 변수, 명령 프롬프트에서 hello 도움말 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-142">toosee all hello parameters available for creation, you can use hello help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="3e83e-143">간단한 예: IoT 허브 호출 toocreate **exampleIoTHubName** hello 리소스 그룹에 **exampleResourceGroup**실행 hello 다음 명령을:</span><span class="sxs-lookup"><span data-stu-id="3e83e-143">Quick example: toocreate an IoT Hub called **exampleIoTHubName** in hello resource group **exampleResourceGroup**, run hello following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="3e83e-144">이 Azure CLI 명령은 대금이 청구되는 S1 표준 IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e83e-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="3e83e-145">Hello IoT 허브를 삭제할 수 있습니다 **exampleIoTHubName** 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="3e83e-145">You can delete hello IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="3e83e-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e83e-146">Next steps</span></span>

<span data-ttu-id="3e83e-147">toolearn IoT 허브에 대 한 개발에 대 한 더 hello 다음 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3e83e-147">toolearn more about developing for IoT Hub, see hello following article:</span></span>

* <span data-ttu-id="3e83e-148">[IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="3e83e-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="3e83e-149">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3e83e-149">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3e83e-150">[Azure 포털 toomanage IoT Hub hello를 사용 하 여][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="3e83e-150">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
