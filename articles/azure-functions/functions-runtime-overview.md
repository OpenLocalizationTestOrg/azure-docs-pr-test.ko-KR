---
title: "aaaAzure 함수 런타임 개요 | Microsoft Docs"
description: "Hello Azure 함수 런타임 미리 보기의 개요"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="a221d-103">Azure Functions 런타임 개요</span><span class="sxs-lookup"><span data-stu-id="a221d-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="a221d-104">hello Azure 함수 런타임은 새로운 방법을 제공 하면 tootake hello 단순성 및 활용할 hello Azure 함수의 유연성에 대 한 모델 온-프레미스를 프로그래밍 합니다.</span><span class="sxs-lookup"><span data-stu-id="a221d-104">hello Azure Functions Runtime provides a new way for you tootake advantage of hello simplicity and flexibility of hello Azure Functions programming model on-premises.</span></span> <span data-ttu-id="a221d-105">Hello 기반 동일 열기 소스 루트 Azure 함수, Azure 함수 런타임은 온-프레미스 배포 tooprovide 거의 동일한 개발 환경을 hello 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="a221d-105">Built on hello same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises tooprovide a nearly identical development experience as hello cloud service.</span></span>

![Azure Functions 런타임 미리 보기 포털][1]

<span data-ttu-id="a221d-107">hello Azure 함수 런타임 toohello 클라우드를 커밋하기 전에 tooexperience Azure 함수에 대 한 방식으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a221d-107">hello Azure Functions Runtime provides a way for you tooexperience Azure Functions before committing toohello cloud.</span></span> <span data-ttu-id="a221d-108">이러한 방식으로 작성 하는 hello 코드 자산 다음 가져올 수 있습니다 toohello 클라우드로 마이그레이션하는 경우.</span><span class="sxs-lookup"><span data-stu-id="a221d-108">In this way, hello code assets you build can then be taken with you toohello cloud when you migrate.</span></span>  <span data-ttu-id="a221d-109">내 온-프레미스 컴퓨터 toorun 일괄 처리 프로세스의 hello 예비 계산 능력을 사용 하는 등,에 대 한 새 옵션을 hello 런타임도 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a221d-109">hello runtime also opens up new options for you, such as using hello spare compute power of your on-premises computers toorun batch processes overnight.</span></span> <span data-ttu-id="a221d-110">조직 tooconditionally 송신 데이터 tooother 시스템을 온-프레미스 및 hello 클라우드에서 장치를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a221d-110">You can also use devices within your organization tooconditionally send data tooother systems, both on-premises and in hello cloud.</span></span>

<span data-ttu-id="a221d-111">hello Azure 함수 런타임 두 부분으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a221d-111">hello Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="a221d-112">Azure Functions 런타임 관리 역할</span><span class="sxs-lookup"><span data-stu-id="a221d-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="a221d-113">Azure Functions 런타임 작업자 역할</span><span class="sxs-lookup"><span data-stu-id="a221d-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="a221d-114">Azure Functions 관리 역할</span><span class="sxs-lookup"><span data-stu-id="a221d-114">Azure Functions Management Role</span></span>

<span data-ttu-id="a221d-115">hello Azure 함수 관리 역할 기능 온-프레미스의 hello 관리에 대 한 호스트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a221d-115">hello Azure Functions Management Role provides a host for hello management of your Functions on-premises.</span></span> <span data-ttu-id="a221d-116">이 역할 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a221d-116">This role performs hello following tasks:</span></span>

* <span data-ttu-id="a221d-117">Hello에 나와 있는 것 동일한 hello hello는 hello Azure 함수 관리 포털에서의 호스팅을 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="a221d-117">Hosting of hello Azure Functions Management Portal, which is hello hello same one you see in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a221d-118">함수를 개발이에서는 hello hello Azure 포털에서에서 사용 하는 방식으로 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="a221d-118">This lets you develop your functions in hello same way as you would in hello Azure portal.</span></span>
* <span data-ttu-id="a221d-119">여러 함수 작업자 간에 함수 배포</span><span class="sxs-lookup"><span data-stu-id="a221d-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="a221d-120">Microsoft Visual Studio에서 직접 함수를 게시할 수 있도록 게시 끝점 제공</span><span class="sxs-lookup"><span data-stu-id="a221d-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="a221d-121">Azure Functions 작업자 역할</span><span class="sxs-lookup"><span data-stu-id="a221d-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="a221d-122">Windows 컨테이너에서 hello Azure 함수 작업자 역할을 배포 하 고이 함수 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a221d-122">hello Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="a221d-123">조직 전체에서 여러 작업자 역할을 배포할 수 있으며 고객이 예비 Compute 능력을 활용할 수 있는 핵심 방법에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="a221d-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="a221d-124">최소 요구 사항</span><span class="sxs-lookup"><span data-stu-id="a221d-124">Minimum Requirements</span></span>

<span data-ttu-id="a221d-125">사용 하는 컴퓨터가 있어야 Azure 함수 런타임 hello로 시작 tooget **Windows Server 2016 또는 Windows 10 작성자가 업데이트** 액세스 tooa와 **SQL Server** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="a221d-125">tooget started with hello Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access tooa **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a221d-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a221d-126">Next Steps</span></span>

<span data-ttu-id="a221d-127">Hello 설치 [함수 런타임 Azure 미리 보기](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="a221d-127">Install hello [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
