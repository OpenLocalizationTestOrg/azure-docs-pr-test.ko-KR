---
title: "Windows 플랫폼 UWP (유니버설) 모바일 앱에서 사용 하 여 aaaCreate | Microsoft Docs"
description: "Azure 모바일 앱 백 엔드를 사용 하 여 C#, Visual Basic 또는 JavaScript에서 유니버설 Windows 플랫폼 (UWP) 앱 개발을 위한 시작 자습서 tooget이를 수행 합니다."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="f2745-103">Windows 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="f2745-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="f2745-104">개요</span><span class="sxs-lookup"><span data-stu-id="f2745-104">Overview</span></span>
<span data-ttu-id="f2745-105">이 자습서에서는 tooadd 클라우드 기반 백 엔드 tooa 유니버설 Windows 플랫폼 (UWP) 앱을 서비스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-105">This tutorial shows you how tooadd a cloud-based backend service tooa Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="f2745-106">자세한 내용은 [모바일 앱 정의](app-service-mobile-value-prop.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2745-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="f2745-107">hello 다음은 완료 하는 hello 응용 프로그램에서 화면 캡처:</span><span class="sxs-lookup"><span data-stu-id="f2745-107">hello following are screen captures from hello completed app:</span></span>

![완료된 데스크톱 앱](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="f2745-109">데스크톱에서 실행</span><span class="sxs-lookup"><span data-stu-id="f2745-109">Running on a desktop.</span></span>

![완료된 휴대폰 앱](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="f2745-111">휴대폰에서 실행</span><span class="sxs-lookup"><span data-stu-id="f2745-111">Running on a phone</span></span>

<span data-ttu-id="f2745-112">먼저 이 자습서를 완료해야만 UWP 앱용 다른 모든 모바일 앱 자습서를 학습할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2745-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f2745-113">Prerequisites</span></span>
<span data-ttu-id="f2745-114">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="f2745-114">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="f2745-115">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="f2745-115">An active Azure account.</span></span> <span data-ttu-id="f2745-116">계정이 없는, Azure 평가판에 등록할 수 있으며 too10 가능한 모바일 앱을 계속 사용할 수 있습니다 프로그램 평가 종료 후에 준비.</span><span class="sxs-lookup"><span data-stu-id="f2745-116">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="f2745-117">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2745-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f2745-118">[Visual Studio Community 2015] 이상 버전</span><span class="sxs-lookup"><span data-stu-id="f2745-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="f2745-119">새 Azure 모바일 앱 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="f2745-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="f2745-120">이러한 단계 toocreate 새로운 모바일 앱 백 엔드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-120">Follow these steps toocreate a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="f2745-121">이제 모바일 클라이언트 응용 프로그램에서 사용할 수 있는 Azure 모바일 앱 백 엔드를 프로비저닝했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="f2745-122">간단한 "할 일 목록"에 대 한 서버 프로젝트를 다운로드는 다음으로 백 엔드 tooAzure 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-122">Next, you will download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="f2745-123">Hello 서버 프로젝트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-123">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a><span data-ttu-id="f2745-124">다운로드 하 고 hello 클라이언트 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-124">Download and run hello client project</span></span>
<span data-ttu-id="f2745-125">모바일 앱 백 엔드를 구성 새 클라이언트 앱 만들기 하거나 기존 앱 tooconnect tooAzure 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app tooconnect tooAzure.</span></span> <span data-ttu-id="f2745-126">이 섹션에서는 사용자 지정 된 tooconnect tooyour 모바일 앱 백 엔드에서 되는 UWP 앱 서식 파일 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-126">In this section, you download a UWP app template project that is customized tooconnect tooyour Mobile App backend.</span></span>

1. <span data-ttu-id="f2745-127">Hello에 다시 **퀵 스타트** 클릭 하 여 모바일 앱 백엔드에 대 한 블레이드 **새 앱 만들기** > **다운로드**, 다음 압축 hello 프로젝트 파일을 추출 tooyour 로컬 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-127">Back in hello **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract hello compressed project files tooyour local computer.</span></span>

    ![Windows 빠른 시작 프로젝트 다운로드](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="f2745-129">(선택 사항) Hello UWP 앱 프로젝트 toohello 추가 hello 서버 프로젝트와 동일한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-129">(Optional) Add hello UWP app project toohello same solution as hello server project.</span></span> <span data-ttu-id="f2745-130">따라서 toodebug 쉽고 테스트에서 앱과 hello 백 엔드 hello 둘 다 toodo 하도록 선택 하는 경우 동일한 Visual Studio 솔루션에 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-130">This makes it easier toodebug and test both hello app and hello backend in hello same Visual Studio solution, if you choose toodo so.</span></span> <span data-ttu-id="f2745-131">UWP 앱 프로젝트 toohello 솔루션 tooadd 사용 해야 Visual Studio 2015 또는 이후 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-131">tooadd a UWP app project toohello solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="f2745-132">UWP 앱 hello 시작 프로젝트로 hello 사용 하 여 hello F5 키 toodeploy 및 실행된 hello 응용 프로그램 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-132">With hello UWP app as hello startup project, press hello F5 key toodeploy and run hello app.</span></span>
4. <span data-ttu-id="f2745-133">Hello 앱 의미 있는 텍스트를 같은 입력 *완료 hello 자습서*, hello에 **Insert a TodoItem** 텍스트 상자 및 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-133">In hello app, type meaningful text, such as *Complete hello tutorial*, in hello **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Windows 빠른 시작 완료 데스크톱](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="f2745-135">POST 요청 toohello 새로운 모바일 앱 백 엔드 호스팅되는 Azure에서 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-135">This sends a POST request toohello new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="f2745-136">(선택 사항) Hello 앱을 중지 하 고 다른 장치 또는 모바일 에뮬레이터에서 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-136">(Optional) Stop hello app and restart it on a different device or mobile emulator.</span></span>

    ![Windows 빠른 시작 완료 휴대폰](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="f2745-138">Hello UWP 앱에서 시작 된 후 Azure에서 hello 이전 단계에서 저장 되는 데이터를 로드 되도록 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-138">Notice that data saved from hello previous step is loaded from Azure after hello UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2745-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f2745-139">Next steps</span></span>
* [<span data-ttu-id="f2745-140">인증 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="f2745-140">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="f2745-141">자세한 내용은 방법 tooauthenticate 사용자가 id 공급자로 사용 하 여 앱의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-141">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="f2745-142">푸시 알림 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="f2745-142">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="f2745-143">Tooadd 푸시 알림을 tooyour 앱을 지원 하는 방법을 알아보고 여 모바일 앱 백 엔드 toouse Azure 알림 허브 toosend 푸시 알림을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-143">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="f2745-144">앱에 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="f2745-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="f2745-145">오프 라인 tooadd는 모바일 앱 백 엔드를 사용 하 여 앱을 지 원하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-145">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="f2745-146">오프 라인 동기화 허용 모바일 앱과 함께 최종 사용자에 게 toointeract&mdash;보기, 추가 또는 데이터 수정&mdash;네트워크 연결이 없는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2745-146">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
