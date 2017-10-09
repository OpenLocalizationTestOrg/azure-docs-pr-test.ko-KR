---
title: "aaaAccessing 모든 장치에서 앱 | Microsoft Docs"
description: "어떤 클라이언트는 Azure RemoteApp에 대 한 지원에 대해 알아봅니다 방법과 tooaccess 앱."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: fb7bd17d-7aa8-43fd-9278-f96e0e9308e4
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 15985b40d870e3155d4132063bf5b9677ff9afed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a><span data-ttu-id="b4dd2-103">Azure RemoteApp에서 앱에 액세스</span><span class="sxs-lookup"><span data-stu-id="b4dd2-103">Accessing your apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b4dd2-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="b4dd2-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="b4dd2-106">Azure RemoteApp의 hello 특징 중 하나입니다 장치 중 어디에서 든 응용 프로그램을 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-106">One of hello beauties of Azure RemoteApp is that you can access apps from any of your devices.</span></span> <span data-ttu-id="b4dd2-107">더 좋은 ְ ֳ  한 장치에서 및 tooa 두 번째 장치를 완벽 하 게 전환 하 수의 나머지 부분은 오른쪽을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-107">Even better, you can start working on one device and then seamlessly transition tooa second device and pick up right where you left off.</span></span> <span data-ttu-id="b4dd2-108">tooget 시작 하면 toodownload hello에 대 한 적절 한 클라이언트 장치에 대 한 필요 하 고 toohello 서비스에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-108">tooget started you need toodownload hello appropriate client for your device and sign in toohello service.</span></span>

<span data-ttu-id="b4dd2-109">이 항목에서는 현재 지원 되는 hello 클라이언트 검토 합니다 방법과 toodownload 방법을 살펴보기 전에 이러한 각 hello 클라이언트에서 tooRemoteApp에 toosign 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-109">In this topic, we'll review hello clients currently supported and how toodownload them before I show you how toosign in tooRemoteApp from each of hello clients.</span></span>

## <a name="supported-clients"></a><span data-ttu-id="b4dd2-110">지원되는 클라이언트</span><span class="sxs-lookup"><span data-stu-id="b4dd2-110">Supported clients</span></span>
<span data-ttu-id="b4dd2-111">장치에 이러한 운영 체제 중 하나를 실행 하는 경우 다음 hello 단계를 사용 하 여 RemoteApp 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-111">You can access RemoteApp using hello steps below if your device is running one of these operating systems:</span></span>

* <span data-ttu-id="b4dd2-112">Windows 10</span><span class="sxs-lookup"><span data-stu-id="b4dd2-112">Windows 10</span></span> 
* <span data-ttu-id="b4dd2-113">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="b4dd2-113">Windows 8.1</span></span>
* <span data-ttu-id="b4dd2-114">Windows 8</span><span class="sxs-lookup"><span data-stu-id="b4dd2-114">Windows 8</span></span>
* <span data-ttu-id="b4dd2-115">Windows 7 서비스 팩 1</span><span class="sxs-lookup"><span data-stu-id="b4dd2-115">Windows 7 Service Pack 1</span></span>
* <span data-ttu-id="b4dd2-116">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="b4dd2-116">Windows Phone 8.1</span></span>
* <span data-ttu-id="b4dd2-117">iOS</span><span class="sxs-lookup"><span data-stu-id="b4dd2-117">iOS</span></span>
* <span data-ttu-id="b4dd2-118">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="b4dd2-118">Mac OS X</span></span>
* <span data-ttu-id="b4dd2-119">Android</span><span class="sxs-lookup"><span data-stu-id="b4dd2-119">Android</span></span>

 <span data-ttu-id="b4dd2-120">씬 클라이언트 어떻습니까? 다음 Windows Embedded 씬 클라이언트 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-120">What about thin clients? hello following Windows Embedded thin clients are supported:</span></span>

* <span data-ttu-id="b4dd2-121">Windows Embedded Standard 7</span><span class="sxs-lookup"><span data-stu-id="b4dd2-121">Windows Embedded Standard 7</span></span>
* <span data-ttu-id="b4dd2-122">Windows Embedded 8 Standard</span><span class="sxs-lookup"><span data-stu-id="b4dd2-122">Windows Embedded 8 Standard</span></span>
* <span data-ttu-id="b4dd2-123">Windows Embedded 8.1 Industry Pro</span><span class="sxs-lookup"><span data-stu-id="b4dd2-123">Windows Embedded 8.1 Industry Pro</span></span>
* <span data-ttu-id="b4dd2-124">Windows 10 IoT Enterprise</span><span class="sxs-lookup"><span data-stu-id="b4dd2-124">Windows 10 IoT Enterprise</span></span>

## <a name="downloading-hello-client"></a><span data-ttu-id="b4dd2-125">Hello 클라이언트 다운로드</span><span class="sxs-lookup"><span data-stu-id="b4dd2-125">Downloading hello client</span></span>
<span data-ttu-id="b4dd2-126">사용 하는 대상 플랫폼에 관계 없이, hello 클라이언트 hello에 RemoteApp 있습니다 tooaccess 필요한 [원격 데스크톱 클라이언트 다운로드](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) 페이지.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-126">No matter what platform you are using, hello client you need tooaccess RemoteApp can be found on hello [Remote Desktop client download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span></span>

<span data-ttu-id="b4dd2-127">Hello 다른 링크를 클릭 하면 hello 클라이언트 다운로드 직접 시작 하거나 됩니다 또는 보내 toohello 클라이언트 다운로드 페이지 해당 플랫폼에 대 한 hello 앱 스토어에 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-127">Clicking hello different links will either directly start downloading hello client or will send you toohello client download page in hello app store for that platform.</span></span> <span data-ttu-id="b4dd2-128">Hello 지침 hello 화면에 따라 hello 클라이언트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-128">Install hello client by following hello instructions on hello screen.</span></span>

<span data-ttu-id="b4dd2-129">Hello 클라이언트 장치에 설치 하 고 시작한 후 점프 toolearn 아래 해당 섹션 toohello 어떻게 toosign 해당 클라이언트에서 tooRemoteApp에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-129">Once you have installed hello client on your device and launched it, jump toohello corresponding section below toolearn how toosign in tooRemoteApp from that client.</span></span>

## <a name="android"></a><span data-ttu-id="b4dd2-130">Android</span><span class="sxs-lookup"><span data-stu-id="b4dd2-130">Android</span></span>
<span data-ttu-id="b4dd2-131">Hello Google Play 스토어에서에서 hello Microsoft 원격 데스크톱 앱을 설치 하면 앱 목록 아래에서 찾을 수 있습니다 **원격 데스크톱**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-131">Once you have installed hello Microsoft Remote Desktop app from hello Google Play store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="b4dd2-132">시작 hello 앱 제공 tooan 빈 연결 센터를 사용 하지 않는 한 이미 되었습니다 hello 앱 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-132">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="b4dd2-133">Azure RemoteApp과 함께 시작 tooget, tap hello 추가 단추 **"" +""** 누릅니다 **Azure RemoteApp**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-133">tooget started with Azure RemoteApp, tap hello add button **""+""** and tap **Azure RemoteApp**.</span></span>    
   
     ![빈 연결 센터](./media/remoteapp-clients/Android1.png)
2. <span data-ttu-id="b4dd2-135">전자 메일 주소 tooaccess hello 서비스를 사용 하 여 toosign을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-135">You need toosign in with your email address tooaccess hello service.</span></span> <span data-ttu-id="b4dd2-136">**시작**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-136">Tap **Get started**.</span></span>
   
    ![로그인 프롬프트](./media/remoteapp-clients/Android2.png)
3. <span data-ttu-id="b4dd2-138">Hello 다음 페이지에 입력 하면 **전자 메일 주소** 누릅니다 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-138">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="b4dd2-139">Hello 로그인 프로세스 Azure Active Directory를 사용 하 여을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-139">This begins hello sign-in process using Azure Active Directory.</span></span>
   
    ![첫 번째 Azure Active Directory 페이지](./media/remoteapp-clients/Android3.png)
4. <span data-ttu-id="b4dd2-141">Microsoft 계정 (이전에 "live Id" 라고 함) 또는 조직 ID를 사용 하 여 hello 화면 toosign에 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-141">Follow hello instructions on hello screen toosign in with your Microsoft account (previously called "LiveID") or organization ID.</span></span> <span data-ttu-id="b4dd2-142">로그인 한 후 모든 hello 초대를 받았습니다. 나열 된 페이지가 제공 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-142">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="b4dd2-143">인 경우 hello 초대를 신뢰 하 고 탭 선택 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-143">If you are, select hello invitations you trust and tap **Done**.</span></span>    
   
    ![초대 페이지](./media/remoteapp-clients/Android4.png)
5. <span data-ttu-id="b4dd2-145">초대, 앱 목록이 hello 수락한 후 액세스 toowill 다운로드 한 tooyour 장치일 수 있고 hello 연결 센터에서에서 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-145">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="b4dd2-146">사용 하 여 hello 앱 toostart 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-146">Tap one of hello apps toostart using it.</span></span>
   
    ![피드가 포함된 연결 센터](./media/remoteapp-clients/Android5.png)
6. <span data-ttu-id="b4dd2-148">초대를 아직 없는 경우 hello 서비스 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-148">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="b4dd2-149">toodo 따라서 탭 **toofree 평가판 이동** 대화 상자가 나타나면 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-149">toodo so, tap **Go toofree trial** when prompted.</span></span>
   
    ![데모 피드 프롬프트](./media/remoteapp-clients/Android6.png)
7. <span data-ttu-id="b4dd2-151">이렇게 하면 tooa RemoteApp과 함께 시작 하는 앱 tooget의 기본 집합에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-151">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a><span data-ttu-id="b4dd2-153">iOS</span><span class="sxs-lookup"><span data-stu-id="b4dd2-153">iOS</span></span>
<span data-ttu-id="b4dd2-154">Hello 앱 스토어에서 hello Microsoft 원격 데스크톱 앱을 설치 하면 앱 목록 아래에서 찾을 수 있습니다 **RD 클라이언트**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-154">Once you have installed hello Microsoft Remote Desktop app from hello App store, you can find it in your app list under **RD Client**.</span></span>

1. <span data-ttu-id="b4dd2-155">시작 hello 앱 제공 tooan 빈 연결 센터를 사용 하지 않는 한 이미 되었습니다 hello 앱 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-155">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="b4dd2-156">Azure RemoteApp과 함께 시작 tooget, tap hello 추가 단추 **"" +""** 누릅니다 **추가 Azure RemoteApp**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-156">tooget started with Azure RemoteApp, tap hello add button **""+""** and tap **Add Azure RemoteApp**.</span></span>
   
    ![빈 연결 센터](./media/remoteapp-clients/IOS1.png)
2. <span data-ttu-id="b4dd2-158">필요한 toosign 전자 메일 주소 tooaccess hello 서비스, toostart 사용 하 여 해당 프로세스를 입력 하면 **전자 메일 주소** 탭 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-158">You need toosign in with your email address tooaccess hello service, toostart that process, type in your **email address** and tap **Continue**.</span></span>
   
    ![로그인 프롬프트](./media/remoteapp-clients/picture1.png)
3. <span data-ttu-id="b4dd2-160">Microsoft 계정 (live Id) 또는 조직 id.를 사용 하 여 hello 화면 toosign에 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-160">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="b4dd2-161">로그인 한 후 모든 hello 초대를 받았습니다. 나열 된 페이지가 제공 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-161">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="b4dd2-162">인 경우 hello 초대를 신뢰 하 고 탭 선택 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-162">If you are, select hello invitations you trust and tap **Done**.</span></span>
   
    ![초대 페이지](./media/remoteapp-clients/IOS3.png)
4. <span data-ttu-id="b4dd2-164">초대, 앱 목록이 hello 수락한 후 액세스 toowill 다운로드 한 tooyour 장치일 수 있고 hello 연결 센터에서에서 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-164">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="b4dd2-165">하 고 바로 hello 앱 toolaunch 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-165">Tap one of hello apps toolaunch it and start using it.</span></span>
   
    ![피드가 포함된 연결 센터](./media/remoteapp-clients/IOS4.png)
5. <span data-ttu-id="b4dd2-167">초대를 아직 없는 경우 hello 서비스 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-167">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="b4dd2-168">toodo 따라서 탭 **toofree 평가판 이동** 대화 상자가 나타나면 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-168">toodo so, tap **Go toofree trial** when prompted.</span></span>
   
    ![데모 피드 프롬프트](./media/remoteapp-clients/IOS5.png)
6. <span data-ttu-id="b4dd2-170">이렇게 하면 tooa RemoteApp과 함께 시작 하는 앱 tooget의 기본 집합에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-170">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a><span data-ttu-id="b4dd2-172">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="b4dd2-172">Mac OS X</span></span>
<span data-ttu-id="b4dd2-173">Hello 앱 스토어에서 hello Microsoft 원격 데스크톱 앱을 설치 하면 앱 목록 아래에서 찾을 수 있습니다 **Microsoft 원격 데스크톱**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-173">Once you have installed hello Microsoft Remote Desktop app from hello App store, you can find it in your app list under **Microsoft Remote Desktop**.</span></span>

1. <span data-ttu-id="b4dd2-174">시작 hello 앱 제공 tooan 빈 연결 센터를 사용 하지 않는 한 이미 되었습니다 hello 앱 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-174">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="b4dd2-175">Azure RemoteApp과 함께 시작 tooget 클릭 hello **Azure RemoteApp** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-175">tooget started with Azure RemoteApp, click hello **Azure RemoteApp** button.</span></span>
   
    ![빈 연결 센터](./media/remoteapp-clients/Mac1.png)
2. <span data-ttu-id="b4dd2-177">Toosign 해야 전자 메일 주소 tooaccess hello 서비스, 처리, toostart 사용 하 여 누릅니다 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-177">You need toosign in with your email address tooaccess hello service, toostart that process, tap **Get Started**.</span></span>
   
    ![로그인 프롬프트](./media/remoteapp-clients/Mac2.png)
3. <span data-ttu-id="b4dd2-179">Hello 다음 페이지에 입력 하면 **전자 메일 주소** 누릅니다 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-179">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="b4dd2-180">Hello 로그인 Azure Active Directory를 사용 하 여 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-180">This begins hello sign in process using Azure Active Directory.</span></span>
   
    ![첫 번째 Azure Active Directory 페이지](./media/remoteapp-clients/picture2.png)
4. <span data-ttu-id="b4dd2-182">Microsoft 계정 (live Id) 또는 조직 id.를 사용 하 여 hello 화면 toosign에 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-182">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="b4dd2-183">로그인 한 후 모든 hello 초대를 받았습니다. 나열 된 페이지가 제공 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-183">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="b4dd2-184">인 경우 hello 초대 신뢰 하 고 hello 대화 상자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-184">If you are, select hello invitations you trust and close hello dialog.</span></span>
   
    ![초대 페이지](./media/remoteapp-clients/Mac4.png)
5. <span data-ttu-id="b4dd2-186">초대, 앱 목록이 hello 수락한 후 액세스 toowill 다운로드 한 tooyour 장치일 수 있고 hello 연결 센터에서에서 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-186">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="b4dd2-187">Hello 앱 toolaunch 중 하나를 두 번 클릭 하 고 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-187">Double-click one of hello apps toolaunch it and start using it.</span></span>
   
    ![피드가 포함된 연결 센터](./media/remoteapp-clients/Mac5.png)
6. <span data-ttu-id="b4dd2-189">초대를 아직 없는 경우 hello 서비스 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-189">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="b4dd2-190">toodo 이므로, 클릭 **toofree 평가판 이동** 대화 상자가 나타나면 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-190">toodo so, click **Go toofree trial** when prompted.</span></span>
   
    ![데모 피드 프롬프트](./media/remoteapp-clients/Mac6.png)
7. <span data-ttu-id="b4dd2-192">이렇게 하면 tooa RemoteApp과 함께 시작 하는 앱 tooget의 기본 집합에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-192">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a><span data-ttu-id="b4dd2-194">Windows(Windows Phone을 제외하고 지원되는 모든 버전)</span><span class="sxs-lookup"><span data-stu-id="b4dd2-194">Windows (All supported versions except Windows Phone)</span></span>
<span data-ttu-id="b4dd2-195">하지만 hello client가 시작 자동으로 설치 tooaccess 필요할 때 나중에 다시 것 있습니다 hello 이름 앱 목록에서 완료 된 후 **Azure RemoteApp**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-195">hello client launches automatically after it finishes installing, however when you need tooaccess it again later it can be found in your app list under hello name **Azure RemoteApp**.</span></span>

1. <span data-ttu-id="b4dd2-196">클라이언트 hello, hello 첫 번째 페이지 실행에서는 tooAzure RemoteApp는 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-196">Ater launching hello client, hello first page you see welcomes you tooAzure RemoteApp.</span></span> <span data-ttu-id="b4dd2-197">tooproceed, 클릭 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-197">tooproceed, click on **Get Started**.</span></span>
   
    ![Hello Azure RemoteApp 클라이언트의 시작 페이지](./media/remoteapp-clients/Windows1.png)
2. <span data-ttu-id="b4dd2-199">hello 다음 페이지는 Azure Active Directory를 사용 하 여 Azure RemoteApp에 대 한 프로세스에서 hello 기호를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-199">hello next page starts hello sign in process for Azure RemoteApp using Azure Active Directory.</span></span> <span data-ttu-id="b4dd2-200">Microsoft 서비스 hello 이전에 사용한 경우에이 프로세스 익숙할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-200">This process should look familiar if you have used Microsoft services in hello past.</span></span> <span data-ttu-id="b4dd2-201">**메일 주소**를 입력하고 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-201">Start by typing your **email address** and click **Continue**.</span></span>
   
    ![첫 번째 Azure Active Directory 프롬프트](./media/remoteapp-clients/Windows2.png)
3. <span data-ttu-id="b4dd2-203">Microsoft 계정 (live Id) 또는 조직 id.를 사용 하 여 hello 화면 toosign에 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-203">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="b4dd2-204">로그인 한 후 모든 hello 초대를 받았습니다. 나열 된 페이지가 제공 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-204">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="b4dd2-205">인 경우 hello 초대를 신뢰 하 고 클릭 선택 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-205">If you are, select hello invitations you trust and click **Done**.</span></span>
   
    ![Hello Azure RemoteApp 클라이언트의 초대 페이지](./media/remoteapp-clients/Windows3.png)
4. <span data-ttu-id="b4dd2-207">초대, 앱 목록이 hello 수락한 후 액세스 toowill 다운로드 한 tooyour 장치일 수 있고 hello 연결 센터에서에서 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-207">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="b4dd2-208">Hello 앱 toolaunch 중 하나를 두 번 클릭 하 고 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-208">Double-click one of hello apps toolaunch it and start using it.</span></span>
   
    ![Hello Azure RemoteApp 클라이언트의 연결 센터](./media/remoteapp-clients/Windows4.png)
5. <span data-ttu-id="b4dd2-210">아직 초대를 받지 못한 경우에도 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-210">If no one has sent you an invitation yet, don't worry we've got you covered!</span></span> <span data-ttu-id="b4dd2-211">여전히 액세스 tooa 데모 컬렉션 hello 서비스를 테스트할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-211">You'll still have access tooa demo collection so you can test out hello service.</span></span>
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a><span data-ttu-id="b4dd2-213">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="b4dd2-213">Windows Phone 8.1</span></span>
<span data-ttu-id="b4dd2-214">Windows Phone 8.1 hello 저장소에서 hello Microsoft 원격 데스크톱 앱을 설치 하면 앱 목록 아래에서 찾을 수 있습니다 **원격 데스크톱**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-214">Once you have installed hello Microsoft Remote Desktop app from hello Windows Phone 8.1 store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="b4dd2-215">시작 hello 앱 제공 직접 tooan 빈 연결 센터를 사용 하지 않는 한 이미 되었습니다 hello 앱 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-215">Launching hello app brings you directly tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="b4dd2-216">Azure RemoteApp과 함께 시작 tooget, tap hello 추가 단추 **"" +""** hello hello 화면 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-216">tooget started with Azure RemoteApp, tap hello add button **""+""** at hello bottom of hello screen.</span></span>
   
    ![빈 연결 센터](./media/remoteapp-clients/WinPhone1.png)
2. <span data-ttu-id="b4dd2-218">**Azure RemoteApp**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-218">Next, tap on **Azure RemoteApp**.</span></span>
   
    ![항목 추가 페이지](./media/remoteapp-clients/WinPhone2.png)
3. <span data-ttu-id="b4dd2-220">Toosign 해야 전자 메일 주소 tooaccess hello 서비스, 처리, toostart 사용 하 여 누릅니다 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-220">You need toosign in with your email address tooaccess hello service, toostart that process, tap **connect**.</span></span>
   
    ![로그인 프롬프트](./media/remoteapp-clients/WinPhone3.png)
4. <span data-ttu-id="b4dd2-222">Hello 다음 페이지에 입력 하면 **전자 메일 주소** 누릅니다 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-222">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="b4dd2-223">Hello 로그인 Azure Active Directory를 사용 하 여 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-223">This begins hello sign in process using Azure Active Directory.</span></span>
   
    ![첫 번째 Azure Active Directory 페이지](./media/remoteapp-clients/WinPhone4.png)
5. <span data-ttu-id="b4dd2-225">Microsoft 계정 (live Id) 또는 조직 id.를 사용 하 여 hello 화면 toosign에 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-225">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="b4dd2-226">로그인 한 후 모든 hello 초대를 받았습니다. 나열 된 페이지가 제공 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-226">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="b4dd2-227">인 경우 hello 초대를 신뢰 하 고 탭 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-227">If you are, select hello invitations you trust and tap **save**.</span></span>
   
    ![초대 페이지](./media/remoteapp-clients/WinPhone5.png)
6. <span data-ttu-id="b4dd2-229">초대, 앱 목록이 hello 수락한 후 액세스 toowill 다운로드 한 tooyour 장치일 수 있고 hello 연결 센터에서에서 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-229">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="b4dd2-230">하 고 바로 hello 앱 toolaunch 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-230">Tap one of hello apps toolaunch it and start using it.</span></span>
   
    ![피드가 포함된 연결 센터](./media/remoteapp-clients/WinPhone6.png)
7. <span data-ttu-id="b4dd2-232">초대를 아직 없는 경우 hello 서비스 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-232">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="b4dd2-233">toodo 따라서 탭 **예** 대화 상자가 나타나면 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-233">toodo so, tap **yes** when prompted.</span></span>
   
    ![데모 피드 프롬프트](./media/remoteapp-clients/WinPhone7.png)
8. <span data-ttu-id="b4dd2-235">이렇게 하면 tooa RemoteApp과 함께 시작 하는 앱 tooget의 기본 집합에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dd2-235">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/WinPhone8.png)

