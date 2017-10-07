---
title: "Windows 10 및 Windows Server 2016 용 aaaTroubleshooting hello 자동 등록의 Azure AD 도메인 연결 컴퓨터 | Microsoft Docs"
description: "Windows 10 및 Windows Server 2016에 대 한 연결 컴퓨터를 Azure AD 도메인의 hello 자동 등록 문제를 해결 합니다."
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="33241-103">가입 된 컴퓨터 tooAzure AD – Windows 10 및 Windows Server 2016 도메인의 자동 등록 문제 해결</span><span class="sxs-lookup"><span data-stu-id="33241-103">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="33241-104">이 항목은 적용 가능한 toohello 다음 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="33241-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="33241-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="33241-105">Windows 10</span></span>
-   <span data-ttu-id="33241-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="33241-106">Windows Server 2016</span></span>

<span data-ttu-id="33241-107">다른 Windows 클라이언트에 대 한 참조 [Windows 하위 클라이언트에 대 한 컴퓨터 tooAzure AD 가입 된 도메인의 자동 등록 문제 해결](active-directory-device-registration-troubleshoot-windows-legacy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="33241-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="33241-108">이 항목에서는 구성 자동 등록의 도메인에 가입 된 장치에서 설명한 대로 설명 된 [어떻게 tooconfigure 자동 등록의 Windows 도메인에 가입 된 장치의 Azure Active Directory와](active-directory-device-registration-get-started.md) 다음 시나리오는 toosupport hello:</span><span class="sxs-lookup"><span data-stu-id="33241-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) toosupport hello following scenarios:</span></span>

- [<span data-ttu-id="33241-109">장치 기반 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="33241-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="33241-110">엔터프라이즈 설정 로밍</span><span class="sxs-lookup"><span data-stu-id="33241-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="33241-111">비즈니스용 Windows Hello</span><span class="sxs-lookup"><span data-stu-id="33241-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="33241-112">이 문서에 어떻게 tooresolve 잠재적 문제 해결 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="33241-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 

<span data-ttu-id="33241-113">hello 등록은 지원 hello windows에서 10 2015 년 11 월 업데이트 이상.</span><span class="sxs-lookup"><span data-stu-id="33241-113">hello registration is supported in hello Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="33241-114">위의 hello 시나리오를 사용 하기 위한 hello Anniversary 업데이트를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="33241-114">We recommend using hello Anniversary Update for enabling hello scenarios above.</span></span>

## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="33241-115">1 단계: hello 등록 상태를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="33241-115">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="33241-116">**tooretrieve hello 등록 상태:**</span><span class="sxs-lookup"><span data-stu-id="33241-116">**tooretrieve hello registration status:**</span></span>

1. <span data-ttu-id="33241-117">관리자 권한으로 hello 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33241-117">Open hello command prompt as an administrator.</span></span>

2. <span data-ttu-id="33241-118">**dsregcmd /status**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33241-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="33241-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="33241-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="33241-120">EnterpriseJoined: DeviceId 없음: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 지문: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft 플랫폼 암호화 공급자 TpmProtected: 예 KeySignTest:: tootest 상승 된 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33241-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="33241-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="33241-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="33241-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="33241-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="33241-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="33241-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="33241-124">2 단계: hello 등록 상태를 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="33241-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="33241-125">Hello 다음 필드를 검토 하 고 hello 예상 값을 갖는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="33241-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="33241-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="33241-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="33241-127">이 필드는 hello 장치가 Azure AD에 등록 되었는지 여부를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="33241-127">This field shows whether hello device is registered with Azure AD.</span></span> <span data-ttu-id="33241-128">Hello 값 '아니요'로 표시 되 면 등록 완료 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="33241-128">If hello value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="33241-129">**가능한 원인:**</span><span class="sxs-lookup"><span data-stu-id="33241-129">**Possible causes:**</span></span>

- <span data-ttu-id="33241-130">등록에 대 한 hello 컴퓨터의 인증에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="33241-130">Authentication of hello computer for registration failed.</span></span>

- <span data-ttu-id="33241-131">Hello 컴퓨터도 찾을 수 없습니다 hello 조직 중인 HTTP 프록시</span><span class="sxs-lookup"><span data-stu-id="33241-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="33241-132">인증을 위해 Azure AD 또는 등록에 대 한 Azure DRS hello 컴퓨터에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="33241-132">hello computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="33241-133">hello 컴퓨터 아닐 hello 조직의 내부 네트워크 또는 VPN의 직선 tooan와 온-프레미스 AD 도메인 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="33241-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="33241-134">Hello 컴퓨터에 TPM이 있으면 잘못 된 상태에 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33241-134">If hello computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="33241-135">서비스에서 잘못 된 구성 앞에서 기록한 hello 문서에 다시 tooverify를 필요 함이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33241-135">There may be a misconfiguration in services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="33241-136">일반적인 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33241-136">Common examples are:</span></span>

    - <span data-ttu-id="33241-137">페더레이션 서버에서 Ws-Trust 끝점이 사용되도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33241-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="33241-138">페더레이션 서버는 Windows 통합 인증을 사용한 네트워크 컴퓨터에서의 인바운드 인증을 허용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33241-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="33241-139">Azure AD에서 hello 컴퓨터 속한 hello AD 포리스트에 tooyour 확인 된 도메인 이름을 가리키는 서비스 연결 지점 개체가 없는</span><span class="sxs-lookup"><span data-stu-id="33241-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="33241-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="33241-140">DomainJoined : YES</span></span>  

<span data-ttu-id="33241-141">이 필드는 hello 장치 조인된 tooan 온-프레미스 Active Directory 인지 여부를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="33241-141">This field shows whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="33241-142">Hello 값으로 표시 되 면 **아니요**, hello 장치 없습니다 자동 등록을 Azure AD와 합니다.</span><span class="sxs-lookup"><span data-stu-id="33241-142">If hello value shows as **NO**, hello device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="33241-143">해당 hello 장치 조인 toohello 온-프레미스 Active Directory와 Azure AD에 등록할 수 전에 먼저 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="33241-143">Check first that hello device joins toohello on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="33241-144">Hello 컴퓨터 tooAzure AD 직접 추가 하기 위해 원하는 경우 Azure Active Directory Join의 기능에 대해 tooLearn 이동 하세요.</span><span class="sxs-lookup"><span data-stu-id="33241-144">If you are looking for joining hello computer tooAzure AD directly, please go tooLearn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="33241-145">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="33241-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="33241-146">이 필드는 hello 장치를 Azure AD와 있지만 개인 장치 (작업 공간 연결로 표시)로 등록 되었는지 여부를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="33241-146">This field shows whether hello device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="33241-147">그러나이 값은 Azure AD에 등록 된 도메인에 가입 된 컴퓨터에 대 한 '아니요'로 표시 해야 하면, 됨을 의미 하는 예로 표시 되는 경우 회사 또는 학교 계정을 추가 된 이전 toohello 컴퓨터 완료 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="33241-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior toohello computer completing registration.</span></span> <span data-ttu-id="33241-148">이 경우 hello 계정은 Windows 10 (1607 때 '실행' 창 또는 명령 프롬프트 창의 hello hello WinVer 명령에서 실행)의 hello Anniversary 업데이트 버전을 사용 하는 경우 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33241-148">In this case hello account will be ignored if using hello Anniversary Update version of Windows 10 (1607 when running hello WinVer command in hello ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="33241-149">WamDefaultSet : YES 및 AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="33241-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="33241-150">이러한 필드에 해당 hello 사용자가 AD tooAzure toohello 장치 로그인 시 인증 성공적으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="33241-150">These fields show that hello user has successfully authenticated tooAzure AD upon signing in toohello device.</span></span> <span data-ttu-id="33241-151">표시 하는 경우 '아니요' hello 다음 원인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33241-151">If they show ‘NO’ hello following are possible causes:</span></span>

- <span data-ttu-id="33241-152">등록 (확인 hello KeySignTest 높은 실행 하는 동안) 시 hello 장치와 연결 된 TPM의 잘못 된 저장소 키 (STK)입니다.</span><span class="sxs-lookup"><span data-stu-id="33241-152">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="33241-153">대체 로그인 ID</span><span class="sxs-lookup"><span data-stu-id="33241-153">Alternate Login ID</span></span>

- <span data-ttu-id="33241-154">HTTP 프록시를 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="33241-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="33241-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="33241-155">Next steps</span></span>

<span data-ttu-id="33241-156">자세한 내용은 참조 hello [자동 장치 등록 FAQ](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="33241-156">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
