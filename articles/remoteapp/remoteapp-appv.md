---
title: "Azure RemoteApp을 사용 하 여 App-v aaaUsing 앱 | Microsoft Docs"
description: "자세한 내용은 방법 Azure RemoteApp에서 toouse App-v 응용 프로그램입니다."
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
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="1038d-103">Azure RemoteApp에서 App-V 앱 사용</span><span class="sxs-lookup"><span data-stu-id="1038d-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1038d-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1038d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1038d-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="1038d-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1038d-106">Azure RemoteApp 하이브리드 컬렉션에서 App-V 응용 프로그램을 사용할 수 있으며, 이때 도메인에 가입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1038d-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="1038d-107">시작 하기 전에 hello 최신 업데이트를 사용 하 여 있는지 tooinstall hello App-v 5.1 클라이언트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1038d-107">Before you get started, make sure tooinstall hello App-V 5.1 client with hello latest updates.</span></span> <span data-ttu-id="1038d-108">Toocreate 해야는 [사용자 지정 이미지](remoteapp-create-custom-image.md) hello App-v 클라이언트를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1038d-108">You will need toocreate a [custom image](remoteapp-create-custom-image.md) that includes hello App-V client.</span></span>  

<span data-ttu-id="1038d-109">쉽게 toouse는 Azure RemoteApp과 함께 기존 App-v 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="1038d-109">It’s easy toouse your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="1038d-110">하이브리드 컬렉션 액세스 tooyour 도메인 컨트롤러가 있는 Azure VNET에 배포 되 고 hello Vm이 도메인에 가입를 기존 app-v 인프라와 배포 메서드 tooeasyily 호스트 App-v 응용 프로그램에서 Azure RemoteApp을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1038d-110">Since a hybrid collection is deployed into an Azure VNET that has access tooyour domain controller and hello VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods tooeasyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="1038d-111">다음은 수의 현재 App-v 배포의 hello 형식을 기반으로 하는 몇 가지 고려 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1038d-111">Here are some considerations that you should be aware of based on hello type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="1038d-112">구성 옵션</span><span class="sxs-lookup"><span data-stu-id="1038d-112">Configuration options</span></span> |  | <span data-ttu-id="1038d-113">Positive</span><span class="sxs-lookup"><span data-stu-id="1038d-113">Positive</span></span> | <span data-ttu-id="1038d-114">Negative</span><span class="sxs-lookup"><span data-stu-id="1038d-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1038d-115">배달 방법</span><span class="sxs-lookup"><span data-stu-id="1038d-115">Delivery method</span></span> |<span data-ttu-id="1038d-116">스트리밍(주문형)</span><span class="sxs-lookup"><span data-stu-id="1038d-116">Streaming (on-demand)</span></span> |<span data-ttu-id="1038d-117">응용 프로그램은 항상 최신 버전과 새 hello</span><span class="sxs-lookup"><span data-stu-id="1038d-117">App is always hello latest and fresh</span></span> |<span data-ttu-id="1038d-118">첫 번째 대기 시간</span><span class="sxs-lookup"><span data-stu-id="1038d-118">First time latency</span></span> |
| <span data-ttu-id="1038d-119">탑재됨</span><span class="sxs-lookup"><span data-stu-id="1038d-119">Mounted</span></span> |<span data-ttu-id="1038d-120">가장 빠른; 앱은 이미 hello VM에</span><span class="sxs-lookup"><span data-stu-id="1038d-120">Fastest; app is already present on hello VM</span></span> |<span data-ttu-id="1038d-121">Bloat - 이미지 공간을 차지함(127 GB 한계)</span><span class="sxs-lookup"><span data-stu-id="1038d-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="1038d-122">앱 위치 저장소</span><span class="sxs-lookup"><span data-stu-id="1038d-122">App location storage</span></span> |<span data-ttu-id="1038d-123">공유 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="1038d-123">Shared content</span></span> |<span data-ttu-id="1038d-124">앱이 Azure RemoteApp 인스턴스의 메모리에서 실행됨</span><span class="sxs-lookup"><span data-stu-id="1038d-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="1038d-125">Hello 앱이 있는 메모리와 좋은 연결 toostreaming (파일) 서버 무시</span><span class="sxs-lookup"><span data-stu-id="1038d-125">Eats memory and good connection toostreaming (file) server where hello app resides</span></span> |
| <span data-ttu-id="1038d-126">디스크(캐시됨)</span><span class="sxs-lookup"><span data-stu-id="1038d-126">Disk (Cached)</span></span> |<span data-ttu-id="1038d-127">고속 실행.</span><span class="sxs-lookup"><span data-stu-id="1038d-127">Fast execution.</span></span> <span data-ttu-id="1038d-128">앱이 콘텐츠 원본의 가용성에 의존하지 않음</span><span class="sxs-lookup"><span data-stu-id="1038d-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="1038d-129">Bloat - 이미지 공간을 차지함(127 GB 한계)</span><span class="sxs-lookup"><span data-stu-id="1038d-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="1038d-130">대상 지정</span><span class="sxs-lookup"><span data-stu-id="1038d-130">Targeting</span></span> |<span data-ttu-id="1038d-131">사용자</span><span class="sxs-lookup"><span data-stu-id="1038d-131">User</span></span> |<span data-ttu-id="1038d-132">전체 독립 실행형 App-V 인프라가 필요함</span><span class="sxs-lookup"><span data-stu-id="1038d-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="1038d-133">글로벌(컴퓨터)</span><span class="sxs-lookup"><span data-stu-id="1038d-133">Global (machine)</span></span> |<span data-ttu-id="1038d-134">게시 서버를 사용하여 미리 게시 또는 대상 지정</span><span class="sxs-lookup"><span data-stu-id="1038d-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="1038d-135">원하는 tooupdate hello 앱 (거 대 한) 경우 tooupdate Azure 이미지를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1038d-135">Need tooupdate your Azure image if you want tooupdate hello app (huge).</span></span> <span data-ttu-id="1038d-136">이미지의 일부 공간을 차지합니다.</span><span class="sxs-lookup"><span data-stu-id="1038d-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="1038d-137">사용자 지정 이미지 및 하이브리드 컬렉션을 만든 후 응용 프로그램을 게시, 사용자 지정 및 tooany 장치 아무 곳 이나 배달 하는 Azure RemoteApp에서 호스트 하 여 기존 App-v 응용 프로그램을 이용 하세요.</span><span class="sxs-lookup"><span data-stu-id="1038d-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered tooany device anywhere.</span></span>

