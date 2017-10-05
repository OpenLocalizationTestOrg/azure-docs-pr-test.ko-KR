---
title: "StorSimple 8000 시리즈용 지원 티켓 또는 사례 만들기 | Microsoft 문서"
description: "StorSimple 8000 시리즈 장치에서 지원 요청을 로깅하고 지원 세션을 시작하는 방법을 알아봅니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: alkohli;
ms.openlocfilehash: 4b5a14237ce79100f980b2186b2c3c887abaa296
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="contact-microsoft-support"></a><span data-ttu-id="f6ba3-103">Microsoft 지원에 문의</span><span class="sxs-lookup"><span data-stu-id="f6ba3-103">Contact Microsoft Support</span></span>

<span data-ttu-id="f6ba3-104">StorSimple 장치 관리자는 서비스 요약 블레이드 내에서 **새로운 지원 요청을 기록**하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-104">The StorSimple Device Manager provides the capability to **log a new support request** within the service summary blade.</span></span> <span data-ttu-id="f6ba3-105">StorSimple 솔루션에 문제가 발생하는 경우 기술 지원을 위해 서비스 요청을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-105">If you encounter any issues with your StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="f6ba3-106">지원 엔지니어와 함께 온라인 세션에서 StorSimple 장치에 지원 세션을 시작해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-106">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="f6ba3-107">이 문서에서는 다음을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-107">This article walks you through:</span></span>

* <span data-ttu-id="f6ba3-108">지원 요청을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f6ba3-108">How to create a support request.</span></span>
* <span data-ttu-id="f6ba3-109">포털 내에서 지원 요청 주기를 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f6ba3-109">How to manage a support request lifecycle from within the portal.</span></span>
* <span data-ttu-id="f6ba3-110">StorSimple 장치의 Windows PowerShell 인터페이스에서 지원 세션을 시작하는 방법</span><span class="sxs-lookup"><span data-stu-id="f6ba3-110">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="f6ba3-111">지원 요청을 만들기 전에 [StorSimple 8000 시리즈 지원 SLA 및 정보](https://msdn.microsoft.com/library/mt433077.aspx) 를 검토하십시오.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-111">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="f6ba3-112">지원 요청 만들기</span><span class="sxs-lookup"><span data-stu-id="f6ba3-112">Create a support request</span></span>

<span data-ttu-id="f6ba3-113">[지원 계획](https://azure.microsoft.com/support/plans/)에 따라 StorSimple 장치 관리자 서비스 요약 블레이드에서 직접 StorSimple 장치 문제에 대한 지원 티켓을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-113">Depending upon your [support plan](https://azure.microsoft.com/support/plans/), you can create support tickets for an issue on your StorSimple device directly from the StorSimple Device Manager service summary blade.</span></span> <span data-ttu-id="f6ba3-114">지원 요청을 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-114">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="f6ba3-115">지원 요청을 만들려면</span><span class="sxs-lookup"><span data-stu-id="f6ba3-115">To create a support request</span></span>

1. <span data-ttu-id="f6ba3-116">StorSimple 장치 관리자 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-116">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="f6ba3-117">서비스 요약 블레이드 설정에서 **지원 + 문제 해결** 섹션으로 이동한 다음 **새 지원 요청**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-117">In the service summary blade settings, go to **SUPPORT + TROUBLESHOOTING** section and then click **New support request**.</span></span>
     
    ![새 포털을 통한 MS 지원 문의](./media/storsimple-8000-contact-microsoft-support/contactsupport1.png)
   
2. <span data-ttu-id="f6ba3-119">**새 지원 요청 블레이드**에서 **기본**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-119">In the **New support request** blade, select **Basics**.</span></span> <span data-ttu-id="f6ba3-120">**기본** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-120">In the **Basics** blade, do the following steps:</span></span>
   1. <span data-ttu-id="f6ba3-121">**문제점 유형** 드롭다운 목록에서 **기술**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="f6ba3-122">현재 **구독**, **서비스** 유형 및 **리소스**(StorSimple 장치 관리자 서비스)가 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-122">The current **Subscription**, **Service** type, and the **Resource** (StorSimple Device Manager service) are automatically chosen.</span></span> 
   3. <span data-ttu-id="f6ba3-123">구독과 관련된 여러 계획이 있는 경우 드롭다운에서 **지원 계획**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-123">Select a **Support plan** from the drop-down list if you have multiple plans associated with your subscription.</span></span> <span data-ttu-id="f6ba3-124">기술 지원을 사용하도록 설정하기 위해 유료 지원 계획이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-124">You need a paid support plan to enable Technical Support.</span></span>
   4. <span data-ttu-id="f6ba3-125">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-125">Click **Next**.</span></span>

       ![새 포털을 통한 MS 지원 문의](./media/storsimple-8000-contact-microsoft-support/contactsupport2.png)

3. <span data-ttu-id="f6ba3-127">**새 지원 요청** 블레이드에서 **2단계 문제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-127">In the **New support request** blade, select **Step 2 Problem**.</span></span> <span data-ttu-id="f6ba3-128">**문제** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-128">In the **Problem** blade, do the following steps:</span></span>
    
    1. <span data-ttu-id="f6ba3-129">**심각도**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-129">Choose the **Severity**.</span></span>
    2. <span data-ttu-id="f6ba3-130">문제가 어플라이언스 또는 StorSimple 장치 관리자 서비스에 관련되어 있는지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-130">Specify if the issue is related to the appliance or the StorSimple Device Manager service.</span></span>
    3. <span data-ttu-id="f6ba3-131">이 문제의 **범주**를 선택하고 문제에 대한 추가 **세부 정보**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-131">Choose a **Category** for this issue and provide more **Details** about the issue.</span></span>
    4. <span data-ttu-id="f6ba3-132">문제의 시작 날짜 및 시간을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-132">Provide the start date and time for the problem.</span></span>
    5. <span data-ttu-id="f6ba3-133">**파일 업로드**에서 폴더 아이콘을 클릭하여 지원 패키지를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-133">In the **File upload**, click the folder icon to browse to your support package.</span></span>
    6. <span data-ttu-id="f6ba3-134">**진단 정보 공유**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-134">Check **Share diagnostic information**.</span></span>
    7. <span data-ttu-id="f6ba3-135">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-135">Click **Next**.</span></span>

       ![새 포털을 통한 MS 지원 문의](./media/storsimple-8000-contact-microsoft-support/contactsupport3.png) 

4. <span data-ttu-id="f6ba3-137">**새 지원 요청** 블레이드에서 **3단계 연락처 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-137">In the **New support request** blade, click **Step 3 Contact information**.</span></span> <span data-ttu-id="f6ba3-138">**연락처 정보** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-138">In the **Contact information** blade, do the following steps:</span></span>

    1. <span data-ttu-id="f6ba3-139">**연락처 옵션**에서 기본 연락 방법(전화 또는 전자 메일) 및 언어를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-139">In the **Contact options**, provide your preferred contact method (phone or email) and the language.</span></span> <span data-ttu-id="f6ba3-140">응답 시간은 구독 계획에 따라 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-140">The response time is automatically selected based on your subscription plan.</span></span>
    2. <span data-ttu-id="f6ba3-141">연락처 정보에 이름, 전자 메일, 선택적 연락처, 국가를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-141">In the Contact information, provide your name, email, optional contact, country.</span></span> <span data-ttu-id="f6ba3-142">**향후 지원 요청에 대한 연락처 변경 내용 저장** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-142">Select the **Save contact changes for future support requests** check box.</span></span>
    3. <span data-ttu-id="f6ba3-143">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-143">Click **Create**.</span></span>
   
        ![새 포털을 통한 MS 지원 문의](./media/storsimple-8000-contact-microsoft-support/contactsupport5.png)   

    <span data-ttu-id="f6ba3-145">Microsoft 기술 지원 서비스는 이 정보를 사용하여 사용자에게 추가 정보, 진단 및 솔루션을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-145">Microsoft Support will use this information to reach out to you for further information, diagnosis, and resolution.</span></span>
<span data-ttu-id="f6ba3-146">요청을 제출한 후에 지원 엔지니어가 요청을 계속 진행하기 위해 가능한 한 빨리 연락할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-146">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="manage-a-support-request"></a><span data-ttu-id="f6ba3-147">지원 요청 관리</span><span class="sxs-lookup"><span data-stu-id="f6ba3-147">Manage a support request</span></span>

<span data-ttu-id="f6ba3-148">지원 티켓을 만든 후에는 포털 내에서 티켓의 수명 주기를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-148">After creating a support ticket, you can manage the lifecycle of the ticket from within the portal.</span></span>

#### <a name="to-manage-your-support-requests"></a><span data-ttu-id="f6ba3-149">지원 요청을 관리하려면</span><span class="sxs-lookup"><span data-stu-id="f6ba3-149">To manage your support requests</span></span>

1. <span data-ttu-id="f6ba3-150">도움말 및 지원 페이지로 이동하려면 **찾아보기 > 도움말 + 지원**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-150">To get to the help and support page, navigate to **Browse > Help + support**.</span></span>

    ![지원 요청 관리](./media/storsimple-8000-contact-microsoft-support/managesupport1.png)

2. <span data-ttu-id="f6ba3-152">모든 지원 요청을 표시하는 테이블이 **도움말 + 지원** 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-152">A tabular listing of All the support requests is displayed in the **Help + support** blade.</span></span>

    ![지원 요청 관리](./media/storsimple-8000-contact-microsoft-support/managesupport2.png)

3. <span data-ttu-id="f6ba3-154">지원 요청을 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-154">Select and click a support request.</span></span> <span data-ttu-id="f6ba3-155">이 요청의 상태 및 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-155">You can view the status and the details for this request.</span></span> <span data-ttu-id="f6ba3-156">이 요청에 대해 후속 작업을 수행하려는 경우 **+ 새 메시지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-156">Click **+ New message** if you want to follow up on this request.</span></span>

    ![지원 요청 관리](./media/storsimple-8000-contact-microsoft-support/managesupport3.png)

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="f6ba3-158">StorSimple용 Windows PowerShell에서 지원 세션 시작</span><span class="sxs-lookup"><span data-stu-id="f6ba3-158">Start a support session in Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="f6ba3-159">StorSimple 장치에서 발생할 수 있는 문제를 해결하려면 Microsoft 기술 지원 서비스 팀과 연계해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-159">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="f6ba3-160">Microsoft 기술 지원 서비스 팀은 장치에 로그온하기 위해 지원 세션을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-160">Microsoft Support may need to use a support session to log on to your device.</span></span>

<span data-ttu-id="f6ba3-161">지원 세션을 시작하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-161">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="f6ba3-162">지원 세션을 시작하려면</span><span class="sxs-lookup"><span data-stu-id="f6ba3-162">To start a support session</span></span>

1. <span data-ttu-id="f6ba3-163">직렬 콘솔을 사용하여 직접 또는 원격 컴퓨터에서 텔넷 세션을 통해 장치에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-163">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="f6ba3-164">이렇게 하려면 [PuTTY를 사용하여 장치 직렬 콘솔에 연결](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-164">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="f6ba3-165">열린 세션에서 **Enter** 키를 눌러 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-165">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="f6ba3-166">직렬 콘솔 메뉴에서 옵션 1, **모든 권한으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-166">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="f6ba3-167">프롬프트에 다음 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-167">At the prompt, type the following password:</span></span>
   
    `Password1`
5. <span data-ttu-id="f6ba3-168">프롬프트에 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-168">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="f6ba3-169">암호화된 문자열을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-169">An encrypted string will be presented to you.</span></span> <span data-ttu-id="f6ba3-170">메모장과 같은 텍스트 편집기에 이 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-170">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="f6ba3-171">이 문자열을 저장하고 Microsoft 기술 지원 서비스에 전자 메일 메시지로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-171">Save this string and send it in an email message to Microsoft Support.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6ba3-172">`Disable-HcsSupportAccess`를 실행하여 지원 액세스를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-172">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="f6ba3-173">StorSimple 장치는 세션이 시작된 8시간 후에 지원 액세스를 비활성화하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-173">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="f6ba3-174">지원 세션을 시작한 후에 StorSimple 장치 자격 증명을 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba3-174">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f6ba3-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6ba3-175">Next steps</span></span>

<span data-ttu-id="f6ba3-176">[StorSimple 8000 시리즈 장치와 관련된 문제를 진단하고 해결](storsimple-troubleshoot-deployment.md)하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="f6ba3-176">Learn how to [diagnose and solve problems related to your StorSimple 8000 series device](storsimple-troubleshoot-deployment.md)</span></span>
