---
title: "사용자 tooyour Azure RemoteApp 컬렉션 aaaAdd | Microsoft Docs"
description: "자세한 내용은 방법 tooadd 사용자 tooyour Azure RemoteApp 컬렉션"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a><span data-ttu-id="6d833-103">어떻게 tooadd 사용자 tooyour Azure RemoteApp 컬렉션</span><span class="sxs-lookup"><span data-stu-id="6d833-103">How tooadd a user tooyour Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6d833-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d833-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6d833-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d833-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6d833-106">사용자가 참조 하 고 Azure RemoteApp에 앱을 사용할 수, toogrant tooyour 컬렉션 액세스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d833-106">Before your users can see and use your apps in Azure RemoteApp, you have toogrant them access tooyour collection.</span></span> <span data-ttu-id="6d833-107">이것은 쉽게 일부 hello: hello에 **사용자 액세스** 탭, hello 사용자에 대 한 hello 계정 정보를 입력 한 후 hello 확인 표시를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d833-107">This is hello easy part: On hello **User Access** tab, enter hello account information for hello user, and then click hello check mark.</span></span>

<span data-ttu-id="6d833-108">어떤 계정 정보가 필요할까요?</span><span class="sxs-lookup"><span data-stu-id="6d833-108">What account information do you need?</span></span> <span data-ttu-id="6d833-109">사용자가 만든 (클라우드 또는 하이브리드) 여부를 사용 하 고 Office 365 ProPlus 해당 컬렉션에 컬렉션의 hello 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6d833-109">That depends on hello type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="6d833-110">지원되는 사용자 ID</span><span class="sxs-lookup"><span data-stu-id="6d833-110">Supported user identities</span></span>
<span data-ttu-id="6d833-111">hello 다른 컬렉션 형식 (및 하이브리드 클라우드) 다른 사용자 id를 사용 하 여 액세스 tooapplications에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="6d833-111">hello different collection types (cloud vs. hybrid) support using different user identities for access tooapplications.</span></span>  

<span data-ttu-id="6d833-112">RemoteApp의 하이브리드 컬렉션에 대 한 사용자 tooset 온-프레미스 및 Directory 통합과 함께 Azure Active Directory 테 넌 트에 Active Directory 도메인 인프라를 필요 (및 필요에 따라 단일 로그온).</span><span class="sxs-lookup"><span data-stu-id="6d833-112">For a hybrid collection of RemoteApp, you need tooset up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="6d833-113">또한 toocreate hello 온-프레미스 디렉터리에 몇 가지 Active Directory 개체가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d833-113">Additionally, you need toocreate some Active Directory objects in hello on-premises directory.</span></span>  

<span data-ttu-id="6d833-114">RemoteApp의 클라우드 컬렉션에 대 한 Azure Active Directory id 지원 권한이 있는 사용자 Microsoft 계정 사용자 액세스 tooRemoteApp tooinclude를 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d833-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access tooRemoteApp tooinclude Microsoft Accounts.</span></span>  <span data-ttu-id="6d833-115">아래 hello 표를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d833-115">See hello table below.</span></span>

<span data-ttu-id="6d833-116">Office 365 사용자는 Azure Active Directory 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="6d833-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="6d833-117">Azure Active Directory 하이브리드, 디렉터리 동기화된 계정이 있는 경우, RemoteApp 하이브리드 배포에서 사용자 액세스 권한이 부여될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d833-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="6d833-118">이 테이블은 identity 컬렉션과 hello Active Directory 요구 사항 이란에서 지원 되는 빠른 참조로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d833-118">You can use this table as a quick reference for which identity is supported in your collection and what hello Active Directory requirements are.</span></span>

| <span data-ttu-id="6d833-119">사용자 계정</span><span class="sxs-lookup"><span data-stu-id="6d833-119">User accounts</span></span> | <span data-ttu-id="6d833-120">클라우드</span><span class="sxs-lookup"><span data-stu-id="6d833-120">Cloud</span></span> | <span data-ttu-id="6d833-121">하이브리드</span><span class="sxs-lookup"><span data-stu-id="6d833-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d833-122">Microsoft 계정</span><span class="sxs-lookup"><span data-stu-id="6d833-122">Microsoft Account</span></span> |<span data-ttu-id="6d833-123">예</span><span class="sxs-lookup"><span data-stu-id="6d833-123">Yes</span></span> |<span data-ttu-id="6d833-124">아니요</span><span class="sxs-lookup"><span data-stu-id="6d833-124">No</span></span> |
| <span data-ttu-id="6d833-125">Azure AD(Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="6d833-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="6d833-126">Azure AD 클라우드만 해당</span><span class="sxs-lookup"><span data-stu-id="6d833-126">Azure AD cloud only</span></span> |<span data-ttu-id="6d833-127">예</span><span class="sxs-lookup"><span data-stu-id="6d833-127">Yes</span></span> |<span data-ttu-id="6d833-128">아니요</span><span class="sxs-lookup"><span data-stu-id="6d833-128">No</span></span> |
| <span data-ttu-id="6d833-129">암호 동기화를 사용하는 ADsync</span><span class="sxs-lookup"><span data-stu-id="6d833-129">ADsync with password sync</span></span> |<span data-ttu-id="6d833-130">예</span><span class="sxs-lookup"><span data-stu-id="6d833-130">Yes</span></span> |<span data-ttu-id="6d833-131">예</span><span class="sxs-lookup"><span data-stu-id="6d833-131">Yes</span></span> |
| <span data-ttu-id="6d833-132">암호 동기화를 사용하지 않는 ADsync</span><span class="sxs-lookup"><span data-stu-id="6d833-132">ADsync without password sync</span></span> |<span data-ttu-id="6d833-133">예</span><span class="sxs-lookup"><span data-stu-id="6d833-133">Yes</span></span> |<span data-ttu-id="6d833-134">아니요</span><span class="sxs-lookup"><span data-stu-id="6d833-134">No</span></span> |
| <span data-ttu-id="6d833-135">AD FS 포함 ADsync</span><span class="sxs-lookup"><span data-stu-id="6d833-135">ADsync with AD FS</span></span> |<span data-ttu-id="6d833-136">예</span><span class="sxs-lookup"><span data-stu-id="6d833-136">Yes</span></span> |<span data-ttu-id="6d833-137">yes</span><span class="sxs-lookup"><span data-stu-id="6d833-137">Yes</span></span> |
| <span data-ttu-id="6d833-138">[타사 Azure 지원 ID 공급자](https://msdn.microsoft.com/library/azure/jj679342.aspx)(예: Ping)</span><span class="sxs-lookup"><span data-stu-id="6d833-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="6d833-139">yes</span><span class="sxs-lookup"><span data-stu-id="6d833-139">Yes</span></span> |<span data-ttu-id="6d833-140">예</span><span class="sxs-lookup"><span data-stu-id="6d833-140">Yes</span></span> |
| <span data-ttu-id="6d833-141">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="6d833-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="6d833-142">예</span><span class="sxs-lookup"><span data-stu-id="6d833-142">Yes</span></span> |<span data-ttu-id="6d833-143">예</span><span class="sxs-lookup"><span data-stu-id="6d833-143">Yes</span></span> |

<span data-ttu-id="6d833-144">RemoteApp에 대한 Active Directory 구성에 대한 [자세한 내용](remoteapp-ad.md) 을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="6d833-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="6d833-145">hello Azure Active Directory 사용자 구독와 관련 된 hello 테 넌 트에서 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d833-145">hello Azure Active Directory users must be from hello tenant that's associated with your subscription.</span></span> <span data-ttu-id="6d833-146">(보고 하 고 hello에 가입 내용을 수정 **설정을** hello 포털에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d833-146">(You can view and modify your subscription on hello **Settings** tab in hello portal.</span></span> <span data-ttu-id="6d833-147">참조 [변경 hello Azure Active Directory 테 넌 트가 RemoteApp에서 사용 하는](remoteapp-changetenant.md) 자세한 정보에 대 한 합니다.)</span><span class="sxs-lookup"><span data-stu-id="6d833-147">See [Change hello Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="6d833-148">Office 365 ProPlus 사용자 계정 정보</span><span class="sxs-lookup"><span data-stu-id="6d833-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="6d833-149">템플릿 이미지를 Office 365 ProPlus hello을 사용 하는 컬렉션의 경우 *또는* hello에 대 한 Office 365 구독이 있는 tooadd Azure Active Directory 사용자를 Office 365를 사용 하는 사용자 지정 이미지를 만든 경우만 허용 됩니다 기본 도메인 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d833-149">If you are using hello Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed tooadd Azure Active Directory users that have Office 365 subscriptions for hello default domain of your subscription.</span></span> <span data-ttu-id="6d833-150">자세한 내용은 [Azure RemoteApp과 함께 Office 365 사용](remoteapp-o365.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d833-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

