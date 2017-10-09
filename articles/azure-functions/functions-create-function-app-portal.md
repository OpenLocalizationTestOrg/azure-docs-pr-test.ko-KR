---
title: "hello Azure 포털에서에서 함수 앱 aaaCreate | Microsoft Docs"
description: "Azure 앱 서비스의 hello 포털에서 새 함수 응용 프로그램을 만듭니다."
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
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a><span data-ttu-id="15b88-103">Hello Azure 포털에서에서 함수 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="15b88-103">Create a function app from hello Azure portal</span></span>

<span data-ttu-id="15b88-104">Azure 기능 앱 hello Azure 앱 서비스 인프라를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-104">Azure Function Apps uses hello Azure App Service infrastructure.</span></span> <span data-ttu-id="15b88-105">이 항목에서는 toocreate hello Azure 포털에서에서 함수 앱.</span><span class="sxs-lookup"><span data-stu-id="15b88-105">This topic shows you how toocreate a function app in hello Azure portal.</span></span> <span data-ttu-id="15b88-106">함수 응용 프로그램은 개별 함수의 hello 실행을 호스팅하는 hello 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-106">A function app is hello container that hosts hello execution of individual functions.</span></span> <span data-ttu-id="15b88-107">Hello 호스팅 앱 서비스 계획에서에서 함수 응용 프로그램을 만들 때 함수 앱 응용 프로그램 서비스의 모든 hello 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-107">When you create a function app in hello App Service hosting plan, your function app can use all hello features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="15b88-108">함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="15b88-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="15b88-109">함수 앱을 만들 때 문자, 숫자 및 하이픈만 포함할 수 있는 유효한 **앱 이름**을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="15b88-110">밑줄(**_**)은 허용되는 문자가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="15b88-111">저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="15b88-112">저장소 계정 이름은 Azure 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="15b88-113">Hello 함수 앱을 만든 후에 하나 이상의 다른 언어에서는 개별 함수를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-113">After hello function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="15b88-114">함수를 만들 [hello 포털을 사용 하 여](functions-create-first-azure-function.md#create-function), [연속 배포](functions-continuous-deployment.md), 또는 [FTP로 업로드](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp)합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-114">Create functions [by using hello portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="15b88-115">서비스 계획</span><span class="sxs-lookup"><span data-stu-id="15b88-115">Service plans</span></span>

<span data-ttu-id="15b88-116">Azure Functions에는 소비 계획 및 App Service 계획이라는 두 가지 서비스 계획이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="15b88-117">hello 소비 계획 코드가 실행 되는 경우 필요한 toohandle 부하로 눈금 아웃 한 다음 눈금-코드 실행 중이지 않을 때 계산 능력을 자동으로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-117">hello Consumption plan automatically allocates compute power when your code is running, scales-out as necessary toohandle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="15b88-118">앱 서비스 계획 hello 함수 앱 서비스 앱 액세스 tooall hello 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-118">hello App Service plan gives your function app access tooall hello facilities of App Service.</span></span> <span data-ttu-id="15b88-119">함수 앱이 만들어지면 서비스 계획을 선택해야 하며 현재는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="15b88-120">자세한 내용은 [Azure Functions 호스팅 계획 선택](functions-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15b88-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="15b88-121">앱 서비스 계획에 toorun JavaScript 함수를 계획 하는 경우 더 적은 코어를 사용 하 여 계획을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-121">If you are planning toorun JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="15b88-122">자세한 내용은 참조 hello [함수에 대 한 JavaScript 참조](functions-reference-node.md#choose-single-core-app-service-plans)합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-122">For more information, see hello [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="15b88-123">저장소 계정 요구 사항</span><span class="sxs-lookup"><span data-stu-id="15b88-123">Storage account requirements</span></span>

<span data-ttu-id="15b88-124">앱 서비스에서 함수 응용 프로그램을 만들 때 만들거나 해야 Blob, 큐 및 테이블 저장소 지 원하는 tooa 범용 하는 Azure 저장소 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-124">When creating a function app in App Service, you must create or link tooa general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="15b88-125">내부적으로 함수는 트리거 관리 및 함수 실행 로깅 등의 작업을 위해 Storage를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="15b88-126">Blob 전용 저장소 계정, Azure Premium Storage 및 ZRS 복제를 포함한 범용 저장소 계정과 같은 일부 저장소 계정은 큐 및 테이블을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="15b88-127">이러한 계정은 함수 응용 프로그램을 만들 때의 저장소 계정 블레이드 hello에서에서 필터링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-127">These accounts are filtered out of from hello Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="15b88-128">Hello 소비 호스팅 계획을 사용할 경우 함수 코드와 바인딩 구성 파일 hello 주 저장소 계정에서 Azure 파일 저장소에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-128">When using hello Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in hello main storage account.</span></span> <span data-ttu-id="15b88-129">Hello 주 저장소 계정을 삭제 하면이 콘텐츠는 삭제 되 고 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-129">When you delete hello main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="15b88-130">저장소 계정 유형에 대 한 자세한 정보는 toolearn 참조 [hello Azure 저장소 서비스 소개](../storage/common/storage-introduction.md#introducing-the-azure-storage-services)합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-130">toolearn more about storage account types, see [Introducing hello Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="15b88-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="15b88-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



