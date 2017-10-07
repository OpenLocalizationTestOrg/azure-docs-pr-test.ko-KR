---
title: "Azure Active Directory의 aaaDedicated 그룹 | Microsoft Docs"
description: "전용된 그룹의 Azure Active Directory를 사용한 작업 방식 및 작성된 방법의 개요입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="da86b-103">Azure Active Directory의 전용 그룹</span><span class="sxs-lookup"><span data-stu-id="da86b-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="da86b-104">Azure Active Directory (Azure AD)에 hello 전용된 그룹 기능은 자동으로 만들고 미리 정의 된 Azure AD 그룹에 대 한 멤버 자격을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-104">In Azure Active Directory (Azure AD), hello dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="da86b-105">전용된 그룹의 구성원을 추가할 수 없습니다 또는 Azure 클래식 포털에서 Windows PowerShell cmdlet을 환영 제거를 사용 하 여 또는 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-105">Members of dedicated groups cannot be added or removed using hello Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="da86b-106">전용 그룹에는 할당된 Azure AD Premium 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="da86b-107">hello 규칙 그룹에서 관리 하는 hello 관리자</span><span class="sxs-lookup"><span data-stu-id="da86b-107">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="da86b-108">hello로 선택 되는 모든 사용자 규칙 toobe hello 그룹의 구성원</span><span class="sxs-lookup"><span data-stu-id="da86b-108">all users who are selected by hello rule toobe a member of hello group</span></span>
>
>

<span data-ttu-id="da86b-109">**전용 tooenable 그룹**</span><span class="sxs-lookup"><span data-stu-id="da86b-109">**tooenable dedicated groups**</span></span>

1. <span data-ttu-id="da86b-110">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory**, 한 다음 조직의 디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-110">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="da86b-111">선택 hello **그룹** 탭을 선택한 tooedit 연 다음 hello 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-111">Select hello **Groups** tab, and then open hello group you want tooedit.</span></span>
3. <span data-ttu-id="da86b-112">선택 hello **구성** 탭을 클릭 한 다음 설정 **전용 그룹 사용** 너무**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-112">Select hello **Configure** tab, and then set **Enable Dedicated Groups** too**Yes**.</span></span>

<span data-ttu-id="da86b-113">전용 그룹 사용 전환 hello 너무 설정 되 고 나면**예**를 추가로 설정할 수 있습니다 hello 디렉터리 tooautomatically hello 설정 하 여 hello 모든 사용자에 게 전용된 그룹을 만들 **"모든 사용자" 그룹** 너무 전환**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-113">Once hello Enable Dedicated Groups switch is set too**Yes**, you can further enable hello directory tooautomatically create hello All Users dedicated group by setting hello **Enable “All Users” Group** switch too**Yes**.</span></span> <span data-ttu-id="da86b-114">그런 다음도 이름을 편집할 수 있습니다 hello 전용 그룹 hello에 입력 하 여 **"모든 사용자"에 대 한 표시 이름을 그룹** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-114">You can then also edit hello name of this dedicated group by typing it in hello **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="da86b-115">hello 모든 사용자 그룹을 사용할 수 있습니다 tooassign hello 디렉터리에 동일한 tooall hello 사용자 사용 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-115">hello All Users group can be used tooassign hello same permissions tooall hello users in your directory.</span></span> <span data-ttu-id="da86b-116">예를 들어 hello 모든 사용자에 게 전용된 그룹 toothis 응용 프로그램에 대 한 액세스를 할당 하 여 모든 사용자에 게 디렉터리 액세스 tooa SaaS 응용 프로그램에에서 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-116">For example, you can grant all users in your directory access tooa SaaS application by assigning access for hello All Users dedicated group toothis application.</span></span>

<span data-ttu-id="da86b-117">게스트 및 외부 사용자를 포함 하 여 hello 디렉터리에 모든 사용자를 포함 하는 전용 hello 모든 사용자 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-117">hello dedicated All Users group includes all users in hello directory, including guests and external users.</span></span> <span data-ttu-id="da86b-118">그룹이 필요한 외부 사용자를 제외 하는 경우 hello 다음과 같은 특성 기반 동적 규칙 그룹을 만들면이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as hello following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="da86b-119">모든 게스트 제외 된 그룹에 대 한 hello 다음과 같은 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-119">For a group that excludes all Guests, use a rule such as hello following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="da86b-120">방법에 대 한 toolearn toocreate *고급* 규칙 (여러 비교를 포함할 수 있는 규칙) 동적 그룹 멤버 자격에 대 한 참조 [toocreate 특성을 사용 하 여 고급 규칙](active-directory-accessmanagement-groups-with-advanced-rules.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-120">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="da86b-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da86b-121">Next steps</span></span>
<span data-ttu-id="da86b-122">이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da86b-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="da86b-123">Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리</span><span class="sxs-lookup"><span data-stu-id="da86b-123">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="da86b-124">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="da86b-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="da86b-125">Azure Active Directory란?</span><span class="sxs-lookup"><span data-stu-id="da86b-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="da86b-126">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="da86b-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
