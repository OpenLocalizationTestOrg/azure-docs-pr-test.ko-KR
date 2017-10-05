---
title: "Azure RemoteApp 컬렉션에 사용자 추가 | Microsoft 문서"
description: "Azure RemoteApp 컬렉션에 사용자를 추가하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 281e74c7941c42d8a3e4351953391229e54ce0a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a><span data-ttu-id="fad0a-103">Azure RemoteApp 컬렉션에 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="fad0a-103">How to add a user to your Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fad0a-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fad0a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="fad0a-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="fad0a-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="fad0a-106">먼저 사용자에게 컬렉션에 대한 액세스 권한을 부여해야 사용자가 Azure RemoteApp에서 앱을 보고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad0a-106">Before your users can see and use your apps in Azure RemoteApp, you have to grant them access to your collection.</span></span> <span data-ttu-id="fad0a-107">이 작업은 간단합니다. **사용자 액세스** 탭에서 사용자의 계정 정보를 입력하고 확인 표시를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad0a-107">This is the easy part: On the **User Access** tab, enter the account information for the user, and then click the check mark.</span></span>

<span data-ttu-id="fad0a-108">어떤 계정 정보가 필요할까요?</span><span class="sxs-lookup"><span data-stu-id="fad0a-108">What account information do you need?</span></span> <span data-ttu-id="fad0a-109">필요한 계정 정보는 만든 컬렉션 유형(클라우드 또는 하이브리드) 및 해당 컬렉션에서 Office 365 ProPlus를 사용하는지 여부에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="fad0a-109">That depends on the type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="fad0a-110">지원되는 사용자 ID</span><span class="sxs-lookup"><span data-stu-id="fad0a-110">Supported user identities</span></span>
<span data-ttu-id="fad0a-111">다양한 컬렉션 형식(클라우드와 하이브리드)에서 응용 프로그램에 대한 액세스를 위해 다양한 사용자 ID 사용을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fad0a-111">The different collection types (cloud vs. hybrid) support using different user identities for access to applications.</span></span>  

<span data-ttu-id="fad0a-112">RemoteApp 하이브리드 컬렉션의 경우 온-프레미스 Active Directory 도메인 인프라와 디렉터리 통합(및 선택적으로 Single Sign-On)이 포함된 Azure Active Directory 테넌트를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad0a-112">For a hybrid collection of RemoteApp, you need to set up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="fad0a-113">또한 온-프레미스 디렉터리에 일부 Active Directory 개체를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad0a-113">Additionally, you need to create some Active Directory objects in the on-premises directory.</span></span>  

<span data-ttu-id="fad0a-114">RemoteApp의 클라우드 컬렉션의 경우, Azure Active Directory 지원 ID가 있는 사용자에게는 Microsoft 계정을 비롯하여 RemoteApp에 대한 사용자 액세스 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad0a-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access to RemoteApp to include Microsoft Accounts.</span></span>  <span data-ttu-id="fad0a-115">아래 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fad0a-115">See the table below.</span></span>

<span data-ttu-id="fad0a-116">Office 365 사용자는 Azure Active Directory 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="fad0a-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="fad0a-117">Azure Active Directory 하이브리드, 디렉터리 동기화된 계정이 있는 경우, RemoteApp 하이브리드 배포에서 사용자 액세스 권한이 부여될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad0a-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="fad0a-118">이 테이블은 컬렉션에서 지원되는 ID 및 Active Directory 요구 사항에 대한 빠른 참조로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad0a-118">You can use this table as a quick reference for which identity is supported in your collection and what the Active Directory requirements are.</span></span>

| <span data-ttu-id="fad0a-119">사용자 계정</span><span class="sxs-lookup"><span data-stu-id="fad0a-119">User accounts</span></span> | <span data-ttu-id="fad0a-120">클라우드</span><span class="sxs-lookup"><span data-stu-id="fad0a-120">Cloud</span></span> | <span data-ttu-id="fad0a-121">하이브리드</span><span class="sxs-lookup"><span data-stu-id="fad0a-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fad0a-122">Microsoft 계정</span><span class="sxs-lookup"><span data-stu-id="fad0a-122">Microsoft Account</span></span> |<span data-ttu-id="fad0a-123">예</span><span class="sxs-lookup"><span data-stu-id="fad0a-123">Yes</span></span> |<span data-ttu-id="fad0a-124">아니요</span><span class="sxs-lookup"><span data-stu-id="fad0a-124">No</span></span> |
| <span data-ttu-id="fad0a-125">Azure AD(Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="fad0a-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="fad0a-126">Azure AD 클라우드만 해당</span><span class="sxs-lookup"><span data-stu-id="fad0a-126">Azure AD cloud only</span></span> |<span data-ttu-id="fad0a-127">예</span><span class="sxs-lookup"><span data-stu-id="fad0a-127">Yes</span></span> |<span data-ttu-id="fad0a-128">아니요</span><span class="sxs-lookup"><span data-stu-id="fad0a-128">No</span></span> |
| <span data-ttu-id="fad0a-129">암호 동기화를 사용하는 ADsync</span><span class="sxs-lookup"><span data-stu-id="fad0a-129">ADsync with password sync</span></span> |<span data-ttu-id="fad0a-130">예</span><span class="sxs-lookup"><span data-stu-id="fad0a-130">Yes</span></span> |<span data-ttu-id="fad0a-131">예</span><span class="sxs-lookup"><span data-stu-id="fad0a-131">Yes</span></span> |
| <span data-ttu-id="fad0a-132">암호 동기화를 사용하지 않는 ADsync</span><span class="sxs-lookup"><span data-stu-id="fad0a-132">ADsync without password sync</span></span> |<span data-ttu-id="fad0a-133">예</span><span class="sxs-lookup"><span data-stu-id="fad0a-133">Yes</span></span> |<span data-ttu-id="fad0a-134">아니요</span><span class="sxs-lookup"><span data-stu-id="fad0a-134">No</span></span> |
| <span data-ttu-id="fad0a-135">AD FS 포함 ADsync</span><span class="sxs-lookup"><span data-stu-id="fad0a-135">ADsync with AD FS</span></span> |<span data-ttu-id="fad0a-136">예</span><span class="sxs-lookup"><span data-stu-id="fad0a-136">Yes</span></span> |<span data-ttu-id="fad0a-137">yes</span><span class="sxs-lookup"><span data-stu-id="fad0a-137">Yes</span></span> |
| <span data-ttu-id="fad0a-138">[타사 Azure 지원 ID 공급자](https://msdn.microsoft.com/library/azure/jj679342.aspx)(예: Ping)</span><span class="sxs-lookup"><span data-stu-id="fad0a-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="fad0a-139">yes</span><span class="sxs-lookup"><span data-stu-id="fad0a-139">Yes</span></span> |<span data-ttu-id="fad0a-140">예</span><span class="sxs-lookup"><span data-stu-id="fad0a-140">Yes</span></span> |
| <span data-ttu-id="fad0a-141">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="fad0a-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="fad0a-142">예</span><span class="sxs-lookup"><span data-stu-id="fad0a-142">Yes</span></span> |<span data-ttu-id="fad0a-143">예</span><span class="sxs-lookup"><span data-stu-id="fad0a-143">Yes</span></span> |

<span data-ttu-id="fad0a-144">RemoteApp에 대한 Active Directory 구성에 대한 [자세한 내용](remoteapp-ad.md) 을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="fad0a-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="fad0a-145">Azure Active Directory 사용자는 구독과 연결된 테넌트로부터 시작되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad0a-145">The Azure Active Directory users must be from the tenant that's associated with your subscription.</span></span> <span data-ttu-id="fad0a-146">(포털의 **설정** 페이지에서 구독을 보고 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad0a-146">(You can view and modify your subscription on the **Settings** tab in the portal.</span></span> <span data-ttu-id="fad0a-147">자세한 내용은 [RemoteApp에서 사용되는 Azure Active Directory 테넌트 변경](remoteapp-changetenant.md) 을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="fad0a-147">See [Change the Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="fad0a-148">Office 365 ProPlus 사용자 계정 정보</span><span class="sxs-lookup"><span data-stu-id="fad0a-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="fad0a-149">컬렉션에서 Office 365 ProPlus 템플릿 이미지를 사용하는 경우 *또는* Office 365를 사용하는 사용자 지정 이미지를 만든 경우 Office 365 구독이 있는 Azure Active Directory 사용자만 구독의 기본 도메인에 대해 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad0a-149">If you are using the Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed to add Azure Active Directory users that have Office 365 subscriptions for the default domain of your subscription.</span></span> <span data-ttu-id="fad0a-150">자세한 내용은 [Azure RemoteApp과 함께 Office 365 사용](remoteapp-o365.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fad0a-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

