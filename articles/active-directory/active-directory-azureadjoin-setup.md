---
title: "사용자의 Azure AD 조인 설정 | Microsoft Docs"
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
ms.openlocfilehash: c37adc2654f7e931fdda22627e4a6ece2789fd86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="fc39e-103">조직에서 Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="fc39e-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="fc39e-104">Azure Active Directory 연결(Azure AD 연결)을 설정하기 전에 사용자의 온-프레미스 디렉터리를 클라우드와 동기화하거나 Azure AD에서 관리되는 계정을 수동으로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-104">Before you set up Azure Active Directory Join (Azure AD Join), you need to either sync up your on-premises directory of users to the cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="fc39e-105">온-프레미스 사용자와 Azure AD의 동기화에 대한 자세한 지침을 보려면 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc39e-105">Detailed instructions for syncing your on-premises users to Azure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="fc39e-106">Azure AD에서 사용자를 수동으로 만들고 관리하려면 [Azure AD에서 사용자 관리](https://msdn.microsoft.com/library/azure/hh967609.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc39e-106">To manually create and manage users in Azure AD, refer to [User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="fc39e-107">장치 등록 설정</span><span class="sxs-lookup"><span data-stu-id="fc39e-107">Set up device registration</span></span>
1. <span data-ttu-id="fc39e-108">관리자 권한으로 Azure 포털에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-108">Log on to the Azure portal as an administrator.</span></span>
2. <span data-ttu-id="fc39e-109">왼쪽 창에서 **Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-109">On the left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="fc39e-110">**디렉터리** 탭에서 해당 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-110">On the **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="fc39e-111">**구성** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-111">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="fc39e-112">**장치** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-112">Go to the **Devices** section.</span></span>
6. <span data-ttu-id="fc39e-113">**장치** 탭에서 다음을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-113">On the **devices** tab, set the following:</span></span>  
   * <span data-ttu-id="fc39e-114">**사용자당 최대 장치 수**: Azure AD에서 사용자가 보유할 수 있는 장치의 최대 수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select the maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="fc39e-115">사용자가 이 할당량에 도달하는 경우 기존 장치 중 하나 이상이 제거될 때까지 장치를 더 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-115">If a user reaches this quota, they will not be able to add additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="fc39e-116">**장치에 연결하기 위해 다단계 인증 필요**: 사용자가 Azure AD에 장치를 연결하기 위해 또 다른 인증 수단을 제공해야 하는지 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-116">**REQUIRE MULTI-FACTOR AUTH TO JOIN DEVICES**: Set whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="fc39e-117">Azure Multi-Factor Authentication에 대한 자세한 내용은 [클라우드에서 Azure Multi-Factor Authentication 시작](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc39e-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in the cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="fc39e-118">**사용자가 Azure AD에 장치를 연결할 수 있음**: Azure AD에 장치를 연결하도록 허용된 사용자 및 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-118">**USERS MAY AZURE AD JOIN DEVICES**: Select the users and groups that are allowed to join devices to Azure AD.</span></span>
   * <span data-ttu-id="fc39e-119">**Azure AD 연결 장치의 추가 관리자**: Azure AD Premium 또는 EMS(Enterprise Mobility Suite)를 사용하여 장치에 대한 로컬 관리자 권한을 부여 받은 사용자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or the Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights to the device.</span></span> <span data-ttu-id="fc39e-120">전역 관리자 및 장치 소유자에게는 기본적으로 로컬 관리자 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="fc39e-121"><center>![장치 등록 설정](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="fc39e-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="fc39e-122">사용자를 위해 Azure AD 조인을 설정하면 해당 회사 또는 개인 장치를 통해 Azure AD에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-122">After you set up Azure AD Join for your users, they can connect to Azure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="fc39e-123">다음은 사용자가 Azure AD 연결을 설정할 수 있는 세 가지 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-123">Following are the three scenarios you can use to enable your users to set up Azure AD Join:</span></span>

* <span data-ttu-id="fc39e-124">사용자가 Azure AD에 직접 회사 소유의 장치를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-124">Users join a company-owned device directly to Azure AD.</span></span>
* <span data-ttu-id="fc39e-125">사용자가 온-프레미스 Active Directory에 회사 소유의 장치를 연결한 다음 장치를 Azure AD로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="fc39e-125">Users domain-join a company-owned device to the on-premises Active Directory and then extend the device to Azure AD.</span></span>
* <span data-ttu-id="fc39e-126">사용자가 개인 장치의 Windows에 회사 또는 학교 계정 추가</span><span class="sxs-lookup"><span data-stu-id="fc39e-126">Users add work or school accounts to Windows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="fc39e-127">추가 정보</span><span class="sxs-lookup"><span data-stu-id="fc39e-127">Additional information</span></span>
* [<span data-ttu-id="fc39e-128">엔터프라이즈를 위한 Windows 10: 작업에 장치를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="fc39e-128">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="fc39e-129">Azure Active Directory 조인을 통해 클라우드 기능을 Windows 10 장치로 확장</span><span class="sxs-lookup"><span data-stu-id="fc39e-129">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="fc39e-130">Azure AD 조인에 대한 사용 시나리오에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="fc39e-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="fc39e-131">Windows 10 환경용 Azure AD에 도메인 가입된 장치 연결</span><span class="sxs-lookup"><span data-stu-id="fc39e-131">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="fc39e-132">Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="fc39e-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

