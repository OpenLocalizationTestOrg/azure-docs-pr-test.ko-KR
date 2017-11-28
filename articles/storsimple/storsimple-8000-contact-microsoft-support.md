---
title: "aaaCreate 지원 티켓 또는 StorSimple 8000 시리즈에 대 한 경우 | Microsoft Docs"
description: "Toolog 요청을 지원 하는 방법을 알아보고 StorSimple 8000 시리즈 장치에서 지원 세션을 시작 합니다."
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
ms.openlocfilehash: 832e3ac739dafa6dd8c24aaea38aef9c6f1b27b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support"></a><span data-ttu-id="82939-103">Microsoft 지원에 문의</span><span class="sxs-lookup"><span data-stu-id="82939-103">Contact Microsoft Support</span></span>

<span data-ttu-id="82939-104">StorSimple 장치 관리자 hello 너무 hello 기능을 제공**새 지원 요청을 기록할** hello 서비스 요약 블레이드 내에서.</span><span class="sxs-lookup"><span data-stu-id="82939-104">hello StorSimple Device Manager provides hello capability too**log a new support request** within hello service summary blade.</span></span> <span data-ttu-id="82939-105">StorSimple 솔루션에 문제가 발생하는 경우 기술 지원을 위해 서비스 요청을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82939-105">If you encounter any issues with your StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="82939-106">지원 엔지니어와 온라인 세션에서 StorSimple 장치에서 지원 세션 toostart를 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82939-106">In an online session with your support engineer, you may also need toostart a support session on your StorSimple device.</span></span> <span data-ttu-id="82939-107">이 문서에서는 다음을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-107">This article walks you through:</span></span>

* <span data-ttu-id="82939-108">어떻게 toocreate 기술 지원 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-108">How toocreate a support request.</span></span>
* <span data-ttu-id="82939-109">어떻게 지원 toomanage hello 포털 내에서 주기를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-109">How toomanage a support request lifecycle from within hello portal.</span></span>
* <span data-ttu-id="82939-110">어떻게 지원 세션을 toostart hello StorSimple 장치의 Windows PowerShell 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="82939-110">How toostart a support session in hello Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="82939-111">검토 hello [StorSimple 8000 시리즈 지원 Sla 및 정보](https://msdn.microsoft.com/library/mt433077.aspx) 지원 요청을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-111">Review hello [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="82939-112">지원 요청 만들기</span><span class="sxs-lookup"><span data-stu-id="82939-112">Create a support request</span></span>

<span data-ttu-id="82939-113">에 따라 프로그램 [지원 플랜](https://azure.microsoft.com/support/plans/), 직접 hello StorSimple 장치 관리자 서비스에 대 한 요약 블레이드에에서 StorSimple 장치에는 문제에 대 한 지원 티켓을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82939-113">Depending upon your [support plan](https://azure.microsoft.com/support/plans/), you can create support tickets for an issue on your StorSimple device directly from hello StorSimple Device Manager service summary blade.</span></span> <span data-ttu-id="82939-114">Hello 단계 toocreate 지원 요청에 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-114">Perform hello following steps toocreate a support request:</span></span>

#### <a name="toocreate-a-support-request"></a><span data-ttu-id="82939-115">toocreate 지원 요청</span><span class="sxs-lookup"><span data-stu-id="82939-115">toocreate a support request</span></span>

1. <span data-ttu-id="82939-116">Tooyour StorSimple 장치 관리자 서비스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-116">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="82939-117">Hello 서비스 요약 블레이드 설정에서 이동 너무**지원 + 문제 해결** 섹션 및 클릭 **새로운 지원 요청**합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-117">In hello service summary blade settings, go too**SUPPORT + TROUBLESHOOTING** section and then click **New support request**.</span></span>
     
    ![새 포털을 통한 MS 지원 문의](./media/storsimple-8000-contact-microsoft-support/contactsupport1.png)
   
2. <span data-ttu-id="82939-119">Hello에 **새로운 지원 요청** 블레이드를 **기본 사항**합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-119">In hello **New support request** blade, select **Basics**.</span></span> <span data-ttu-id="82939-120">Hello에 **기본 사항** 블레이드에서 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82939-120">In hello **Basics** blade, do hello following steps:</span></span>
   1. <span data-ttu-id="82939-121">Hello에서 **종류를 발급** 드롭 다운 목록 **기술**합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-121">From hello **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="82939-122">현재 hello **구독**, **서비스** 유형과 hello **리소스** (StorSimple 장치 관리자 서비스)으로 자동 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82939-122">hello current **Subscription**, **Service** type, and hello **Resource** (StorSimple Device Manager service) are automatically chosen.</span></span> 
   3. <span data-ttu-id="82939-123">선택 된 **지원 플랜** 구독과 관련 계획이 여러 개인 경우 hello 드롭 다운 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-123">Select a **Support plan** from hello drop-down list if you have multiple plans associated with your subscription.</span></span> <span data-ttu-id="82939-124">기술 지원 서비스 유료 지원 계획이 tooenable가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-124">You need a paid support plan tooenable Technical Support.</span></span>
   4. <span data-ttu-id="82939-125">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="82939-125">Click **Next**.</span></span>

       ![새 포털을 통한 MS 지원 문의](./media/storsimple-8000-contact-microsoft-support/contactsupport2.png)

3. <span data-ttu-id="82939-127">Hello에 **새로운 지원 요청** 블레이드를 **단계 2 문제**합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-127">In hello **New support request** blade, select **Step 2 Problem**.</span></span> <span data-ttu-id="82939-128">Hello에 **문제** 블레이드에서 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82939-128">In hello **Problem** blade, do hello following steps:</span></span>
    
    1. <span data-ttu-id="82939-129">Hello 선택 **심각도**합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-129">Choose hello **Severity**.</span></span>
    2. <span data-ttu-id="82939-130">Hello 문제 관련된 toohello 어플라이언스 또는 hello StorSimple 장치 관리자 서비스를 지정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="82939-130">Specify if hello issue is related toohello appliance or hello StorSimple Device Manager service.</span></span>
    3. <span data-ttu-id="82939-131">선택 된 **범주** 이 발급 및 높아지며 **세부 정보** hello 문제에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-131">Choose a **Category** for this issue and provide more **Details** about hello issue.</span></span>
    4. <span data-ttu-id="82939-132">Hello 시작 날짜 및 hello 문제에 대 한 시간을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-132">Provide hello start date and time for hello problem.</span></span>
    5. <span data-ttu-id="82939-133">Hello에 **파일 업로드**, hello 폴더 아이콘 toobrowse tooyour 지원 패키지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-133">In hello **File upload**, click hello folder icon toobrowse tooyour support package.</span></span>
    6. <span data-ttu-id="82939-134">**진단 정보 공유**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-134">Check **Share diagnostic information**.</span></span>
    7. <span data-ttu-id="82939-135">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="82939-135">Click **Next**.</span></span>

       ![새 포털을 통한 MS 지원 문의](./media/storsimple-8000-contact-microsoft-support/contactsupport3.png) 

4. <span data-ttu-id="82939-137">Hello에 **새로운 지원 요청** 블레이드에서 클릭 **단계 3 연락처 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-137">In hello **New support request** blade, click **Step 3 Contact information**.</span></span> <span data-ttu-id="82939-138">Hello에 **연락처 정보** 블레이드에서 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82939-138">In hello **Contact information** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="82939-139">Hello에 **연락처 옵션**기본 연락 방법 (전화 또는 전자 메일)를 입력 하 여 hello 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="82939-139">In hello **Contact options**, provide your preferred contact method (phone or email) and hello language.</span></span> <span data-ttu-id="82939-140">hello 응답 시간 구독 계획에 따라 자동으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82939-140">hello response time is automatically selected based on your subscription plan.</span></span>
    2. <span data-ttu-id="82939-141">Hello 연락처 정보, 이름, 전자 메일, 선택적 연락처, 국가 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-141">In hello Contact information, provide your name, email, optional contact, country.</span></span> <span data-ttu-id="82939-142">선택 hello **이후 지원 요청에 대 한 연락처 변경 내용을 저장** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-142">Select hello **Save contact changes for future support requests** check box.</span></span>
    3. <span data-ttu-id="82939-143">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-143">Click **Create**.</span></span>
   
        ![새 포털을 통한 MS 지원 문의](./media/storsimple-8000-contact-microsoft-support/contactsupport5.png)   

    <span data-ttu-id="82939-145">자세한 내용은, 진단 및 해결에 대 한 Microsoft 지원 tooyou 아웃 정보 tooreach이를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-145">Microsoft Support will use this information tooreach out tooyou for further information, diagnosis, and resolution.</span></span>
<span data-ttu-id="82939-146">요청을 제출 하 고 나면 지원 엔지니어 연락을 드릴 가능한 한 빨리 tooproceed 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-146">After you have submitted your request, a Support engineer will contact you as soon as possible tooproceed with your request.</span></span>

## <a name="manage-a-support-request"></a><span data-ttu-id="82939-147">지원 요청 관리</span><span class="sxs-lookup"><span data-stu-id="82939-147">Manage a support request</span></span>

<span data-ttu-id="82939-148">지원 티켓을 만든 후 hello 포털 내에서 hello 티켓의 hello 수명 주기를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82939-148">After creating a support ticket, you can manage hello lifecycle of hello ticket from within hello portal.</span></span>

#### <a name="toomanage-your-support-requests"></a><span data-ttu-id="82939-149">toomanage 기술 지원 요청</span><span class="sxs-lookup"><span data-stu-id="82939-149">toomanage your support requests</span></span>

1. <span data-ttu-id="82939-150">도움말 및 지원 페이지, 탐색 너무 tooget toohello**찾아보기 > 도움말 + 지원**합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-150">tooget toohello help and support page, navigate too**Browse > Help + support**.</span></span>

    ![지원 요청 관리](./media/storsimple-8000-contact-microsoft-support/managesupport1.png)

2. <span data-ttu-id="82939-152">Hello에 표시 되는 모든 hello 지원의 테이블 형식 목록 요청 **도움말 + 지원** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="82939-152">A tabular listing of All hello support requests is displayed in hello **Help + support** blade.</span></span>

    ![지원 요청 관리](./media/storsimple-8000-contact-microsoft-support/managesupport2.png)

3. <span data-ttu-id="82939-154">지원 요청을 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-154">Select and click a support request.</span></span> <span data-ttu-id="82939-155">Hello 상태 및이 요청에 대 한 hello 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82939-155">You can view hello status and hello details for this request.</span></span> <span data-ttu-id="82939-156">클릭 **+ 새 메시지** 이 요청에를 toofollow 사용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="82939-156">Click **+ New message** if you want toofollow up on this request.</span></span>

    ![지원 요청 관리](./media/storsimple-8000-contact-microsoft-support/managesupport3.png)

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="82939-158">StorSimple용 Windows PowerShell에서 지원 세션 시작</span><span class="sxs-lookup"><span data-stu-id="82939-158">Start a support session in Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="82939-159">hello StorSimple 장치 발생할 수 있는 문제를 tootroubleshoot, tooengage hello Microsoft 지원 팀과 함께 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-159">tootroubleshoot any issues that you might experience with hello StorSimple device, you will need tooengage with hello Microsoft Support team.</span></span> <span data-ttu-id="82939-160">Microsoft 지원 toouse tooyour 장치의 지원 세션 toolog 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-160">Microsoft Support may need toouse a support session toolog on tooyour device.</span></span>

<span data-ttu-id="82939-161">Hello 다음이 수행 지원 세션 toostart 단계:</span><span class="sxs-lookup"><span data-stu-id="82939-161">Perform hello following steps toostart a support session:</span></span>

#### <a name="toostart-a-support-session"></a><span data-ttu-id="82939-162">지원 세션 toostart</span><span class="sxs-lookup"><span data-stu-id="82939-162">toostart a support session</span></span>

1. <span data-ttu-id="82939-163">액세스 hello 직렬 콘솔을 사용 하 여 직접 또는 원격 컴퓨터에서 텔넷 세션을 통해 hello 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="82939-163">Access hello device directly by using hello serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="82939-164">toodo hello 단계에서 수행이, [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-164">toodo this, follow hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="82939-165">열린 hello 세션에서 hello를 눌러 **Enter** 키 tooget 명령 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="82939-165">In hello session that opens, press hello **Enter** key tooget a command prompt.</span></span>
3. <span data-ttu-id="82939-166">Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-166">In hello serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="82939-167">Hello 프롬프트 hello 다음 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-167">At hello prompt, type hello following password:</span></span>
   
    `Password1`
5. <span data-ttu-id="82939-168">Hello 프롬프트에서 다음 명령을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-168">At hello prompt, type hello following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="82939-169">암호화 된 문자열이 tooyou를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82939-169">An encrypted string will be presented tooyou.</span></span> <span data-ttu-id="82939-170">메모장과 같은 텍스트 편집기에 이 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-170">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="82939-171">이 문자열을 저장해 전자 메일 메시지 tooMicrosoft 지원에에서 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="82939-171">Save this string and send it in an email message tooMicrosoft Support.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82939-172">`Disable-HcsSupportAccess`를 실행하여 지원 액세스를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82939-172">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="82939-173">hello StorSimple 장치 toodisable 지원 액세스 hello 세션이 시작 된 후 8 시간이 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="82939-173">hello StorSimple device will also attempt toodisable support access 8 hours after hello session was initiated.</span></span> <span data-ttu-id="82939-174">지원 세션을 초기화 한 후 StorSimple 장치 자격 증명 모범 사례 toochange 이며</span><span class="sxs-lookup"><span data-stu-id="82939-174">It is a best practice toochange your StorSimple device credentials after initiating a support session.</span></span>


## <a name="next-steps"></a><span data-ttu-id="82939-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="82939-175">Next steps</span></span>

<span data-ttu-id="82939-176">너무 방법에 대해 알아봅니다[진단 하 고 관련된 tooyour StorSimple 8000 시리즈 장치 문제 해결](storsimple-troubleshoot-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="82939-176">Learn how too[diagnose and solve problems related tooyour StorSimple 8000 series device](storsimple-troubleshoot-deployment.md)</span></span>
