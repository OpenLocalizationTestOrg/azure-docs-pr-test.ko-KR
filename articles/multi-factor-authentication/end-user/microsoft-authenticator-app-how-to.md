---
title: "휴대폰에 대 한 aaaMicrosoft ऍ | Microsoft Docs"
description: "자세한 내용은 방법 tooupgrade toohello 최신 버전의 Azure Authenticator 합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="d4a1f-103">Hello Microsoft Authenticator 앱 시작</span><span class="sxs-lookup"><span data-stu-id="d4a1f-103">Get started with hello Microsoft Authenticator app</span></span>
<span data-ttu-id="d4a1f-104">hello Microsoft Authenticator 앱 추가 수준을 제공 하는 회사 또는 학교 계정에 보안 (예를 들어 bsimon@contoso.com) 또는 Microsoft 계정 (예를 들어 bsimon@outlook.com).</span><span class="sxs-lookup"><span data-stu-id="d4a1f-104">hello Microsoft Authenticator app provides an additional level of security in your work or school account (for example, bsimon@contoso.com) or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="d4a1f-105">hello 앱 두 가지 방법 중 하나에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-105">hello app works in one of two ways:</span></span>

* <span data-ttu-id="d4a1f-106">**알림**.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-106">**Notification**.</span></span> <span data-ttu-id="d4a1f-107">hello 앱 tooaccounts 무단된 액세스를 방지 하 고 알림 tooyour 스마트폰 또는 태블릿에 푸시하여 사기성 트랜잭션을 중지 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-107">hello app can help prevent unauthorized access tooaccounts and stop fraudulent transactions by pushing a notification tooyour smartphone or tablet.</span></span> <span data-ttu-id="d4a1f-108">Hello 알림을 본 합법적인 이면 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-108">Simply view hello notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="d4a1f-109">그렇지 않으면 **거부**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-109">Otherwise, you can select **Deny**.</span></span> 
* <span data-ttu-id="d4a1f-110">**확인 코드**.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-110">**Verification code**.</span></span> <span data-ttu-id="d4a1f-111">hello 앱을 소프트웨어 토큰 toogenerate OAuth 확인 코드 처럼 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-111">hello app can be used as a software token toogenerate an OAuth verification code.</span></span> <span data-ttu-id="d4a1f-112">사용자 이름 및 암호를 입력 한 후 hello 로그인 화면에 hello 응용 프로그램에서 제공 하는 hello 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-112">After you enter your username and password, you enter hello code provided by hello app into hello sign-in screen.</span></span> <span data-ttu-id="d4a1f-113">hello 확인 코드는 두 번째 형식의 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-113">hello verification code provides a second form of authentication.</span></span>

<span data-ttu-id="d4a1f-114">hello Microsoft Authenticator 앱 hello Azure Authenticator 앱을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-114">hello Microsoft Authenticator app replaces hello Azure Authenticator app.</span></span> <span data-ttu-id="d4a1f-115">hello Azure Authenticator 앱 작동 하지만 toomove toohello 새 Microsoft Authenticator 앱을 결정 한 경우이 문서는 고객을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-115">hello Azure Authenticator app still works, but if you decide toomove toohello new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="opt-in-for-two-step-verification"></a><span data-ttu-id="d4a1f-116">2단계 인증에 옵트인</span><span class="sxs-lookup"><span data-stu-id="d4a1f-116">Opt in for two-step verification</span></span>

<span data-ttu-id="d4a1f-117">hello Microsoft Authenticator 앱은 자체적으로 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-117">hello Microsoft Authenticator app doesn't work by itself.</span></span> <span data-ttu-id="d4a1f-118">각 사용자 이름 및 암호를 사용 하 여 로그인 한 후 두 번째 확인 방법에 대 한 하 여 계정 tooprompt를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-118">Configure each of your accounts tooprompt you for a second verification method after you sign in with your username and password.</span></span> 

<span data-ttu-id="d4a1f-119">회사 또는 학교 계정에 대 한 일반적으로 얻지 toochoose이이 기능은 자신에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-119">For a work or school account, you don't usually get toochoose this feature for yourself.</span></span> <span data-ttu-id="d4a1f-120">대신 보안 관리자가 사용자 대신 옵트인 하 고를 다음 계정에 대해 tooregister 확인 방법을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-120">Instead, a security administrator opts in on your behalf and then notifies you tooregister verification methods for your account.</span></span> <span data-ttu-id="d4a1f-121">이 시나리오에 tooyou 적용 되는 경우에서 자세한 내용을 [무엇 Azure Multi-factor Authentication을 의미 합니까 내](multi-factor-authentication-end-user.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-121">If this scenario applies tooyou, learn more in [What does Azure Multi-Factor Authentication mean for me](multi-factor-authentication-end-user.md).</span></span>

<span data-ttu-id="d4a1f-122">개인 계정으로 자신에 대 한 2 단계 확인을 tooset이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-122">For a personal account, you need tooset up two-step verification for yourself.</span></span> <span data-ttu-id="d4a1f-123">Microsoft 계정이 있는 경우 이러한 단계는 [2단계 인증 정보](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-123">If you have a Microsoft account, those steps are available in [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span> 

<span data-ttu-id="d4a1f-124">또한 Microsoft가 아닌 타사 계정으로 Microsoft Authenticator hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-124">You can also use hello Microsoft Authenticator with non-Microsoft accounts.</span></span> <span data-ttu-id="d4a1f-125">Hello 기능 이외의 노드 2 단계 인증 호출 수 있지만 수 toofind 있어야 보안 또는 로그인 설정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-125">They may call hello feature something other than two-step verification, but you should be able toofind it under security or sign-in settings.</span></span> 

## <a name="install-hello-app"></a><span data-ttu-id="d4a1f-126">Hello 앱 설치</span><span class="sxs-lookup"><span data-stu-id="d4a1f-126">Install hello app</span></span>
<span data-ttu-id="d4a1f-127">hello Microsoft Authenticator 앱에 사용할 수 있는 [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), 및 [iOS](http://go.microsoft.com/fwlink/?Linkid=825073)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-127">hello Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-toohello-app"></a><span data-ttu-id="d4a1f-128">계정을 toohello 앱 추가</span><span class="sxs-lookup"><span data-stu-id="d4a1f-128">Add accounts toohello app</span></span>
<span data-ttu-id="d4a1f-129">Tooadd toohello Microsoft Authenticator 앱을 지정 하는 각 계정에 대해 다음 절차를 수행 하는 hello 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-129">For each account that you want tooadd toohello Microsoft Authenticator app, use one of hello following procedures:</span></span>

### <a name="add-a-personal-microsoft-account-toohello-app"></a><span data-ttu-id="d4a1f-130">개인 Microsoft 계정 toohello 앱 추가</span><span class="sxs-lookup"><span data-stu-id="d4a1f-130">Add a personal Microsoft account toohello app</span></span>

<span data-ttu-id="d4a1f-131">개인 Microsoft 계정에 대 한 (하나 toosign를 사용 하는 등의 tooOutlook.com, Xbox, Skype,), 하면 toodo 됩니다 tooyour 계정 hello Microsoft Authenticator 앱에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-131">For a personal Microsoft account (one that you use toosign in tooOutlook.com, Xbox, Skype, etc.), all you have toodo is sign in tooyour account in hello Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a><span data-ttu-id="d4a1f-132">작업을 추가 또는 학교 계정 toohello hello QR 코드 스캐너를 사용 하 여 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d4a1f-132">Add a work or school account toohello app using hello QR code scanner</span></span>
1. <span data-ttu-id="d4a1f-133">Toohello 보안 확인 설정 화면을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-133">Go toohello security verification settings screen.</span></span>  <span data-ttu-id="d4a1f-134">방법에 대 한 내용은 tooget toothis 화면 참조 [보안 설정 변경](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-134">For information on how tooget toothis screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="d4a1f-135">확인란 hello 다음 너무**Authenticator 앱** 다음 선택 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-135">Check hello box next too**Authenticator app** then select **Configure**.</span></span>

    ![hello 보안 확인 설정 화면에 hello 구성 단추](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="d4a1f-137">QR 코드가 있는 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-137">This brings up a screen with a QR code on it.</span></span>

    ![Hello QR 코드를 제공 하는 화면](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="d4a1f-139">열기 hello Microsoft Authenticator 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-139">Open hello Microsoft Authenticator app.</span></span> <span data-ttu-id="d4a1f-140">Hello에 **계정** 화면에서  **+** , 한 다음 회사 또는 학교 계정 tooadd 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-140">On hello **accounts** screen, select **+**, and then specify that you want tooadd a work or school account.</span></span>
4. <span data-ttu-id="d4a1f-141">Hello 카메라 tooscan hello QR 코드를 사용 하 여 선택한 후 **수행** tooclose hello QR 코드 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-141">Use hello camera tooscan hello QR code, and then select **Done** tooclose hello QR code screen.</span></span>

    <span data-ttu-id="d4a1f-142">카메라 제대로 작동 하지 않는 경우 다음을 할 수 있습니다 [hello QR 코드와 URL을 수동으로 입력](#add-an-account-to-the-app-manually)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-142">If your camera is not working properly, you can [enter hello QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="d4a1f-143">Hello 응용 프로그램 아래에 6 자리 코드를 사용자 계정 이름에 표시 될 경우 작업이 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-143">When hello app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![계정 화면](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a><span data-ttu-id="d4a1f-145">계정 toohello 응용 프로그램을 수동으로 추가</span><span class="sxs-lookup"><span data-stu-id="d4a1f-145">Add an account toohello app manually</span></span>
1. <span data-ttu-id="d4a1f-146">Toohello 보안 확인 설정 화면을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-146">Go toohello security verification settings screen.</span></span>  <span data-ttu-id="d4a1f-147">방법에 대 한 내용은 tooget toothis 화면 참조 [보안 설정 변경](multi-factor-authentication-end-user-manage-settings.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-147">For information on how tooget toothis screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="d4a1f-148">**구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-148">Select **Configure**.</span></span>

    ![hello 보안 확인 설정 화면에 hello 구성 단추](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="d4a1f-150">QR 코드가 있는 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-150">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="d4a1f-151">참고 hello 코드와 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-151">Note hello code and URL.</span></span>

    ![Hello QR 코드와 URL을 제공 하는 화면](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="d4a1f-153">열기 hello Microsoft Authenticator 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-153">Open hello Microsoft Authenticator app.</span></span> <span data-ttu-id="d4a1f-154">Hello에 **계정** 화면에서  **+** , 한 다음 회사 또는 학교 계정 tooadd 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-154">On hello **accounts** screen, select **+**, and then specify that you want tooadd a work or school account.</span></span>

4. <span data-ttu-id="d4a1f-155">Hello 스캐너에서 선택 **코드를 수동으로 입력**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-155">In hello scanner, select **enter code manually**.</span></span>

    ![QR 코드를 스캔하는 화면](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="d4a1f-157">Hello 코드와 URL hello hello hello 응용 프로그램에서 해당 상자에 입력 한 다음 선택 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-157">Enter hello code and hello URL in hello appropriate boxes in hello app, then select **Finish**.</span></span>

    ![코드와 URL을 입력하기 위한 화면](./media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="d4a1f-159">Hello 응용 프로그램 아래에 6 자리 코드를 사용자 계정 이름에 표시 될 경우 작업이 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-159">When hello app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![계정 화면](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a><span data-ttu-id="d4a1f-161">Touch ID를 사용 하 여 계정 toohello 앱 추가</span><span class="sxs-lookup"><span data-stu-id="d4a1f-161">Add an account toohello app using Touch ID</span></span>
<span data-ttu-id="d4a1f-162">iOS에서 hello Microsoft Authenticator 앱이 터치 ID 지원</span><span class="sxs-lookup"><span data-stu-id="d4a1f-162">hello Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="d4a1f-163">Azure Multi-factor Authentication 조직 toorequire 장치에 대 한 PIN을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-163">Azure Multi-Factor Authentication allows organizations toorequire a PIN for devices.</span></span> <span data-ttu-id="d4a1f-164">Touch ID로, iOS 사용자는 PIN tooenter가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-164">With Touch ID, iOS users don’t need tooenter a PIN.</span></span> <span data-ttu-id="d4a1f-165">대신 지문을 스캔하고 **승인**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-165">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="d4a1f-166">Microsoft Authenticator를 통한 Touch ID 설정은 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-166">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="d4a1f-167">PIN을 사용하여 일반 확인 인증을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-167">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="d4a1f-168">장치에서 Touch ID를 지원하는 경우 Microsoft Authenticator는 자동으로 해당 계정에 대해 Touch ID를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-168">If your device supports Touch ID, Microsoft Authenticator sets it up automatically for that account.</span></span>

![Touch ID 설정 확인](./media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="d4a1f-170">때부터 앞으로 이동 했으면 사용자 로그인을 tooverify 필요한 푸시 알림을 수신 하는 hello를 선택 하 고 PIN을 입력 하는 대신 지문을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-170">From that point forward, when you're required tooverify your sign-in, you select hello received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![푸시 알림](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a><span data-ttu-id="d4a1f-172">에 로그인 할 때 사용 하 여 hello 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d4a1f-172">Use hello app when you sign in</span></span>

<span data-ttu-id="d4a1f-173">계정 toohello 응용 프로그램에 추가 되 면 모든 항목이 올바르게 구성 되어 있는지 테스트 확인 toomake 증명된 toodo 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-173">Once your account is added toohello app, you may be prompted toodo a test verification toomake sure everything was configured correctly.</span></span> <span data-ttu-id="d4a1f-174">그런 다음 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-174">After that, you're done!</span></span> <span data-ttu-id="d4a1f-175">않아도 toodo 다른 항목이 hello 다음 번에 로그인 할 때까지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-175">You don't need toodo anything else until hello next time you sign in.</span></span>

<span data-ttu-id="d4a1f-176">Toosee 시작 hello 응용 프로그램에서 확인 코드 toouse 했다면 hello 홈 페이지에서.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-176">If you chose toouse verification codes in hello app, you start toosee them on hello home page.</span></span> <span data-ttu-id="d4a1f-177">필요한 경우에 항상 새 코드를 갖도록 30초마다 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-177">They change every 30 seconds so that you always have a new code when you need one.</span></span> <span data-ttu-id="d4a1f-178">하지만 필요는 없습니다 toodo 아무것도에 로그인 하 고 확인 코드 입력 정보 요청된 tooenter 됩니다 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a1f-178">But you don't need toodo anything with them until you sign in and are prompted tooenter a verification code.</span></span>  
