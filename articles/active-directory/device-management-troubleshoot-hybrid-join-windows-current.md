---
title: "aaaTroubleshooting 하이브리드 Azure Active Directory 가입 Windows 10 및 Windows Server 2016 장치 | Microsoft Docs"
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
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="1543c-103">Windows 10 및 Windows Server 2016 장치에 조인된 하이브리드 Azure Active Directory 문제 해결</span><span class="sxs-lookup"><span data-stu-id="1543c-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="1543c-104">이 항목은 적용 가능한 toohello 다음 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="1543c-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="1543c-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="1543c-105">Windows 10</span></span>
-   <span data-ttu-id="1543c-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="1543c-106">Windows Server 2016</span></span>

<span data-ttu-id="1543c-107">다른 Windows 클라이언트의 경우 [하위 수준 장치에 조인된 하이브리드 Azure Active Directory 문제 해결](device-management-troubleshoot-hybrid-join-windows-legacy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1543c-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="1543c-108">이 항목에서는 있다고 가정 [구성 된 하이브리드 Azure Active Directory 가입 장치](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello 다음 시나리오:</span><span class="sxs-lookup"><span data-stu-id="1543c-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="1543c-109">장치 기반 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="1543c-109">Device-based conditional access</span></span>

- [<span data-ttu-id="1543c-110">엔터프라이즈 설정 로밍</span><span class="sxs-lookup"><span data-stu-id="1543c-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="1543c-111">비즈니스용 Windows Hello</span><span class="sxs-lookup"><span data-stu-id="1543c-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="1543c-112">이 문서에 어떻게 tooresolve 잠재적 문제 해결 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 


<span data-ttu-id="1543c-113">Azure Active Directory join 지원 hello Windows 하이브리드 Windows 10 및 Windows Server 2016에 대 한 10 2015 년 11 월 업데이트 이상.</span><span class="sxs-lookup"><span data-stu-id="1543c-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports hello Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="1543c-114">Hello Anniversary 업데이트를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-114">We recommend using hello Anniversary update.</span></span>

## <a name="step-1-retrieve-hello-join-status"></a><span data-ttu-id="1543c-115">1 단계: hello 조인 상태를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-115">Step 1: Retrieve hello join status</span></span> 

<span data-ttu-id="1543c-116">**tooretrieve hello 조인 상태:**</span><span class="sxs-lookup"><span data-stu-id="1543c-116">**tooretrieve hello join status:**</span></span>

1. <span data-ttu-id="1543c-117">관리자 권한으로 명령 프롬프트를 열고 hello</span><span class="sxs-lookup"><span data-stu-id="1543c-117">Open hello command prompt as an administrator</span></span>

2. <span data-ttu-id="1543c-118">**dsregcmd /status**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="1543c-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="1543c-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="1543c-120">EnterpriseJoined: DeviceId 없음: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 지문: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft 플랫폼 암호화 공급자 TpmProtected: 예 KeySignTest:: tootest 상승 된 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="1543c-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="1543c-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="1543c-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="1543c-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="1543c-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span><span class="sxs-lookup"><span data-stu-id="1543c-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-hello-join-status"></a><span data-ttu-id="1543c-124">2 단계: hello 조인 상태를 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-124">Step 2: Evaluate hello join status</span></span> 

<span data-ttu-id="1543c-125">Hello 다음 필드를 검토 하 고 hello 예상 값을 갖는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1543c-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="1543c-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="1543c-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="1543c-127">이 필드는 hello 장치가 Azure AD와 연결 되 고 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-127">This field indicates whether hello device is joined with Azure AD.</span></span> <span data-ttu-id="1543c-128">Hello 값이 **아니요**, hello 조인 tooAzure AD 아직 완료 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-128">If hello value is **NO**, hello join tooAzure AD has not completed yet.</span></span> 

<span data-ttu-id="1543c-129">**가능한 원인:**</span><span class="sxs-lookup"><span data-stu-id="1543c-129">**Possible causes:**</span></span>

- <span data-ttu-id="1543c-130">조인에 대 한 hello 컴퓨터의 인증에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-130">Authentication of hello computer for a join failed.</span></span>

- <span data-ttu-id="1543c-131">Hello 컴퓨터도 찾을 수 없습니다 hello 조직 중인 HTTP 프록시</span><span class="sxs-lookup"><span data-stu-id="1543c-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="1543c-132">hello 컴퓨터 등록에 대 한 Azure AD tooauthenticate 또는 Azure DRS에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-132">hello computer cannot reach Azure AD tooauthenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="1543c-133">hello 컴퓨터 아닐 hello 조직의 내부 네트워크 또는 VPN의 직선 tooan와 온-프레미스 AD 도메인 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="1543c-134">Hello 컴퓨터에서 TPM을 잘못 된 상태에 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-134">If hello computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="1543c-135">Hello 서비스에서 잘못 된 구성 앞에서 기록한 hello 문서에 다시 tooverify를 필요 함이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-135">There might be a misconfiguration in hello services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="1543c-136">일반적인 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-136">Common examples are:</span></span>

    - <span data-ttu-id="1543c-137">페더레이션 서버에서 Ws-Trust 끝점이 사용되도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="1543c-138">페더레이션 서버는 Windows 통합 인증을 사용한 네트워크 컴퓨터에서의 인바운드 인증을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="1543c-139">Azure AD에서 hello 컴퓨터 속한 hello AD 포리스트에 tooyour 확인 된 도메인 이름을 가리키는 서비스 연결 지점 개체가 없는</span><span class="sxs-lookup"><span data-stu-id="1543c-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="1543c-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="1543c-140">DomainJoined : YES</span></span>  

<span data-ttu-id="1543c-141">이 필드는 hello 장치가 가입 된 여부 tooan 온-프레미스 Active Directory 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-141">This field indicates whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="1543c-142">Hello 값이 **아니요**, hello 장치는 Azure AD 하이브리드 조인을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-142">If hello value is **NO**, hello device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="1543c-143">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="1543c-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="1543c-144">이 필드 hello 장치를 개인 장치로 Azure AD에 등록 되었는지 여부를 나타냅니다 (로 표시 된 *작업 공간 연결*).</span><span class="sxs-lookup"><span data-stu-id="1543c-144">This field indicates whether hello device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="1543c-145">이 값은 하이브리드 Azure AD 조인된 도메인에 가입된 컴퓨터에 대해 **아니요**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="1543c-146">Hello 값이 **예**, 회사 또는 학교 계정을 hello Azure AD 하이브리드 조인의 이전 toohello 완료 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-146">If hello value is **YES**, a work or school account was added prior toohello completion of hello hybrid Azure AD join.</span></span> <span data-ttu-id="1543c-147">이 경우 hello 계정은 Windows 10 (1607)의 hello Anniversary 업데이트 버전을 사용 하는 경우 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-147">In this case, hello account is ignored when using hello Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="1543c-148">WamDefaultSet : YES 및 AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="1543c-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="1543c-149">이러한 필드는 hello 사용자 tooAzure AD가 성공적으로 인증 여부를 나타내는 toohello 장치에 로그인 할 때입니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-149">These fields indicate whether hello user has successfully authenticated tooAzure AD when signing in toohello device.</span></span> <span data-ttu-id="1543c-150">Hello 값이 **아니요**, 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-150">If hello values are **NO**, it could be due:</span></span>

- <span data-ttu-id="1543c-151">등록 (확인 hello KeySignTest 높은 실행 하는 동안) 시 hello 장치와 연결 된 TPM의 잘못 된 저장소 키 (STK)입니다.</span><span class="sxs-lookup"><span data-stu-id="1543c-151">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="1543c-152">대체 로그인 ID</span><span class="sxs-lookup"><span data-stu-id="1543c-152">Alternate Login ID</span></span>

- <span data-ttu-id="1543c-153">HTTP 프록시를 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="1543c-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="1543c-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1543c-154">Next steps</span></span>

<span data-ttu-id="1543c-155">질문에 대 한 참조 hello [장치 관리 FAQ](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="1543c-155">For questions, see hello [device management FAQ](device-management-faq.md)</span></span> 
