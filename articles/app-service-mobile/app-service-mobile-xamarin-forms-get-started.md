---
title: "Xamarin.Forms를 사용 하 여 aaaGet 모바일 앱 시작"
description: "Xamarin.Forms 개발에 대 한 모바일 앱을 사용 하 여이 자습서 toostart를 수행 합니다."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="0fe1c-103">Xamarin.Forms 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0fe1c-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="0fe1c-104">개요</span><span class="sxs-lookup"><span data-stu-id="0fe1c-104">Overview</span></span>
<span data-ttu-id="0fe1c-105">이 자습서를 사용 하 여 클라우드 기반 백 엔드 서비스 tooa Xamarin.Forms 모바일 앱 tooadd hello 백 엔드 Azure 앱 서비스 모바일 앱 기능 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-105">This tutorial shows you how tooadd a cloud-based back-end service tooa Xamarin.Forms mobile app by using hello Mobile Apps feature of Azure App Service as hello back end.</span></span> <span data-ttu-id="0fe1c-106">새 Mobile Apps 백 엔드와 앱 데이터를 Azure에 저장하는 간단한 할 일 모음 Xamarin.Forms 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="0fe1c-107">이 자습서를 완료해야 다른 모든 Xamarin.Forms용 모바일 앱 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fe1c-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0fe1c-108">Prerequisites</span></span>
<span data-ttu-id="0fe1c-109">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="0fe1c-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="0fe1c-110">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-110">An active Azure account.</span></span> <span data-ttu-id="0fe1c-111">계정이 없는, Azure 평가판에 등록할 수 있으며 too10 가능한 모바일 앱을 계속 사용할 수 있습니다 프로그램 평가 종료 후에 준비.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-111">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="0fe1c-112">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="0fe1c-113">Xamarin이 포함된 Visual Studio입니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="0fe1c-114">내용은 hello를 참조 하십시오. [설정 및 Visual Studio 및 Xamarin이 설치](https://msdn.microsoft.com/library/mt613162.aspx) 페이지.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-114">For information, see hello [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="0fe1c-115">Xcode v7.0 이상 및 Xamarin Studio Community가 설치된 Mac입니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="0fe1c-116">자세한 내용은 [Visual Studio 및 Xamarin을 위한 설정 및 설치](https://msdn.microsoft.com/library/mt613162.aspx) 및 [Mac 사용자를 위한 설정, 설치 및 확인](https://msdn.microsoft.com/library/mt488770.aspx)(MSDN)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="0fe1c-117">새 Mobile Apps 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="0fe1c-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="0fe1c-118">다시 한 새로운 모바일 앱을 종료 toocreate 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-118">toocreate a new Mobile Apps back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="0fe1c-119">이제 모바일 클라이언트 응용 프로그램에서 사용할 수 있는 Mobile Apps 백 엔드를 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="0fe1c-120">다음으로 간단한 할 일 목록 백 엔드에 대 한 서버 프로젝트를 다운로드 하 고 tooAzure 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-120">Next, you download a server project for a simple to-do list back end and then publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="0fe1c-121">Hello 서버 프로젝트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-121">Configure hello server project</span></span>

<span data-ttu-id="0fe1c-122">tooconfigure hello 서버 프로젝트 toouse Node.js 또는.NET 백 엔드 hello 중 하나, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-122">tooconfigure hello server project toouse either hello Node.js or .NET back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a><span data-ttu-id="0fe1c-123">다운로드 하 고 hello Xamarin.Forms 솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="0fe1c-123">Download and run hello Xamarin.Forms solution</span></span>

<span data-ttu-id="0fe1c-124">두 가지 방법 중 하나로 hello 솔루션을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-124">You can download hello solution in either of two ways.</span></span> <span data-ttu-id="0fe1c-125">Mac tooa 다운로드 하 고 Xamarin Studio에서 엽니다 다운로드 tooa Windows 컴퓨터 한 hello iOS 앱을 작성 하기 위한 네트워크로 연결 된 Mac을 사용 하 여 Visual Studio에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-125">Download it tooa Mac and open it in Xamarin Studio, or download it tooa Windows computer and open it in Visual Studio by using a networked Mac for building hello iOS app.</span></span> <span data-ttu-id="0fe1c-126">자세한 내용은 [Visual Studio 및 Xamarin 설정 및 설치](https://msdn.microsoft.com/library/mt613162.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="0fe1c-127">Windows 또는 Mac 컴퓨터에서 수행 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="0fe1c-127">On a Mac or Windows computer, do hello following:</span></span>

1. <span data-ttu-id="0fe1c-128">Toohello 이동 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-128">Go toohello [Azure portal].</span></span>

2. <span data-ttu-id="0fe1c-129">Hello에 **설정** 블레이드 모바일 앱에 대 한 아래 **모바일**선택, **시작** > **Xamarin.Forms**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-129">On hello **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="0fe1c-130">**3단계** 아래에서 **새 앱 만들기**를 선택한 후 **다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="0fe1c-131">이 작업은 연결 된 tooyour 모바일 앱 하는 클라이언트 응용 프로그램을 포함 하는 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-131">This action downloads a project that contains a client application that's connected tooyour mobile app.</span></span> <span data-ttu-id="0fe1c-132">Hello 압축 된 프로젝트 파일 tooyour 로컬 컴퓨터를 저장 하 고 저장할 위치를 메모 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-132">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="0fe1c-133">Hello 프로젝트 다운로드 한 압축을 풀고 Visual Studio (Windows) 또는 Xamarin Studio (Mac)에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-133">Extract hello project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![Xamarin Studio에서 추출된 프로젝트][9]

   ![Visual Studio에서 추출된 프로젝트][8]

## <a name="optional-run-hello-ios-project"></a><span data-ttu-id="0fe1c-136">(선택 사항) Hello iOS 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-136">(Optional) Run hello iOS project</span></span>
<span data-ttu-id="0fe1c-137">이 섹션에서는 iOS 장치에 대 한 hello Xamarin iOS 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-137">In this section, you run hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="0fe1c-138">iOS 장치를 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="0fe1c-139">Xamarin Studio에서</span><span class="sxs-lookup"><span data-stu-id="0fe1c-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="0fe1c-140">Hello iOS 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **시작 프로젝트로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-140">Right-click hello iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="0fe1c-141">Hello에 **실행** 메뉴 선택 **디버깅 시작** toobuild 프로젝트 hello 및 hello iPhone 에뮬레이터의 hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-141">On hello **Run** menu, select **Start Debugging** toobuild hello project and start hello app in hello iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="0fe1c-142">Visual Studio에서</span><span class="sxs-lookup"><span data-stu-id="0fe1c-142">In Visual Studio</span></span>
1. <span data-ttu-id="0fe1c-143">Hello iOS 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **시작 프로젝트로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-143">Right-click hello iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="0fe1c-144">Hello에 **빌드** 메뉴 선택 **Configuration Manager**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-144">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="0fe1c-145">Hello에 **Configuration Manager** 대화 상자, 선택 hello **빌드** 및 **배포** 확인란 다음 toohello iOS 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-145">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello iOS project.</span></span>

4. <span data-ttu-id="0fe1c-146">toobuild 프로젝트 hello 및 선택 hello hello iPhone 에뮬레이터의 hello 응용 프로그램을 시작 **F5** 키입니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-146">toobuild hello project and start hello app in hello iPhone emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0fe1c-147">Hello 프로젝트를 구축 하는 데 문제가 있으면 hello NuGet 패키지 관리자 및 update toohello 최신 버전의 hello Xamarin 지원 패키지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-147">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="0fe1c-148">퀵 스타트 프로젝트 느린 tooupdate toohello 최신 버전을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-148">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="0fe1c-149">Hello 앱 의미 있는 텍스트를 같은 입력 *알아보려면 Xamarin*, 한 다음 선택 hello 더하기 기호 (**+**).</span><span class="sxs-lookup"><span data-stu-id="0fe1c-149">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="0fe1c-150">이 작업에는 새 모바일 앱 백 엔드 Azure에서 호스팅되는 post 요청 toohello를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-150">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="0fe1c-151">Hello 요청에서 데이터는 hello TodoItem 테이블에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-151">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="0fe1c-152">Hello 테이블에 저장 된 항목을 데이터 hello 목록에 표시 되며 다시 모바일 앱을 종료 하 고 hello hello 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-152">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0fe1c-153">모바일 앱 백 엔드 hello TodoItemManager.cs C# 솔루션의 hello 이식 가능한 클래스 라이브러리 프로젝트의 파일에에서 액세스 하는 hello 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-153">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-android-project"></a><span data-ttu-id="0fe1c-154">(선택 사항) Hello Android 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-154">(Optional) Run hello Android project</span></span>
<span data-ttu-id="0fe1c-155">이 섹션에서는 Android 용 hello Xamarin 로봇 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-155">In this section, you run hello Xamarin droid project for Android.</span></span> <span data-ttu-id="0fe1c-156">Android 장치를 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="0fe1c-157">Xamarin Studio에서</span><span class="sxs-lookup"><span data-stu-id="0fe1c-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="0fe1c-158">Hello Android 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **시작 프로젝트로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-158">Right-click hello Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="0fe1c-159">toobuild 프로젝트 hello 및 hello에 Android 에뮬레이터의 hello 응용 프로그램을 시작 **실행** 메뉴 선택 **디버깅 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-159">toobuild hello project and start hello app in an Android emulator, on hello **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="0fe1c-160">Visual Studio에서</span><span class="sxs-lookup"><span data-stu-id="0fe1c-160">In Visual Studio</span></span>

1. <span data-ttu-id="0fe1c-161">Hello (로봇) Android 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **시작 프로젝트로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-161">Right-click hello Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="0fe1c-162">Hello에 **빌드** 메뉴 선택 **Configuration Manager**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-162">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="0fe1c-163">Hello에 **Configuration Manager** 대화 상자, 선택 hello **빌드** 및 **배포** 확인란 다음 toohello Android 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-163">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Android project.</span></span>

4. <span data-ttu-id="0fe1c-164">toobuild 프로젝트 hello 및 선택 hello Android 에뮬레이터의 hello 응용 프로그램을 시작 **F5** 키입니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-164">toobuild hello project and start hello app in an Android emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0fe1c-165">Hello 프로젝트를 구축 하는 데 문제가 있으면 hello NuGet 패키지 관리자 및 update toohello 최신 버전의 hello Xamarin 지원 패키지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-165">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="0fe1c-166">퀵 스타트 프로젝트 느린 tooupdate toohello 최신 버전을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-166">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="0fe1c-167">Hello 앱 의미 있는 텍스트를 같은 입력 *알아보려면 Xamarin*, 한 다음 선택 hello 더하기 기호 (**+**).</span><span class="sxs-lookup"><span data-stu-id="0fe1c-167">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="0fe1c-168">이 작업에는 새 모바일 앱 백 엔드 Azure에서 호스팅되는 post 요청 toohello를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-168">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="0fe1c-169">Hello 요청에서 데이터는 hello TodoItem 테이블에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-169">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="0fe1c-170">Hello 테이블에 저장 된 항목을 데이터 hello 목록에 표시 되며 다시 모바일 앱을 종료 하 고 hello hello 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-170">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="0fe1c-171">모바일 앱 백 엔드 hello TodoItemManager.cs C# 솔루션의 hello 이식 가능한 클래스 라이브러리 프로젝트의 파일에에서 액세스 하는 hello 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-171">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-windows-project"></a><span data-ttu-id="0fe1c-172">(선택 사항) Hello Windows 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-172">(Optional) Run hello Windows project</span></span>

<span data-ttu-id="0fe1c-173">이 섹션에서는 Windows 장치에 대 한 Xamarin WinApp 프로젝트 hello를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-173">In this section, you run hello Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="0fe1c-174">Windows 장치를 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="0fe1c-175">Visual Studio에서</span><span class="sxs-lookup"><span data-stu-id="0fe1c-175">In Visual Studio</span></span>

1. <span data-ttu-id="0fe1c-176">Hello Windows 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **시작 프로젝트로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-176">Right-click any of hello Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="0fe1c-177">Hello에 **빌드** 메뉴 선택 **Configuration Manager**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-177">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="0fe1c-178">Hello에 **Configuration Manager** 대화 상자, 선택 hello **빌드** 및 **배포** 확인란 다음 toohello Windows 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-178">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Windows project that you chose.</span></span>

4. <span data-ttu-id="0fe1c-179">toobuild 프로젝트 hello 및 선택 hello Windows 에뮬레이터의 hello 응용 프로그램을 시작 **F5** 키입니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-179">toobuild hello project and start hello app in a Windows emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0fe1c-180">Hello 프로젝트를 구축 하는 데 문제가 있으면 hello NuGet 패키지 관리자 및 update toohello 최신 버전의 hello Xamarin 지원 패키지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-180">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="0fe1c-181">퀵 스타트 프로젝트 느린 tooupdate toohello 최신 버전을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-181">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="0fe1c-182">Hello 앱 의미 있는 텍스트를 같은 입력 *알아보려면 Xamarin*, 한 다음 선택 hello 더하기 기호 (**+**).</span><span class="sxs-lookup"><span data-stu-id="0fe1c-182">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    <span data-ttu-id="0fe1c-183">이 작업에는 새 모바일 앱 백 엔드 Azure에서 호스팅되는 post 요청 toohello를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-183">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="0fe1c-184">Hello 요청에서 데이터는 hello TodoItem 테이블에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-184">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="0fe1c-185">Hello 테이블에 저장 된 항목을 데이터 hello 목록에 표시 되며 다시 모바일 앱을 종료 하 고 hello hello 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-185">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="0fe1c-186">모바일 앱 백 엔드 hello TodoItemManager.cs C# 솔루션의 hello 이식 가능한 클래스 라이브러리 프로젝트의 파일에에서 액세스 하는 hello 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-186">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="0fe1c-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0fe1c-187">Next steps</span></span>

* [<span data-ttu-id="0fe1c-188">인증 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="0fe1c-188">Add authentication tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="0fe1c-189">자세한 내용은 방법 tooauthenticate 사용자가 id 공급자로 사용 하 여 앱의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-189">Learn how tooauthenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="0fe1c-190">푸시 알림 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="0fe1c-190">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="0fe1c-191">Tooadd 푸시 알림을 tooyour 앱을 지원 하는 방법을 알아보고 모바일 앱 백 엔드 toouse Azure 알림 허브 toosend hello 푸시 알림을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-191">Learn how tooadd push notifications support tooyour app and configure your Mobile Apps back end toouse Azure Notification Hubs toosend hello push notifications.</span></span>

* [<span data-ttu-id="0fe1c-192">앱에 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="0fe1c-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="0fe1c-193">자세한 방법을 모바일 앱을 사용 하 여 앱에 대 한 오프 라인 지원 tooadd 백 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-193">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="0fe1c-194">오프라인 동기화를 사용하면 네트워크에 연결되어 있지 않은 경우에도 모바일 앱의 데이터를 보거나, 추가하거나, 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="0fe1c-195">모바일 앱에 대 한 관리 되는 클라이언트 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0fe1c-195">Use hello managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="0fe1c-196">Hello로 toowork SDK Xamarin 앱에 클라이언트를 관리 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0fe1c-196">Learn how toowork with hello managed client SDK in your Xamarin app.</span></span>

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure 포털]: https://portal.azure.com/
