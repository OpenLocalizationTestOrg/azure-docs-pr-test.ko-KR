---
title: "Azure Functions 런타임 개요 | Microsoft Docs"
description: "Azure Functions 런타임 미리 보기 개요"
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
ms.openlocfilehash: cb98d5f2aaa526555820c15ba5a32fb7e78ffc5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="eb628-103">Azure Functions 런타임 개요</span><span class="sxs-lookup"><span data-stu-id="eb628-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="eb628-104">Azure Functions 런타임은Azure Functions 프로그래밍 모델 온-프레미스의 간편성 및 유연성을 활용하는 새로운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb628-104">The Azure Functions Runtime provides a new way for you to take advantage of the simplicity and flexibility of the Azure Functions programming model on-premises.</span></span> <span data-ttu-id="eb628-105">Azure Functions와 같은 오픈 소스 루트 기술을 기반으로 하는 Azure Functions 런타임은 온-프레미스에 배포되어 클라우드 서비스와 거의 동일한 개발 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb628-105">Built on the same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises to provide a nearly identical development experience as the cloud service.</span></span>

![Azure Functions 런타임 미리 보기 포털][1]

<span data-ttu-id="eb628-107">Azure Functions 런타임은 클라우드로 커밋하기 전에 Azure Functions를 사용해볼 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb628-107">The Azure Functions Runtime provides a way for you to experience Azure Functions before committing to the cloud.</span></span> <span data-ttu-id="eb628-108">이러한 방식으로 빌드하는 코드 자산을 마이그레이션 시 클라우드로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb628-108">In this way, the code assets you build can then be taken with you to the cloud when you migrate.</span></span>  <span data-ttu-id="eb628-109">또한 이 런타임은 온-프레미스 컴퓨터의 예비 Compute 능력을 사용하여 야간에 배치 프로세스를 실행하는 것과 같은 새로운 옵션을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb628-109">The runtime also opens up new options for you, such as using the spare compute power of your on-premises computers to run batch processes overnight.</span></span> <span data-ttu-id="eb628-110">조직 내에서 장치를 사용하여 온-프레미스 및 클라우드의 다른 시스템으로 조건에 따라 데이터를 전송할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb628-110">You can also use devices within your organization to conditionally send data to other systems, both on-premises and in the cloud.</span></span>

<span data-ttu-id="eb628-111">Azure Functions 런타임은 다음 두 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb628-111">The Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="eb628-112">Azure Functions 런타임 관리 역할</span><span class="sxs-lookup"><span data-stu-id="eb628-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="eb628-113">Azure Functions 런타임 작업자 역할</span><span class="sxs-lookup"><span data-stu-id="eb628-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="eb628-114">Azure Functions 관리 역할</span><span class="sxs-lookup"><span data-stu-id="eb628-114">Azure Functions Management Role</span></span>

<span data-ttu-id="eb628-115">Azure Functions 관리 역할은 온-프레미스에서 함수의 관리를 위한 호스트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb628-115">The Azure Functions Management Role provides a host for the management of your Functions on-premises.</span></span> <span data-ttu-id="eb628-116">이 역할은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="eb628-116">This role performs the following tasks:</span></span>

* <span data-ttu-id="eb628-117">Azure Functions 관리 포털 호스트([Azure Portal](https://portal.azure.com)에 표시되는 것과 동일함).</span><span class="sxs-lookup"><span data-stu-id="eb628-117">Hosting of the Azure Functions Management Portal, which is the the same one you see in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="eb628-118">따라서 Azure Portal에서와 같은 방식으로 함수를 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb628-118">This lets you develop your functions in the same way as you would in the Azure portal.</span></span>
* <span data-ttu-id="eb628-119">여러 함수 작업자 간에 함수 배포</span><span class="sxs-lookup"><span data-stu-id="eb628-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="eb628-120">Microsoft Visual Studio에서 직접 함수를 게시할 수 있도록 게시 끝점 제공</span><span class="sxs-lookup"><span data-stu-id="eb628-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="eb628-121">Azure Functions 작업자 역할</span><span class="sxs-lookup"><span data-stu-id="eb628-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="eb628-122">Azure Functions 작업자 역할은 Windows 컨테이너에 배포되며 여기서 함수 코드가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb628-122">The Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="eb628-123">조직 전체에서 여러 작업자 역할을 배포할 수 있으며 고객이 예비 Compute 능력을 활용할 수 있는 핵심 방법에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="eb628-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="eb628-124">최소 요구 사항</span><span class="sxs-lookup"><span data-stu-id="eb628-124">Minimum Requirements</span></span>

<span data-ttu-id="eb628-125">Azure Functions 런타임을 시작하려면 **SQL Server** 인스턴스에 대한 액세스 권한이 있는 **Windows Server 2016 또는 Windows 10 작성자 업데이트**가 있는 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eb628-125">To get started with the Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access to a **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb628-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb628-126">Next Steps</span></span>

<span data-ttu-id="eb628-127">[Azure Functions 런타임 미리 보기](https://aka.ms/azafr) 설치</span><span class="sxs-lookup"><span data-stu-id="eb628-127">Install the [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
