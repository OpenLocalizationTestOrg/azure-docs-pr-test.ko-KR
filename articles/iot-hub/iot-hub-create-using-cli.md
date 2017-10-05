---
title: "Azure CLI(az.py)를 사용하여 IoT Hub 만들기 | Microsoft Docs"
description: "플랫폼 간 Azure CLI 2.0(az.py)을 사용하여 Azure IoT hub를 만드는 방법"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 161089159999a4a63a39b059e69a08b7a9297445
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-cli-20"></a><span data-ttu-id="fb528-103">Azure CLI 2.0을 사용하여 IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="fb528-103">Create an IoT hub using the Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="fb528-104">소개</span><span class="sxs-lookup"><span data-stu-id="fb528-104">Introduction</span></span>

<span data-ttu-id="fb528-105">Azure CLI 2.0(az.py)을 사용하여 Azure IoT Hub를 프로그래밍 방식으로 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-105">You can use Azure CLI 2.0 (az.py) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="fb528-106">이 문서는 Azure CLI 2.0(az.py)을 사용하여 IoT Hub를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-106">This article shows you how to use the Azure CLI 2.0 (az.py) to create an IoT hub.</span></span>

<span data-ttu-id="fb528-107">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="fb528-108">[Azure CLI(azure.js)](iot-hub-create-using-cli-nodejs.md) - 클래식 및 리소스 관리 배포 모델용 CLI</span><span class="sxs-lookup"><span data-stu-id="fb528-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – the CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="fb528-109">Azure CLI 2.0(az.py) - 이 문서에 설명된 대로 리소스 관리 배포 모델용 차세대 CLI입니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-109">Azure CLI 2.0 (az.py) - the next generation CLI for the resource management deployment model as described in this article.</span></span>

<span data-ttu-id="fb528-110">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="fb528-111">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="fb528-111">An active Azure account.</span></span> <span data-ttu-id="fb528-112">계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="fb528-113">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="fb528-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="fb528-114">Azure 계정 로그인 및 설정</span><span class="sxs-lookup"><span data-stu-id="fb528-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="fb528-115">Azure 계정에 로그인하고 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="fb528-116">명령 프롬프트에서 [login 명령][lnk-login-command]을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-116">At the command prompt, run the [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="fb528-117">지침에 따라 코드를 사용하여 인증하고 웹 브라우저를 통해 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

2. <span data-ttu-id="fb528-118">여러 Azure 구독이 있는 경우 Azure에 로그인하면 자격 증명과 연결된 모든 Azure 계정에 대한 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="fb528-119">다음 [Azure 계정을 나열하는 명령][lnk-az-account-command]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="fb528-120">다음 명령을 사용하여 IoT Hub를 만드는 명령을 실행하는 데 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="fb528-121">이전 명령의 출력에서 구독 이름 또는 ID를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="fb528-122">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="fb528-122">Create an IoT Hub</span></span>

<span data-ttu-id="fb528-123">Azure CLI를 사용하여 리소스 그룹을 만든 다음 IoT Hub를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-123">Use the Azure CLI to create a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="fb528-124">IoT Hub는 리소스 그룹에서 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="fb528-125">기존 리소스 그룹을 사용하거나 다음 [리소스 그룹을 만드는 명령][lnk-az-resource-command]을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-125">Either use an existing resource group, or run the following [command to create a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="fb528-126">이전 예제에서는 미국 서부 위치에서 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-126">The previous example creates the resource group in the West US location.</span></span> <span data-ttu-id="fb528-127">`az account list-locations -o table` 명령을 실행하여 사용할 수 있는 위치의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-127">You can view a list of available locations by running the command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="fb528-128">리소스 그룹에서 IoT Hub에 대해 전역 고유 이름을 사용하여 다음 [IoT Hub를 만드는 명령][lnk-az-iot-command]을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-128">Run the following [command to create an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="fb528-129">이전 명령은 청구 대상인 S1 가격 책정 계층에 IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-129">The previous command creates an IoT hub in the S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="fb528-130">자세한 내용은 [Azure IoT Hub 가격 책정][lnk-iot-pricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb528-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="fb528-131">IoT Hub 제거</span><span class="sxs-lookup"><span data-stu-id="fb528-131">Remove an IoT Hub</span></span>

<span data-ttu-id="fb528-132">Azure CLI를 사용하여 IoT Hub 같은 [개별 리소스 삭제][lnk-az-resource-command] 또는 IoT Hub를 포함한 리소스 그룹 및 모든 해당 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-132">You can use the Azure CLI to [delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="fb528-133">IoT Hub를 삭제하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-133">To delete an IoT hub, run the following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="fb528-134">리소스 그룹 및 모든 해당 리소스를 삭제하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fb528-134">To delete a resource group and all its resources, run the following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="fb528-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fb528-135">Next steps</span></span>
<span data-ttu-id="fb528-136">IoT Hub를 개발하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb528-136">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="fb528-137">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="fb528-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="fb528-138">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb528-138">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="fb528-139">[Azure Portal을 사용하여 IoT Hub 관리][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="fb528-139">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
