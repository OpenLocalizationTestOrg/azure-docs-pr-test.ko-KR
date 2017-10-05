---
title: "RemoteApp VNET에서 Azure VNET으로 마이그레이션하는 방법 | Microsoft 문서"
description: "VNET RemoteApp에서 Azure VNET으로 마이그레이션하는 방법을 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 10b5f4844a38fe97852dee8634e8cf54f1a23a1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-a-hybrid-collection-from-a-remoteapp-vnet-to-an-azure-vnet"></a><span data-ttu-id="3f9d3-103">RemoteApp VNET에서 Azure VNET으로 하이브리드 컬렉션을 마이그레이션하는 방법</span><span class="sxs-lookup"><span data-stu-id="3f9d3-103">How to migrate a hybrid collection from a RemoteApp VNET to an Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3f9d3-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3f9d3-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3f9d3-106">기쁘게도</span><span class="sxs-lookup"><span data-stu-id="3f9d3-106">Good news!</span></span> <span data-ttu-id="3f9d3-107">RemoteApp별 VNET(가상 네트워크)을 만드는 대신 기존 Azure VNET에 하이브리드 RemoteApp 컬렉션을 직접 배포하도록 허용했습니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-107">We have enabled you to deploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="3f9d3-108">이렇게 하면 최신 VNET 기능(예: Express 경로)을 활용하고 하이브리드 컬렉션에서 해당 VNET에 배포된 다른 Azure 서비스 및 가상 컴퓨터에 네트워크로 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-108">This lets you take advantage of the latest VNET features (like ExpressRoute) and give your hybrid collections direct network access to other Azure services and virtual machines deployed to that VNET.</span></span>  <span data-ttu-id="3f9d3-109">따라서 VNET 간 구성보다 성능이 더 우수하고 더 쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="3f9d3-110">*OriginalCollection*이라는 하이브리드 RemoteApp 컬렉션과 *RemoteAppVNET*이라는 RemoteApp VNET을 이미 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="3f9d3-111">이 컬렉션을 *AzureVNET*이라는 새 Azure VNET에 마이그레이션하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-111">Here are the steps to migrate it to a new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="3f9d3-112">[관리 포털](http://manage.windowsazure.com/)의 **네트워크** 탭에서 *AzureVNET* 서브넷 중 하나 이상에 대해 *RemoteAppVNET*에 사용한 것과 동일한 위치, DNS 구성 및 주소 공간을 사용하여 *AzureVNET*이라는 VNET을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-112">On the **Networks** tab in the [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using the same location, DNS configuration, and address space (for at least one of the *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="3f9d3-113">*OriginalCollection* 도메인에 가입된 Active Directory 배포에 대한 네트워크 연결을 호스팅하거나 설정하도록 *AzureVNET*을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-113">Configure *AzureVNET* to either host or have network connectivity to the Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="3f9d3-114">**RemoteApps** 탭에서 *New Collection*이라는 새 RemoteApp 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-114">On the **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="3f9d3-115">이때 **빨리 만들기** 대신 **VNET으로 만들기** 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-115">(Use the **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="3f9d3-116">*AzureVNET*의 서브넷에 배포하도록 *NewCollection*을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-116">Configure *NewCollection* to be deployed to a subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="3f9d3-117">*OriginalCollection*에 사용한 것과 동일한 이미지와 도메인 가입 정보를 사용하도록 *NewCollection*을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-117">Configure *NewCollection* to use the same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="3f9d3-118">몇 시간 후 *NewCollection* 이 컬렉션 목록에 활성 상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="3f9d3-119">이제 원본 컬렉션에서 새 컬렉션으로 사용자 정보를 마이그레이션할 필요가 없는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-119">Now, if you DON’T need to migrate any user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="3f9d3-120">*OriginalCollection*을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="3f9d3-121">*RemoteAppVNET*을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="3f9d3-122">완료되었습니다!</span><span class="sxs-lookup"><span data-stu-id="3f9d3-122">And, you’re done!</span></span>

<span data-ttu-id="3f9d3-123">또는 원본 컬렉션에서 새 컬렉션으로 사용자 정보를 마이그레이션해야 하는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-123">Alternately, if you DO need to migrate user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="3f9d3-124">Azure 구독 ID, 원본 컬렉션 이름, 새 컬렉션 이름을 사용하여 [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) 에 메일을 보내서, 사용자 정보를 마이그레이션하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-124">Send an email to [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, the name of your original collection, and the name of your new collection, and ask them to migrate your user information.</span></span>
2. <span data-ttu-id="3f9d3-125">업무일 기준 2일 이내에 RemoteApp 팀사용자 액세스 목록과 모든 사용자 문서 및 사용자 설정을 원본 컬렉션에서 새 컬렉션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-125">Within 2 business days the RemoteApp team will move the user access list and all user documents and user settings from the original collection to the new collection.</span></span>
3. <span data-ttu-id="3f9d3-126">*OriginalCollection*을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="3f9d3-127">*RemoteAppVNET*을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="3f9d3-128">완료되었습니다!</span><span class="sxs-lookup"><span data-stu-id="3f9d3-128">And now, you’re done!</span></span>

<span data-ttu-id="3f9d3-129">궁금한 사항이 있거나 특별한 지원이 필요한 경우 [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help)이라는 RemoteApp VNET을 이미 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f9d3-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

