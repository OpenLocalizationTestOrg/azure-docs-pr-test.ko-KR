---
title: "Azure Active Directory 인증서 기반 인증 - 시작 | Microsoft Docs"
description: "사용자 환경에서 인증서 기반 인증을 구성하는 방법 알아보기"
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
ms.openlocfilehash: 8ebc6f2dd7502fd75ffdd4d5d68338382cb1a46b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="d84a5-103">Azure Active Directory에서 인증서 기반 인증 시작</span><span class="sxs-lookup"><span data-stu-id="d84a5-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="d84a5-104">인증서 기반 인증을 사용하면 Exchange Online 계정을 다음에 연결할 때 Windows, Android 또는 iOS 장치의 클라이언트 인증서를 사용하여 Azure Active Directory에서 인증을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-104">Certificate-based authentication enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="d84a5-105">Microsoft Outlook 및 Microsoft Word와 같은 Office 모바일 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d84a5-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="d84a5-106">EAS(Exchange ActiveSync) 클라이언트</span><span class="sxs-lookup"><span data-stu-id="d84a5-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="d84a5-107">이 기능을 구성하면 모바일 장치의 특정 메일 및 Microsoft Office 응용 프로그램에 사용자 이름 및 암호 조합을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="d84a5-108">항목 내용:</span><span class="sxs-lookup"><span data-stu-id="d84a5-108">This topic:</span></span>

- <span data-ttu-id="d84a5-109">Office 365 Enterprise, Business, Education 및 미국 정보 계획의 테넌트 사용자를 위해 인증서 기반 인증을 구성하고 활용하는 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-109">Provides you with the steps to configure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="d84a5-110">이 기능은 Office 365 중국, 미국 국방부 및 연방 정부 계획에서 미리 보기 상태로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="d84a5-111">[PKI(공개 키 인프라)](https://go.microsoft.com/fwlink/?linkid=841737) 및 [AD FS](connect/active-directory-aadconnectfed-whatis.md)가 이미 구성되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="d84a5-112">요구 사항</span><span class="sxs-lookup"><span data-stu-id="d84a5-112">Requirements</span></span>

<span data-ttu-id="d84a5-113">인증서 기반 인증을 구성하려면 다음에 해당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-113">To configure certificate-based authentication, the following must be true:</span></span>  

- <span data-ttu-id="d84a5-114">CBA(인증서 기반 인증)는 최신 인증(ADAL)을 사용하는 브라우저 응용 프로그램 또는 네이티브 클라이언트의 페더레이션 환경에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="d84a5-115">단, 페더레이션 및 관리 계정 모두에 사용할 수 있는 EXO용 EAS(Exchange Active Sync)는 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-115">The one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="d84a5-116">Azure Active Directory에는 루트 인증 기관 및 중간 인증 기관을 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-116">The root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="d84a5-117">각 인증 기관에는 인터넷 연결 URL을 통해 참조될 수 있는 CRL(인증서 해지 목록)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="d84a5-118">Azure Active Directory에 해당 인증 기관이 하나 이상 구성되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="d84a5-119">[인증 기관 구성](#step-2-configure-the-certificate-authorities) 섹션에서 관련 단계를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-119">You can find related steps in the [Configure the certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="d84a5-120">Exchange ActiveSync 클라이언트의 경우, 보안 주체 이름 또는 주체 대체 이름 필드의 RFC822 이름 값에 Exchange Online 사용자가 라우팅할 수 있는 전자 메일 주소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-120">For Exchange ActiveSync clients, the client certificate must have the user’s routable email address in Exchange online in either the Principal Name or the RFC822 Name value of the Subject Alternative Name field.</span></span> <span data-ttu-id="d84a5-121">Azure Active Directory는 디렉터리의 프록시 주소 특성에 RFC822 값을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-121">Azure Active Directory maps the RFC822 value to the Proxy Address attribute in the directory.</span></span>  

- <span data-ttu-id="d84a5-122">클라이언트 장치는 클라이언트 인증서를 발급하는 하나 이상의 인증 기관에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-122">Your client device must have access to at least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="d84a5-123">클라이언트 인증을 위한 클라이언트 인증서가 클라이언트에 발급되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-123">A client certificate for client authentication must have been issued to your client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="d84a5-124">1단계: 장치 플랫폼 선택</span><span class="sxs-lookup"><span data-stu-id="d84a5-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="d84a5-125">첫 번째 단계로 대상 장치 플랫폼에 대해 다음을 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-125">As a first step, for the device platform you care about, you need to review the following:</span></span>

- <span data-ttu-id="d84a5-126">Office 모바일 응용 프로그램 지원</span><span class="sxs-lookup"><span data-stu-id="d84a5-126">The Office mobile applications support</span></span> 
- <span data-ttu-id="d84a5-127">특정 구현 요구 사항</span><span class="sxs-lookup"><span data-stu-id="d84a5-127">The specific implementation requirements</span></span>  

<span data-ttu-id="d84a5-128">다음 장치 플랫폼에 대한 관련 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-128">The related information exists for the following device platforms:</span></span>

- [<span data-ttu-id="d84a5-129">Android</span><span class="sxs-lookup"><span data-stu-id="d84a5-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="d84a5-130">iOS</span><span class="sxs-lookup"><span data-stu-id="d84a5-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-the-certificate-authorities"></a><span data-ttu-id="d84a5-131">2단계: 인증 기관 구성</span><span class="sxs-lookup"><span data-stu-id="d84a5-131">Step 2: Configure the certificate authorities</span></span> 

<span data-ttu-id="d84a5-132">Azure Active Directory에서 인증 기관을 구성하려면 각 인증 기관에 대해 다음을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-132">To configure your certificate authorities in Azure Active Directory, for each certificate authority, upload the following:</span></span> 

* <span data-ttu-id="d84a5-133">인증서의 공개 부분( *.cer* 형식)</span><span class="sxs-lookup"><span data-stu-id="d84a5-133">The public portion of the certificate, in *.cer* format</span></span> 
* <span data-ttu-id="d84a5-134">CRL(인증서 해지 목록)이 있는 인터넷 연결 URL</span><span class="sxs-lookup"><span data-stu-id="d84a5-134">The Internet facing URLs where the Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="d84a5-135">인증 기관에 대한 스키마는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-135">The schema for a certificate authority looks as follows:</span></span> 

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

<span data-ttu-id="d84a5-136">구성에는 [Azure Active Directory PowerShell 버전 2](/powershell/azure/install-adv2?view=azureadps-2.0)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-136">For the configuration, you can use the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="d84a5-137">관리자 권한으로 Windows PowerShell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="d84a5-138">Azure AD 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-138">Install the Azure AD module.</span></span> <span data-ttu-id="d84a5-139">버전 [2.0.0.33](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) 이상을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-139">You need to install Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="d84a5-140">첫 번째 구성 단계로 테넌트와 연결을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-140">As a first configuration step, you need to establish a connection with your tenant.</span></span> <span data-ttu-id="d84a5-141">테넌트에 대한 연결이 있으면 디렉터리에 정의된 신뢰할 수 있는 인증 기관을 검토, 추가, 삭제 및 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-141">As soon as a connection to your tenant exists, you can review, add, delete and modify the trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="d84a5-142">연결</span><span class="sxs-lookup"><span data-stu-id="d84a5-142">Connect</span></span>

<span data-ttu-id="d84a5-143">테넌트와 연결을 설정하려면 [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-143">To establish a connection with your tenant, use the [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="d84a5-144">장치</span><span class="sxs-lookup"><span data-stu-id="d84a5-144">Retrieve</span></span> 

<span data-ttu-id="d84a5-145">디렉터리에 정의된 신뢰할 수 있는 인증 기관을 검색하려면 [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-145">To retrieve the trusted certificate authorities that are defined in your directory, use the [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="d84a5-146">추가</span><span class="sxs-lookup"><span data-stu-id="d84a5-146">Add</span></span>

<span data-ttu-id="d84a5-147">신뢰할 수 있는 인증 기관을 만들려면 [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet을 사용하고 **crlDistributionPoint** 특성을 올바른 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-147">To create a trusted certificate authority, use the [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set the **crlDistributionPoint** attribute to a correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF THE CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="d84a5-148">제거</span><span class="sxs-lookup"><span data-stu-id="d84a5-148">Remove</span></span>

<span data-ttu-id="d84a5-149">신뢰할 수 있는 인증 기관을 제거하려면 [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-149">To remove a trusted certificate authority, use the [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="d84a5-150">수정</span><span class="sxs-lookup"><span data-stu-id="d84a5-150">Modfiy</span></span>

<span data-ttu-id="d84a5-151">신뢰할 수 있는 인증 기관을 수정하려면 [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-151">To modify a trusted certificate authority, use the [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="d84a5-152">3단계: 해지 구성</span><span class="sxs-lookup"><span data-stu-id="d84a5-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="d84a5-153">클라이언트 인증서를 해지할 수 있게 Azure Active Directory는 인증 기관 정보의 일부로 업로드된 URL에서 CRL(인증서 해지 목록)을 가져온 후 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-153">To revoke a client certificate, Azure Active Directory fetches the certificate revocation list (CRL) from the URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="d84a5-154">CRL의 마지막 게시 타임스탬프(**개시 날짜** 속성)는 CRL이 여전히 유효한지 확인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-154">The last publish timestamp (**Effective Date** property) in the CRL is used to ensure the CRL is still valid.</span></span> <span data-ttu-id="d84a5-155">CRL은 목록의 일부인 인증서에 대한 액세스 권한을 해지하기 위해 주기적으로 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-155">The CRL is periodically referenced to revoke access to certificates that are a part of the list.</span></span>

<span data-ttu-id="d84a5-156">추가 인스턴트 해지가 필요하면(예: 사용자가 장치를 분실한 경우) 사용자의 권한 부여 토큰이 무효화될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-156">If a more instant revocation is required (for example, if a user loses a device), the authorization token of the user can be invalidated.</span></span> <span data-ttu-id="d84a5-157">권한 부여 토큰을 무효화하려면 Windows PowerShell을 사용하여 이 특정 사용자에 대한 **StsRefreshTokenValidFrom** 필드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-157">To invalidate the authorization token, set the **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="d84a5-158">액세스 권한을 해지하려는 각 사용자에 대한 **StsRefreshTokenValidFrom** 필드를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-158">You must update the **StsRefreshTokenValidFrom** field for each user you want to revoke access for.</span></span>

<span data-ttu-id="d84a5-159">해지가 지속되도록 하려면 **개시 날짜**를 **StsRefreshTokenValidFrom**으로 설정한 값 이후의 날짜로 설정하고 문제의 인증서가 CRL에 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-159">To ensure that the revocation persists, you must set the **Effective Date** of the CRL to a date after the value set by **StsRefreshTokenValidFrom** and ensure the certificate in question is in the CRL.</span></span>

<span data-ttu-id="d84a5-160">다음 단계에서는 **StsRefreshTokenValidFrom** 필드를 설정하여 권한 부여 토큰을 업데이트 및 무효화하기 위한 프로세스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-160">The following steps outline the process for updating and invalidating the authorization token by setting the **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="d84a5-161">**해지를 구성하려면**</span><span class="sxs-lookup"><span data-stu-id="d84a5-161">**To configure revocation:**</span></span> 

1. <span data-ttu-id="d84a5-162">관리 자격 증명을 MSOL 서비스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-162">Connect with admin credentials to the MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="d84a5-163">사용자에 대한 현재 StsRefreshTokensValidFrom 값을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-163">Retrieve the current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="d84a5-164">사용자에 대한 새 StsRefreshTokensValidFrom 값을 현재 타임스탬프와 같게 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-164">Configure a new StsRefreshTokensValidFrom value for the user equal to the current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="d84a5-165">설정하는 날짜는 이후 날짜여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-165">The date you set must be in the future.</span></span> <span data-ttu-id="d84a5-166">날짜가 이후 날짜가 아닌 경우 **StsRefreshTokensValidFrom** 속성이 설정되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-166">If the date is not in the future, the **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="d84a5-167">날짜가 이후 날짜인 경우 **StsRefreshTokensValidFrom** 이 현재 시간(Set-MsolUser 명령으로 지정된 날짜 아님)으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-167">If the date is in the future, **StsRefreshTokensValidFrom** is set to the current time (not the date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="d84a5-168">4단계: 구성 테스트</span><span class="sxs-lookup"><span data-stu-id="d84a5-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="d84a5-169">인증서 테스트</span><span class="sxs-lookup"><span data-stu-id="d84a5-169">Testing your certificate</span></span>

<span data-ttu-id="d84a5-170">첫 번째 구성 테스트로 **장치의 브라우저**를 사용하여 [Outlook Web Access](https://outlook.office365.com) 또는 [SharePoint Online](https://microsoft.sharepoint.com)에 로그인을 시도해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-170">As a first configuration test, you should try to sign in to [Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="d84a5-171">로그인에 성공했으면 다음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="d84a5-172">테스트 장치에 사용자 인증서가 프로비전되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-172">The user certificate has been provisioned to your test device</span></span>
- <span data-ttu-id="d84a5-173">AD FS가 올바르게 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="d84a5-174">Office 모바일 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="d84a5-174">Testing Office mobile applications</span></span>

<span data-ttu-id="d84a5-175">**모바일 Office 응용 프로그램에서 인증서 인증을 테스트하려면**</span><span class="sxs-lookup"><span data-stu-id="d84a5-175">**To test certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="d84a5-176">테스트 장치에서 Office 모바일 응용 프로그램(예: OneDrive)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="d84a5-177">응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-177">Launch the application.</span></span> 
4. <span data-ttu-id="d84a5-178">사용자 이름을 입력하고 사용하려는 사용자 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-178">Enter your user name, and then select the user certificate you want to use.</span></span> 

<span data-ttu-id="d84a5-179">정상적으로 로그인되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="d84a5-180">Exchange ActiveSync 클라이언트 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="d84a5-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="d84a5-181">인증서 기반 인증을 통해 EAS(Exchange ActiveSync)에 액세스하려면 클라이언트 인증서를 포함하는 EAS 프로필을 응용 프로그램에서 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-181">To access Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing the client certificate must be available to the application.</span></span> 

<span data-ttu-id="d84a5-182">EAS 프로필은 다음 정보를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-182">The EAS profile must contain the following information:</span></span>

- <span data-ttu-id="d84a5-183">인증에 사용할 사용자 인증서</span><span class="sxs-lookup"><span data-stu-id="d84a5-183">The user certificate to be used for authentication</span></span> 

- <span data-ttu-id="d84a5-184">EAS 끝점(예: outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="d84a5-184">The EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="d84a5-185">Intune과 같은 MDM(모바일 장치 관리)을 활용하거나 장치의 EAS 프로필에 인증서를 수동으로 배치하여 장치에서 EAS 프로필을 구성하고 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-185">An EAS profile can be configured and placed on the device through the utilization of Mobile device management (MDM) such as Intune or by manually placing the certificate in the EAS profile on the device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="d84a5-186">Android에서 EAS 클라이언트 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="d84a5-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="d84a5-187">**인증서 인증을 테스트하려면**</span><span class="sxs-lookup"><span data-stu-id="d84a5-187">**To test certificate authentication:**</span></span>  

1. <span data-ttu-id="d84a5-188">위의 요구 사항을 충족하는 EAS 프로필을 응용 프로그램에서 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-188">Configure an EAS profile in the application that satisfies the requirements above.</span></span>  
2. <span data-ttu-id="d84a5-189">응용 프로그램을 열고 메일이 동기화되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d84a5-189">Open the application, and verify that mail is synchronizing.</span></span> 

