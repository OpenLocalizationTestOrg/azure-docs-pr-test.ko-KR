---
title: "Windows 10 및 Windows Server 2016에 대한 Azure AD 도메인 조인 컴퓨터의 자동 등록 문제 해결 | Microsoft Docs"
description: "Windows 10 및 Windows Server 2016에 대한 Azure AD 도메인 조인 컴퓨터의 자동 등록 문제 해결"
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
ms.openlocfilehash: 5b7f95f302f716d9221b5fae59aa2df5c956a524
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="81d34-103">Windows 10 및 Windows Server 2016에 대한 Azure AD 도메인 조인 컴퓨터의 자동 등록 문제 해결</span><span class="sxs-lookup"><span data-stu-id="81d34-103">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="81d34-104">이 항목은 다음 클라이언트에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="81d34-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="81d34-105">Windows 10</span></span>
-   <span data-ttu-id="81d34-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="81d34-106">Windows Server 2016</span></span>

<span data-ttu-id="81d34-107">기타 Windows 클라이언트의 경우 [Windows 하위 수준 클라이언트에 대한 Azure AD 도메인 조인 컴퓨터의 자동 등록 문제 해결](active-directory-device-registration-troubleshoot-windows-legacy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81d34-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="81d34-108">이 항목에서는 다음 시나리오를 지원하기 위해 [Windows 도메인 가입 장치의 Azure Active Directory 자동 등록을 구성하는 방법](active-directory-device-registration-get-started.md)에 설명된 대로 도메인 가입 장치의 자동 등록을 구성했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) to support the following scenarios:</span></span>

- [<span data-ttu-id="81d34-109">장치 기반 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="81d34-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="81d34-110">엔터프라이즈 설정 로밍</span><span class="sxs-lookup"><span data-stu-id="81d34-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="81d34-111">비즈니스용 Windows Hello</span><span class="sxs-lookup"><span data-stu-id="81d34-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="81d34-112">이 문서에서는 잠재적인 문제를 해결하는 방법에 대한 문제 해결 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 

<span data-ttu-id="81d34-113">등록은 Windows 10 2015년 11월 업데이트 이상에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-113">The registration is supported in the Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="81d34-114">위 시나리오를 사용하려면 기념일 업데이트를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-114">We recommend using the Anniversary Update for enabling the scenarios above.</span></span>

## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="81d34-115">1단계: 등록 상태 검색</span><span class="sxs-lookup"><span data-stu-id="81d34-115">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="81d34-116">**등록 상태를 검색하려면**</span><span class="sxs-lookup"><span data-stu-id="81d34-116">**To retrieve the registration status:**</span></span>

1. <span data-ttu-id="81d34-117">관리자 권한으로 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-117">Open the command prompt as an administrator.</span></span>

2. <span data-ttu-id="81d34-118">**dsregcmd /status**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="81d34-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="81d34-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="81d34-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span><span class="sxs-lookup"><span data-stu-id="81d34-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="81d34-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="81d34-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="81d34-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="81d34-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="81d34-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="81d34-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="81d34-124">2단계: 등록 상태 평가</span><span class="sxs-lookup"><span data-stu-id="81d34-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="81d34-125">다음 필드를 검토하고 예상 값을 갖는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="81d34-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="81d34-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="81d34-127">이 필드는 장치가 Azure AD에 등록되어 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-127">This field shows whether the device is registered with Azure AD.</span></span> <span data-ttu-id="81d34-128">이 값이 'NO'로 표시되면 등록이 완료되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-128">If the value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="81d34-129">**가능한 원인:**</span><span class="sxs-lookup"><span data-stu-id="81d34-129">**Possible causes:**</span></span>

- <span data-ttu-id="81d34-130">등록을 위한 컴퓨터 인증이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-130">Authentication of the computer for registration failed.</span></span>

- <span data-ttu-id="81d34-131">조직에 컴퓨터에서 검색될 수 없는 HTTP 프록시가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="81d34-132">컴퓨터가 인증을 위해 Azure AD에, 또는 등록을 위해 Azure DRS에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-132">The computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="81d34-133">컴퓨터가 조직의 내부 네트워크 또는 온-프레미스 AD 도메인 컨트롤러의 직접 가시선 내에 있는 VPN에 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="81d34-134">컴퓨터에 TPM이 있는 경우 잘못된 상태일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-134">If the computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="81d34-135">이전에 문서에 설명된 것처럼 다시 확인해야 하는 잘못된 서비스 구성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-135">There may be a misconfiguration in services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="81d34-136">일반적인 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-136">Common examples are:</span></span>

    - <span data-ttu-id="81d34-137">페더레이션 서버에서 Ws-Trust 끝점이 사용되도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="81d34-138">페더레이션 서버는 Windows 통합 인증을 사용한 네트워크 컴퓨터에서의 인바운드 인증을 허용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="81d34-139">컴퓨터가 속한 AD 포리스트의 Azure AD에서 확인된 도메인 이름을 가리키는 서비스 연결 지점 개체가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="81d34-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="81d34-140">DomainJoined : YES</span></span>  

<span data-ttu-id="81d34-141">이 필드는 장치가 온-프레미스 Active Directory에 조인되는지 여부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-141">This field shows whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="81d34-142">값이 **NO**로 표시되면 장치는 Azure AD에 자동으로 등록될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-142">If the value shows as **NO**, the device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="81d34-143">Azure AD에 등록할 수 있으려면 먼저 장치가 온-프레미스 Active Directory에 조인되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-143">Check first that the device joins to the on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="81d34-144">Azure AD에 컴퓨터를 직접 조인하려면 Azure Active Directory 조인 기능 알아보기로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="81d34-144">If you are looking for joining the computer to Azure AD directly, please go to Learn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="81d34-145">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="81d34-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="81d34-146">이 필드는 장치가 Azure AD에 개인 장치로 등록되어 있는지 여부를 보여 줍니다(“작업 영역 조인”으로 표시).</span><span class="sxs-lookup"><span data-stu-id="81d34-146">This field shows whether the device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="81d34-147">이 값이 Azure AD에 등록된 도메인 조인 컴퓨터에 대해 'NO'로 표시되어야 하는데 YES로 표시되면 컴퓨터 등록을 완료하기 전에 회사 또는 학교 계정이 추가되었다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior to the computer completing registration.</span></span> <span data-ttu-id="81d34-148">이 경우 Windows 10 기념일 업데이트 버전(1607 '실행' 창 또는 명령 프롬프트 창에서 WinVer 명령을 실행하는 경우 1607 표시)을 사용하면 이러한 계정은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-148">In this case the account will be ignored if using the Anniversary Update version of Windows 10 (1607 when running the WinVer command in the ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="81d34-149">WamDefaultSet : YES 및 AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="81d34-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="81d34-150">이러한 필드는 장치에 로그인 시 Azure AD에서 성공적으로 인증되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-150">These fields show that the user has successfully authenticated to Azure AD upon signing in to the device.</span></span> <span data-ttu-id="81d34-151">‘NO’가 표시될 경우 가능한 원인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81d34-151">If they show ‘NO’ the following are possible causes:</span></span>

- <span data-ttu-id="81d34-152">등록 시 장치에 연결된 TPM에 잘못된 저장소 키(STK)가 있습니다(상승된 권한으로 실행하면서 KeySignTest 확인).</span><span class="sxs-lookup"><span data-stu-id="81d34-152">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="81d34-153">대체 로그인 ID</span><span class="sxs-lookup"><span data-stu-id="81d34-153">Alternate Login ID</span></span>

- <span data-ttu-id="81d34-154">HTTP 프록시를 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="81d34-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="81d34-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="81d34-155">Next steps</span></span>

<span data-ttu-id="81d34-156">자세한 내용은 [자동 장치 등록 FAQ](active-directory-device-registration-faq.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81d34-156">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 