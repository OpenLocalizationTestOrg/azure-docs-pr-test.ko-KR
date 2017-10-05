---
title: "비갤러리 응용 프로그램을 추가할 때 발생하는 문제 | Microsoft Docs"
description: "사용자 지정 비갤러리 응용 프로그램을 추가할 때 일반적으로 발생하는 문제 이해"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: bb3fc7877f4e7cafc3904fc67abd87b897874d8a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-adding-a-non-gallery-application"></a><span data-ttu-id="7b5a9-103">비갤러리 응용 프로그램을 추가할 때 발생하는 문제</span><span class="sxs-lookup"><span data-stu-id="7b5a9-103">Problem adding a non-gallery application</span></span>

<span data-ttu-id="7b5a9-104">이 문서는 **사용자 지정 비갤러리 응용 프로그램**을 추가하는 경우 직면하는 일반적인 문제 및 문제를 해결하기 위해 수행할 수 있는 작업을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-104">This article help you to understand the common problems people face when adding **custom non-gallery applications** and what you can do to resolve them.</span></span> 

## <a name="i-clicked-the-add-button-and-my-application-took-a-long-time-to-appear"></a><span data-ttu-id="7b5a9-105">"추가" 단추를 클릭했고 응용 프로그램이 나타나는 데 시간이 오래 걸렸음</span><span class="sxs-lookup"><span data-stu-id="7b5a9-105">I clicked the “add” button and my application took a long time to appear</span></span>

<span data-ttu-id="7b5a9-106">경우에 따라 디렉터리에 추가한 후 응용 프로그램이 나타나는 데 1-2분 정도(경우에 따라 더 길게) 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application to appear after adding it to your directory.</span></span> <span data-ttu-id="7b5a9-107">이는 일반적인 예상되는 성능이 아니지만 [Azure Portal](https://portal.azure.com/)의 오른쪽 위에 있는 **알림** 아이콘(벨)을 클릭하고 **진행 중** 또는 **완료** 알림 레이블이 지정된 **응용 프로그램 만들기**를 찾아 응용 프로그램 추가가 진행 중임을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-107">While this is not the normal expected performance, you can see the application addition is in progress by clicking on the **Notifications** icon (the bell) in the upper right of the [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application**.</span></span>

<span data-ttu-id="7b5a9-108">응용 프로그램이 추가되지 않거나 **추가** 단추를 클릭할 때 오류가 발생하는 경우 **오류** 상태에 **알림**이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-108">If your application is never added, or you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="7b5a9-109">더 자세히 알아보거나 지원 엔지니어와 공유하기 위해 오류에 대한 자세한 정보를 원하는 경우 [포털 알림의 세부 정보를 확인하는 방법](#how-to-see-the-details-of-a-portal-notification) 섹션의 단계를 따라 오류에 대한 자세한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-109">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="7b5a9-110">"추가" 단추를 클릭했고 응용 프로그램이 나타나지 않았음</span><span class="sxs-lookup"><span data-stu-id="7b5a9-110">I clicked the “add” button and my application didn’t appear</span></span>

<span data-ttu-id="7b5a9-111">경우에 따라 일시적인 문제, 네트워킹 문제 또는 버그로 인해 응용 프로그램 추가에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-111">Sometimes, due to transient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="7b5a9-112">Azure Portal의 오른쪽 위에 있는 **알림** 아이콘(벨)을 클릭하고 **응용 프로그램 만들기** 알림 옆의 빨간색(!) 아이콘이 표시되는 경우 이러한 상황이 발생한다고 말할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-112">You can tell this happens when you click the **Notifications** icon (the bell) in the upper right of the Azure Portal and you see a red (!) icon next to your **Create application** notification.</span></span> <span data-ttu-id="7b5a9-113">이는 응용 프로그램을 만들 때 오류가 있었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-113">This indicates there was an error when creating the application.</span></span>

<span data-ttu-id="7b5a9-114">**추가** 단추를 클릭할 때 오류가 발생하는 경우 **오류** 상태에 **알림**이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-114">If you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="7b5a9-115">더 자세히 알아보거나 지원 엔지니어와 공유하기 위해 오류에 대한 자세한 정보를 원하는 경우 [포털 알림의 세부 정보를 확인하는 방법](#how-to-see-the-details-of-a-portal-notification) 섹션의 단계를 따라 오류에 대한 자세한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-115">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-dont-know-how-to-set-up-my-application-once-ive-added-it"></a><span data-ttu-id="7b5a9-116">추가한 후 내 응용 프로그램을 설정하는 방법을 모름</span><span class="sxs-lookup"><span data-stu-id="7b5a9-116">I don’t know how to set up my application once I’ve added it</span></span>

<span data-ttu-id="7b5a9-117">사용자 지정 응용 프로그램을 배워야 할 경우 [Azure AD 응용 프로그램 문서 라이브러리](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index)를 통해 Azure AD로 Single Sign-On 및 작동 방법에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-117">If you need help learning about custom applications, the [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you to learn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="7b5a9-118">포털 알림의 세부 정보를 확인하는 방법</span><span class="sxs-lookup"><span data-stu-id="7b5a9-118">How to see the details of a portal notification</span></span>

<span data-ttu-id="7b5a9-119">다음 단계를 수행하여 포털 알림의 세부 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-119">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="7b5a9-120">Azure Portal의 오른쪽 위에 있는 **알림** 아이콘(벨)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-120">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="7b5a9-121">**오류** 상태(옆에 빨간색(!)이 있는)에서 알림을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-121">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

   >[!NOTE]
   ><span data-ttu-id="7b5a9-122">**성공** 또는 **진행 중** 상태에서 알림을 클릭할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-122">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
   >
   >

3.  <span data-ttu-id="7b5a9-123">**알림 세부 정보** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-123">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="7b5a9-124">이 정보를 사용하여 문제에 대한 자세한 내용을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-124">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="7b5a9-125">여전히 도움이 필요한 경우 문제에 대한 도움을 얻도록 이 정보를 지원 엔지니어 또는 제품 그룹과 공유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-125">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="7b5a9-126">**오류 복사** 텍스트 상자 오른쪽의 **복사 아이콘**을 클릭하여 지원 또는 제품 그룹 엔지니어와 공유하도록 모든 알림 세부 정보를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-126">Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="7b5a9-127">지원 엔지니어에게 알림 세부 정보를 전송하여 도움을 얻는 방법</span><span class="sxs-lookup"><span data-stu-id="7b5a9-127">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="7b5a9-128">도움이 필요한 경우 지원 엔지니어가 신속하게 도움을 줄 수 있도록 **아래에 나열된 모든 세부 정보**를 공유하는 것은 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-128">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="7b5a9-129">**스크린샷을 찍거나** **오류 복사** 텍스트 상자 오른쪽에 있는 **오류 복사 아이콘**을 클릭하여 이를 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-129">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="7b5a9-130">알림 세부 정보 설명</span><span class="sxs-lookup"><span data-stu-id="7b5a9-130">Notification Details Explained</span></span>

<span data-ttu-id="7b5a9-131">다음은 각 알림 항목이 의미하는 내용을 자세히 설명하고 각 항목의 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7b5a9-131">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="7b5a9-132">중요 알림 항목</span><span class="sxs-lookup"><span data-stu-id="7b5a9-132">Essential Notification Items</span></span>

-   <span data-ttu-id="7b5a9-133">**제목** - 알림의 설명이 포함된 제목</span><span class="sxs-lookup"><span data-stu-id="7b5a9-133">**Title** – the descriptive title of the notification</span></span>
   *  <span data-ttu-id="7b5a9-134">예제 - **응용 프로그램 프록시 설정**</span><span class="sxs-lookup"><span data-stu-id="7b5a9-134">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="7b5a9-135">**설명** – 작업의 결과로 발생한 문제에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="7b5a9-135">**Description** – the description of what occurred as a result of the operation</span></span>

   *  <span data-ttu-id="7b5a9-136">예제 - **입력한 내부 url은 이미 다른 응용 프로그램에서 사용 중입니다.**</span><span class="sxs-lookup"><span data-stu-id="7b5a9-136">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="7b5a9-137">**알림 ID** - 알림의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="7b5a9-137">**Notification Id** – the unique id of the notification</span></span>

   *  <span data-ttu-id="7b5a9-138">예제 – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="7b5a9-138">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="7b5a9-139">**클라이언트 요청 ID** -브라우저에서 만든 특정 요청 ID</span><span class="sxs-lookup"><span data-stu-id="7b5a9-139">**Client Request Id** – the specific request id made by your browser</span></span>

   *  <span data-ttu-id="7b5a9-140">예제 – **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="7b5a9-140">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="7b5a9-141">**타임스탬프 UTC** – 알림이 발생한 동안의 타임스탬프(UTC)</span><span class="sxs-lookup"><span data-stu-id="7b5a9-141">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

   *  <span data-ttu-id="7b5a9-142">예제 – **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="7b5a9-142">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="7b5a9-143">**내부 트랜잭션 ID** – 시스템에서 오류를 찾는 데 사용할 수 있는 내부 ID</span><span class="sxs-lookup"><span data-stu-id="7b5a9-143">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

   *  <span data-ttu-id="7b5a9-144">예제 – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="7b5a9-144">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="7b5a9-145">**UPN** – 작업을 수행한 사용자</span><span class="sxs-lookup"><span data-stu-id="7b5a9-145">**UPN** – the user who performed the operation</span></span>

   *  <span data-ttu-id="7b5a9-146">예제 – **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="7b5a9-146">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="7b5a9-147">**테넌트 ID** – 작업을 수행한 사용자가 구성원인 테넌트의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="7b5a9-147">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

   *  <span data-ttu-id="7b5a9-148">예제 – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="7b5a9-148">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="7b5a9-149">**사용자 개체 ID** – 작업을 수행한 사용자의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="7b5a9-149">**User object Id** – the unique ID of the user who performed the operation</span></span>

 *  <span data-ttu-id="7b5a9-150">예제 – **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="7b5a9-150">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="7b5a9-151">자세한 알림 항목</span><span class="sxs-lookup"><span data-stu-id="7b5a9-151">Detailed Notification Items</span></span>

-   <span data-ttu-id="7b5a9-152">**표시 이름** – **(비어 있을 수 있음)** 오류에 대한 보다 자세한 표시 이름</span><span class="sxs-lookup"><span data-stu-id="7b5a9-152">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

  *  <span data-ttu-id="7b5a9-153">예제 - **응용 프로그램 프록시 설정**</span><span class="sxs-lookup"><span data-stu-id="7b5a9-153">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="7b5a9-154">**상태** - 알림의 특정 상태</span><span class="sxs-lookup"><span data-stu-id="7b5a9-154">**Status** – the specific status of the notification</span></span>

   *  <span data-ttu-id="7b5a9-155">예제 – **실패**</span><span class="sxs-lookup"><span data-stu-id="7b5a9-155">Example – **Failed**</span></span>

-   <span data-ttu-id="7b5a9-156">**개체 ID** – **(비어 있을 수 있음)** 작업이 수행된 개체 ID</span><span class="sxs-lookup"><span data-stu-id="7b5a9-156">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

   *  <span data-ttu-id="7b5a9-157">예제 – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="7b5a9-157">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="7b5a9-158">**세부 정보** – 작업의 결과로 발생한 문제에 대한 자세한 설명</span><span class="sxs-lookup"><span data-stu-id="7b5a9-158">**Details** – the detailed description of what occurred as a result of the operation</span></span>

   *  <span data-ttu-id="7b5a9-159">예제 – **내부 url 'http://bing.com/'은 이미 사용 중이므로 유효하지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="7b5a9-159">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="7b5a9-160">**오류 복사** - **오류 복사** 텍스트 상자 오른쪽의 **복사 아이콘**을 클릭하여 지원 또는 제품 그룹 엔지니어와 공유하도록 모든 알림 세부 정보 복사</span><span class="sxs-lookup"><span data-stu-id="7b5a9-160">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

   *  <span data-ttu-id="7b5a9-161">예제 ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="7b5a9-161">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b5a9-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b5a9-162">Next steps</span></span>
[<span data-ttu-id="7b5a9-163">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="7b5a9-163">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)



