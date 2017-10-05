---
title: "Azure RemoteApp에서 App-V 앱 사용|Microsoft 문서"
description: "Azure RemoteApp에서 App-V 앱 사용 방법 배우기"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e55bb8db83c04025c46b383a9ebbef4399178116
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="fa1f9-103">Azure RemoteApp에서 App-V 앱 사용</span><span class="sxs-lookup"><span data-stu-id="fa1f9-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fa1f9-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fa1f9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="fa1f9-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="fa1f9-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="fa1f9-106">Azure RemoteApp 하이브리드 컬렉션에서 App-V 응용 프로그램을 사용할 수 있으며, 이때 도메인에 가입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa1f9-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="fa1f9-107">시작하기 전에 최신 업데이트를 통해 App-V 5.1 클라이언트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa1f9-107">Before you get started, make sure to install the App-V 5.1 client with the latest updates.</span></span> <span data-ttu-id="fa1f9-108">App-V 클라이언트가 포함된 [사용자 지정 이미지](remoteapp-create-custom-image.md) 를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa1f9-108">You will need to create a [custom image](remoteapp-create-custom-image.md) that includes the App-V client.</span></span>  

<span data-ttu-id="fa1f9-109">Azure RemoteApp를 통해 기존 App-V 인프라를 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa1f9-109">It’s easy to use your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="fa1f9-110">하이브리드 컬렉션은 도메인 컨트롤러에 대한 액세스 권한이 있는 Azure VNET에 배포되고 VM이 도메인에 가입되므로, 기존 App-V 인프라 및 배포 방법을 이용하여 Azure RemoteApp에서 App-V 응용 프로그램을 쉽게 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa1f9-110">Since a hybrid collection is deployed into an Azure VNET that has access to your domain controller and the VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods to easyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="fa1f9-111">다음은 현재 가지고 있는 App-V 배포 유형에 따라 알고 있어야 하는 몇 가지 고려사항입니다.</span><span class="sxs-lookup"><span data-stu-id="fa1f9-111">Here are some considerations that you should be aware of based on the type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="fa1f9-112">구성 옵션</span><span class="sxs-lookup"><span data-stu-id="fa1f9-112">Configuration options</span></span> |  | <span data-ttu-id="fa1f9-113">Positive</span><span class="sxs-lookup"><span data-stu-id="fa1f9-113">Positive</span></span> | <span data-ttu-id="fa1f9-114">Negative</span><span class="sxs-lookup"><span data-stu-id="fa1f9-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fa1f9-115">배달 방법</span><span class="sxs-lookup"><span data-stu-id="fa1f9-115">Delivery method</span></span> |<span data-ttu-id="fa1f9-116">스트리밍(주문형)</span><span class="sxs-lookup"><span data-stu-id="fa1f9-116">Streaming (on-demand)</span></span> |<span data-ttu-id="fa1f9-117">앱은 언제나 최신의 새 앱임</span><span class="sxs-lookup"><span data-stu-id="fa1f9-117">App is always the latest and fresh</span></span> |<span data-ttu-id="fa1f9-118">첫 번째 대기 시간</span><span class="sxs-lookup"><span data-stu-id="fa1f9-118">First time latency</span></span> |
| <span data-ttu-id="fa1f9-119">탑재됨</span><span class="sxs-lookup"><span data-stu-id="fa1f9-119">Mounted</span></span> |<span data-ttu-id="fa1f9-120">가장 빠름; 앱이 VM에 이미 있음</span><span class="sxs-lookup"><span data-stu-id="fa1f9-120">Fastest; app is already present on the VM</span></span> |<span data-ttu-id="fa1f9-121">Bloat - 이미지 공간을 차지함(127 GB 한계)</span><span class="sxs-lookup"><span data-stu-id="fa1f9-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="fa1f9-122">앱 위치 저장소</span><span class="sxs-lookup"><span data-stu-id="fa1f9-122">App location storage</span></span> |<span data-ttu-id="fa1f9-123">공유 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="fa1f9-123">Shared content</span></span> |<span data-ttu-id="fa1f9-124">앱이 Azure RemoteApp 인스턴스의 메모리에서 실행됨</span><span class="sxs-lookup"><span data-stu-id="fa1f9-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="fa1f9-125">앱이 상주하는 스트리밍(파일) 서버에 메모리 및 양호한 연결이 소비됨</span><span class="sxs-lookup"><span data-stu-id="fa1f9-125">Eats memory and good connection to streaming (file) server where the app resides</span></span> |
| <span data-ttu-id="fa1f9-126">디스크(캐시됨)</span><span class="sxs-lookup"><span data-stu-id="fa1f9-126">Disk (Cached)</span></span> |<span data-ttu-id="fa1f9-127">고속 실행.</span><span class="sxs-lookup"><span data-stu-id="fa1f9-127">Fast execution.</span></span> <span data-ttu-id="fa1f9-128">앱이 콘텐츠 원본의 가용성에 의존하지 않음</span><span class="sxs-lookup"><span data-stu-id="fa1f9-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="fa1f9-129">Bloat - 이미지 공간을 차지함(127 GB 한계)</span><span class="sxs-lookup"><span data-stu-id="fa1f9-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="fa1f9-130">대상 지정</span><span class="sxs-lookup"><span data-stu-id="fa1f9-130">Targeting</span></span> |<span data-ttu-id="fa1f9-131">사용자</span><span class="sxs-lookup"><span data-stu-id="fa1f9-131">User</span></span> |<span data-ttu-id="fa1f9-132">전체 독립 실행형 App-V 인프라가 필요함</span><span class="sxs-lookup"><span data-stu-id="fa1f9-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="fa1f9-133">글로벌(컴퓨터)</span><span class="sxs-lookup"><span data-stu-id="fa1f9-133">Global (machine)</span></span> |<span data-ttu-id="fa1f9-134">게시 서버를 사용하여 미리 게시 또는 대상 지정</span><span class="sxs-lookup"><span data-stu-id="fa1f9-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="fa1f9-135">앱(대용량)을 업데이트하려면 Azure 이미지를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa1f9-135">Need to update your Azure image if you want to update the app (huge).</span></span> <span data-ttu-id="fa1f9-136">이미지의 일부 공간을 차지합니다.</span><span class="sxs-lookup"><span data-stu-id="fa1f9-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="fa1f9-137">사용자 지정 이미지 및 하이브리드 컬렉션을 만든 후 응용 프로그램을 게시하고, 사용자를 할당하고, 어디서나 임의 장치에 배달된 Azure RemoteApp에서 호스팅되는 기존 App-V 응용 프로그램을 즐길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa1f9-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered to any device anywhere.</span></span>

