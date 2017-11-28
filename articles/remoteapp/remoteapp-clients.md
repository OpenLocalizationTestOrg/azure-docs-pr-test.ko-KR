---
title: "모든 장치에서 앱에 액세스 | Microsoft Docs"
description: "Azure RemoteApp에 지원되는 클라이언트 및 앱에 액세스하는 방법을 알아봅니다."
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
ms.openlocfilehash: 10a5be6251765b59fac92a33120cedcf8091a677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a><span data-ttu-id="30e5a-103">Azure RemoteApp에서 앱에 액세스</span><span class="sxs-lookup"><span data-stu-id="30e5a-103">Accessing your apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="30e5a-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="30e5a-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="30e5a-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="30e5a-106">Azure RemoteApp의 장점 중 하나는 앱을 모든 장치에서 액세스할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-106">One of the beauties of Azure RemoteApp is that you can access apps from any of your devices.</span></span> <span data-ttu-id="30e5a-107">한 장치에서 작업을 시작한 다음 두 번째 장치로 매끄럽게 전환하고 중지한 위치에서 바로 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-107">Even better, you can start working on one device and then seamlessly transition to a second device and pick up right where you left off.</span></span> <span data-ttu-id="30e5a-108">시작하려면 장치에 적절한 클라이언트를 다운로드하고 서비스에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-108">To get started you need to download the appropriate client for your device and sign in to the service.</span></span>

<span data-ttu-id="30e5a-109">이 항목에서는 각 클라이언트에서 RemoteApp에 로그인하는 방법에 앞서 현재 지원되는 클라이언트 및 다운로드 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-109">In this topic, we'll review the clients currently supported and how to download them before I show you how to sign in to RemoteApp from each of the clients.</span></span>

## <a name="supported-clients"></a><span data-ttu-id="30e5a-110">지원되는 클라이언트</span><span class="sxs-lookup"><span data-stu-id="30e5a-110">Supported clients</span></span>
<span data-ttu-id="30e5a-111">장치가 다음 운영 체제 중 하나를 실행하는 경우 아래 단계에 따라 RemoteApp에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-111">You can access RemoteApp using the steps below if your device is running one of these operating systems:</span></span>

* <span data-ttu-id="30e5a-112">Windows 10</span><span class="sxs-lookup"><span data-stu-id="30e5a-112">Windows 10</span></span> 
* <span data-ttu-id="30e5a-113">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="30e5a-113">Windows 8.1</span></span>
* <span data-ttu-id="30e5a-114">Windows 8</span><span class="sxs-lookup"><span data-stu-id="30e5a-114">Windows 8</span></span>
* <span data-ttu-id="30e5a-115">Windows 7 서비스 팩 1</span><span class="sxs-lookup"><span data-stu-id="30e5a-115">Windows 7 Service Pack 1</span></span>
* <span data-ttu-id="30e5a-116">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="30e5a-116">Windows Phone 8.1</span></span>
* <span data-ttu-id="30e5a-117">iOS</span><span class="sxs-lookup"><span data-stu-id="30e5a-117">iOS</span></span>
* <span data-ttu-id="30e5a-118">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="30e5a-118">Mac OS X</span></span>
* <span data-ttu-id="30e5a-119">Android</span><span class="sxs-lookup"><span data-stu-id="30e5a-119">Android</span></span>

 <span data-ttu-id="30e5a-120">씬 클라이언트의 경우</span><span class="sxs-lookup"><span data-stu-id="30e5a-120">What about thin clients?</span></span> <span data-ttu-id="30e5a-121">다음과 같은 Windows Embedded 씬 클라이언트가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-121">The following Windows Embedded thin clients are supported:</span></span>

* <span data-ttu-id="30e5a-122">Windows Embedded Standard 7</span><span class="sxs-lookup"><span data-stu-id="30e5a-122">Windows Embedded Standard 7</span></span>
* <span data-ttu-id="30e5a-123">Windows Embedded 8 Standard</span><span class="sxs-lookup"><span data-stu-id="30e5a-123">Windows Embedded 8 Standard</span></span>
* <span data-ttu-id="30e5a-124">Windows Embedded 8.1 Industry Pro</span><span class="sxs-lookup"><span data-stu-id="30e5a-124">Windows Embedded 8.1 Industry Pro</span></span>
* <span data-ttu-id="30e5a-125">Windows 10 IoT Enterprise</span><span class="sxs-lookup"><span data-stu-id="30e5a-125">Windows 10 IoT Enterprise</span></span>

## <a name="downloading-the-client"></a><span data-ttu-id="30e5a-126">클라이언트 다운로드</span><span class="sxs-lookup"><span data-stu-id="30e5a-126">Downloading the client</span></span>
<span data-ttu-id="30e5a-127">사용하는 플랫폼에 관계없이 [원격 데스크톱 클라이언트 다운로드](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) 페이지에서 RemoteApp에 액세스하는 데 필요한 클라이언트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-127">No matter what platform you are using, the client you need to access RemoteApp can be found on the [Remote Desktop client download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span></span>

<span data-ttu-id="30e5a-128">다양한 링크를 클릭하여 바로 클라이언트 다운로드를 시작하거나 해당 플랫폼에 대한 앱 스토어의 클라이언트 다운로드 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-128">Clicking the different links will either directly start downloading the client or will send you to the client download page in the app store for that platform.</span></span> <span data-ttu-id="30e5a-129">화면의 지침에 따라 클라이언트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-129">Install the client by following the instructions on the screen.</span></span>

<span data-ttu-id="30e5a-130">장치에 클라이언트를 설치하고 시작한 후 아래의 해당 섹션으로 이동하여 클라이언트에서 RemoteApp에 로그인하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-130">Once you have installed the client on your device and launched it, jump to the corresponding section below to learn how to sign in to RemoteApp from that client.</span></span>

## <a name="android"></a><span data-ttu-id="30e5a-131">Android</span><span class="sxs-lookup"><span data-stu-id="30e5a-131">Android</span></span>
<span data-ttu-id="30e5a-132">Google Play 스토어에서 Microsoft 원격 데스크톱 앱을 설치하고 나면 앱 목록의 **원격 데스크톱**아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-132">Once you have installed the Microsoft Remote Desktop app from the Google Play store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="30e5a-133">아직 앱을 사용한 적이 없는 경우 앱을 시작하면 빈 연결 센터로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-133">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="30e5a-134">Azure RemoteApp을 시작하려면 **"" +""** 추가 단추, **Azure RemoteApp**을 차례로 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-134">To get started with Azure RemoteApp, tap the add button **""+""** and tap **Azure RemoteApp**.</span></span>    
   
     ![빈 연결 센터](./media/remoteapp-clients/Android1.png)
2. <span data-ttu-id="30e5a-136">서비스에 액세스하려면 메일 주소로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-136">You need to sign in with your email address to access the service.</span></span> <span data-ttu-id="30e5a-137">**시작**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-137">Tap **Get started**.</span></span>
   
    ![로그인 프롬프트](./media/remoteapp-clients/Android2.png)
3. <span data-ttu-id="30e5a-139">다음 페이지에서 **메일 주소**를 입력하고 **계속**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-139">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="30e5a-140">Azure Active Directory를 사용하여 로그인 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-140">This begins the sign-in process using Azure Active Directory.</span></span>
   
    ![첫 번째 Azure Active Directory 페이지](./media/remoteapp-clients/Android3.png)
4. <span data-ttu-id="30e5a-142">화면의 지침에 따라 Microsoft 계정(이전 "LiveID") 또는 조직 ID로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-142">Follow the instructions on the screen to sign in with your Microsoft account (previously called "LiveID") or organization ID.</span></span> <span data-ttu-id="30e5a-143">로그인된 후 수신한 모든 초대를 나열하는 페이지가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-143">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="30e5a-144">표시되는 경우 신뢰하는 초대를 선택하고 **완료**를 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-144">If you are, select the invitations you trust and tap **Done**.</span></span>    
   
    ![초대 페이지](./media/remoteapp-clients/Android4.png)
5. <span data-ttu-id="30e5a-146">초대를 수락하면 액세스할 수 있는 앱 목록이 장치에 다운로드되며 연결 센터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-146">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="30e5a-147">앱 중 하나를 탭하여 시작하고 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-147">Tap one of the apps to start using it.</span></span>
   
    ![피드가 포함된 연결 센터](./media/remoteapp-clients/Android5.png)
6. <span data-ttu-id="30e5a-149">아직 초대가 없는 경우에도 서비스를 체험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-149">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="30e5a-150">이렇게 하려면 메시지가 표시될 때 **무료 평가판으로 이동** 을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-150">To do so, tap **Go to free trial** when prompted.</span></span>
   
    ![데모 피드 프롬프트](./media/remoteapp-clients/Android6.png)
7. <span data-ttu-id="30e5a-152">이 경우 RemoteApp을 시작하기 위한 기본적인 앱 집합에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-152">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a><span data-ttu-id="30e5a-154">iOS</span><span class="sxs-lookup"><span data-stu-id="30e5a-154">iOS</span></span>
<span data-ttu-id="30e5a-155">앱 스토어에서 Microsoft 원격 데스크톱 앱을 설치하고 나면 앱 목록의 **RD 클라이언트**아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-155">Once you have installed the Microsoft Remote Desktop app from the App store, you can find it in your app list under **RD Client**.</span></span>

1. <span data-ttu-id="30e5a-156">아직 앱을 사용한 적이 없는 경우 앱을 시작하면 빈 연결 센터로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-156">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="30e5a-157">Azure RemoteApp을 시작하려면 **"" +""** 추가 단추, **Azure RemoteApp 추가**를 차례로 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-157">To get started with Azure RemoteApp, tap the add button **""+""** and tap **Add Azure RemoteApp**.</span></span>
   
    ![빈 연결 센터](./media/remoteapp-clients/IOS1.png)
2. <span data-ttu-id="30e5a-159">서비스에 액세스하려면 메일 주소로 로그인해야 합니다. 해당 프로세스를 시작하려면 **메일 주소**를 입력하고 **계속**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-159">You need to sign in with your email address to access the service, to start that process, type in your **email address** and tap **Continue**.</span></span>
   
    ![로그인 프롬프트](./media/remoteapp-clients/picture1.png)
3. <span data-ttu-id="30e5a-161">화면의 지침에 따라 Microsoft 계정(LiveID) 또는 조직 ID로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-161">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="30e5a-162">로그인된 후 수신한 모든 초대를 나열하는 페이지가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-162">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="30e5a-163">표시되는 경우 신뢰하는 초대를 선택하고 **완료**를 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-163">If you are, select the invitations you trust and tap **Done**.</span></span>
   
    ![초대 페이지](./media/remoteapp-clients/IOS3.png)
4. <span data-ttu-id="30e5a-165">초대를 수락하면 액세스할 수 있는 앱 목록이 장치에 다운로드되며 연결 센터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-165">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="30e5a-166">앱 중 하나를 탭하여 시작하고 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-166">Tap one of the apps to launch it and start using it.</span></span>
   
    ![피드가 포함된 연결 센터](./media/remoteapp-clients/IOS4.png)
5. <span data-ttu-id="30e5a-168">아직 초대가 없는 경우에도 서비스를 체험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-168">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="30e5a-169">이렇게 하려면 메시지가 표시될 때 **무료 평가판으로 이동** 을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-169">To do so, tap **Go to free trial** when prompted.</span></span>
   
    ![데모 피드 프롬프트](./media/remoteapp-clients/IOS5.png)
6. <span data-ttu-id="30e5a-171">이 경우 RemoteApp을 시작하기 위한 기본적인 앱 집합에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-171">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a><span data-ttu-id="30e5a-173">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="30e5a-173">Mac OS X</span></span>
<span data-ttu-id="30e5a-174">앱 스토어에서 Microsoft 원격 데스크톱 앱을 설치하고 나면 앱 목록의 **Microsoft 원격 데스크톱**아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-174">Once you have installed the Microsoft Remote Desktop app from the App store, you can find it in your app list under **Microsoft Remote Desktop**.</span></span>

1. <span data-ttu-id="30e5a-175">아직 앱을 사용한 적이 없는 경우 앱을 시작하면 빈 연결 센터로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-175">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="30e5a-176">Azure RemoteApp을 시작하려면 **Azure RemoteApp** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-176">To get started with Azure RemoteApp, click the **Azure RemoteApp** button.</span></span>
   
    ![빈 연결 센터](./media/remoteapp-clients/Mac1.png)
2. <span data-ttu-id="30e5a-178">서비스에 액세스하려면 메일 주소로 로그인해야 하며, 해당 프로세스를 시작하려면 **시작**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-178">You need to sign in with your email address to access the service, to start that process, tap **Get Started**.</span></span>
   
    ![로그인 프롬프트](./media/remoteapp-clients/Mac2.png)
3. <span data-ttu-id="30e5a-180">다음 페이지에서 **메일 주소**를 입력하고 **계속**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-180">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="30e5a-181">Azure Active Directory를 사용하여 로그인 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-181">This begins the sign in process using Azure Active Directory.</span></span>
   
    ![첫 번째 Azure Active Directory 페이지](./media/remoteapp-clients/picture2.png)
4. <span data-ttu-id="30e5a-183">화면의 지침에 따라 Microsoft 계정(LiveID) 또는 조직 ID로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-183">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="30e5a-184">로그인된 후 수신한 모든 초대를 나열하는 페이지가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-184">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="30e5a-185">표시되는 경우 신뢰하는 초대를 선택하고 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-185">If you are, select the invitations you trust and close the dialog.</span></span>
   
    ![초대 페이지](./media/remoteapp-clients/Mac4.png)
5. <span data-ttu-id="30e5a-187">초대를 수락하면 액세스할 수 있는 앱 목록이 장치에 다운로드되며 연결 센터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-187">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="30e5a-188">앱 중 하나를 두 번 클릭하여 시작하고 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-188">Double-click one of the apps to launch it and start using it.</span></span>
   
    ![피드가 포함된 연결 센터](./media/remoteapp-clients/Mac5.png)
6. <span data-ttu-id="30e5a-190">아직 초대가 없는 경우에도 서비스를 체험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-190">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="30e5a-191">이렇게 하려면 메시지가 표시될 때 **무료 평가판으로 이동** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-191">To do so, click **Go to free trial** when prompted.</span></span>
   
    ![데모 피드 프롬프트](./media/remoteapp-clients/Mac6.png)
7. <span data-ttu-id="30e5a-193">이 경우 RemoteApp을 시작하기 위한 기본적인 앱 집합에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-193">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a><span data-ttu-id="30e5a-195">Windows(Windows Phone을 제외하고 지원되는 모든 버전)</span><span class="sxs-lookup"><span data-stu-id="30e5a-195">Windows (All supported versions except Windows Phone)</span></span>
<span data-ttu-id="30e5a-196">설치가 완료되면 클라이언트가 자동으로 시작되지만 나중에 다시 액세스해야 하는 경우 앱 목록의 **Azure RemoteApp**아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-196">The client launches automatically after it finishes installing, however when you need to access it again later it can be found in your app list under the name **Azure RemoteApp**.</span></span>

1. <span data-ttu-id="30e5a-197">클라이언트를 시작한 후 표시되는 첫 페이지는 Azure RemoteApp 시작 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-197">Ater launching the client, the first page you see welcomes you to Azure RemoteApp.</span></span> <span data-ttu-id="30e5a-198">계속하려면 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-198">To proceed, click on **Get Started**.</span></span>
   
    ![Azure RemoteApp 클라이언트의 시작 페이지](./media/remoteapp-clients/Windows1.png)
2. <span data-ttu-id="30e5a-200">다음 페이지는 Azure Active Directory를 사용하여 Azure RemoteApp에 대한 로그인 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-200">The next page starts the sign in process for Azure RemoteApp using Azure Active Directory.</span></span> <span data-ttu-id="30e5a-201">이전에 Microsoft 서비스를 사용한 적이 있다면 이 프로세스가 익숙할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-201">This process should look familiar if you have used Microsoft services in the past.</span></span> <span data-ttu-id="30e5a-202">**메일 주소**를 입력하고 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-202">Start by typing your **email address** and click **Continue**.</span></span>
   
    ![첫 번째 Azure Active Directory 프롬프트](./media/remoteapp-clients/Windows2.png)
3. <span data-ttu-id="30e5a-204">화면의 지침에 따라 Microsoft 계정(LiveID) 또는 조직 ID로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-204">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="30e5a-205">로그인된 후 수신한 모든 초대를 나열하는 페이지가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-205">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="30e5a-206">표시되는 경우 신뢰하는 초대를 선택하고 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-206">If you are, select the invitations you trust and click **Done**.</span></span>
   
    ![Azure RemoteApp 클라이언트의 초대 페이지](./media/remoteapp-clients/Windows3.png)
4. <span data-ttu-id="30e5a-208">초대를 수락하면 액세스할 수 있는 앱 목록이 장치에 다운로드되며 연결 센터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-208">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="30e5a-209">앱 중 하나를 두 번 클릭하여 시작하고 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-209">Double-click one of the apps to launch it and start using it.</span></span>
   
    ![Azure RemoteApp 클라이언트의 연결 센터](./media/remoteapp-clients/Windows4.png)
5. <span data-ttu-id="30e5a-211">아직 초대를 받지 못한 경우에도 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-211">If no one has sent you an invitation yet, don't worry we've got you covered!</span></span> <span data-ttu-id="30e5a-212">데모 컬렉션에 액세스하여 서비스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-212">You'll still have access to a demo collection so you can test out the service.</span></span>
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a><span data-ttu-id="30e5a-214">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="30e5a-214">Windows Phone 8.1</span></span>
<span data-ttu-id="30e5a-215">Windows Phone 8.1 스토어에서 Microsoft 원격 데스크톱 앱을 설치하고 나면 앱 목록의 **원격 데스크톱**아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-215">Once you have installed the Microsoft Remote Desktop app from the Windows Phone 8.1 store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="30e5a-216">아직 앱을 사용한 적이 없는 경우 앱을 시작하면 빈 연결 센터로 바로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-216">Launching the app brings you directly to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="30e5a-217">Azure RemoteApp을 시작하려면 화면 맨 아래의 추가 단추 **""+""** 를 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-217">To get started with Azure RemoteApp, tap the add button **""+""** at the bottom of the screen.</span></span>
   
    ![빈 연결 센터](./media/remoteapp-clients/WinPhone1.png)
2. <span data-ttu-id="30e5a-219">**Azure RemoteApp**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-219">Next, tap on **Azure RemoteApp**.</span></span>
   
    ![항목 추가 페이지](./media/remoteapp-clients/WinPhone2.png)
3. <span data-ttu-id="30e5a-221">서비스에 액세스하려면 메일 주소로 로그인해야 하며, 해당 프로세스를 시작하려면 **연결**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-221">You need to sign in with your email address to access the service, to start that process, tap **connect**.</span></span>
   
    ![로그인 프롬프트](./media/remoteapp-clients/WinPhone3.png)
4. <span data-ttu-id="30e5a-223">다음 페이지에서 **메일 주소**를 입력하고 **계속**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-223">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="30e5a-224">Azure Active Directory를 사용하여 로그인 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-224">This begins the sign in process using Azure Active Directory.</span></span>
   
    ![첫 번째 Azure Active Directory 페이지](./media/remoteapp-clients/WinPhone4.png)
5. <span data-ttu-id="30e5a-226">화면의 지침에 따라 Microsoft 계정(LiveID) 또는 조직 ID로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-226">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="30e5a-227">로그인된 후 수신한 모든 초대를 나열하는 페이지가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-227">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="30e5a-228">표시되는 경우 신뢰하는 초대를 선택하고 **저장**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-228">If you are, select the invitations you trust and tap **save**.</span></span>
   
    ![초대 페이지](./media/remoteapp-clients/WinPhone5.png)
6. <span data-ttu-id="30e5a-230">초대를 수락하면 액세스할 수 있는 앱 목록이 장치에 다운로드되며 연결 센터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-230">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="30e5a-231">앱 중 하나를 탭하여 시작하고 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-231">Tap one of the apps to launch it and start using it.</span></span>
   
    ![피드가 포함된 연결 센터](./media/remoteapp-clients/WinPhone6.png)
7. <span data-ttu-id="30e5a-233">아직 초대가 없는 경우에도 서비스를 체험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-233">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="30e5a-234">이렇게 하려면 메시지가 표시될 때 **예** 를 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-234">To do so, tap **yes** when prompted.</span></span>
   
    ![데모 피드 프롬프트](./media/remoteapp-clients/WinPhone7.png)
8. <span data-ttu-id="30e5a-236">이 경우 RemoteApp을 시작하기 위한 기본적인 앱 집합에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e5a-236">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/WinPhone8.png)

