---
title: "갤러리 아닌 응용 프로그램을 추가 하는 aaaProblem | Microsoft Docs"
description: "사용자 지정 갤러리 아닌 응용 프로그램을 추가 하는 경우 일반적인 문제 사람이 면 hello 이해"
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
ms.openlocfilehash: cfe9b657ae18cbacaddbd85658471a2c57c9cf95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-adding-a-non-gallery-application"></a><span data-ttu-id="81328-103">비갤러리 응용 프로그램을 추가할 때 발생하는 문제</span><span class="sxs-lookup"><span data-stu-id="81328-103">Problem adding a non-gallery application</span></span>

<span data-ttu-id="81328-104">이 문서가 도움이 되었나요 toounderstand hello 일반적인 문제 사람이 면 추가할 때 **사용자 지정 갤러리 아닌 응용 프로그램** 수행할 수 있는 동작 tooresolve 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="81328-104">This article help you toounderstand hello common problems people face when adding **custom non-gallery applications** and what you can do tooresolve them.</span></span> 

## <a name="i-clicked-hello-add-button-and-my-application-took-a-long-time-tooappear"></a><span data-ttu-id="81328-105">Hello 단추와 응용 프로그램 걸린 시간이 오래 tooappear "추가" 클릭</span><span class="sxs-lookup"><span data-stu-id="81328-105">I clicked hello “add” button and my application took a long time tooappear</span></span>

<span data-ttu-id="81328-106">상황에 따라 1-2 분 정도 걸릴 수 있습니다 (및 더 길 수도)는 응용 프로그램 tooappear tooyour 디렉터리를 추가한 후에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="81328-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application tooappear after adding it tooyour directory.</span></span> <span data-ttu-id="81328-107">이것이 hello 정상적인 예상된 성능 동안 hello 응용 프로그램 추가 hello를 클릭 하 여 진행 중인 볼 수 있습니다 **알림** hello 오른쪽 상단의 hello 아이콘 (hello 벨) [Azure 포털](https://portal.azure.com/)하 고 찾고는 **진행 중인** 또는 **완료** 레이블이 지정 된 알림 **응용 프로그램을 만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="81328-107">While this is not hello normal expected performance, you can see hello application addition is in progress by clicking on hello **Notifications** icon (hello bell) in hello upper right of hello [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application**.</span></span>

<span data-ttu-id="81328-108">Hello를 클릭 하면 오류가 발생 하거나 응용 프로그램 추가 되지 않는 경우 **추가** 단추를 표시 한 **알림** 에 **오류** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="81328-108">If your application is never added, or you encounter an error when clicking hello **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="81328-109">Hello hello 단계를 수행 하 여 hello 오류에 대 한 자세한 정보를 볼 수 hello 오류 toolearn 자세한 tooor 지원 engingeer와 공유 하는 방법에 대 한 자세한 세부 정보를 원하는 경우 [어떻게 toosee hello 세부 정보는 포털 알림](#how-to-see-the-details-of-a-portal-notification) 섹션.</span><span class="sxs-lookup"><span data-stu-id="81328-109">If you want more details about hello error toolearn more tooor share with a support engingeer, you can see more information about hello error by following hello steps in hello [How toosee hello details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-hello-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="81328-110">Hello "추가" 단추를 클릭 하 고 응용 프로그램 나타나지 않다는 사실이 표시</span><span class="sxs-lookup"><span data-stu-id="81328-110">I clicked hello “add” button and my application didn’t appear</span></span>

<span data-ttu-id="81328-111">경우에 따라 tootransient 문제 때문 네트워킹 문제 또는 버그를 추가 하는 응용 프로그램 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="81328-111">Sometimes, due tootransient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="81328-112">Hello를 클릭할 때 발생 하는이 알 수 있습니다 **알림** (hello 벨) hello hello Azure 포털의 오른쪽 위에 있는 아이콘에 빨간색 (!)를 참조 아이콘 다음 tooyour **응용 프로그램을 만들** 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="81328-112">You can tell this happens when you click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal and you see a red (!) icon next tooyour **Create application** notification.</span></span> <span data-ttu-id="81328-113">이 hello 응용 프로그램을 만들 때 오류가 발생 했습니다. 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="81328-113">This indicates there was an error when creating hello application.</span></span>

<span data-ttu-id="81328-114">Hello를 클릭 하면 오류가 발생 하는 경우 **추가** 단추를 표시 한 **알림** 에 **오류** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="81328-114">If you encounter an error when clicking hello **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="81328-115">Hello hello 단계를 수행 하 여 hello 오류에 대 한 자세한 정보를 볼 수 hello 오류 toolearn 자세한 tooor 지원 engingeer와 공유 하는 방법에 대 한 자세한 세부 정보를 원하는 경우 [어떻게 toosee hello 세부 정보는 포털 알림](#how-to-see-the-details-of-a-portal-notification) 섹션.</span><span class="sxs-lookup"><span data-stu-id="81328-115">If you want more details about hello error toolearn more tooor share with a support engingeer, you can see more information about hello error by following hello steps in hello [How toosee hello details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-dont-know-how-tooset-up-my-application-once-ive-added-it"></a><span data-ttu-id="81328-116">어떻게 tooset 내 응용 프로그램을 한 번 추가한 것을 모릅니다.</span><span class="sxs-lookup"><span data-stu-id="81328-116">I don’t know how tooset up my application once I’ve added it</span></span>

<span data-ttu-id="81328-117">를 사용자 지정 응용 프로그램에 대해 알아보기 도움이 필요 하면 경우 hello [Azure AD 응용 프로그램 문서 라이브러리](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) 더에 대 한 single sign on Azure AD와 toolearn 및 청구 방식 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81328-117">If you need help learning about custom applications, hello [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you toolearn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="81328-118">어떻게 포털 알림의 toosee hello 세부 정보</span><span class="sxs-lookup"><span data-stu-id="81328-118">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="81328-119">다음 hello 단계를 수행 하 여 포털 알림에 대 한 hello 세부 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81328-119">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="81328-120">hello 클릭 **알림** hello hello Azure 포털의 오른쪽 위에 있는 아이콘 (hello 벨)</span><span class="sxs-lookup"><span data-stu-id="81328-120">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="81328-121">에 모든 알림 선택는 **오류** 상태 (빨강 (!) 다음 toothem 순위가).</span><span class="sxs-lookup"><span data-stu-id="81328-121">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

   >[!NOTE]
   ><span data-ttu-id="81328-122">**성공** 또는 **진행 중** 상태에서 알림을 클릭할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81328-122">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
   >
   >

3.  <span data-ttu-id="81328-123">이 열린 hello **알림 세부 정보** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="81328-123">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="81328-124">사용 하 여이 정보 직접 toounderstand hello 문제에 대 한 세부 정보.</span><span class="sxs-lookup"><span data-stu-id="81328-124">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="81328-125">여전히 도움이 필요 하거나, 문제에는 지원 엔지니어 또는 hello 제품 그룹 tooget 도움말와이 정보를도 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81328-125">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="81328-126">Hello 클릭 **복사 아이콘** hello의 오른쪽 toohello **오류 복사** textbox toocopy 모든 지원 또는 제품 그룹 엔지니어와 알림 세부 정보 tooshare hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="81328-126">Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer.</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="81328-127">알림 세부 정보 tooa 지원 엔지니어 전송 하 여 tooget 도움말 하는 방법</span><span class="sxs-lookup"><span data-stu-id="81328-127">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="81328-128">공유 하는 것이 중요 **세부 정보 아래에 나열 된 모든 hello** 신속 하 게 이용할 수 있도록, 한 도움이 필요한 경우 지원 엔지니어와 합니다.</span><span class="sxs-lookup"><span data-stu-id="81328-128">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="81328-129">있습니다 수 간편 하 게 **는 스크린샷을 만든** hello를 클릭 하 여 **복사 오류 아이콘**, toohello 오른쪽 hello에 찾을 **오류 복사** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="81328-129">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="81328-130">알림 세부 정보 설명</span><span class="sxs-lookup"><span data-stu-id="81328-130">Notification Details Explained</span></span>

<span data-ttu-id="81328-131">아래 hello 의미 더 어떤 항목에는 각각 hello 알림 및 각각의 사용 예를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="81328-131">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="81328-132">중요 알림 항목</span><span class="sxs-lookup"><span data-stu-id="81328-132">Essential Notification Items</span></span>

-   <span data-ttu-id="81328-133">**제목** – hello 알림 설명이 포함 된 제목을 hello</span><span class="sxs-lookup"><span data-stu-id="81328-133">**Title** – hello descriptive title of hello notification</span></span>
   *  <span data-ttu-id="81328-134">예제 - **응용 프로그램 프록시 설정**</span><span class="sxs-lookup"><span data-stu-id="81328-134">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="81328-135">**설명** – hello에 대 한 hello 작업의 결과로 발생 한 문제 설명</span><span class="sxs-lookup"><span data-stu-id="81328-135">**Description** – hello description of what occurred as a result of hello operation</span></span>

   *  <span data-ttu-id="81328-136">예제 - **입력한 내부 url은 이미 다른 응용 프로그램에서 사용 중입니다.**</span><span class="sxs-lookup"><span data-stu-id="81328-136">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="81328-137">**알림 Id** – hello hello 알림의 고유 id</span><span class="sxs-lookup"><span data-stu-id="81328-137">**Notification Id** – hello unique id of hello notification</span></span>

   *  <span data-ttu-id="81328-138">예제 – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="81328-138">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="81328-139">**클라이언트 요청 Id** – 브라우저 수행한 hello 특정 요청 id</span><span class="sxs-lookup"><span data-stu-id="81328-139">**Client Request Id** – hello specific request id made by your browser</span></span>

   *  <span data-ttu-id="81328-140">예제 – **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="81328-140">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="81328-141">**스탬프의 UTC 시간** – hello는 hello 알림이 발생 한 utc에서 타임 스탬프</span><span class="sxs-lookup"><span data-stu-id="81328-141">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

   *  <span data-ttu-id="81328-142">예제 – **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="81328-142">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="81328-143">**내부 트랜잭션 Id** – hello toolook hello 오류 시스템에 사용 하는 내부 ID</span><span class="sxs-lookup"><span data-stu-id="81328-143">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

   *  <span data-ttu-id="81328-144">예제 – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="81328-144">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="81328-145">**UPN** – hello 작업을 수행한 hello 사용자</span><span class="sxs-lookup"><span data-stu-id="81328-145">**UPN** – hello user who performed hello operation</span></span>

   *  <span data-ttu-id="81328-146">예제 – **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="81328-146">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="81328-147">**테 넌 트 Id** – hello 테 넌 트의 사용자 hello hello 작업을 수행한 hello 고유 ID는의 구성원</span><span class="sxs-lookup"><span data-stu-id="81328-147">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

   *  <span data-ttu-id="81328-148">예제 – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="81328-148">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="81328-149">**사용자 개체 Id** – hello hello 작업을 수행한 hello 사용자의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="81328-149">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

 *  <span data-ttu-id="81328-150">예제 – **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="81328-150">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="81328-151">자세한 알림 항목</span><span class="sxs-lookup"><span data-stu-id="81328-151">Detailed Notification Items</span></span>

-   <span data-ttu-id="81328-152">**표시 이름** – **(비어 있을 수 있습니다)** hello 오류에 대 한 보다 자세한 표시 이름</span><span class="sxs-lookup"><span data-stu-id="81328-152">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

  *  <span data-ttu-id="81328-153">예제 - **응용 프로그램 프록시 설정**</span><span class="sxs-lookup"><span data-stu-id="81328-153">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="81328-154">**상태** – hello hello 알림의 특정 상태</span><span class="sxs-lookup"><span data-stu-id="81328-154">**Status** – hello specific status of hello notification</span></span>

   *  <span data-ttu-id="81328-155">예제 – **실패**</span><span class="sxs-lookup"><span data-stu-id="81328-155">Example – **Failed**</span></span>

-   <span data-ttu-id="81328-156">**개체 Id** – **(비어 있을 수 있습니다)** 개체 ID는 hello에 대 한 작업을 수행한 hello</span><span class="sxs-lookup"><span data-stu-id="81328-156">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

   *  <span data-ttu-id="81328-157">예제 – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="81328-157">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="81328-158">**세부 정보** – hello를 자세하게 hello 작업의 결과로 발생 한 문제 설명</span><span class="sxs-lookup"><span data-stu-id="81328-158">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

   *  <span data-ttu-id="81328-159">예제 – **내부 url 'http://bing.com/'은 이미 사용 중이므로 유효하지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="81328-159">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="81328-160">**오류 복사** – hello 클릭 **복사 아이콘** toohello hello의 오른쪽 **오류 복사** textbox toocopy 모든 지원 또는 제품 그룹 엔지니어와 알림 세부 정보 tooshare hello</span><span class="sxs-lookup"><span data-stu-id="81328-160">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

   *  <span data-ttu-id="81328-161">예제 ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="81328-161">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="81328-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="81328-162">Next steps</span></span>
[<span data-ttu-id="81328-163">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="81328-163">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)



