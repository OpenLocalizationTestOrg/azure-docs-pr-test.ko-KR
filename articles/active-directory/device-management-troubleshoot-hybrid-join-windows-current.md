---
title: "Windows 10 및 Windows Server 2016 장치에 조인된 하이브리드 Azure Active Directory 문제 해결 | Microsoft Docs"
description: "Windows 10 및 Windows Server 2016 장치에 조인된 하이브리드 Azure Active Directory 문제 해결"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 51962c14a3c32bbfa9a613fa203cc48cfea50c0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="c0739-103">Windows 10 및 Windows Server 2016 장치에 조인된 하이브리드 Azure Active Directory 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c0739-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="c0739-104">이 항목은 다음 클라이언트에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="c0739-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="c0739-105">Windows 10</span></span>
-   <span data-ttu-id="c0739-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c0739-106">Windows Server 2016</span></span>

<span data-ttu-id="c0739-107">다른 Windows 클라이언트의 경우 [하위 수준 장치에 조인된 하이브리드 Azure Active Directory 문제 해결](device-management-troubleshoot-hybrid-join-windows-legacy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0739-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="c0739-108">이 항목에서는 다음 시나리오를 지원하도록 [장치에 조인된 하이브리드 Azure Active Directory를 구성](device-management-hybrid-azuread-joined-devices-setup.md)했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) to support the following scenarios:</span></span>

- <span data-ttu-id="c0739-109">장치 기반 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="c0739-109">Device-based conditional access</span></span>

- [<span data-ttu-id="c0739-110">엔터프라이즈 설정 로밍</span><span class="sxs-lookup"><span data-stu-id="c0739-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="c0739-111">비즈니스용 Windows Hello</span><span class="sxs-lookup"><span data-stu-id="c0739-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="c0739-112">이 문서에서는 잠재적인 문제를 해결하는 방법에 대한 문제 해결 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 


<span data-ttu-id="c0739-113">Windows 10 및 Windows Server 2016의 경우 하이브리드 Azure Active Directory 조인은 Windows 10 2015년 11월 업데이트 이상을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports the Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="c0739-114">1주년 업데이트를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-114">We recommend using the Anniversary update.</span></span>

## <a name="step-1-retrieve-the-join-status"></a><span data-ttu-id="c0739-115">1단계: 조인 상태 검색</span><span class="sxs-lookup"><span data-stu-id="c0739-115">Step 1: Retrieve the join status</span></span> 

<span data-ttu-id="c0739-116">**조인 상태를 검색하려면:**</span><span class="sxs-lookup"><span data-stu-id="c0739-116">**To retrieve the join status:**</span></span>

1. <span data-ttu-id="c0739-117">관리자 권한으로 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-117">Open the command prompt as an administrator</span></span>

2. <span data-ttu-id="c0739-118">**dsregcmd /status**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="c0739-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="c0739-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="c0739-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated to test.</span><span class="sxs-lookup"><span data-stu-id="c0739-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="c0739-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="c0739-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="c0739-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="c0739-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="c0739-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span><span class="sxs-lookup"><span data-stu-id="c0739-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-the-join-status"></a><span data-ttu-id="c0739-124">2단계: 조인 상태 평가</span><span class="sxs-lookup"><span data-stu-id="c0739-124">Step 2: Evaluate the join status</span></span> 

<span data-ttu-id="c0739-125">다음 필드를 검토하고 예상 값을 갖는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="c0739-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="c0739-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="c0739-127">이 필드는 장치가 Azure AD에 조인되어 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-127">This field indicates whether the device is joined with Azure AD.</span></span> <span data-ttu-id="c0739-128">값이 **아니요**인 경우 Azure AD에 대한 조인은 아직 완료되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-128">If the value is **NO**, the join to Azure AD has not completed yet.</span></span> 

<span data-ttu-id="c0739-129">**가능한 원인:**</span><span class="sxs-lookup"><span data-stu-id="c0739-129">**Possible causes:**</span></span>

- <span data-ttu-id="c0739-130">조인을 위한 컴퓨터 인증이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-130">Authentication of the computer for a join failed.</span></span>

- <span data-ttu-id="c0739-131">조직에 컴퓨터에서 검색될 수 없는 HTTP 프록시가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="c0739-132">컴퓨터가 인증을 위해 Azure AD에, 또는 등록을 위해 Azure DRS에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-132">The computer cannot reach Azure AD to authenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="c0739-133">컴퓨터가 조직의 내부 네트워크 또는 온-프레미스 AD 도메인 컨트롤러의 직접 가시선 내에 있는 VPN에 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="c0739-134">컴퓨터에 TPM이 있는 경우 잘못된 상태일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-134">If the computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="c0739-135">이전에 문서에 설명된 것처럼 다시 확인해야 하는 잘못된 서비스 구성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-135">There might be a misconfiguration in the services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="c0739-136">일반적인 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-136">Common examples are:</span></span>

    - <span data-ttu-id="c0739-137">페더레이션 서버에서 Ws-Trust 끝점이 사용되도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="c0739-138">페더레이션 서버는 Windows 통합 인증을 사용한 네트워크 컴퓨터에서의 인바운드 인증을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="c0739-139">컴퓨터가 속한 AD 포리스트의 Azure AD에서 확인된 도메인 이름을 가리키는 서비스 연결 지점 개체가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="c0739-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="c0739-140">DomainJoined : YES</span></span>  

<span data-ttu-id="c0739-141">이 필드는 장치가 온-프레미스 Active Directory에 조인되는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-141">This field indicates whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="c0739-142">값이 **아니요**인 경우 장치는 하이브리드 Azure AD 조인을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-142">If the value is **NO**, the device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="c0739-143">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="c0739-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="c0739-144">이 필드는 장치가 Azure AD에 개인 장치로 등록되어 있는지 여부를 나타냅니다(*작업 영역 조인*으로 표시).</span><span class="sxs-lookup"><span data-stu-id="c0739-144">This field indicates whether the device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="c0739-145">이 값은 하이브리드 Azure AD 조인된 도메인에 가입된 컴퓨터에 대해 **아니요**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="c0739-146">값이 **예**인 경우 하이브리드 Azure AD 조인을 완료하기 전에 회사 또는 학교 계정이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-146">If the value is **YES**, a work or school account was added prior to the completion of the hybrid Azure AD join.</span></span> <span data-ttu-id="c0739-147">이 경우 Windows 10 버전의 1주년 업데이트(1607)를 사용하는 경우 계정은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-147">In this case, the account is ignored when using the Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="c0739-148">WamDefaultSet : YES 및 AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="c0739-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="c0739-149">이러한 필드는 사용자가 장치에 로그인 시 Azure AD에서 성공적으로 인증되었는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-149">These fields indicate whether the user has successfully authenticated to Azure AD when signing in to the device.</span></span> <span data-ttu-id="c0739-150">값이 **아니요**인 경우 다음의 원인 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0739-150">If the values are **NO**, it could be due:</span></span>

- <span data-ttu-id="c0739-151">등록 시 장치에 연결된 TPM에 잘못된 저장소 키(STK)가 있습니다(상승된 권한으로 실행하면서 KeySignTest 확인).</span><span class="sxs-lookup"><span data-stu-id="c0739-151">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="c0739-152">대체 로그인 ID</span><span class="sxs-lookup"><span data-stu-id="c0739-152">Alternate Login ID</span></span>

- <span data-ttu-id="c0739-153">HTTP 프록시를 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="c0739-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0739-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c0739-154">Next steps</span></span>

<span data-ttu-id="c0739-155">질문은 [장치 관리 FAQ](device-management-faq.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0739-155">For questions, see the [device management FAQ](device-management-faq.md)</span></span> 