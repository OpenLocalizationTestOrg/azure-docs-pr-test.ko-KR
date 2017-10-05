---
title: "Office 365 및 Azure AD 사용자를 위한 인증서 갱신 | Microsoft Docs"
description: "이 문서에서는 Office 365 사용자가 인증서 갱신에 대해 알리는 전자 메일을 받는 경우 문제를 해결하는 방법에 대해 설명합니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 543b7dc1-ccc9-407f-85a1-a9944c0ba1be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 7f1a3303eff9c413602e745b702baa659343eba6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="renew-federation-certificates-for-office-365-and-azure-active-directory"></a><span data-ttu-id="962fc-103">Office 365 및 Azure Active Directory에 대한 페더레이션 인증서 갱신</span><span class="sxs-lookup"><span data-stu-id="962fc-103">Renew federation certificates for Office 365 and Azure Active Directory</span></span>
## <a name="overview"></a><span data-ttu-id="962fc-104">개요</span><span class="sxs-lookup"><span data-stu-id="962fc-104">Overview</span></span>
<span data-ttu-id="962fc-105">Azure AD(Azure Active Directory)와 AD FS(Active Directory Federation Services) 간의 성공적인 페더레이션을 위해 AD FS에서 Azure AD에 대한 보안 토큰을 서명하는 데 사용하는 인증서는 Azure AD에서 구성된 인증서와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-105">For successful federation between Azure Active Directory (Azure AD) and Active Directory Federation Services (AD FS), the certificates used by AD FS to sign security tokens to Azure AD should match what is configured in Azure AD.</span></span> <span data-ttu-id="962fc-106">불일치로 인해 끊어진 트러스트가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-106">Any mismatch can lead to broken trust.</span></span> <span data-ttu-id="962fc-107">엑스트라넷에 액세스하기 위해 AD FS 및 웹 응용 프로그램 프록시를 배포하는 경우 Azure AD는 이 정보의 동기화를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-107">Azure AD ensures that this information is kept in sync when you deploy AD FS and Web Application Proxy (for extranet access).</span></span>

<span data-ttu-id="962fc-108">이 문서에서는 다음과 같은 경우 토큰 서명 인증서를 관리하고 Azure AD와 동기화하는 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-108">This article provides you additional information to manage your token signing certificates and keep them in sync with Azure AD, in the following cases:</span></span>

* <span data-ttu-id="962fc-109">웹 응용 프로그램 프록시를 배포하지 않았고 따라서 엑스트라넷에서 페더레이션 메타데이터를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-109">You are not deploying the Web Application Proxy, and therefore the federation metadata is not available in the extranet.</span></span>
* <span data-ttu-id="962fc-110">토큰 서명 인증서에 AD FS의 기본 구성을 사용하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="962fc-110">You are not using the default configuration of AD FS for token signing certificates.</span></span>
* <span data-ttu-id="962fc-111">타사 ID 공급자를 사용하는 경우.</span><span class="sxs-lookup"><span data-stu-id="962fc-111">You are using a third-party identity provider.</span></span>

## <a name="default-configuration-of-ad-fs-for-token-signing-certificates"></a><span data-ttu-id="962fc-112">토큰 서명 인증서에 대한 AD FS의 기본 구성</span><span class="sxs-lookup"><span data-stu-id="962fc-112">Default configuration of AD FS for token signing certificates</span></span>
<span data-ttu-id="962fc-113">토큰 서명 및 인증서의 암호를 해독하는 토큰은 일반적으로 자체 서명된 인증서이며 1년 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-113">The token signing and token decrypting certificates are usually self-signed certificates, and are good for one year.</span></span> <span data-ttu-id="962fc-114">기본적으로 AD FS는 **AutoCertificateRollover**라는 자동 갱신 프로세스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-114">By default, AD FS includes an auto-renewal process called **AutoCertificateRollover**.</span></span> <span data-ttu-id="962fc-115">AD FS 2.0 이상을 사용하는 경우는 인증서가 만료되기 전에 Office 365 및 Azure AD에서 자동으로 인증서를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-115">If you are using AD FS 2.0 or later, Office 365 and Azure AD automatically update your certificate before it expires.</span></span>

### <a name="renewal-notification-from-the-office-365-portal-or-an-email"></a><span data-ttu-id="962fc-116">Office 365 포털 또는 전자 메일로 갱신 알림</span><span class="sxs-lookup"><span data-stu-id="962fc-116">Renewal notification from the Office 365 portal or an email</span></span>
> [!NOTE]
> <span data-ttu-id="962fc-117">Office용 인증서를 갱신하도록 요청하는 전자 메일 또는 포털 알림을 받은 경우 [토큰 서명 인증서에 대한 변경 내용 관리](#managecerts) 를 참조하여 조치를 취해야 하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-117">If you received an email or a portal notification asking you to renew your certificate for Office, see [Managing changes to token signing certificates](#managecerts) to check if you need to take any action.</span></span> <span data-ttu-id="962fc-118">Microsoft에서는 아무 조치도 필요하지 않은 경우에도 인증서 갱신에 대한 알림이 보내지도록 이끌 수 있는 가능한 문제에 주의를 기울입니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-118">Microsoft is aware of a possible issue that can lead to notifications for certificate renewal being sent, even when no action is required.</span></span>
>
>

<span data-ttu-id="962fc-119">Azure AD는 이 메타데이터에서 표시한 대로 페더레이션 메타데이터를 모니터링하고 토큰 서명 인증서를 업데이트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-119">Azure AD attempts to monitor the federation metadata, and update the token signing certificates as indicated by this metadata.</span></span> <span data-ttu-id="962fc-120">토큰 서명 인증서 만료 30일 전에 Azure AD는 페더레이션 메타데이터를 폴링하여 새 인증서를 사용할 수 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-120">30 days before the expiration of the token signing certificates, Azure AD checks if new certificates are available by polling the federation metadata.</span></span>

* <span data-ttu-id="962fc-121">페더레이션 메타데이터를 성공적으로 폴링하고 새 인증서를 검색할 수 있는 경우 사용자에게 전자 메일 알림 또는 Office 365 포털 내의 경고가 주어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-121">If it can successfully poll the federation metadata and retrieve the new certificates, no email notification or warning in the Office 365 portal is issued to the user.</span></span>
* <span data-ttu-id="962fc-122">페더레이션 메타데이터가 연결할 수 없거나 자동 인증서 롤오버를 사용할 수 없기 때문에 새 토큰 서명 인증서를 검색할 수 없는 경우 Azure AD는 전자 메일 알림과 Office 365 포털 내의 경고를 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-122">If it cannot retrieve the new token signing certificates, either because the federation metadata is not reachable or automatic certificate rollover is not enabled, Azure AD issues an email notification and a warning in the Office 365 portal.</span></span>

![Office 365 포털 알림](./media/active-directory-aadconnect-o365-certs/notification.png)

> [!IMPORTANT]
> <span data-ttu-id="962fc-124">비즈니스 연속성을 위해 AD FS를 사용하는 경우 알려진 문제에 대한 인증 실패가 발생하지 않도록 서버에 다음 업데이트를 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-124">If you are using AD FS, to ensure business continuity, please verify that your servers have the following updates so that authentication failures for known issues do not occur.</span></span> <span data-ttu-id="962fc-125">이는 갱신 및 향후 갱신 기간에 대해 알려진 AD FS 프록시 서버 문제를 완화합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-125">This mitigates known AD FS proxy server issues for this renewal and future renewal periods:</span></span>
>
> <span data-ttu-id="962fc-126">서버 2012 R2 - [Windows Server 2014년 5월 롤업](http://support.microsoft.com/kb/2955164)</span><span class="sxs-lookup"><span data-stu-id="962fc-126">Server 2012 R2 - [Windows Server May 2014 rollup](http://support.microsoft.com/kb/2955164)</span></span>
>
> <span data-ttu-id="962fc-127">Server 2008 R2 및 2012 - [Windows Server 2008 또는 Windows 2012 R2 SP1에서 프록시를 통한 인증 실패](http://support.microsoft.com/kb/3094446)</span><span class="sxs-lookup"><span data-stu-id="962fc-127">Server 2008 R2 and 2012 - [Authentication through proxy fails in Windows Server 2012 or Windows 2008 R2 SP1](http://support.microsoft.com/kb/3094446)</span></span>
>
>

## <span data-ttu-id="962fc-128">인증서를 업데이트해야 하는지를 확인합니다. <a name="managecerts"></a></span><span class="sxs-lookup"><span data-stu-id="962fc-128">Check if the certificates need to be updated <a name="managecerts"></a></span></span>
### <a name="step-1-check-the-autocertificaterollover-state"></a><span data-ttu-id="962fc-129">1단계: AutoCertificateRollover 상태 검사</span><span class="sxs-lookup"><span data-stu-id="962fc-129">Step 1: Check the AutoCertificateRollover state</span></span>
<span data-ttu-id="962fc-130">AD FS 서버에서 PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-130">On your AD FS server, open PowerShell.</span></span> <span data-ttu-id="962fc-131">AutoCertificateRollover 값을 True로 설정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-131">Check that the AutoCertificateRollover value is set to True.</span></span>

    Get-Adfsproperties

![AutoCertificateRollover](./media/active-directory-aadconnect-o365-certs/autocertrollover.png)

>[!NOTE] 
><span data-ttu-id="962fc-133">AD FS 2.0을 사용하는 경우 Add-Pssnapin 먼저 Microsoft.Adfs.Powershell을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-133">If you are using AD FS 2.0, first run Add-Pssnapin Microsoft.Adfs.Powershell.</span></span>

### <a name="step-2-confirm-that-ad-fs-and-azure-ad-are-in-sync"></a><span data-ttu-id="962fc-134">2단계: AD FS와 Azure AD가 동기화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="962fc-134">Step 2: Confirm that AD FS and Azure AD are in sync</span></span>
<span data-ttu-id="962fc-135">AD FS 서버에서 Azure AD PowerShell 프롬프트를 열고 Azure AD에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-135">On your AD FS server, open the Azure AD PowerShell prompt, and connect to Azure AD.</span></span>

> [!NOTE]
> <span data-ttu-id="962fc-136">Azure AD PowerShell을 [여기](https://technet.microsoft.com/library/jj151815.aspx)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-136">You can download Azure AD PowerShell [here](https://technet.microsoft.com/library/jj151815.aspx).</span></span>
>
>

    Connect-MsolService

<span data-ttu-id="962fc-137">AD FS에서 구성된 인증서 및 지정된 도메인에 대한 Azure AD 트러스트 속성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-137">Check the certificates configured in AD FS and Azure AD trust properties for the specified domain.</span></span>

    Get-MsolFederationProperty -DomainName <domain.name> | FL Source, TokenSigningCertificate

![Get-MsolFederationProperty](./media/active-directory-aadconnect-o365-certs/certsync.png)

<span data-ttu-id="962fc-139">두 출력의 지문이 일치하는 경우 인증서는 Azure AD와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-139">If the thumbprints in both the outputs match, your certificates are in sync with Azure AD.</span></span>

### <a name="step-3-check-if-your-certificate-is-about-to-expire"></a><span data-ttu-id="962fc-140">3단계: 인증서가 만료되려고 하는지 확인</span><span class="sxs-lookup"><span data-stu-id="962fc-140">Step 3: Check if your certificate is about to expire</span></span>
<span data-ttu-id="962fc-141">Get-MsolFederationProperty 또는 Get-AdfsCertificate 중 하나의 출력에서 "이후가 아님" 아래에 있는 날짜를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-141">In the output of either Get-MsolFederationProperty or Get-AdfsCertificate, check for the date under "Not After."</span></span> <span data-ttu-id="962fc-142">날짜가 30일 이내인 경우 조치를 취해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-142">If the date is less than 30 days away, you should take action.</span></span>

| <span data-ttu-id="962fc-143">AutoCertificateRollover</span><span class="sxs-lookup"><span data-stu-id="962fc-143">AutoCertificateRollover</span></span> | <span data-ttu-id="962fc-144">Azure AD와 동기화된 인증서</span><span class="sxs-lookup"><span data-stu-id="962fc-144">Certificates in sync with Azure AD</span></span> | <span data-ttu-id="962fc-145">페더레이션 메타데이터는 공개적으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-145">Federation metadata is publicly accessible</span></span> | <span data-ttu-id="962fc-146">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="962fc-146">Validity</span></span> | <span data-ttu-id="962fc-147">동작</span><span class="sxs-lookup"><span data-stu-id="962fc-147">Action</span></span> |
|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="962fc-148">예</span><span class="sxs-lookup"><span data-stu-id="962fc-148">Yes</span></span> |<span data-ttu-id="962fc-149">예</span><span class="sxs-lookup"><span data-stu-id="962fc-149">Yes</span></span> |<span data-ttu-id="962fc-150">예</span><span class="sxs-lookup"><span data-stu-id="962fc-150">Yes</span></span> |- |<span data-ttu-id="962fc-151">어떤 조치도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-151">No action needed.</span></span> <span data-ttu-id="962fc-152">[자동으로 토큰 서명 인증서 갱신](#autorenew)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="962fc-152">See [Renew token signing certificate automatically](#autorenew).</span></span> |
| <span data-ttu-id="962fc-153">예</span><span class="sxs-lookup"><span data-stu-id="962fc-153">Yes</span></span> |<span data-ttu-id="962fc-154">아니요</span><span class="sxs-lookup"><span data-stu-id="962fc-154">No</span></span> |- |<span data-ttu-id="962fc-155">15일 이내</span><span class="sxs-lookup"><span data-stu-id="962fc-155">Less than 15 days</span></span> |<span data-ttu-id="962fc-156">즉시 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-156">Renew immediately.</span></span> <span data-ttu-id="962fc-157">[수동으로 토큰 서명 인증서 갱신](#manualrenew)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="962fc-157">See [Renew token signing certificate manually](#manualrenew).</span></span> |
| <span data-ttu-id="962fc-158">아니요</span><span class="sxs-lookup"><span data-stu-id="962fc-158">No</span></span> |- |- |<span data-ttu-id="962fc-159">30일 이내</span><span class="sxs-lookup"><span data-stu-id="962fc-159">Less than 30 days</span></span> |<span data-ttu-id="962fc-160">즉시 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-160">Renew immediately.</span></span> <span data-ttu-id="962fc-161">[수동으로 토큰 서명 인증서 갱신](#manualrenew)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="962fc-161">See [Renew token signing certificate manually](#manualrenew).</span></span> |

<span data-ttu-id="962fc-162">\[-] 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-162">\[-]  Does not matter</span></span>

## <span data-ttu-id="962fc-163">토큰 서명 인증서를 자동으로 갱신(권장됨) <a name="autorenew"></a></span><span class="sxs-lookup"><span data-stu-id="962fc-163">Renew the token signing certificate automatically (recommended) <a name="autorenew"></a></span></span>
<span data-ttu-id="962fc-164">다음 두 가지가 true일 경우 수동 단계를 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-164">You don't need to perform any manual steps if both of the following are true:</span></span>

* <span data-ttu-id="962fc-165">엑스트라넷에서 페더레이션 메타데이터에 액세스할 수 있는 웹 응용 프로그램 프록시를 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-165">You have deployed Web Application Proxy, which can enable access to the federation metadata from the extranet.</span></span>
* <span data-ttu-id="962fc-166">AD FS 기본 구성(AutoCertificateRollover 사용)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-166">You are using the AD FS default configuration (AutoCertificateRollover is enabled).</span></span>

<span data-ttu-id="962fc-167">다음을 확인하여 인증서를 자동으로 업데이트할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-167">Check the following to confirm that the certificate can be automatically updated.</span></span>

<span data-ttu-id="962fc-168">**1. AD FS 속성 AutoCertificateRollover를 True로 설정해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="962fc-168">**1. The AD FS property AutoCertificateRollover must be set to True.**</span></span> <span data-ttu-id="962fc-169">이는 기존 항목이 만료되기 전에 AD FS가 자동으로 새 토큰 서명 및 토큰 암호 해독 인증서를 생성함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-169">This indicates that AD FS will automatically generate new token signing and token decryption certificates, before the old ones expire.</span></span>

<span data-ttu-id="962fc-170">**2. AD FS 페더레이션 메타데이터는 공개적으로 액세스할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="962fc-170">**2. The AD FS federation metadata is publicly accessible.**</span></span> <span data-ttu-id="962fc-171">공용 인터넷(회사 네트워크 외부)에 있는 컴퓨터에서 다음 URL로 이동하여 공개적으로 페더레이션 메타 데이터에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-171">Check that your federation metadata is publicly accessible by navigating to the following URL from a computer on the public internet (off of the corporate network):</span></span>

<span data-ttu-id="962fc-172">https://(your_FS_name)/federationmetadata/2007-06/federationmetadata.xml</span><span class="sxs-lookup"><span data-stu-id="962fc-172">https://(your_FS_name)/federationmetadata/2007-06/federationmetadata.xml</span></span>

<span data-ttu-id="962fc-173">여기서 `(your_FS_name) `은 fs.contoso.com과 같이 조직에서 사용하는 페더레이션 서비스 호스트 이름으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-173">where `(your_FS_name) `is replaced with the federation service host name your organization uses, such as fs.contoso.com.</span></span>  <span data-ttu-id="962fc-174">두 설정을 모두 확인할 수 있는 경우 그 밖에 다른 작업을 수행할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-174">If you are able to verify both of these settings successfully, you do not have to do anything else.</span></span>  

<span data-ttu-id="962fc-175">예: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml</span><span class="sxs-lookup"><span data-stu-id="962fc-175">Example: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml</span></span>

## <span data-ttu-id="962fc-176">수동으로 토큰 서명 인증서 갱신 <a name="manualrenew"></a></span><span class="sxs-lookup"><span data-stu-id="962fc-176">Renew the token signing certificate manually <a name="manualrenew"></a></span></span>
<span data-ttu-id="962fc-177">토큰 서명 인증서를 수동으로 갱신하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-177">You may choose to renew the token signing certificates manually.</span></span> <span data-ttu-id="962fc-178">예를 들어, 다음과 같은 경우 수동 갱신에 대 한 더 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-178">For example, the following scenarios might work better for manual renewal:</span></span>

* <span data-ttu-id="962fc-179">토큰 서명 인증서는 자체 서명된 인증서가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-179">Token signing certificates are not self-signed certificates.</span></span> <span data-ttu-id="962fc-180">가장 일반적인 이유는 조직이 조직 인증 기관에서 등록한 AD FS 인증서를 관리하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-180">The most common reason for this is that your organization manages AD FS certificates enrolled from an organizational certificate authority.</span></span>
* <span data-ttu-id="962fc-181">네트워크 보안은 페더레이션 메타데이터를 공개적으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-181">Network security does not allow the federation metadata to be publicly available.</span></span>

<span data-ttu-id="962fc-182">토큰 서명 인증서를 업데이트할 때마다 이러한 시나리오에서는 PowerShell 명령인 Update-MsolFederatedDomain을 사용하여 Office 365 도메인을 또한 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-182">In these scenarios, every time you update the token signing certificates, you must also update your Office 365 domain by using the PowerShell command, Update-MsolFederatedDomain.</span></span>

### <a name="step-1-ensure-that-ad-fs-has-new-token-signing-certificates"></a><span data-ttu-id="962fc-183">1단계: AD FS에 새 토큰 서명 인증서가 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="962fc-183">Step 1: Ensure that AD FS has new token signing certificates</span></span>
<span data-ttu-id="962fc-184">**기본이 아닌 구성**</span><span class="sxs-lookup"><span data-stu-id="962fc-184">**Non-default configuration**</span></span>

<span data-ttu-id="962fc-185">**AutoCertificateRollover**가 **False**로 설정된 AD FS의 기본이 아닌 구성을 사용하는 경우 사용자 지정 인증서(자체 서명되지 않음)을 사용할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-185">If you are using a non-default configuration of AD FS (where **AutoCertificateRollover** is set to **False**), you are probably using custom certificates (not self-signed).</span></span> <span data-ttu-id="962fc-186">AD FS 토큰 서명 인증서를 갱신하는 방법에 대한 포괄적인 지침은 [AD FS 자체 서명된 인증서를 사용하지 않는 고객에 대한 지침](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert)을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="962fc-186">For more information about how to renew the AD FS token signing certificates, see [Guidance for customers not using AD FS self-signed certificates](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert).</span></span>

<span data-ttu-id="962fc-187">**페더레이션 메타데이터를 공개적으로 사용할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="962fc-187">**Federation metadata is not publicly available**</span></span>

<span data-ttu-id="962fc-188">반면에 **AutoCertificateRollover**가 **True**로 설정되었지만 페더레이션 메타데이터가 공개적으로 액세스할 수 없는 경우 먼저 AD FS에서 새 토큰 서명 인증서를 생성했는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-188">On the other hand, if **AutoCertificateRollover** is set to **True**, but your federation metadata is not publicly accessible, first make sure that new token signing certificates have been generated by AD FS.</span></span> <span data-ttu-id="962fc-189">다음 단계를 수행하여 새 토큰 서명 인증서를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-189">Confirm you have new token signing certificates by taking the following steps:</span></span>

1. <span data-ttu-id="962fc-190">기본 AD FS 서버에 로그온했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-190">Verify that you are logged on to the primary AD FS server.</span></span>
2. <span data-ttu-id="962fc-191">PowerShell 명령 창을 열고 다음 명령을 실행하여 AD FS에서 현재 서명 인증서를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-191">Check the current signing certificates in AD FS by opening a PowerShell command window, and running the following command:</span></span>

    <span data-ttu-id="962fc-192">PS C:\>Get-ADFSCertificate –CertificateType token-signing</span><span class="sxs-lookup"><span data-stu-id="962fc-192">PS C:\>Get-ADFSCertificate –CertificateType token-signing</span></span>

   > [!NOTE]
   > <span data-ttu-id="962fc-193">AD FS 2.0을 사용하는 경우 Add-Pssnapin Microsoft.Adfs.Powershell을 먼저 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-193">If you are using AD FS 2.0, you should run Add-Pssnapin Microsoft.Adfs.Powershell first.</span></span>
   >
   >
3. <span data-ttu-id="962fc-194">나열된 모든 인증서에서 명령 출력을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-194">Look at the command output at any certificates listed.</span></span> <span data-ttu-id="962fc-195">AD FS에서 새 인증서를 생성했으면 두 인증서가 출력에 표시됩니다. 하나는 **IsPrimary** 값이 **True**이고 **NotAfter** 날짜는 5일 이내이며 다른 하나는 **IsPrimary**가 **False**이고 **NotAfter**는 향후 1년 정도입니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-195">If AD FS has generated a new certificate, you should see two certificates in the output: one for which the **IsPrimary** value is **True** and the **NotAfter** date is within 5 days, and one for which **IsPrimary** is **False** and **NotAfter** is about a year in the future.</span></span>
4. <span data-ttu-id="962fc-196">인증서가 하나만 표시되는 경우 **NotAfter** 날짜가 5일 이내이면 새 인증서를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-196">If you only see one certificate, and the **NotAfter** date is within 5 days, you need to generate a new certificate.</span></span>
5. <span data-ttu-id="962fc-197">새 인증서를 생성하려면 PowerShell 명령 프롬프트에서 다음 명령을 실행합니다: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`.</span><span class="sxs-lookup"><span data-stu-id="962fc-197">To generate a new certificate, execute the following command at a PowerShell command prompt: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`.</span></span>
6. <span data-ttu-id="962fc-198">PS C:\>Get-ADFSCertificate –CertificateType token-signing 명령을 다시 실행하여 업데이트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-198">Verify the update by running the following command again: PS C:\>Get-ADFSCertificate –CertificateType token-signing</span></span>

<span data-ttu-id="962fc-199">이제 두 인증서 나열되어야 하며 둘 중 하나의 **NotAfter** 날짜가 향후 약 1년 정도이고 **IsPrimary** 값은 **False**입니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-199">Two certificates should be listed now, one of which has a **NotAfter** date of approximately one year in the future, and for which the **IsPrimary** value is **False**.</span></span>

### <a name="step-2-update-the-new-token-signing-certificates-for-the-office-365-trust"></a><span data-ttu-id="962fc-200">2단계: Office 365 트러스트에 대한 새 토큰 서명 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="962fc-200">Step 2: Update the new token signing certificates for the Office 365 trust</span></span>
<span data-ttu-id="962fc-201">새 토큰 서명 인증서를 가진 Office 365를 다음과 같이 트러스트에 사용하도록 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-201">Update Office 365 with the new token signing certificates to be used for the trust, as follows.</span></span>

1. <span data-ttu-id="962fc-202">Windows PowerShell용 Microsoft Azure Active Directory 모듈을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-202">Open the Microsoft Azure Active Directory Module for Windows PowerShell.</span></span>
2. <span data-ttu-id="962fc-203">$cred=Get-Credential을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-203">Run $cred=Get-Credential.</span></span> <span data-ttu-id="962fc-204">이 cmdlet에서 자격 증명을 물어보면 클라우드 서비스 관리자 계정 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-204">When this cmdlet prompts you for credentials, type your cloud service administrator account credentials.</span></span>
3. <span data-ttu-id="962fc-205">Connect-MsolService –Credential $cred를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-205">Run Connect-MsolService –Credential $cred.</span></span> <span data-ttu-id="962fc-206">이 cmdlet을 실행하면 클라우드 서비스에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-206">This cmdlet connects you to the cloud service.</span></span> <span data-ttu-id="962fc-207">도구를 통해 설치되는 추가 cmdlet을 실행하려면 먼저 클라우드 서비스에 연결되는 컨텍스트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-207">Creating a context that connects you to the cloud service is required before running any of the additional cmdlets installed by the tool.</span></span>
4. <span data-ttu-id="962fc-208">AD FS 기본 페더레이션 서버가 아닌 컴퓨터에서 이러한 명령을 실행하는 경우 Set-MSOLAdfscontext -Computer <AD FS primary server>을 실행합니다. 여기서 <AD FS primary server>는 기본 AD FS 서버의 내부 FQDN 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-208">If you are running these commands on a computer that is not the AD FS primary federation server, run Set-MSOLAdfscontext -Computer <AD FS primary server>, where <AD FS primary server> is the internal FQDN name of the primary AD FS server.</span></span> <span data-ttu-id="962fc-209">이 cmdlet은 AD FS에 연결되는 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-209">This cmdlet creates a context that connects you to AD FS.</span></span>
5. <span data-ttu-id="962fc-210">Update-MSOLFederatedDomain –DomainName <domain>을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-210">Run Update-MSOLFederatedDomain –DomainName <domain>.</span></span> <span data-ttu-id="962fc-211">이 cmdlet은 AD FS에서 클라우드 서비스로 설정을 업데이트하고 둘 사이의 트러스트 관계를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-211">This cmdlet updates the settings from AD FS into the cloud service, and configures the trust relationship between the two.</span></span>

> [!NOTE]
> <span data-ttu-id="962fc-212">contoso.com과 fabrikam.com 등의 여러 최상위 도메인을 지원해야 하는 경우에는 cmdlet과 함께 **SupportMultipleDomain** 스위치를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-212">If you need to support multiple top-level domains, such as contoso.com and fabrikam.com, you must use the **SupportMultipleDomain** switch with any cmdlets.</span></span> <span data-ttu-id="962fc-213">자세한 내용은 [여러 최상위 도메인에 대한 지원](active-directory-aadconnect-multiple-domains.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="962fc-213">For more information, see [Support for Multiple Top Level Domains](active-directory-aadconnect-multiple-domains.md).</span></span>
>
>

## <span data-ttu-id="962fc-214">Azure AD Connect를 사용하여 Azure AD 트러스트 복구 <a name="connectrenew"></a></span><span class="sxs-lookup"><span data-stu-id="962fc-214">Repair Azure AD trust by using Azure AD Connect <a name="connectrenew"></a></span></span>
<span data-ttu-id="962fc-215">Azure AD Connect를 사용하여 AD FS 팜/Azure AD 트러스트를 구성했다면 Azure AD Connect을 사용하여 토큰 서명 인증서에 대한 어떤 작업을 할 필요가 있는지 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-215">If you configured your AD FS farm and Azure AD trust by using Azure AD Connect, you can use Azure AD Connect to detect if you need to take any action for your token signing certificates.</span></span> <span data-ttu-id="962fc-216">인증서를 갱신해야 하는 경우 Azure AD Connect를 사용하여 이렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-216">If you need to renew the certificates, you can use Azure AD Connect to do so.</span></span>

<span data-ttu-id="962fc-217">자세한 내용은 [트러스트 복구](active-directory-aadconnect-federation-management.md)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="962fc-217">For more information, see [Repairing the trust](active-directory-aadconnect-federation-management.md).</span></span>
