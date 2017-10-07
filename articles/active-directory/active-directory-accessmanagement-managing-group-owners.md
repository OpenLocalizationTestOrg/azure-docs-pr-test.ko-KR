---
title: "그룹을 사용 하 여 액세스 관리를 위해 aaaNext 단계 | Microsoft Docs"
description: "고급 방법-에 대 한의 하려면 보안 그룹 관리 방법과 toouse 이러한 그룹 toomanage 액세스 tooa 리소스입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4fd55f893290fac3551a130f29bd12709cf551e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="9463f-103">그룹에 대한 소유자 관리</span><span class="sxs-lookup"><span data-stu-id="9463f-103">Managing owners for a group</span></span>
<span data-ttu-id="9463f-104">리소스 소유자가 액세스 tooa 리소스 tooan Azure AD 그룹에 할당 되 면 hello 그룹의 구성원 hello hello 그룹 소유자에 의해 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9463f-104">Once a resource owner has assigned access tooa resource tooan Azure AD group, hello membership of hello group is managed by hello group owner.</span></span> <span data-ttu-id="9463f-105">hello 리소스 소유자 hello 권한 tooassign 사용자 toohello 리소스 toohello hello 그룹 소유자를 효과적으로 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="9463f-105">hello resource owner effectively delegates hello permission tooassign users toohello resource toohello owner of hello group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9463f-106">Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9463f-106">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="9463f-107">그룹 소유권 할당</span><span class="sxs-lookup"><span data-stu-id="9463f-107">Assigning group ownership</span></span>
<span data-ttu-id="9463f-108">**tooadd 소유자 tooa 그룹**</span><span class="sxs-lookup"><span data-stu-id="9463f-108">**tooadd an owner tooa group**</span></span>

1. <span data-ttu-id="9463f-109">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory**, 한 다음 조직의 디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9463f-109">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="9463f-110">선택 hello **그룹** 탭을 원하는 tooadd 소유자가 데이터를 연 다음 hello 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="9463f-110">Select hello **Groups** tab, and then open hello group that you want tooadd owners to.</span></span>
3. <span data-ttu-id="9463f-111">**소유자 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9463f-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="9463f-112">Hello에 **소유자 추가** 페이지,이 그룹의 hello 소유자로 tooadd 원하는이 이름은 toohello 추가 되어 있는지 확인 하는 select hello 사용자 **선택한** 창.</span><span class="sxs-lookup"><span data-stu-id="9463f-112">On hello **Add owners** page, select hello user that you want tooadd as hello owner of this group, and make sure this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="9463f-113">**그룹에서 소유자 tooremove**</span><span class="sxs-lookup"><span data-stu-id="9463f-113">**tooremove an owner from a group**</span></span>

1. <span data-ttu-id="9463f-114">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory**, 한 다음 조직의 디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9463f-114">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="9463f-115">선택 hello **그룹** 탭을 연 다음 hello 그룹을 tooremove에서 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="9463f-115">Select hello **Groups** tab, and then open hello group that you want tooremove an owner from.</span></span>
3. <span data-ttu-id="9463f-116">선택 hello **소유자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9463f-116">Select hello **Owners** tab.</span></span>
4. <span data-ttu-id="9463f-117">이 그룹에서 tooremove 원하고 다음 선택 select hello 소유자 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="9463f-117">Select hello owner that you want tooremove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="9463f-118">추가 정보</span><span class="sxs-lookup"><span data-stu-id="9463f-118">Additional information</span></span>
<span data-ttu-id="9463f-119">이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9463f-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="9463f-120">Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리</span><span class="sxs-lookup"><span data-stu-id="9463f-120">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="9463f-121">그룹 설정을 구성하는 Azure Active Directory cmdlets</span><span class="sxs-lookup"><span data-stu-id="9463f-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="9463f-122">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="9463f-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="9463f-123">Azure Active Directory란?</span><span class="sxs-lookup"><span data-stu-id="9463f-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="9463f-124">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="9463f-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
