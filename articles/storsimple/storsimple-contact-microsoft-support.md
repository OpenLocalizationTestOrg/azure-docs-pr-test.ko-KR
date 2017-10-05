---
title: "StorSimple 8000 시리즈에 대한 지원 티켓 로그 | Microsoft Docs"
description: "StorSimple 장치에서 지원 요청을 만들고 지원 세션을 시작하는 방법을 알아봅니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cecc2566b432e897b5eff0c12e66598f0518ed80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="7909c-103">StorSimple의 Microsoft 지원에 문의</span><span class="sxs-lookup"><span data-stu-id="7909c-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="7909c-104">Microsoft Azure StorSimple 솔루션에 문제가 발생하는 경우 기술 지원을 위해 서비스 요청을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="7909c-105">지원 엔지니어와 함께 온라인 세션에서 StorSimple 장치에 지원 세션을 시작해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-105">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="7909c-106">이 문서에서는 다음을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-106">This article walks you through:</span></span>

* <span data-ttu-id="7909c-107">지원 요청을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="7909c-107">How to create a support request.</span></span>
* <span data-ttu-id="7909c-108">StorSimple 장치의 Windows PowerShell 인터페이스에서 지원 세션을 시작하는 방법</span><span class="sxs-lookup"><span data-stu-id="7909c-108">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="7909c-109">지원 요청을 만들기 전에 [StorSimple 8000 시리즈 지원 SLA 및 정보](https://msdn.microsoft.com/library/mt433077.aspx) 를 검토하십시오.</span><span class="sxs-lookup"><span data-stu-id="7909c-109">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="7909c-110">지원 요청 만들기</span><span class="sxs-lookup"><span data-stu-id="7909c-110">Create a support request</span></span>
<span data-ttu-id="7909c-111">지원 요청을 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-111">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="7909c-112">지원 요청을 만들려면</span><span class="sxs-lookup"><span data-stu-id="7909c-112">To create a support request</span></span>
1. <span data-ttu-id="7909c-113">[Azure 클래식 포털](https://manage.windowsazure.com/)의 오른쪽 위에서 계정 이름을 클릭한 다음 **Microsoft 지원에 문의**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-113">In the [Azure classic portal](https://manage.windowsazure.com/), in the upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![ManagementPortal을 통한 MS 지원 문의](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="7909c-115">새 Azure 포털(portal.azure.com)로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-115">You will be redirected to the new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="7909c-116">**새 지원 요청** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-116">Click the **New support request** tile.</span></span>
   
    ![새 포털을 통한 MS 지원 문의](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="7909c-118">화면의 오른쪽에 **새 지원 요청** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-118">On the right side of the screen, the **New support request** pane appears.</span></span> 
   
    ![새 지원 요청 창](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="7909c-120">**기본 사항** 대화 상자에서 다음을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-120">In the **Basics** dialog box, complete the following:</span></span>                                
   
   1. <span data-ttu-id="7909c-121">**문제점 유형** 드롭다운 목록에서 **기술**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="7909c-122">드롭다운 목록에서 **구독** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-122">Select a **Subscription** from the drop-down list.</span></span>
   3. <span data-ttu-id="7909c-123">**서비스** 드롭다운 목록에서 **StorSimple**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-123">From the **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="7909c-124">드롭다운 목록에서 **지원 계획** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-124">Select a **Support plan** from the drop-down list.</span></span> <span data-ttu-id="7909c-125">기술 지원을 사용하도록 설정하기 위해 유료 지원 계획이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-125">You need a paid support plan to enable Technical Support.</span></span>
4. <span data-ttu-id="7909c-126">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-126">Click **Next**.</span></span> <span data-ttu-id="7909c-127">**문제** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-127">The **Problem** dialog box appears.</span></span>
   
    ![새 지원 요청 창](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="7909c-129">**문제** 대화 상자에서 다음을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-129">In the **Problem** dialog box, complete the following:</span></span>
   
   1. <span data-ttu-id="7909c-130">드롭다운 목록에서 **심각도** 수준을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-130">Select a **Severity** level from the drop-down list.</span></span>
   2. <span data-ttu-id="7909c-131">드롭다운 목록에서 **문제 유형** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-131">Select a **Problem type** from the drop-down list.</span></span>
   3. <span data-ttu-id="7909c-132">드롭다운 목록에서 **범주** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-132">Select a **Category** from the drop-down list.</span></span> 
   4. <span data-ttu-id="7909c-133">**세부 정보** 상자에 문제를 간략히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-133">In the **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="7909c-134">**시간 프레임** 상자에서 가장 최근에 문제가 발생한 날짜, 시간 및 표준 시간대를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-134">In the **Time frame** box, indicate the date, time, and time zone that corresponds to the most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="7909c-135">**파일 업로드**에서 폴더 아이콘을 클릭하여 지원 패키지를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-135">Under **File upload**, click the folder icon to browse to your support package.</span></span>
   7. <span data-ttu-id="7909c-136">**진단 정보 공유** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-136">Select the **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="7909c-137">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-137">Click **Next**.</span></span> <span data-ttu-id="7909c-138">**연락처 정보** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-138">The **Contact information** dialog box appears.</span></span>
   
    ![새 지원 요청 창](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="7909c-140">연락처 정보를 입력하고 연락 방법(전화 또는 전자 메일)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="7909c-141">**향후 지원 요청에 대한 연락처 변경 내용 저장** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-141">Select the **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="7909c-142">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-142">Click **Create**.</span></span>

<span data-ttu-id="7909c-143">요청을 제출한 후에 지원 엔지니어가 요청을 계속 진행하기 위해 가능한 한 빨리 연락할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-143">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="7909c-144">StorSimple용 Windows PowerShell에서 지원 세션 시작</span><span class="sxs-lookup"><span data-stu-id="7909c-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="7909c-145">StorSimple 장치에서 발생할 수 있는 문제를 해결하려면 Microsoft 기술 지원 서비스 팀과 연계해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-145">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="7909c-146">Microsoft 기술 지원 서비스 팀은 장치에 로그온하기 위해 지원 세션을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-146">Microsoft Support may need to use a support session to log on to your device.</span></span> 

<span data-ttu-id="7909c-147">지원 세션을 시작하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-147">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="7909c-148">지원 세션을 시작하려면</span><span class="sxs-lookup"><span data-stu-id="7909c-148">To start a support session</span></span>
1. <span data-ttu-id="7909c-149">직렬 콘솔을 사용하여 직접 또는 원격 컴퓨터에서 텔넷 세션을 통해 장치에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-149">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="7909c-150">이렇게 하려면 [PuTTY를 사용하여 장치 직렬 콘솔에 연결](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="7909c-150">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="7909c-151">열린 세션에서 **Enter** 키를 눌러 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-151">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="7909c-152">직렬 콘솔 메뉴에서 옵션 1, **모든 권한으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-152">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="7909c-153">프롬프트에 다음 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-153">At the prompt, type the following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="7909c-154">프롬프트에 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-154">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="7909c-155">암호화된 문자열을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-155">An encrypted string will be presented to you.</span></span> <span data-ttu-id="7909c-156">메모장과 같은 텍스트 편집기에 이 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="7909c-157">이 문자열을 저장하고 Microsoft 기술 지원 서비스에 전자 메일 메시지로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-157">Save this string and send it in an email message to Microsoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7909c-158">`Disable-HcsSupportAccess`를 실행하여 지원 액세스를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="7909c-159">StorSimple 장치는 세션이 시작된 8시간 후에 지원 액세스를 비활성화하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-159">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="7909c-160">지원 세션을 시작한 후에 StorSimple 장치 자격 증명을 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7909c-160">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>
> 
> 

