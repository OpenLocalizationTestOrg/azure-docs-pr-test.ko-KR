---
title: "Azure RemoteApp에 대한 앱 요구 사항 | Microsoft Docs"
description: "Azure RemoteApp에서 사용할 앱에 대한 요구 사항에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 13d42df97ea2b090180f5865a4eac25945f9f34c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="app-requirements"></a><span data-ttu-id="ead77-103">앱 요구 사항</span><span class="sxs-lookup"><span data-stu-id="ead77-103">App requirements</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ead77-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ead77-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="ead77-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ead77-106">Azure RemoteApp은 Windows Server 2012 R2 이미지로 스트리밍 32비트 또는 64비트 Windows 기반 응용 프로그램을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-106">Azure RemoteApp supports streaming 32-bit or 64-bit Windows-based applications from a Windows Server 2012 R2 image.</span></span> <span data-ttu-id="ead77-107">대부분 기존 32비트 또는 64비트 Windows 기반 응용 프로그램은 Azure RemoteApp(원격 데스크톱 서비스 또는 이전의 터미널 서비스) 환경에서 "있는 그대로" 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-107">Most existing 32-bit or 64-bit Windows-based applications run "as is" in Azure RemoteApp (Remote Desktop Services or formerly known as Terminal Services) environment.</span></span> <span data-ttu-id="ead77-108">그러나 실행과 잘 실행되고 있는 것 사이에는 차이가 있습니다. 일부 응용 프로그램은 제대로 작동되고 잘 수행되고 있지만 일부는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-108">However, there is a difference between running and running well - some applications function correctly and perform well, while others do not.</span></span> <span data-ttu-id="ead77-109">다음 정보는 원격 데스크톱 서비스 환경에서의 응용 프로그램 개발 및 호환성을 위한 테스트에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-109">The following information provides guidance for developing applications in a Remote Desktop Services environment and testing to ensure compatibility.</span></span>

<span data-ttu-id="ead77-110">팁: Microsoft는 작동하는 앱의 예를 만들고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-110">Tip: We're working on creating some working examples of apps for you.</span></span> <span data-ttu-id="ead77-111">RemoteApp에서 Microsoft Access, QuickBooks 및 App-v를 사용하여 설명하는 새 항목을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-111">You'll see new topics that discuss using Microsoft Access, QuickBooks, and App-V in RemoteApp.</span></span>

## <a name="requirements"></a><span data-ttu-id="ead77-112">요구 사항</span><span class="sxs-lookup"><span data-stu-id="ead77-112">Requirements</span></span>
<span data-ttu-id="ead77-113">다음 세가지 요구 사항은, 따르는 경우, RemoteApp에서 응용 프로그램을 잘 실행되는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-113">These three requirements, if followed, help your application run well in RemoteApp:</span></span>

1. <span data-ttu-id="ead77-114">[Windows 데스크톱 앱에 대한 인증 요구 사항](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx)을 모두 충족하고 [원격 데스크톱 서비스 프로그래밍 지침](https://msdn.microsoft.com/library/aa383490.aspx)을 준수하는 응용 프로그램은 RemoteApp과 완전히 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-114">Applications that meet all [Certification requirements for Windows desktop apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) and adhere to [Remote Desktop Services programming guidelines](https://msdn.microsoft.com/library/aa383490.aspx) will have complete compatibility with RemoteApp.</span></span>
2. <span data-ttu-id="ead77-115">응용 프로그램은 손실 될 수 있는 이미지나 RemoteApp 인스턴스에 로컬로 데이터를 저장 해서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-115">Applications should never store data locally on the image or RemoteApp instances that can be lost.</span></span>  <span data-ttu-id="ead77-116">RemoteApp 컬렉션을 만든 후 인스턴스는 복제 및 상태 비저장 상태이며 응용 프로그램만을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-116">After you create a RemoteApp collection, the instances are cloned and are stateless and should only contain applications.</span></span> <span data-ttu-id="ead77-117">사용자의 프로필 내 또는 외부 소스에 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-117">Store data in an external source or within the user's profile.</span></span>
3. <span data-ttu-id="ead77-118">사용자 지정 이미지는 손실 될 수 있는 데이터를 포함하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-118">Custom images should never contain data that can be lost.</span></span>  

## <a name="testing-your-apps"></a><span data-ttu-id="ead77-119">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="ead77-119">Testing your apps</span></span>
<span data-ttu-id="ead77-120">응용 프로그램을 테스트하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-120">Use these steps to testing applications:</span></span>

1. <span data-ttu-id="ead77-121">Windows Server 2012 R2 및 응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="ead77-121">Install Windows Server 2012 R2 and your application</span></span>
2. <span data-ttu-id="ead77-122">원격 데스크톱 사용</span><span class="sxs-lookup"><span data-stu-id="ead77-122">Enable Remote Desktop</span></span>
3. <span data-ttu-id="ead77-123">원격 데스크톱 보안 그룹에 두 사용자 계정을 추가하는 사용자 A 및 사용자 B의 두 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-123">Create two user accounts, UserA and UserB, adding both user accounts to the Remote Desktop security group.</span></span>
4. <span data-ttu-id="ead77-124">응용 프로그램을 시작하는 동안 두 동시 RDS 세션을 PC에 설정하여 다중 세션 호환성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-124">Check multi-session compatibility by establishing two simultaneous RDS sessions to the PC while launching the application.</span></span>
5. <span data-ttu-id="ead77-125">앱 동작의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="ead77-125">Validate app behavior</span></span>

## <a name="application-development-guidelines"></a><span data-ttu-id="ead77-126">응용 프로그램 개발 지침</span><span class="sxs-lookup"><span data-stu-id="ead77-126">Application development guidelines</span></span>
<span data-ttu-id="ead77-127">RemoteApp용 응용 프로그램을 개발하기 위해 다음 지침을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-127">Use the following guidelines for developing applications for RemoteApp.</span></span>

### <a name="multiple-users"></a><span data-ttu-id="ead77-128">여러 사용자</span><span class="sxs-lookup"><span data-stu-id="ead77-128">Multiple users</span></span>
* <span data-ttu-id="ead77-129">[단일 사용자를 위한 응용 프로그램 ](https://msdn.microsoft.com/library/aa380661.aspx)을 설치하면 다중 사용자 환경에서 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-129">Installing an [application for a single user ](https://msdn.microsoft.com/library/aa380661.aspx)can create problems in a multiuser environment.</span></span>
* <span data-ttu-id="ead77-130">응용 프로그램은 [사용자 관련 정보](https://msdn.microsoft.com/library/aa383452.aspx) 를 모든 사용자에게 적용되는 전역 정보와 별도로 개별적으로 사용자 고유의 위치에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-130">Applications should [store user-specific information](https://msdn.microsoft.com/library/aa383452.aspx) in user-specific locations, separately from global information that applies to all users.</span></span>
* <span data-ttu-id="ead77-131">RemoteApp은 여러 개의 [커널 개체의 네임스페이스](https://msdn.microsoft.com/library/aa382954.aspx)를 사용하며, 전역 네임스페이스는 주로 클라이언트/서버 응용 프로그램의 서비스에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-131">RemoteApp uses multiple [namespaces for kernel objects](https://msdn.microsoft.com/library/aa382954.aspx); a global namespace is used primarily by services in client/server applications.</span></span>
* <span data-ttu-id="ead77-132">여러 사용자가 원격 데스크톱 세션 호스트(RD 세션 호스트) 서버에 동시에 로그인할 수 있기 때문에 컴퓨터에 할당된 컴퓨터 이름 또는 [IP 주소](https://msdn.microsoft.com/library/aa382942.aspx) 가 한 명의 사용자와 연결된다는 가정은 안전하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-132">It is not safe to assume that the computer name or the [IP address](https://msdn.microsoft.com/library/aa382942.aspx) assigned to the computer are associated with a single user because multiple users can be logged on simultaneously to a Remote Desktop Session Host (RD Session Host) server.</span></span>

### <a name="performance"></a><span data-ttu-id="ead77-133">성능</span><span class="sxs-lookup"><span data-stu-id="ead77-133">Performance</span></span>
* <span data-ttu-id="ead77-134">앱을 RemoteApp에 추가하기 전에 [그래픽 효과](https://msdn.microsoft.com/library/aa380822.aspx) 를 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-134">Disable [graphic effects](https://msdn.microsoft.com/library/aa380822.aspx) before you add your app to RemoteApp.</span></span>
* <span data-ttu-id="ead77-135">모든 사용자를 위해 CPU 가용성을 최대화하려면 [백그라운드 작업 ](https://msdn.microsoft.com/library/aa380665.aspx) 을 비활성화하거나 리소스를 많이 사용하지 않는 효율적인 백그라운드 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-135">To maximize CPU availability for all users, either disable [background tasks ](https://msdn.microsoft.com/library/aa380665.aspx) or create efficient background tasks that are not resource-intensive.</span></span>
* <span data-ttu-id="ead77-136">다중 사용자, 다중 프로세서 환경을 위해 응용 프로그램 [스레드 사용량](https://msdn.microsoft.com/library/aa383520.aspx) 을 조정하여 균형을 맞추어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-136">You should tune and balance application [thread usage](https://msdn.microsoft.com/library/aa383520.aspx) for a multiuser, multiprocessor environment.</span></span>
* <span data-ttu-id="ead77-137">성능을 최적화하려면 응용 프로그램이 클라이언트 세션에서 실행 중인지 [감지](https://msdn.microsoft.com/library/aa380798.aspx) 하도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ead77-137">To optimize performance, it is good practice for applications to [detect](https://msdn.microsoft.com/library/aa380798.aspx) whether they are running in a client session.</span></span>

