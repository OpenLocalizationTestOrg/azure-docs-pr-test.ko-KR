---
title: "사용자를 위해 Azure AD Join를 aaaSetting | Microsoft Docs"
description: "관리자가 온-프레미스 디렉터리 및 장치 등록에 Azure AD 조인을 설치하는 방법을 설명합니다."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="a5af3-103">조직에서 Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="a5af3-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="a5af3-104">Tooeither 동기화가 필요한 Azure Active Directory Join (Azure AD Join)를 설정 하기 전에 온-프레미스 디렉터리의 사용자가 toohello 클라우드 또는 Azure AD에서 관리 되는 계정을 수동으로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-104">Before you set up Azure Active Directory Join (Azure AD Join), you need tooeither sync up your on-premises directory of users toohello cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="a5af3-105">에 대해서는 온-프레미스 사용자 tooAzure AD를 동기화 하는 중에 대 한 자세한 정보가 [Azure Active Directory와 온-프레미스 id 통합](active-directory-aadconnect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-105">Detailed instructions for syncing your on-premises users tooAzure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="a5af3-106">만들기 및 Azure AD에서 사용자 관리, 너무 참조 toomanually[Azure AD의 사용자 관리](https://msdn.microsoft.com/library/azure/hh967609.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-106">toomanually create and manage users in Azure AD, refer too[User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="a5af3-107">장치 등록 설정</span><span class="sxs-lookup"><span data-stu-id="a5af3-107">Set up device registration</span></span>
1. <span data-ttu-id="a5af3-108">관리자 권한으로 Azure 포털 toohello에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-108">Log on toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="a5af3-109">Hello 왼쪽된 창에서 선택 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-109">On hello left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="a5af3-110">Hello에 **디렉터리** 탭에서 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-110">On hello **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="a5af3-111">선택 hello **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-111">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="a5af3-112">Toohello 이동 **장치** 섹션.</span><span class="sxs-lookup"><span data-stu-id="a5af3-112">Go toohello **Devices** section.</span></span>
6. <span data-ttu-id="a5af3-113">Hello에 **장치** 탭, hello 다음을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-113">On hello **devices** tab, set hello following:</span></span>  
   * <span data-ttu-id="a5af3-114">**최대 수의 장치 사용자 단위**: hello 최대 Azure AD에서 사용자가 있는 장치 수를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select hello maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="a5af3-115">사용자가이 할당량에 도달 됩니다 수 tooadd 추가 장치 하나 이상의 기존 장치가 제거 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-115">If a user reaches this quota, they will not be able tooadd additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="a5af3-116">**필요한 MULTI-FACTOR AUTH tooJOIN 장치**: 사용자가 필요한 tooprovide 쓸지를 설정할 두 번째 인증 단계 toojoin 자신의 장치 tooAzure AD 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-116">**REQUIRE MULTI-FACTOR AUTH tooJOIN DEVICES**: Set whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="a5af3-117">Azure Multi-factor Authentication에 대 한 자세한 내용은 참조 하십시오. [hello 클라우드에서 Azure Multi-factor Authentication 시작](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in hello cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="a5af3-118">**사용자가 AZURE AD 조인 장치의 수 있습니다.**: toojoin 장치 tooAzure AD는 사용할 수 있는 hello 사용자 및 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-118">**USERS MAY AZURE AD JOIN DEVICES**: Select hello users and groups that are allowed toojoin devices tooAzure AD.</span></span>
   * <span data-ttu-id="a5af3-119">**추가 관리자에 AZURE AD 조인 장치의**: Azure AD Premium 또는 Enterprise Mobility Suite (EMS) hello 있습니다 선택할 수 있는 사용자는 로컬 관리자 권한이 부여 됩니다 toohello 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or hello Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights toohello device.</span></span> <span data-ttu-id="a5af3-120">전역 관리자 및 장치 소유자에게는 기본적으로 로컬 관리자 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="a5af3-121"><center>![장치 등록 설정](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="a5af3-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="a5af3-122">사용자를 위해 Azure AD Join를 설정한 후 tooAzure AD 통해 자신의 회사 또는 개인 장치를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-122">After you set up Azure AD Join for your users, they can connect tooAzure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="a5af3-123">다음은 hello 세 가지 시나리오를 Azure AD Join tooenable 사용자 tooset을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-123">Following are hello three scenarios you can use tooenable your users tooset up Azure AD Join:</span></span>

* <span data-ttu-id="a5af3-124">사용자가 회사 소유의 장치를 조인할 tooAzure AD 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-124">Users join a company-owned device directly tooAzure AD.</span></span>
* <span data-ttu-id="a5af3-125">사용자가 회사 소유의 도메인 가입 장치 toohello 온-프레미스 Active Directory와 hello 장치 tooAzure AD까지 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-125">Users domain-join a company-owned device toohello on-premises Active Directory and then extend hello device tooAzure AD.</span></span>
* <span data-ttu-id="a5af3-126">사용자가 추가 작업 또는 학교 계정 tooWindows 개인 장치에</span><span class="sxs-lookup"><span data-stu-id="a5af3-126">Users add work or school accounts tooWindows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="a5af3-127">추가 정보</span><span class="sxs-lookup"><span data-stu-id="a5af3-127">Additional information</span></span>
* [<span data-ttu-id="a5af3-128">Hello 엔터프라이즈용 Windows 10: 작업에 대 한 방법으로 toouse 장치</span><span class="sxs-lookup"><span data-stu-id="a5af3-128">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="a5af3-129">Azure Active Directory Join을 통해 기능 10 tooWindows 장치 클라우드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="a5af3-129">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="a5af3-130">Azure AD 조인에 대한 사용 시나리오에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="a5af3-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="a5af3-131">Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결</span><span class="sxs-lookup"><span data-stu-id="a5af3-131">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="a5af3-132">Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="a5af3-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

