---
title: "Active Directory 인증서 기반 인증-aaaAzure 시작 | Microsoft Docs"
description: "자세한 내용은 방법 tooconfigure 사용자 환경에서 인증서 기반 인증"
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="93058-103">Azure Active Directory에서 인증서 기반 인증 시작</span><span class="sxs-lookup"><span data-stu-id="93058-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="93058-104">인증서 기반 인증을 사용 하려면 Exchange online 계정을 연결할 때 Windows, Android 또는 iOS 장치에 클라이언트 인증서와 함께 Azure Active Directory에 의해 인증 toobe가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93058-104">Certificate-based authentication enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="93058-105">Microsoft Outlook 및 Microsoft Word와 같은 Office 모바일 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="93058-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="93058-106">EAS(Exchange ActiveSync) 클라이언트</span><span class="sxs-lookup"><span data-stu-id="93058-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="93058-107">Hello 필요 tooenter 사용자 이름 및 암호 조합을 특정 메일 및 모바일 장치에서 Microsoft Office 응용 프로그램에이 기능을 구성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="93058-108">항목 내용:</span><span class="sxs-lookup"><span data-stu-id="93058-108">This topic:</span></span>

- <span data-ttu-id="93058-109">미국 정부 계획 및 tooconfigure 단계 hello로 하 고 Office 365 Enterprise, Business, 교육, 테 넌 트의 사용자에 대 한 인증서 기반 인증을 이용 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-109">Provides you with hello steps tooconfigure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="93058-110">이 기능은 Office 365 중국, 미국 국방부 및 연방 정부 계획에서 미리 보기 상태로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="93058-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="93058-111">[PKI(공개 키 인프라)](https://go.microsoft.com/fwlink/?linkid=841737) 및 [AD FS](connect/active-directory-aadconnectfed-whatis.md)가 이미 구성되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="93058-112">요구 사항</span><span class="sxs-lookup"><span data-stu-id="93058-112">Requirements</span></span>

<span data-ttu-id="93058-113">인증서 기반 인증 tooconfigure hello 다음 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-113">tooconfigure certificate-based authentication, hello following must be true:</span></span>  

- <span data-ttu-id="93058-114">CBA(인증서 기반 인증)는 최신 인증(ADAL)을 사용하는 브라우저 응용 프로그램 또는 네이티브 클라이언트의 페더레이션 환경에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="93058-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="93058-115">Exchange Active Sync (EAS) 모두, 페더레이션 및 관리 되는 계정에 대해 사용할 수 있는 EXO에 대 한는 hello 예외가입니다.</span><span class="sxs-lookup"><span data-stu-id="93058-115">hello one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="93058-116">hello 루트 인증 기관 및 중간 인증 기관을 Azure Active Directory에서 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-116">hello root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="93058-117">각 인증 기관에는 인터넷 연결 URL을 통해 참조될 수 있는 CRL(인증서 해지 목록)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="93058-118">Azure Active Directory에 해당 인증 기관이 하나 이상 구성되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="93058-119">Hello에 관련된 단계를 확인할 수 있습니다 [hello 인증 기관 구성](#step-2-configure-the-certificate-authorities) 섹션.</span><span class="sxs-lookup"><span data-stu-id="93058-119">You can find related steps in hello [Configure hello certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="93058-120">Exchange ActiveSync 클라이언트에 대 한 클라이언트 인증서 hello hello 사용자 라우팅할 수 있는 전자 메일 hello hello 주체 대체 이름 필드의 RFC822 이름 값 또는 hello 사용자 이름 중 하나를 온라인 Exchange 주소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-120">For Exchange ActiveSync clients, hello client certificate must have hello user’s routable email address in Exchange online in either hello Principal Name or hello RFC822 Name value of hello Subject Alternative Name field.</span></span> <span data-ttu-id="93058-121">Azure Active Directory hello 디렉터리의 hello RFC822 값 toohello 프록시 주소 특성을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-121">Azure Active Directory maps hello RFC822 value toohello Proxy Address attribute in hello directory.</span></span>  

- <span data-ttu-id="93058-122">클라이언트 장치에 클라이언트 인증서를 발급 하는 액세스 tooat 중 하나 이상이 인증 기관이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-122">Your client device must have access tooat least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="93058-123">클라이언트 인증용 클라이언트 인증서가 발행 되어 있어야 tooyour 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="93058-123">A client certificate for client authentication must have been issued tooyour client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="93058-124">1단계: 장치 플랫폼 선택</span><span class="sxs-lookup"><span data-stu-id="93058-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="93058-125">첫 번째 단계로, 조사 하려는 hello 장치 플랫폼에 대 한 필요 tooreview hello 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-125">As a first step, for hello device platform you care about, you need tooreview hello following:</span></span>

- <span data-ttu-id="93058-126">hello Office 모바일 응용 프로그램 지원</span><span class="sxs-lookup"><span data-stu-id="93058-126">hello Office mobile applications support</span></span> 
- <span data-ttu-id="93058-127">hello 특정 구현 요구 사항</span><span class="sxs-lookup"><span data-stu-id="93058-127">hello specific implementation requirements</span></span>  

<span data-ttu-id="93058-128">hello 관련 hello 다음 장치 플랫폼에 대 한 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93058-128">hello related information exists for hello following device platforms:</span></span>

- [<span data-ttu-id="93058-129">Android</span><span class="sxs-lookup"><span data-stu-id="93058-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="93058-130">iOS</span><span class="sxs-lookup"><span data-stu-id="93058-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a><span data-ttu-id="93058-131">2 단계: hello 인증 기관 구성</span><span class="sxs-lookup"><span data-stu-id="93058-131">Step 2: Configure hello certificate authorities</span></span> 

<span data-ttu-id="93058-132">tooconfigure 각 인증 기관에 대 한 Azure Active Directory에서 인증 기관에 따라 hello를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-132">tooconfigure your certificate authorities in Azure Active Directory, for each certificate authority, upload hello following:</span></span> 

* <span data-ttu-id="93058-133">hello 인증서의 공개 부분에 hello *.cer* 형식</span><span class="sxs-lookup"><span data-stu-id="93058-133">hello public portion of hello certificate, in *.cer* format</span></span> 
* <span data-ttu-id="93058-134">hello 여기서 hello 인터넷 Url 인증서 해지 목록 (Crl) 상주</span><span class="sxs-lookup"><span data-stu-id="93058-134">hello Internet facing URLs where hello Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="93058-135">인증 기관에 대 한 hello 스키마 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93058-135">hello schema for a certificate authority looks as follows:</span></span> 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

<span data-ttu-id="93058-136">Hello 구성에 대 한 hello를 사용할 수 있습니다 [Azure Active Directory PowerShell 버전 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="93058-136">For hello configuration, you can use hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="93058-137">관리자 권한으로 Windows PowerShell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="93058-138">Hello Azure AD 모듈을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-138">Install hello Azure AD module.</span></span> <span data-ttu-id="93058-139">버전 tooinstall 필요한 [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) 이상.</span><span class="sxs-lookup"><span data-stu-id="93058-139">You need tooinstall Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="93058-140">첫 번째 구성 단계로 테 넌 트와 연결 tooestablish 필요.</span><span class="sxs-lookup"><span data-stu-id="93058-140">As a first configuration step, you need tooestablish a connection with your tenant.</span></span> <span data-ttu-id="93058-141">연결 tooyour 테 넌 트 존재 하는 즉시 있습니다 수 검토, 추가, 삭제 및 수정 디렉터리에 정의 된 hello 신뢰할 수 있는 인증 기관입니다.</span><span class="sxs-lookup"><span data-stu-id="93058-141">As soon as a connection tooyour tenant exists, you can review, add, delete and modify hello trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="93058-142">연결</span><span class="sxs-lookup"><span data-stu-id="93058-142">Connect</span></span>

<span data-ttu-id="93058-143">테 넌 트를 사용 하 여 hello와의 연결을 tooestablish [연결-azure Ad](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="93058-143">tooestablish a connection with your tenant, use hello [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="93058-144">장치</span><span class="sxs-lookup"><span data-stu-id="93058-144">Retrieve</span></span> 

<span data-ttu-id="93058-145">hello를 사용 하는 디렉터리에 정의 된 tooretrieve hello 신뢰할 수 있는 인증 기관 [Get AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="93058-145">tooretrieve hello trusted certificate authorities that are defined in your directory, use hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="93058-146">추가</span><span class="sxs-lookup"><span data-stu-id="93058-146">Add</span></span>

<span data-ttu-id="93058-147">신뢰할 수 있는 인증 기관 toocreate hello를 사용 하 여 [새로 AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet 및 집합 hello **crlDistributionPoint** 특성 tooa 올바른 값:</span><span class="sxs-lookup"><span data-stu-id="93058-147">toocreate a trusted certificate authority, use hello [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set hello **crlDistributionPoint** attribute tooa correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="93058-148">제거</span><span class="sxs-lookup"><span data-stu-id="93058-148">Remove</span></span>

<span data-ttu-id="93058-149">신뢰할 수 있는 인증 기관 tooremove hello를 사용 하 여 [제거 AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="93058-149">tooremove a trusted certificate authority, use hello [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="93058-150">수정</span><span class="sxs-lookup"><span data-stu-id="93058-150">Modfiy</span></span>

<span data-ttu-id="93058-151">신뢰할 수 있는 인증 기관 toomodify hello를 사용 하 여 [집합 AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="93058-151">toomodify a trusted certificate authority, use hello [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="93058-152">3단계: 해지 구성</span><span class="sxs-lookup"><span data-stu-id="93058-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="93058-153">Azure Active Directory 클라이언트 인증서를 toorevoke hello 인증서 해지 목록 (CRL) hello Url에서 인증 기관 정보의 일부로 업로드 하 고 캐시를 인출 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-153">toorevoke a client certificate, Azure Active Directory fetches hello certificate revocation list (CRL) from hello URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="93058-154">hello 타임 스탬프를 마지막 게시 (**발효일** 속성)에 CRL이 사용 하는 hello tooensure hello CRL 여전히 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-154">hello last publish timestamp (**Effective Date** property) in hello CRL is used tooensure hello CRL is still valid.</span></span> <span data-ttu-id="93058-155">hello CRL hello 목록의 일부인 주기적으로 참조 된 toorevoke 액세스 toocertificates입니다.</span><span class="sxs-lookup"><span data-stu-id="93058-155">hello CRL is periodically referenced toorevoke access toocertificates that are a part of hello list.</span></span>

<span data-ttu-id="93058-156">더 즉각적인 해지 (예: 사용자가 장치를 잃어버린 경우) 필요한 경우 hello 사용자의 권한 부여 토큰 hello 무효화 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93058-156">If a more instant revocation is required (for example, if a user loses a device), hello authorization token of hello user can be invalidated.</span></span> <span data-ttu-id="93058-157">tooinvalidate hello 권한 부여 토큰으로 설정 hello **StsRefreshTokenValidFrom** Windows PowerShell을 사용 하 여이 특정 사용자에 대 한 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="93058-157">tooinvalidate hello authorization token, set hello **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="93058-158">Hello를 업데이트 해야 **StsRefreshTokenValidFrom** toorevoke 액세스할 각 사용자에 대 한 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="93058-158">You must update hello **StsRefreshTokenValidFrom** field for each user you want toorevoke access for.</span></span>

<span data-ttu-id="93058-159">hello 해지 유지 하는 tooensure, hello 설정 해야 **발효일** hello 값을 설정한 후 hello CRL tooa 날짜의 **StsRefreshTokenValidFrom** 문제의 hello 인증서가 확인 하 고 CRL 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="93058-159">tooensure that hello revocation persists, you must set hello **Effective Date** of hello CRL tooa date after hello value set by **StsRefreshTokenValidFrom** and ensure hello certificate in question is in hello CRL.</span></span>

<span data-ttu-id="93058-160">업데이트 및 hello 설정 하 여 hello 권한 부여 토큰이 무효화를 위한 단계 개요 hello 프로세스 hello **StsRefreshTokenValidFrom** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="93058-160">hello following steps outline hello process for updating and invalidating hello authorization token by setting hello **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="93058-161">**tooconfigure 해지 합니다.**</span><span class="sxs-lookup"><span data-stu-id="93058-161">**tooconfigure revocation:**</span></span> 

1. <span data-ttu-id="93058-162">관리자 자격 증명 toohello MSOL 서비스와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-162">Connect with admin credentials toohello MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="93058-163">사용자에 대 한 hello 현재 StsRefreshTokensValidFrom 값을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-163">Retrieve hello current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="93058-164">Hello 사용자 같은 toohello 현재 타임 스탬프에 대 한 새 StsRefreshTokensValidFrom 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-164">Configure a new StsRefreshTokensValidFrom value for hello user equal toohello current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="93058-165">설정한 hello 날짜 이후 hello에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-165">hello date you set must be in hello future.</span></span> <span data-ttu-id="93058-166">Hello 날짜 이후 hello에 없는 경우 hello **StsRefreshTokensValidFrom** 속성이 설정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="93058-166">If hello date is not in hello future, hello **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="93058-167">Hello 날짜 hello 미래에 있으면 **StsRefreshTokensValidFrom** toohello 현재 시간 (hello 날짜가 아닌 Set-msoluser 명령으로 지정) 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93058-167">If hello date is in hello future, **StsRefreshTokensValidFrom** is set toohello current time (not hello date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="93058-168">4단계: 구성 테스트</span><span class="sxs-lookup"><span data-stu-id="93058-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="93058-169">인증서 테스트</span><span class="sxs-lookup"><span data-stu-id="93058-169">Testing your certificate</span></span>

<span data-ttu-id="93058-170">첫 번째 구성 테스트를 시도해 야 toosign에 너무[Outlook Web Access](https://outlook.office365.com) 또는 [SharePoint Online](https://microsoft.sharepoint.com) 를 사용 하 여 **장치에서 브라우저**합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-170">As a first configuration test, you should try toosign in too[Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="93058-171">로그인에 성공했으면 다음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="93058-172">hello 사용자 인증서를 프로 비전 된 tooyour 테스트 장치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="93058-172">hello user certificate has been provisioned tooyour test device</span></span>
- <span data-ttu-id="93058-173">AD FS가 올바르게 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="93058-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="93058-174">Office 모바일 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="93058-174">Testing Office mobile applications</span></span>

<span data-ttu-id="93058-175">**모바일 Office 응용 프로그램에서 인증서 기반 인증 tootest:**</span><span class="sxs-lookup"><span data-stu-id="93058-175">**tootest certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="93058-176">테스트 장치에서 Office 모바일 응용 프로그램(예: OneDrive)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="93058-177">Hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-177">Launch hello application.</span></span> 
4. <span data-ttu-id="93058-178">사용자 이름을 입력 하 고 원하는 toouse hello 사용자 인증서를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-178">Enter your user name, and then select hello user certificate you want toouse.</span></span> 

<span data-ttu-id="93058-179">정상적으로 로그인되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="93058-180">Exchange ActiveSync 클라이언트 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="93058-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="93058-181">인증서 기반 인증 일 경우 hello 클라이언트 인증서를 포함 하는 EAS 프로필을 통해 tooaccess EAS (Exchange ActiveSync) 사용 가능한 toohello 응용 프로그램 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-181">tooaccess Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing hello client certificate must be available toohello application.</span></span> 

<span data-ttu-id="93058-182">hello EAS 프로필 hello 다음 정보를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-182">hello EAS profile must contain hello following information:</span></span>

- <span data-ttu-id="93058-183">인증에 사용 되는 사용자 인증서 toobe hello</span><span class="sxs-lookup"><span data-stu-id="93058-183">hello user certificate toobe used for authentication</span></span> 

- <span data-ttu-id="93058-184">hello EAS 끝점 (예를 들어 outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="93058-184">hello EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="93058-185">EAS 프로필을 구성 하 고 모바일 장치 관리 (MDM) 또는 hello hello 장치에 대 한 EAS 프로필에에서 hello 인증서를 수동으로 배치 하 여 Intune 등의 hello 사용률을 통해 hello 장치에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93058-185">An EAS profile can be configured and placed on hello device through hello utilization of Mobile device management (MDM) such as Intune or by manually placing hello certificate in hello EAS profile on hello device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="93058-186">Android에서 EAS 클라이언트 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="93058-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="93058-187">**tootest 인증서 인증:**</span><span class="sxs-lookup"><span data-stu-id="93058-187">**tootest certificate authentication:**</span></span>  

1. <span data-ttu-id="93058-188">위의 hello 요구 사항을 충족 하는 hello 응용 프로그램에서 EAS 프로필을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-188">Configure an EAS profile in hello application that satisfies hello requirements above.</span></span>  
2. <span data-ttu-id="93058-189">Hello 응용 프로그램을 열고 메일 동기화를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="93058-189">Open hello application, and verify that mail is synchronizing.</span></span> 

