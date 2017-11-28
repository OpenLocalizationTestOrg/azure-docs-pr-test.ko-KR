---
title: "Azure RemoteApp에 대 한 요구 사항 aaaApp | Microsoft Docs"
description: "Azure RemoteApp에서 toouse 원하는 앱에 대 한 hello 요구 사항 정보"
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
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a><span data-ttu-id="91ba6-103">앱 요구 사항</span><span class="sxs-lookup"><span data-stu-id="91ba6-103">App requirements</span></span>
> [!IMPORTANT]
> <span data-ttu-id="91ba6-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="91ba6-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="91ba6-106">Azure RemoteApp은 Windows Server 2012 R2 이미지로 스트리밍 32비트 또는 64비트 Windows 기반 응용 프로그램을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-106">Azure RemoteApp supports streaming 32-bit or 64-bit Windows-based applications from a Windows Server 2012 R2 image.</span></span> <span data-ttu-id="91ba6-107">대부분 기존 32비트 또는 64비트 Windows 기반 응용 프로그램은 Azure RemoteApp(원격 데스크톱 서비스 또는 이전의 터미널 서비스) 환경에서 "있는 그대로" 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-107">Most existing 32-bit or 64-bit Windows-based applications run "as is" in Azure RemoteApp (Remote Desktop Services or formerly known as Terminal Services) environment.</span></span> <span data-ttu-id="91ba6-108">그러나 실행과 잘 실행되고 있는 것 사이에는 차이가 있습니다. 일부 응용 프로그램은 제대로 작동되고 잘 수행되고 있지만 일부는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-108">However, there is a difference between running and running well - some applications function correctly and perform well, while others do not.</span></span> <span data-ttu-id="91ba6-109">다음 정보는 hello tooensure 호환성 테스트를 원격 데스크톱 서비스 환경에서 응용 프로그램을 개발 하기 위한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-109">hello following information provides guidance for developing applications in a Remote Desktop Services environment and testing tooensure compatibility.</span></span>

<span data-ttu-id="91ba6-110">팁: Microsoft는 작동하는 앱의 예를 만들고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-110">Tip: We're working on creating some working examples of apps for you.</span></span> <span data-ttu-id="91ba6-111">RemoteApp에서 Microsoft Access, QuickBooks 및 App-v를 사용하여 설명하는 새 항목을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-111">You'll see new topics that discuss using Microsoft Access, QuickBooks, and App-V in RemoteApp.</span></span>

## <a name="requirements"></a><span data-ttu-id="91ba6-112">요구 사항</span><span class="sxs-lookup"><span data-stu-id="91ba6-112">Requirements</span></span>
<span data-ttu-id="91ba6-113">다음 세가지 요구 사항은, 따르는 경우, RemoteApp에서 응용 프로그램을 잘 실행되는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-113">These three requirements, if followed, help your application run well in RemoteApp:</span></span>

1. <span data-ttu-id="91ba6-114">모두 충족 하는 응용 프로그램 [Windows 데스크톱 앱에 대 한 인증 요구 사항을](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) 너무 준수[프로그래밍 지침 원격 데스크톱 서비스](https://msdn.microsoft.com/library/aa383490.aspx) 완전 한 호환성 RemoteApp 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-114">Applications that meet all [Certification requirements for Windows desktop apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) and adhere too[Remote Desktop Services programming guidelines](https://msdn.microsoft.com/library/aa383490.aspx) will have complete compatibility with RemoteApp.</span></span>
2. <span data-ttu-id="91ba6-115">응용 프로그램 hello 이미지 또는 손실 될 수 있는 RemoteApp 인스턴스에서 로컬로 데이터를 저장 하지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-115">Applications should never store data locally on hello image or RemoteApp instances that can be lost.</span></span>  <span data-ttu-id="91ba6-116">RemoteApp 컬렉션을 만든 후 hello 인스턴스는 복제 하 고는 상태 비저장 및 응용 프로그램 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-116">After you create a RemoteApp collection, hello instances are cloned and are stateless and should only contain applications.</span></span> <span data-ttu-id="91ba6-117">Hello 사용자의 프로필 내에서 또는 외부 소스에서 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-117">Store data in an external source or within hello user's profile.</span></span>
3. <span data-ttu-id="91ba6-118">사용자 지정 이미지는 손실 될 수 있는 데이터를 포함하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-118">Custom images should never contain data that can be lost.</span></span>  

## <a name="testing-your-apps"></a><span data-ttu-id="91ba6-119">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="91ba6-119">Testing your apps</span></span>
<span data-ttu-id="91ba6-120">이러한 단계 tootesting 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-120">Use these steps tootesting applications:</span></span>

1. <span data-ttu-id="91ba6-121">Windows Server 2012 R2 및 응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="91ba6-121">Install Windows Server 2012 R2 and your application</span></span>
2. <span data-ttu-id="91ba6-122">원격 데스크톱 사용</span><span class="sxs-lookup"><span data-stu-id="91ba6-122">Enable Remote Desktop</span></span>
3. <span data-ttu-id="91ba6-123">사용자 a와 두 사용자 계정을 toohello 원격 데스크톱 보안 그룹을 추가 하는 사용자 b의 두 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-123">Create two user accounts, UserA and UserB, adding both user accounts toohello Remote Desktop security group.</span></span>
4. <span data-ttu-id="91ba6-124">Hello 응용 프로그램을 시작 하는 동안 두 개의 동시 RDS 세션 toohello PC를 설정 하 여 다중 세션 호환성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-124">Check multi-session compatibility by establishing two simultaneous RDS sessions toohello PC while launching hello application.</span></span>
5. <span data-ttu-id="91ba6-125">앱 동작의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="91ba6-125">Validate app behavior</span></span>

## <a name="application-development-guidelines"></a><span data-ttu-id="91ba6-126">응용 프로그램 개발 지침</span><span class="sxs-lookup"><span data-stu-id="91ba6-126">Application development guidelines</span></span>
<span data-ttu-id="91ba6-127">RemoteApp에 대 한 응용 프로그램을 개발 하기 위한 지침을 따르는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-127">Use hello following guidelines for developing applications for RemoteApp.</span></span>

### <a name="multiple-users"></a><span data-ttu-id="91ba6-128">여러 사용자</span><span class="sxs-lookup"><span data-stu-id="91ba6-128">Multiple users</span></span>
* <span data-ttu-id="91ba6-129">[단일 사용자를 위한 응용 프로그램 ](https://msdn.microsoft.com/library/aa380661.aspx)을 설치하면 다중 사용자 환경에서 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-129">Installing an [application for a single user ](https://msdn.microsoft.com/library/aa380661.aspx)can create problems in a multiuser environment.</span></span>
* <span data-ttu-id="91ba6-130">응용 프로그램 해야 [사용자 관련 정보를 저장](https://msdn.microsoft.com/library/aa383452.aspx) 사용자 관련 위치에 개별적으로 전역 정보에서 적용 되는 tooall 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-130">Applications should [store user-specific information](https://msdn.microsoft.com/library/aa383452.aspx) in user-specific locations, separately from global information that applies tooall users.</span></span>
* <span data-ttu-id="91ba6-131">RemoteApp은 여러 개의 [커널 개체의 네임스페이스](https://msdn.microsoft.com/library/aa382954.aspx)를 사용하며, 전역 네임스페이스는 주로 클라이언트/서버 응용 프로그램의 서비스에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-131">RemoteApp uses multiple [namespaces for kernel objects](https://msdn.microsoft.com/library/aa382954.aspx); a global namespace is used primarily by services in client/server applications.</span></span>
* <span data-ttu-id="91ba6-132">컴퓨터 이름 또는 hello hello 안전 tooassume 없으면 [IP 주소](https://msdn.microsoft.com/library/aa382942.aspx) 할당된 toohello 컴퓨터 사용 되므로 단일 사용자와 연결 된 여러 사용자가 원격 데스크톱 세션 호스트 (RD 세션 tooa 동시에 로그온 할 수 있습니다 호스트) 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-132">It is not safe tooassume that hello computer name or hello [IP address](https://msdn.microsoft.com/library/aa382942.aspx) assigned toohello computer are associated with a single user because multiple users can be logged on simultaneously tooa Remote Desktop Session Host (RD Session Host) server.</span></span>

### <a name="performance"></a><span data-ttu-id="91ba6-133">성능</span><span class="sxs-lookup"><span data-stu-id="91ba6-133">Performance</span></span>
* <span data-ttu-id="91ba6-134">사용 안 함 [그래픽 효과](https://msdn.microsoft.com/library/aa380822.aspx) 앱 tooRemoteApp를 추가 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="91ba6-134">Disable [graphic effects](https://msdn.microsoft.com/library/aa380822.aspx) before you add your app tooRemoteApp.</span></span>
* <span data-ttu-id="91ba6-135">모든 사용자에 대 한 CPU toomaximize 가용성 해제 하거나 [백그라운드 작업 ](https://msdn.microsoft.com/library/aa380665.aspx) 하거나 리소스를 많이 사용 하지 않은 효율적인 백그라운드 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-135">toomaximize CPU availability for all users, either disable [background tasks ](https://msdn.microsoft.com/library/aa380665.aspx) or create efficient background tasks that are not resource-intensive.</span></span>
* <span data-ttu-id="91ba6-136">다중 사용자, 다중 프로세서 환경을 위해 응용 프로그램 [스레드 사용량](https://msdn.microsoft.com/library/aa383520.aspx) 을 조정하여 균형을 맞추어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-136">You should tune and balance application [thread usage](https://msdn.microsoft.com/library/aa383520.aspx) for a multiuser, multiprocessor environment.</span></span>
* <span data-ttu-id="91ba6-137">toooptimize 성능 너무는 응용 프로그램에 대 한 것이 좋습니다[검색](https://msdn.microsoft.com/library/aa380798.aspx) 클라이언트 세션의 실행 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="91ba6-137">toooptimize performance, it is good practice for applications too[detect](https://msdn.microsoft.com/library/aa380798.aspx) whether they are running in a client session.</span></span>

