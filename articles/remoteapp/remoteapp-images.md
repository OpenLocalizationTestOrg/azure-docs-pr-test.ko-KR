---
title: "aaaWhat은 hello Azure RemoteApp 템플릿 이미지는? | Microsoft Docs"
description: "Azure RemoteApp과 함께 포함 된 hello 템플릿 이미지에 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a><span data-ttu-id="d10d6-104">Hello Azure RemoteApp 템플릿 이미지에는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d10d6-104">What is in hello Azure RemoteApp template images?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d10d6-105">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d10d6-106">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-106">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d10d6-107">Azure RemoteApp 구독에는 다음 세 개의 템플릿 이미지가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-107">Your Azure RemoteApp subscription includes three template images:</span></span>

* <span data-ttu-id="d10d6-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d10d6-108">Windows Server 2012</span></span>
* <span data-ttu-id="d10d6-109">Microsoft Office 365 ProPlus(Office 365 구독 필요)</span><span class="sxs-lookup"><span data-stu-id="d10d6-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span></span>
* <span data-ttu-id="d10d6-110">Microsoft Office 2013 Professional Plus(평가판 전용)</span><span class="sxs-lookup"><span data-stu-id="d10d6-110">Microsoft Office 2013 Professional Plus (trial only)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d10d6-111">Azure RemoteApp 구독 toohello 소프트웨어 Office 365 ProPlus, 별도 구독을 요구 하 고 프로덕션 환경에서 사용할 수 없는 Office 2013의 hello 예외를 사용 하 여 hello 이미지에서 액세스 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-111">Your Azure RemoteApp subscription grants you access toohello software in hello images, with hello exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span></span> <span data-ttu-id="d10d6-112">즉, 사용자와 hello 프로그램 또는 hello 템플릿 이미지에 앱을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-112">This means that you can share hello programs or apps on hello template images with your users.</span></span> <span data-ttu-id="d10d6-113">예를 들어 hello Windows Server 2012 R2 이미지를 사용 하는 컬렉션을 만들면 RemoteApp 통해 사용자가 tooaccess에 대 한 System Center Endpoint Protection을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-113">For example, if you create a collection that uses hello Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users tooaccess through RemoteApp.</span></span>
> 
> <span data-ttu-id="d10d6-114">체크 아웃 hello [세부 정보를 라이선스 하는 RemoteApp](remoteapp-licensing.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-114">Check out hello [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span></span> <span data-ttu-id="d10d6-115">및 [Azure RemoteApp과 함께 사용 하 여 Office](remoteapp-o365.md) hello Office 라이센스 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for hello Office licensing info.</span></span>
> 
> 

<span data-ttu-id="d10d6-116">각 이미지에 포함된 항목에 대한 내용도 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="d10d6-116">Read on for details on what each image contains.</span></span>

## <a name="windows-server-2012-r2--hello-vanilla-image"></a><span data-ttu-id="d10d6-117">Windows Server 2012 R2 ("hello 바닐라 이미지")</span><span class="sxs-lookup"><span data-stu-id="d10d6-117">Windows Server 2012 R2  ("hello vanilla image")</span></span>
<span data-ttu-id="d10d6-118">이 이미지는 Microsoft Windows Server 2012 R2 Datacenter 운영 체제에 따라 및 hello 다음 역할 및 기능 설치에 대 한 Azure RemoteApp 템플릿 이미지 toomeet hello 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="d10d6-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has hello following roles and features installed toomeet hello requirements for Azure RemoteApp template images:</span></span>

* <span data-ttu-id="d10d6-119">.NET Framework 4.5, 3.5.1, 3.5</span><span class="sxs-lookup"><span data-stu-id="d10d6-119">.NET Framework 4.5, 3.5.1, 3.5</span></span>
* <span data-ttu-id="d10d6-120">데스크톱 경험</span><span class="sxs-lookup"><span data-stu-id="d10d6-120">Desktop Experience</span></span>
* <span data-ttu-id="d10d6-121">잉크 및 필기 서비스</span><span class="sxs-lookup"><span data-stu-id="d10d6-121">Ink and Handwriting Services</span></span>
* <span data-ttu-id="d10d6-122">미디어 파운데이션</span><span class="sxs-lookup"><span data-stu-id="d10d6-122">Media Foundation</span></span>
* <span data-ttu-id="d10d6-123">원격 데스크톱 세션 호스트</span><span class="sxs-lookup"><span data-stu-id="d10d6-123">Remote Desktop Session Host</span></span>
* <span data-ttu-id="d10d6-124">Windows PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="d10d6-124">Windows PowerShell 4.0</span></span>
* <span data-ttu-id="d10d6-125">Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="d10d6-125">Windows PowerShell ISE</span></span>
* <span data-ttu-id="d10d6-126">WoW64 지원</span><span class="sxs-lookup"><span data-stu-id="d10d6-126">WoW64 Support</span></span>

<span data-ttu-id="d10d6-127">이 이미지에는 다음 응용 프로그램을 설치 하는 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-127">This image also has hello following applications installed:</span></span>

* <span data-ttu-id="d10d6-128">Adobe Flash Player</span><span class="sxs-lookup"><span data-stu-id="d10d6-128">Adobe Flash Player</span></span>
* <span data-ttu-id="d10d6-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="d10d6-129">Microsoft Silverlight</span></span>
* <span data-ttu-id="d10d6-130">Microsoft System Center 2012 Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="d10d6-130">Microsoft System Center 2012 Endpoint Protection</span></span>
* <span data-ttu-id="d10d6-131">Microsoft Windows Media Player</span><span class="sxs-lookup"><span data-stu-id="d10d6-131">Microsoft Windows Media Player</span></span>

## <a name="microsoft-office-365-proplus-subscription-required"></a><span data-ttu-id="d10d6-132">Microsoft Office 365 ProPlus(구독 필요)</span><span class="sxs-lookup"><span data-stu-id="d10d6-132">Microsoft Office 365 ProPlus (subscription required)</span></span>
<span data-ttu-id="d10d6-133">Office 365는 "custom" 이미지에 작성 된 toowork 하므로 가장 요청한 응용 프로그램을 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-133">Office 365 is hello most requested application, so we created a "custom" image for you toowork with.</span></span>

<span data-ttu-id="d10d6-134">이 이미지는 hello 바닐라 이미지의 확장 및 hello Microsoft Office 365 ProPlus의 다음 구성 요소 설치 또한 hello Windows Server 2012 R2 이미지에서 설명 하는 toohello 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="d10d6-134">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 365 ProPlus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="d10d6-135">Access</span><span class="sxs-lookup"><span data-stu-id="d10d6-135">Access</span></span>
* <span data-ttu-id="d10d6-136">Excel</span><span class="sxs-lookup"><span data-stu-id="d10d6-136">Excel</span></span>
* <span data-ttu-id="d10d6-137">Lync</span><span class="sxs-lookup"><span data-stu-id="d10d6-137">Lync</span></span>
* <span data-ttu-id="d10d6-138">OneNote</span><span class="sxs-lookup"><span data-stu-id="d10d6-138">OneNote</span></span>
* <span data-ttu-id="d10d6-139">비즈니스용 OneDrive (참고: Azure RemoteApp과 함께 사용 하기 위해 해당 hello 동기화 에이전트를 사용할 수 없습니다)</span><span class="sxs-lookup"><span data-stu-id="d10d6-139">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="d10d6-140">Outlook</span><span class="sxs-lookup"><span data-stu-id="d10d6-140">Outlook</span></span>
* <span data-ttu-id="d10d6-141">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d10d6-141">PowerPoint</span></span>
* <span data-ttu-id="d10d6-142">Word</span><span class="sxs-lookup"><span data-stu-id="d10d6-142">Word</span></span>
* <span data-ttu-id="d10d6-143">Microsoft Office 언어 교정 도구</span><span class="sxs-lookup"><span data-stu-id="d10d6-143">Microsoft Office Proofing Tools</span></span>

<span data-ttu-id="d10d6-144">hello 이미지에는 Visio Pro 및 Pro 프로젝트도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-144">hello image also includes Visio Pro and Project Pro.</span></span>

<span data-ttu-id="d10d6-145">및 응용 프로그램에도 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="d10d6-145">And hello following applications, as well:</span></span>

* <span data-ttu-id="d10d6-146">SQL Native client</span><span class="sxs-lookup"><span data-stu-id="d10d6-146">SQL Native client</span></span>
* <span data-ttu-id="d10d6-147">ODBC 드라이버</span><span class="sxs-lookup"><span data-stu-id="d10d6-147">ODBC Driver</span></span>
* <span data-ttu-id="d10d6-148">SQL Server 데이터 마이닝 클라이언트</span><span class="sxs-lookup"><span data-stu-id="d10d6-148">SQL Server Data Mining client</span></span>
* <span data-ttu-id="d10d6-149">MasterDataServices 클라이언트</span><span class="sxs-lookup"><span data-stu-id="d10d6-149">MasterDataServices client</span></span>
* <span data-ttu-id="d10d6-150">Microsoft Publisher</span><span class="sxs-lookup"><span data-stu-id="d10d6-150">Microsoft Publisher</span></span>
* <span data-ttu-id="d10d6-151">PowerQuery</span><span class="sxs-lookup"><span data-stu-id="d10d6-151">PowerQuery</span></span>
* <span data-ttu-id="d10d6-152">PowerMap</span><span class="sxs-lookup"><span data-stu-id="d10d6-152">PowerMap</span></span>

<span data-ttu-id="d10d6-153">Office 365 ProPlus 계획이 있는 사용자만 Office 365 ProPlus 앱의 모든 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span></span> <span data-ttu-id="d10d6-154">Hello Office 365 구독에 대 한 자세한 내용은 계획 참조 [Office 365 서비스 계획](http://technet.microsoft.com/library/office-365-plan-options.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-154">For more details on hello Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span> <span data-ttu-id="d10d6-155">질문이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="d10d6-155">Still have questions?</span></span> <span data-ttu-id="d10d6-156">체크 아웃 hello [Office 365 + RemoteApp](remoteapp-o365.md) 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-156">Check out hello [Office 365 + RemoteApp](remoteapp-o365.md) information.</span></span> <span data-ttu-id="d10d6-157">Hello 새 문서를 확인해 [어떻게 toouse Azure RemoteApp과 함께 Office 365 구독](remoteapp-officesubscription.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-157">Also check out hello new article, [How toouse your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

<span data-ttu-id="d10d6-158">자신의 라이선스를 사용할 구성 파일은 각각 할 toolicense Office 365 ProPlus, Visio Pro 및 프로젝트 Pro 별도로-참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-158">Note that you need toolicense Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span></span>

## <a name="microsoft-office-2013-professional-plus-trial-only"></a><span data-ttu-id="d10d6-159">Microsoft Office 2013 Professional Plus(평가판 전용)</span><span class="sxs-lookup"><span data-stu-id="d10d6-159">Microsoft Office 2013 Professional Plus (trial only)</span></span>
<span data-ttu-id="d10d6-160">Hello 무료 평가 기간 중 hello Office 2013 이미지로 hello 서비스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-160">During hello free trial period, you can test hello service with hello Office 2013 image.</span></span>

<span data-ttu-id="d10d6-161">이 이미지는 hello 바닐라 이미지의 확장 및 hello Microsoft Office 2013 Professional Plus의 다음 구성 요소 설치 또한 hello Windows Server 2012 R2 이미지에서 설명 하는 toohello 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="d10d6-161">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 2013 Professional Plus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="d10d6-162">Access</span><span class="sxs-lookup"><span data-stu-id="d10d6-162">Access</span></span>
* <span data-ttu-id="d10d6-163">Excel</span><span class="sxs-lookup"><span data-stu-id="d10d6-163">Excel</span></span>
* <span data-ttu-id="d10d6-164">Lync</span><span class="sxs-lookup"><span data-stu-id="d10d6-164">Lync</span></span>
* <span data-ttu-id="d10d6-165">OneNote</span><span class="sxs-lookup"><span data-stu-id="d10d6-165">OneNote</span></span>
* <span data-ttu-id="d10d6-166">비즈니스용 OneDrive (참고: Azure RemoteApp과 함께 사용 하기 위해 해당 hello 동기화 에이전트를 사용할 수 없습니다)</span><span class="sxs-lookup"><span data-stu-id="d10d6-166">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="d10d6-167">Outlook</span><span class="sxs-lookup"><span data-stu-id="d10d6-167">Outlook</span></span>
* <span data-ttu-id="d10d6-168">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d10d6-168">PowerPoint</span></span>
* <span data-ttu-id="d10d6-169">Project</span><span class="sxs-lookup"><span data-stu-id="d10d6-169">Project</span></span>
* <span data-ttu-id="d10d6-170">Visio</span><span class="sxs-lookup"><span data-stu-id="d10d6-170">Visio</span></span>
* <span data-ttu-id="d10d6-171">Word</span><span class="sxs-lookup"><span data-stu-id="d10d6-171">Word</span></span>
* <span data-ttu-id="d10d6-172">Microsoft Office 언어 교정 도구</span><span class="sxs-lookup"><span data-stu-id="d10d6-172">Microsoft Office Proofing Tools</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d10d6-173">**법적 정보:** 이 이미지에는 Microsoft Office 라이선스를 포함하지 않으며 *프로덕션에 사용할 수 없습니다*.</span><span class="sxs-lookup"><span data-stu-id="d10d6-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span></span> <span data-ttu-id="d10d6-174">hello Office 2013 Professional 더하기 이미지 평가판에 사용이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-174">hello Office 2013 Professional Plus image is intended for trial use only.</span></span> <span data-ttu-id="d10d6-175">프로덕션에 대 한 Azure RemoteApp에서 toouse 오피스 응용 프로그램을 원하는 경우 toouse hello Office 365 ProPlus 이미지를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d10d6-175">If you want toouse Office apps in Azure RemoteApp for production, you need toouse hello Office 365 ProPlus image.</span></span> <span data-ttu-id="d10d6-176">라이선스 Office에 대한 자세한 내용은 [Azure RemoteApp과 함께 Office 365 사용](remoteapp-o365.md)</span><span class="sxs-lookup"><span data-stu-id="d10d6-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span></span>
> 
> 

