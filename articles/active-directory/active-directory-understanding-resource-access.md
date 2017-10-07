---
title: "Azure에서 리소스 액세스 aaaUnderstanding | Microsoft Docs"
description: "이 항목에서는 구독 관리자가 toocontrol 리소스 액세스를 사용 하 여 hello에 대 한 개념을 설명 전체 Azure 포털"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 06b9c4166bdea849faae67cae3146c6c278deb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-resource-access-in-azure"></a><span data-ttu-id="6ea31-103">Azure의 리소스 액세스 이해</span><span class="sxs-lookup"><span data-stu-id="6ea31-103">Understanding resource access in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6ea31-104">Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-104">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="6ea31-105">hello Azure 포털에서 제공 [역할 기반 액세스 제어](role-based-access-control-configure.md) Azure 리소스를 보다 정확 하 게 관리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-105">hello Azure portal provides [role-based access control](role-based-access-control-configure.md) so Azure resources can be managed more precisely.</span></span>
> 
> 

<span data-ttu-id="6ea31-106">2013 년 10 월 hello Azure 클래식 포털 및 서비스 관리 Api는 Azure Active Directory와 통합 되었습니다 tooAzure 리소스에 액세스를 관리 하기 위한 hello 사용자 환경을 개선 하기 위한 순서 toolay hello 기반이에서.</span><span class="sxs-lookup"><span data-stu-id="6ea31-106">In October 2013, hello Azure classic portal and Service Management APIs were integrated with Azure Active Directory in order toolay hello groundwork for improving hello user experience for managing access tooAzure resources.</span></span> <span data-ttu-id="6ea31-107">Azure Active Directory는 이미 사용자 관리, 온-프레미스 디렉터리 동기화, 다단계 인증 및 응용 프로그램 액세스 제어와 같은 훌륭한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-107">Azure Active Directory already provides great capabilities such as user management, on-premises directory sync, multi-factor authentication, and application access control.</span></span> <span data-ttu-id="6ea31-108">물론 이러한 기능들로 Azure 리소스를 전반적으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-108">Naturally, these should also be made available for managing Azure resources across-the-board.</span></span>

<span data-ttu-id="6ea31-109">Azure의 액세스 제어는 결제 관점에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-109">Access control in Azure starts from a billing perspective.</span></span> <span data-ttu-id="6ea31-110">hello를 방문 하 여 액세스 하는 Azure 계정의 소유자 hello [Azure 계정 센터](https://account.windowsazure.com/subscriptions)는 hello AA (계정 관리자)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-110">hello owner of an Azure account, accessed by visiting hello  [Azure Accounts Center](https://account.windowsazure.com/subscriptions), is hello Account Administrator (AA).</span></span> <span data-ttu-id="6ea31-111">구독은 결제를 위한 컨테이너 이지만 보안 경계로도 작동 합니다: 각 구독에는 서비스 관리자 (SA) 추가, 제거 및 hello를 사용 하 여 해당 구독의 Azure 리소스를 수정할 수 있는 [Azure클래식포털](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="6ea31-111">Subscriptions are a container for billing, but they also act as a security boundary: each subscription has a Service Administrator (SA) who can add, remove, and modify Azure resources in that subscription by using hello [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="6ea31-112">새 구독의 기본 SA hello hello AA 이지만 AA hello hello Azure 계정 센터에서에서 hello SA를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-112">hello default SA of a new subscription is hello AA, but hello AA can change hello SA in hello Azure Accounts Center.</span></span>

<br><br>![Azure 계정][1]

<span data-ttu-id="6ea31-114">또한 구독은 디렉터리와 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-114">Subscriptions also have an association with a directory.</span></span> <span data-ttu-id="6ea31-115">hello 디렉터리 사용자 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-115">hello directory defines a set of users.</span></span> <span data-ttu-id="6ea31-116">Hello 회사 또는 학교 hello 디렉터리를 만든 사용자가 될 수 있습니다. 또는 외부 사용자 (즉, Microsoft 계정) 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-116">These can be users from hello work or school that created hello directory or they can be external users (that is, Microsoft Accounts).</span></span> <span data-ttu-id="6ea31-117">구독을 서비스 관리자 (SA) 또는 CA (공동 관리자);에 지정 된 해당 디렉터리 사용자의 하위 집합에서 액세스할 수 있습니다. hello 예외만, 레거시의 이유로 Microsoft 계정 (이전의 Windows Live ID) 할당할 수 있는 SA 또는 CA로 hello 디렉터리에 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-117">Subscriptions are accessible by a subset of those directory users who have been assigned as either Service Administrator (SA) or Co-Administrator (CA); hello only exception is that, for legacy reasons, Microsoft Accounts (formerly Windows Live ID) can be assigned as SA or CA without being present in hello directory.</span></span>

<br><br>![Azure의 액세스 제어][2]

<span data-ttu-id="6ea31-119">Hello Azure 클래식 포털 내에서 기능을 통해 구독 hello를 사용 하 여 연결 된 Microsoft 계정 toochange hello 디렉터리를 사용 하 여 로그인 하는 Sa **디렉터리 편집** hello 명령을**구독** 페이지 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-119">Functionality within hello Azure classic portal enables SAs that are signed in using a Microsoft Account toochange hello directory that a subscription is associated with by using hello **Edit Directory** command on hello **Subscriptions** page in **Settings**.</span></span> <span data-ttu-id="6ea31-120">이 작업은 해당 구독의 hello 액세스 제어에 미치는 영향 메모 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-120">Note that this operation has implications on hello access control of that subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="6ea31-121">hello **디렉터리 편집** hello Azure 클래식 포털을 사용할 수 있는 toousers는 작업을 사용 하 여 로그인 없습니다 또는 학교 계정을 해당 계정이 속한만 toohello 디렉터리 toowhich 로그인 할 수 있으므로 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-121">hello **Edit Directory** command in hello Azure classic portal is not available toousers who are signed in using a work or school account because those accounts can sign in only toohello directory toowhich they belong.</span></span>
> 
> 

<br><br>![간단한 사용자 로그인 흐름][3]

<span data-ttu-id="6ea31-123">Hello 단순한 경우, 조직 (예: Contoso) 청구를 적용 한 액세스 제어를 한 구독 설정 같은 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-123">In hello simple case, an organization (such as Contoso) will enforce billing and access control across hello same set of subscriptions.</span></span> <span data-ttu-id="6ea31-124">즉, hello 디렉터리는 단일 Azure 계정이 소유한 관련된 toosubscriptions입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-124">That is, hello directory is associated toosubscriptions that are owned by a single Azure Account.</span></span> <span data-ttu-id="6ea31-125">성공한 로그인 toohello Azure 클래식 포털 하면 사용자는 두 개의 리소스 (hello 앞의 그림에서 주황색으로 표시 된) 컬렉션을 볼:</span><span class="sxs-lookup"><span data-stu-id="6ea31-125">Upon successful login toohello Azure classic portal, users see two collections of resources (depicted in orange in hello previous illustration):</span></span>

* <span data-ttu-id="6ea31-126">사용자 계정이 있는 디렉터리 (원본 또는 외래 사용자로 추가).</span><span class="sxs-lookup"><span data-stu-id="6ea31-126">Directories where their user account exists (sourced or added as a foreign principal).</span></span> <span data-ttu-id="6ea31-127">Note 로그인에 사용 되는 해당 hello 디렉터리 없는 관련 toothis 계산 하므로 사용자가 로그인 하는 것에 관계 없이 디렉터리가 항상 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-127">Note that hello directory used for login isn’t relevant toothis computation, so your directories will always be shown regardless of where you logged in.</span></span>
* <span data-ttu-id="6ea31-128">연결 된 로그인에 사용 되는 hello 디렉터리는 hello 사용자 구독의 일부인 리소스 (여기서은 SA 또는 CA) 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-128">Resources that are part of subscriptions that are associated with hello directory used for login AND which hello user can access (where they are an SA or CA).</span></span>

<br><br>![여러 구독 및 디렉터리가 있는 사용자][4]

<span data-ttu-id="6ea31-130">여러 디렉터리에 구독이 있는 사용자 hello 기능 tooswitch hello 현재 컨텍스트가 제공 hello Azure 클래식 포털의 hello 구독 필터를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-130">Users with subscriptions across multiple directories have hello ability tooswitch hello current context of hello Azure classic portal by using hello subscription filter.</span></span> <span data-ttu-id="6ea31-131">Hello 내부적으로 별도 로그인 tooa 다른 디렉터리에 있는이 발생 하지만이 위해서는 single sign on (SSO) 원활 하 게 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-131">Under hello covers, this results in a separate login tooa different directory, but this is accomplished seamlessly using single sign-on (SSO).</span></span>

<span data-ttu-id="6ea31-132">구독 간에 리소스를 이동하는 등의 작업은 구독의 단일 디렉터리 보기의 결과로 더 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea31-132">Operations such as moving resources between subscriptions can be more difficult as a result of this single directory view of subscriptions.</span></span> <span data-ttu-id="6ea31-133">tooperform hello 리소스 전송 해야 toofirst hello를 사용 하 여 **디렉터리 편집** hello 구독 페이지에서 명령을 **설정을** tooassociate hello 구독 toohello 동일한 디렉터리 .</span><span class="sxs-lookup"><span data-stu-id="6ea31-133">tooperform hello resource transfer, it may be necessary toofirst use hello **Edit Directory** command on hello Subscriptions page in **Settings** tooassociate hello subscriptions toohello same directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ea31-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ea31-134">Next Steps</span></span>
* <span data-ttu-id="6ea31-135">toochange 관리자는 Azure 구독에 대 한 참조 하는 방법에 대해 더 알아봅니다을 toolearn [어떻게 tooadd 또는 변경 Azure 관리자 역할](../billing/billing-add-change-azure-subscription-administrator.md)</span><span class="sxs-lookup"><span data-stu-id="6ea31-135">toolearn more about how toochange administrators for an Azure subscription, see [How tooadd or change Azure administrator roles](../billing/billing-add-change-azure-subscription-administrator.md)</span></span>
* <span data-ttu-id="6ea31-136">Azure Active Directory tooyour Azure 구독 연결 되는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure 구독은 Azure Active Directory와 연결](active-directory-how-subscriptions-associated-directory.md)</span><span class="sxs-lookup"><span data-stu-id="6ea31-136">For more information on how Azure Active Directory relates tooyour Azure subscription, see [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)</span></span>
* <span data-ttu-id="6ea31-137">방법에 대 한 자세한 내용은 Azure AD에서 tooassign 역할 참조 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="6ea31-137">For more information on how tooassign roles in Azure AD, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md)</span></span>

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
