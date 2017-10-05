---
title: "휴대폰용 Microsoft Authenticator 앱 | Microsoft Docs"
description: "최신 버전의 Azure Authenticator로 업그레이드하는 방법에 알아봅니다."
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
ms.openlocfilehash: 6bcb6d9f7a1e9b241fa70690016b03d6eb5887ab
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-the-microsoft-authenticator-app"></a><span data-ttu-id="ecf93-103">Microsoft Authenticator 앱 시작</span><span class="sxs-lookup"><span data-stu-id="ecf93-103">Get started with the Microsoft Authenticator app</span></span>
<span data-ttu-id="ecf93-104">Microsoft Authenticator 앱은 회사 또는 학교 계정(예: bsimon@contoso.com) 또는 Microsoft 계정(예: bsimon@outlook.com)의 추가 보안 수준을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-104">The Microsoft Authenticator app provides an additional level of security in your work or school account (for example, bsimon@contoso.com) or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="ecf93-105">이 앱은 두 가지 방법 중 하나로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-105">The app works in one of two ways:</span></span>

* <span data-ttu-id="ecf93-106">**알림**.</span><span class="sxs-lookup"><span data-stu-id="ecf93-106">**Notification**.</span></span> <span data-ttu-id="ecf93-107">이 앱을 사용하면 스마트폰 또는 태블릿에 알림을 푸시하여 계정에 대한 무단 액세스를 방지하고 사기성 트랜잭션을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-107">The app can help prevent unauthorized access to accounts and stop fraudulent transactions by pushing a notification to your smartphone or tablet.</span></span> <span data-ttu-id="ecf93-108">알림을 확인한 후 올바르면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-108">Simply view the notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="ecf93-109">그렇지 않으면 **거부**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-109">Otherwise, you can select **Deny**.</span></span> 
* <span data-ttu-id="ecf93-110">**확인 코드**.</span><span class="sxs-lookup"><span data-stu-id="ecf93-110">**Verification code**.</span></span> <span data-ttu-id="ecf93-111">이 앱을 소프트웨어 토큰으로 사용하여 OATH 확인 코드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-111">The app can be used as a software token to generate an OAuth verification code.</span></span> <span data-ttu-id="ecf93-112">사용자 이름 및 암호를 입력한 후 앱에서 제공한 코드를 로그인 화면에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-112">After you enter your username and password, you enter the code provided by the app into the sign-in screen.</span></span> <span data-ttu-id="ecf93-113">확인 코드는 두 번째 인증 형식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-113">The verification code provides a second form of authentication.</span></span>

<span data-ttu-id="ecf93-114">Microsoft Authenticator 앱은 Azure Authenticator 앱을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-114">The Microsoft Authenticator app replaces the Azure Authenticator app.</span></span> <span data-ttu-id="ecf93-115">Azure Authenticator 앱은 여전히 작동하지만 새 Microsoft Authenticator 앱으로 전환할 것인지 결정해야 하며 이 문서에서 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-115">The Azure Authenticator app still works, but if you decide to move to the new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="opt-in-for-two-step-verification"></a><span data-ttu-id="ecf93-116">2단계 인증에 옵트인</span><span class="sxs-lookup"><span data-stu-id="ecf93-116">Opt in for two-step verification</span></span>

<span data-ttu-id="ecf93-117">Microsoft Authenticator 앱은 자체적으로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-117">The Microsoft Authenticator app doesn't work by itself.</span></span> <span data-ttu-id="ecf93-118">사용자 이름 및 암호로 로그인한 후 두 번째 확인 방법에 대해 묻도록 각 계정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-118">Configure each of your accounts to prompt you for a second verification method after you sign in with your username and password.</span></span> 

<span data-ttu-id="ecf93-119">회사 또는 학교 계정의 경우 일반적으로 이 기능에 대해 선택하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-119">For a work or school account, you don't usually get to choose this feature for yourself.</span></span> <span data-ttu-id="ecf93-120">대신 보안 관리자는 사용자를 대신해서 옵트인한 다음 계정에 대해 확인 메서드를 등록하라고 알립니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-120">Instead, a security administrator opts in on your behalf and then notifies you to register verification methods for your account.</span></span> <span data-ttu-id="ecf93-121">이 시나리오에 해당하는 경우 [Azure Multi-Factor Authentication은 무엇을 의미하나요](multi-factor-authentication-end-user.md)에서 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-121">If this scenario applies to you, learn more in [What does Azure Multi-Factor Authentication mean for me](multi-factor-authentication-end-user.md).</span></span>

<span data-ttu-id="ecf93-122">개인 계정의 경우 2단계 인증을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-122">For a personal account, you need to set up two-step verification for yourself.</span></span> <span data-ttu-id="ecf93-123">Microsoft 계정이 있는 경우 이러한 단계는 [2단계 인증 정보](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-123">If you have a Microsoft account, those steps are available in [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span> 

<span data-ttu-id="ecf93-124">또한 Microsoft가 아닌 계정으로 Microsoft Authenticator를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-124">You can also use the Microsoft Authenticator with non-Microsoft accounts.</span></span> <span data-ttu-id="ecf93-125">2단계 인증 이외의 기능을 호출할 수 있지만 보안 또는 로그인 설정에서 찾을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-125">They may call the feature something other than two-step verification, but you should be able to find it under security or sign-in settings.</span></span> 

## <a name="install-the-app"></a><span data-ttu-id="ecf93-126">앱 설치</span><span class="sxs-lookup"><span data-stu-id="ecf93-126">Install the app</span></span>
<span data-ttu-id="ecf93-127">[Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072) 및 [iOS](http://go.microsoft.com/fwlink/?Linkid=825073) 장치의 경우 Microsoft Authenticator 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-127">The Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-to-the-app"></a><span data-ttu-id="ecf93-128">앱에 계정 추가</span><span class="sxs-lookup"><span data-stu-id="ecf93-128">Add accounts to the app</span></span>
<span data-ttu-id="ecf93-129">Microsoft Authenticator 앱에 추가하려는 각 계정에 대해 다음 절차 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-129">For each account that you want to add to the Microsoft Authenticator app, use one of the following procedures:</span></span>

### <a name="add-a-personal-microsoft-account-to-the-app"></a><span data-ttu-id="ecf93-130">앱에 개인 Microsoft 계정 추가</span><span class="sxs-lookup"><span data-stu-id="ecf93-130">Add a personal Microsoft account to the app</span></span>

<span data-ttu-id="ecf93-131">개인 Microsoft 계정(Outlook.com, Xbox, Skype 등에 로그인하는 데 사용하는 계정)의 경우, Microsoft Authenticator 앱의 사용자 계정에 로그인하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-131">For a personal Microsoft account (one that you use to sign in to Outlook.com, Xbox, Skype, etc.), all you have to do is sign in to your account in the Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-to-the-app-using-the-qr-code-scanner"></a><span data-ttu-id="ecf93-132">QR 코드 스캐너를 사용하여 앱에 회사 또는 학교 계정 추가</span><span class="sxs-lookup"><span data-stu-id="ecf93-132">Add a work or school account to the app using the QR code scanner</span></span>
1. <span data-ttu-id="ecf93-133">보안 확인 설정 화면으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-133">Go to the security verification settings screen.</span></span>  <span data-ttu-id="ecf93-134">이 화면으로 이동하는 방법은 [보안 설정 변경](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecf93-134">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="ecf93-135">**Authenticator 앱** 옆에 있는 확인란을 선택한 후 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-135">Check the box next to **Authenticator app** then select **Configure**.</span></span>

    ![보안 확인 설정 화면의 구성 단추](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="ecf93-137">QR 코드가 있는 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-137">This brings up a screen with a QR code on it.</span></span>

    ![QR 코드를 제공하는 화면](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="ecf93-139">Microsoft Authenticator 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-139">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="ecf93-140">**계정** 화면에서 **+**를 선택한 다음 회사 또는 학교 계정을 추가할지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-140">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>
4. <span data-ttu-id="ecf93-141">카메라를 사용하여 QR 코드를 스캔한 다음 **완료** 를 선택하여 QR 코드 화면을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-141">Use the camera to scan the QR code, and then select **Done** to close the QR code screen.</span></span>

    <span data-ttu-id="ecf93-142">카메라가 올바르게 작동하지 않으면 [QR 코드 및 URL을 수동](#add-an-account-to-the-app-manually)으로 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-142">If your camera is not working properly, you can [enter the QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="ecf93-143">앱에 그 아래 6자리 코드가 있는 계정 이름이 표시되면 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-143">When the app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![계정 화면](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-manually"></a><span data-ttu-id="ecf93-145">앱에 수동으로 계정 추가</span><span class="sxs-lookup"><span data-stu-id="ecf93-145">Add an account to the app manually</span></span>
1. <span data-ttu-id="ecf93-146">보안 확인 설정 화면으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-146">Go to the security verification settings screen.</span></span>  <span data-ttu-id="ecf93-147">이 화면으로 이동하는 방법은 [보안 설정 변경](multi-factor-authentication-end-user-manage-settings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecf93-147">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="ecf93-148">**구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-148">Select **Configure**.</span></span>

    ![보안 확인 설정 화면의 구성 단추](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="ecf93-150">QR 코드가 있는 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-150">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="ecf93-151">코드와 URL을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-151">Note the code and URL.</span></span>

    ![QR 코드와 URL을 제공하는 화면](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="ecf93-153">Microsoft Authenticator 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-153">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="ecf93-154">**계정** 화면에서 **+**를 선택한 다음 회사 또는 학교 계정을 추가할지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-154">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>

4. <span data-ttu-id="ecf93-155">스캐너에서 **수동으로 코드 입력**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-155">In the scanner, select **enter code manually**.</span></span>

    ![QR 코드를 스캔하는 화면](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="ecf93-157">앱에서 해당 상자에 코드와 URL을 입력한 후 **마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-157">Enter the code and the URL in the appropriate boxes in the app, then select **Finish**.</span></span>

    ![코드와 URL을 입력하기 위한 화면](./media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="ecf93-159">앱에 그 아래 6자리 코드가 있는 계정 이름이 표시되면 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-159">When the app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![계정 화면](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-using-touch-id"></a><span data-ttu-id="ecf93-161">Touch ID를 사용하여 앱에 계정 추가</span><span class="sxs-lookup"><span data-stu-id="ecf93-161">Add an account to the app using Touch ID</span></span>
<span data-ttu-id="ecf93-162">IOS의 Microsoft Authenticator 앱은 Touch ID를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-162">The Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="ecf93-163">Azure Multi-Factor Authentication을 사용하면 조직에서 장치에 대해 PIN을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-163">Azure Multi-Factor Authentication allows organizations to require a PIN for devices.</span></span> <span data-ttu-id="ecf93-164">Touch ID를 사용할 경우 iOS 사용자는 PIN을 입력할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-164">With Touch ID, iOS users don’t need to enter a PIN.</span></span> <span data-ttu-id="ecf93-165">대신 지문을 스캔하고 **승인**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-165">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="ecf93-166">Microsoft Authenticator를 통한 Touch ID 설정은 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-166">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="ecf93-167">PIN을 사용하여 일반 확인 인증을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-167">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="ecf93-168">장치에서 Touch ID를 지원하는 경우 Microsoft Authenticator는 자동으로 해당 계정에 대해 Touch ID를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-168">If your device supports Touch ID, Microsoft Authenticator sets it up automatically for that account.</span></span>

![Touch ID 설정 확인](./media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="ecf93-170">해당 위치 다음부터 로그인 확인이 필요한 경우 받은 푸시 알림을 선택하고 PIN을 입력하는 대신 지문을 스캔합니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-170">From that point forward, when you're required to verify your sign-in, you select the received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![푸시 알림](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-the-app-when-you-sign-in"></a><span data-ttu-id="ecf93-172">로그인할 때 앱 사용</span><span class="sxs-lookup"><span data-stu-id="ecf93-172">Use the app when you sign in</span></span>

<span data-ttu-id="ecf93-173">앱에 계정이 추가되면 모두 제대로 구성되었는지 확인하는 테스트 확인을 수행하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-173">Once your account is added to the app, you may be prompted to do a test verification to make sure everything was configured correctly.</span></span> <span data-ttu-id="ecf93-174">그런 다음 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-174">After that, you're done!</span></span> <span data-ttu-id="ecf93-175">다음에 로그인할 때까지 다른 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-175">You don't need to do anything else until the next time you sign in.</span></span>

<span data-ttu-id="ecf93-176">앱에서 확인 코드를 사용하도록 선택한 경우 홈페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-176">If you chose to use verification codes in the app, you start to see them on the home page.</span></span> <span data-ttu-id="ecf93-177">필요한 경우에 항상 새 코드를 갖도록 30초마다 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-177">They change every 30 seconds so that you always have a new code when you need one.</span></span> <span data-ttu-id="ecf93-178">하지만 로그인하고 확인 코드를 입력하라는 메시지가 나타날 때까지 아무것도 할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ecf93-178">But you don't need to do anything with them until you sign in and are prompted to enter a verification code.</span></span>  