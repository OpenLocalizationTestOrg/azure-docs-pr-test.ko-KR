---
title: "Azure Portal에서 함수 앱 만들기 | Microsoft Docs"
description: "포털의 Azure App Service에서 새 함수 앱을 만듭니다."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 85a88c537415cd6f2b6bc005cc18e3baaa29e9a4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-app-from-the-azure-portal"></a><span data-ttu-id="a8131-103">Azure Portal에서 함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="a8131-103">Create a function app from the Azure portal</span></span>

<span data-ttu-id="a8131-104">Azure Function 앱에서는 Azure App Service 인프라를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-104">Azure Function Apps uses the Azure App Service infrastructure.</span></span> <span data-ttu-id="a8131-105">이 항목에서는 Azure Portal에서 함수 앱을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-105">This topic shows you how to create a function app in the Azure portal.</span></span> <span data-ttu-id="a8131-106">함수 앱은 개별 함수의 실행을 호스팅하는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-106">A function app is the container that hosts the execution of individual functions.</span></span> <span data-ttu-id="a8131-107">App Service 호스팅 계획에서 함수 앱을 만들면 함수 앱에서는 모든 기능 및 App Service를 사용하여 App Service의 모든 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-107">When you create a function app in the App Service hosting plan, your function app can use all the features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="a8131-108">함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="a8131-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="a8131-109">함수 앱을 만들 때 문자, 숫자 및 하이픈만 포함할 수 있는 유효한 **앱 이름**을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="a8131-110">밑줄(**_**)은 허용되는 문자가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="a8131-111">저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="a8131-112">저장소 계정 이름은 Azure 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="a8131-113">함수 앱을 만든 후에 하나 이상의 서로 다른 언어로 개별 함수를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-113">After the function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="a8131-114">[포털을 사용하여](functions-create-first-azure-function.md#create-function), [연속 배포](functions-continuous-deployment.md) 또는 [FTP를 사용하여 업로드](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp)하여 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-114">Create functions [by using the portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="a8131-115">서비스 계획</span><span class="sxs-lookup"><span data-stu-id="a8131-115">Service plans</span></span>

<span data-ttu-id="a8131-116">Azure Functions에는 소비 계획 및 App Service 계획이라는 두 가지 서비스 계획이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="a8131-117">소비 계획은 코드가 실행 중일 때 계산 용량을 자동으로 할당하고, 로드를 처리하는 데 필요한 만큼 확장한 다음 코드가 실행되지 않을 때 축소합니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-117">The Consumption plan automatically allocates compute power when your code is running, scales-out as necessary to handle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="a8131-118">App Service 계획은 App Service의 모든 기능이 함수 앱 액세스 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-118">The App Service plan gives your function app access to all the facilities of App Service.</span></span> <span data-ttu-id="a8131-119">함수 앱이 만들어지면 서비스 계획을 선택해야 하며 현재는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="a8131-120">자세한 내용은 [Azure Functions 호스팅 계획 선택](functions-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8131-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="a8131-121">App Service 계획에서 JavaScript 함수를 실행하려는 경우 코어 수가 더 작은 계획을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-121">If you are planning to run JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="a8131-122">자세한 내용은 [함수에 대한 JavaScript 참조](functions-reference-node.md#choose-single-core-app-service-plans)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8131-122">For more information, see the [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="a8131-123">저장소 계정 요구 사항</span><span class="sxs-lookup"><span data-stu-id="a8131-123">Storage account requirements</span></span>

<span data-ttu-id="a8131-124">App Service에서 함수 앱을 만들 때 Blob, 큐 및 Table Storage를 지원하는 범용 Azure Storage 계정을 만들거나 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-124">When creating a function app in App Service, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="a8131-125">내부적으로 함수는 트리거 관리 및 함수 실행 로깅 등의 작업을 위해 Storage를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="a8131-126">Blob 전용 저장소 계정, Azure Premium Storage 및 ZRS 복제를 포함한 범용 저장소 계정과 같은 일부 저장소 계정은 큐 및 테이블을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="a8131-127">이러한 계정은 함수 앱을 만들 때 저장소 계정 블레이드에서 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-127">These accounts are filtered out of from the Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="a8131-128">소비 호스팅 계획을 사용할 경우 함수 코드 및 바인딩 구성 파일은 기본 저장소 계정의 Azure File Storage에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-128">When using the Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in the main storage account.</span></span> <span data-ttu-id="a8131-129">기본 저장소 계정을 삭제하면 이 콘텐츠는 삭제되고 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8131-129">When you delete the main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="a8131-130">저장소 계정 유형에 대해 자세히 알아보려면 [Azure Storage 서비스 소개](../storage/common/storage-introduction.md#introducing-the-azure-storage-services)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8131-130">To learn more about storage account types, see [Introducing the Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a8131-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a8131-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



