---
title: "Office 365 및 Azure AD 사용자에 대 한 aaaCertificate 갱신 | Microsoft Docs"
description: "이 문서에서는 tooOffice 365 사용자가 인증서를 갱신 하는 방법에 대 한 알리는 전자 메일을 tooresolve 발급 하는 방법을 설명 합니다."
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
ms.openlocfilehash: b9b309e06949dc5488cd628650be413f366ed347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="renew-federation-certificates-for-office-365-and-azure-active-directory"></a><span data-ttu-id="c75d0-103">Office 365 및 Azure Active Directory에 대한 페더레이션 인증서 갱신</span><span class="sxs-lookup"><span data-stu-id="c75d0-103">Renew federation certificates for Office 365 and Azure Active Directory</span></span>
## <a name="overview"></a><span data-ttu-id="c75d0-104">개요</span><span class="sxs-lookup"><span data-stu-id="c75d0-104">Overview</span></span>
<span data-ttu-id="c75d0-105">Azure Active Directory (Azure AD)와 Active Directory Federation Services (AD FS) 사이의 성공적인 페더레이션에 대 한 AD FS toosign 보안 토큰 tooAzure AD에서 사용 하는 hello 인증서는 Azure AD에 구성 된 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-105">For successful federation between Azure Active Directory (Azure AD) and Active Directory Federation Services (AD FS), hello certificates used by AD FS toosign security tokens tooAzure AD should match what is configured in Azure AD.</span></span> <span data-ttu-id="c75d0-106">불일치는 toobroken 트러스트가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-106">Any mismatch can lead toobroken trust.</span></span> <span data-ttu-id="c75d0-107">엑스트라넷에 액세스하기 위해 AD FS 및 웹 응용 프로그램 프록시를 배포하는 경우 Azure AD는 이 정보의 동기화를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-107">Azure AD ensures that this information is kept in sync when you deploy AD FS and Web Application Proxy (for extranet access).</span></span>

<span data-ttu-id="c75d0-108">이 문서는 추가 정보 toomanage 토큰 서명 인증서를 제공 하 고 비활성화 hello에 Azure AD와 동기화 유지:</span><span class="sxs-lookup"><span data-stu-id="c75d0-108">This article provides you additional information toomanage your token signing certificates and keep them in sync with Azure AD, in hello following cases:</span></span>

* <span data-ttu-id="c75d0-109">Hello 웹 응용 프로그램 프록시를 배포 하지 않은 hello 페더레이션 메타 데이터 이므로 hello 엑스트라넷에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-109">You are not deploying hello Web Application Proxy, and therefore hello federation metadata is not available in hello extranet.</span></span>
* <span data-ttu-id="c75d0-110">토큰 서명 인증서에 대 한 AD FS의 기본 구성은 hello를 사용 하지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-110">You are not using hello default configuration of AD FS for token signing certificates.</span></span>
* <span data-ttu-id="c75d0-111">타사 ID 공급자를 사용하는 경우.</span><span class="sxs-lookup"><span data-stu-id="c75d0-111">You are using a third-party identity provider.</span></span>

## <a name="default-configuration-of-ad-fs-for-token-signing-certificates"></a><span data-ttu-id="c75d0-112">토큰 서명 인증서에 대한 AD FS의 기본 구성</span><span class="sxs-lookup"><span data-stu-id="c75d0-112">Default configuration of AD FS for token signing certificates</span></span>
<span data-ttu-id="c75d0-113">hello 토큰 서명 및 인증서의 암호를 해독 하는 토큰은 일반적으로 자체 서명된 된 인증서를 이며 1 년 동안 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-113">hello token signing and token decrypting certificates are usually self-signed certificates, and are good for one year.</span></span> <span data-ttu-id="c75d0-114">기본적으로 AD FS는 **AutoCertificateRollover**라는 자동 갱신 프로세스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-114">By default, AD FS includes an auto-renewal process called **AutoCertificateRollover**.</span></span> <span data-ttu-id="c75d0-115">AD FS 2.0 이상을 사용하는 경우는 인증서가 만료되기 전에 Office 365 및 Azure AD에서 자동으로 인증서를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-115">If you are using AD FS 2.0 or later, Office 365 and Azure AD automatically update your certificate before it expires.</span></span>

### <a name="renewal-notification-from-hello-office-365-portal-or-an-email"></a><span data-ttu-id="c75d0-116">Hello Office 365 포털 또는 전자 메일에서 갱신 알림</span><span class="sxs-lookup"><span data-stu-id="c75d0-116">Renewal notification from hello Office 365 portal or an email</span></span>
> [!NOTE]
> <span data-ttu-id="c75d0-117">전자 메일 또는 포털 toorenew 묻는 알림을 받은 경우 사무실에 대 한 인증서 참조 [관리 tootoken 서명 인증서 변경](#managecerts) toocheck tootake 조치가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-117">If you received an email or a portal notification asking you toorenew your certificate for Office, see [Managing changes tootoken signing certificates](#managecerts) toocheck if you need tootake any action.</span></span> <span data-ttu-id="c75d0-118">Microsoft는 아무런 작업도 수행할 필요가 있는 경우에 전송 되는 인증서 갱신을 위해 toonotifications 시킬 수 있는 가능한 문제를 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-118">Microsoft is aware of a possible issue that can lead toonotifications for certificate renewal being sent, even when no action is required.</span></span>
>
>

<span data-ttu-id="c75d0-119">Azure AD toomonitor hello 페더레이션 메타 데이터 및 업데이트 hello 토큰 서명 인증서를이 메타 데이터에 표시 된 대로 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-119">Azure AD attempts toomonitor hello federation metadata, and update hello token signing certificates as indicated by this metadata.</span></span> <span data-ttu-id="c75d0-120">30 일 hello hello 토큰 서명 인증서가 만료 되기 전에 Azure AD hello 페더레이션 메타 데이터를 폴링하여 새 인증서를 사용할 수 있으면 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-120">30 days before hello expiration of hello token signing certificates, Azure AD checks if new certificates are available by polling hello federation metadata.</span></span>

* <span data-ttu-id="c75d0-121">성공적으로 hello 페더레이션 메타 데이터를 폴링할 하 고 hello 새 인증서를 검색할 수, 하는 경우 전자 메일 알림 또는 hello Office 365 포털에 경고 없음 toohello 사용자를 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-121">If it can successfully poll hello federation metadata and retrieve hello new certificates, no email notification or warning in hello Office 365 portal is issued toohello user.</span></span>
* <span data-ttu-id="c75d0-122">Hello 새 토큰 서명 인증서를 검색할 수 없는 경우 하거나 자동 인증서 롤오버를 사용 하지 않는 또는 hello 페더레이션 메타 데이터에 연결할 수 없기 때문에 Azure AD에서 발행 전자 메일 알림 및 hello Office 365 포털에 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-122">If it cannot retrieve hello new token signing certificates, either because hello federation metadata is not reachable or automatic certificate rollover is not enabled, Azure AD issues an email notification and a warning in hello Office 365 portal.</span></span>

![Office 365 포털 알림](./media/active-directory-aadconnect-o365-certs/notification.png)

> [!IMPORTANT]
> <span data-ttu-id="c75d0-124">Tooensure 비즈니스 연속성을 AD FS를 사용 하는 경우에 서버 hello 알려진된 문제에 대 한 인증 실패가 발생 하지 않도록 있도록 업데이트 수행 되었는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c75d0-124">If you are using AD FS, tooensure business continuity, please verify that your servers have hello following updates so that authentication failures for known issues do not occur.</span></span> <span data-ttu-id="c75d0-125">이는 갱신 및 향후 갱신 기간에 대해 알려진 AD FS 프록시 서버 문제를 완화합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-125">This mitigates known AD FS proxy server issues for this renewal and future renewal periods:</span></span>
>
> <span data-ttu-id="c75d0-126">서버 2012 R2 - [Windows Server 2014년 5월 롤업](http://support.microsoft.com/kb/2955164)</span><span class="sxs-lookup"><span data-stu-id="c75d0-126">Server 2012 R2 - [Windows Server May 2014 rollup](http://support.microsoft.com/kb/2955164)</span></span>
>
> <span data-ttu-id="c75d0-127">Server 2008 R2 및 2012 - [Windows Server 2008 또는 Windows 2012 R2 SP1에서 프록시를 통한 인증 실패](http://support.microsoft.com/kb/3094446)</span><span class="sxs-lookup"><span data-stu-id="c75d0-127">Server 2008 R2 and 2012 - [Authentication through proxy fails in Windows Server 2012 or Windows 2008 R2 SP1](http://support.microsoft.com/kb/3094446)</span></span>
>
>

## <span data-ttu-id="c75d0-128">Hello 인증서 업데이트 toobe 경우 확인<a name="managecerts"></a></span><span class="sxs-lookup"><span data-stu-id="c75d0-128">Check if hello certificates need toobe updated <a name="managecerts"></a></span></span>
### <a name="step-1-check-hello-autocertificaterollover-state"></a><span data-ttu-id="c75d0-129">1 단계: hello AutoCertificateRollover 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-129">Step 1: Check hello AutoCertificateRollover state</span></span>
<span data-ttu-id="c75d0-130">AD FS 서버에서 PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-130">On your AD FS server, open PowerShell.</span></span> <span data-ttu-id="c75d0-131">Hello AutoCertificateRollover 값 tooTrue 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-131">Check that hello AutoCertificateRollover value is set tooTrue.</span></span>

    Get-Adfsproperties

![AutoCertificateRollover](./media/active-directory-aadconnect-o365-certs/autocertrollover.png)

>[!NOTE] 
><span data-ttu-id="c75d0-133">AD FS 2.0을 사용하는 경우 Add-Pssnapin 먼저 Microsoft.Adfs.Powershell을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-133">If you are using AD FS 2.0, first run Add-Pssnapin Microsoft.Adfs.Powershell.</span></span>

### <a name="step-2-confirm-that-ad-fs-and-azure-ad-are-in-sync"></a><span data-ttu-id="c75d0-134">2단계: AD FS와 Azure AD가 동기화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="c75d0-134">Step 2: Confirm that AD FS and Azure AD are in sync</span></span>
<span data-ttu-id="c75d0-135">AD FS 서버의 hello Azure AD PowerShell 프롬프트를 열고 tooAzure AD 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-135">On your AD FS server, open hello Azure AD PowerShell prompt, and connect tooAzure AD.</span></span>

> [!NOTE]
> <span data-ttu-id="c75d0-136">Azure AD PowerShell을 [여기](https://technet.microsoft.com/library/jj151815.aspx)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-136">You can download Azure AD PowerShell [here](https://technet.microsoft.com/library/jj151815.aspx).</span></span>
>
>

    Connect-MsolService

<span data-ttu-id="c75d0-137">AD FS의에서 hello 인증서 구성 및 Azure AD 트러스트 속성 hello에 대 한 지정 된 도메인을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-137">Check hello certificates configured in AD FS and Azure AD trust properties for hello specified domain.</span></span>

    Get-MsolFederationProperty -DomainName <domain.name> | FL Source, TokenSigningCertificate

![Get-MsolFederationProperty](./media/active-directory-aadconnect-o365-certs/certsync.png)

<span data-ttu-id="c75d0-139">모두 hello 지문이 hello 출력 하는 경우 일치 하는 인증서가 Azure AD와 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-139">If hello thumbprints in both hello outputs match, your certificates are in sync with Azure AD.</span></span>

### <a name="step-3-check-if-your-certificate-is-about-tooexpire"></a><span data-ttu-id="c75d0-140">3 단계: tooexpire에 대 한 인증서 인지 확인</span><span class="sxs-lookup"><span data-stu-id="c75d0-140">Step 3: Check if your certificate is about tooexpire</span></span>
<span data-ttu-id="c75d0-141">Get-msolfederationproperty 또는 Get AdfsCertificate hello 출력에서 하지 이후"."에서 hello 날짜에 대 한 확인</span><span class="sxs-lookup"><span data-stu-id="c75d0-141">In hello output of either Get-MsolFederationProperty or Get-AdfsCertificate, check for hello date under "Not After."</span></span> <span data-ttu-id="c75d0-142">Hello 날짜가 30 일 이내 자리를 비울 이면 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-142">If hello date is less than 30 days away, you should take action.</span></span>

| <span data-ttu-id="c75d0-143">AutoCertificateRollover</span><span class="sxs-lookup"><span data-stu-id="c75d0-143">AutoCertificateRollover</span></span> | <span data-ttu-id="c75d0-144">Azure AD와 동기화된 인증서</span><span class="sxs-lookup"><span data-stu-id="c75d0-144">Certificates in sync with Azure AD</span></span> | <span data-ttu-id="c75d0-145">페더레이션 메타데이터는 공개적으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-145">Federation metadata is publicly accessible</span></span> | <span data-ttu-id="c75d0-146">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="c75d0-146">Validity</span></span> | <span data-ttu-id="c75d0-147">동작</span><span class="sxs-lookup"><span data-stu-id="c75d0-147">Action</span></span> |
|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="c75d0-148">예</span><span class="sxs-lookup"><span data-stu-id="c75d0-148">Yes</span></span> |<span data-ttu-id="c75d0-149">예</span><span class="sxs-lookup"><span data-stu-id="c75d0-149">Yes</span></span> |<span data-ttu-id="c75d0-150">예</span><span class="sxs-lookup"><span data-stu-id="c75d0-150">Yes</span></span> |- |<span data-ttu-id="c75d0-151">어떤 조치도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-151">No action needed.</span></span> <span data-ttu-id="c75d0-152">[자동으로 토큰 서명 인증서 갱신](#autorenew)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c75d0-152">See [Renew token signing certificate automatically](#autorenew).</span></span> |
| <span data-ttu-id="c75d0-153">예</span><span class="sxs-lookup"><span data-stu-id="c75d0-153">Yes</span></span> |<span data-ttu-id="c75d0-154">아니요</span><span class="sxs-lookup"><span data-stu-id="c75d0-154">No</span></span> |- |<span data-ttu-id="c75d0-155">15일 이내</span><span class="sxs-lookup"><span data-stu-id="c75d0-155">Less than 15 days</span></span> |<span data-ttu-id="c75d0-156">즉시 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-156">Renew immediately.</span></span> <span data-ttu-id="c75d0-157">[수동으로 토큰 서명 인증서 갱신](#manualrenew)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c75d0-157">See [Renew token signing certificate manually](#manualrenew).</span></span> |
| <span data-ttu-id="c75d0-158">아니요</span><span class="sxs-lookup"><span data-stu-id="c75d0-158">No</span></span> |- |- |<span data-ttu-id="c75d0-159">30일 이내</span><span class="sxs-lookup"><span data-stu-id="c75d0-159">Less than 30 days</span></span> |<span data-ttu-id="c75d0-160">즉시 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-160">Renew immediately.</span></span> <span data-ttu-id="c75d0-161">[수동으로 토큰 서명 인증서 갱신](#manualrenew)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c75d0-161">See [Renew token signing certificate manually](#manualrenew).</span></span> |

<span data-ttu-id="c75d0-162">\[-] 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-162">\[-]  Does not matter</span></span>

## <span data-ttu-id="c75d0-163">Hello 토큰 서명 인증서를 자동으로 갱신 (권장)<a name="autorenew"></a></span><span class="sxs-lookup"><span data-stu-id="c75d0-163">Renew hello token signing certificate automatically (recommended) <a name="autorenew"></a></span></span>
<span data-ttu-id="c75d0-164">필요 없음 tooperform는 수동으로 설치 hello 다음 모두 해당 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="c75d0-164">You don't need tooperform any manual steps if both of hello following are true:</span></span>

* <span data-ttu-id="c75d0-165">Hello 엑스트라넷에서 액세스 toohello 페더레이션 메타 데이터를 사용할 수 있는 웹 응용 프로그램 프록시를 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-165">You have deployed Web Application Proxy, which can enable access toohello federation metadata from hello extranet.</span></span>
* <span data-ttu-id="c75d0-166">AD FS hello 기본 구성 (AutoCertificateRollover 사용)를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-166">You are using hello AD FS default configuration (AutoCertificateRollover is enabled).</span></span>

<span data-ttu-id="c75d0-167">다음 인증서 hello tooconfirm 검사 hello는 자동으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-167">Check hello following tooconfirm that hello certificate can be automatically updated.</span></span>

<span data-ttu-id="c75d0-168">**1. hello AD FS 속성 AutoCertificateRollover tooTrue 설정 되어야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c75d0-168">**1. hello AD FS property AutoCertificateRollover must be set tooTrue.**</span></span> <span data-ttu-id="c75d0-169">이 새 토큰 서명 및 토큰 암호 해독 인증서 만료 된 hello 이전 하기 전에 AD FS 자동으로 생성 됩니다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-169">This indicates that AD FS will automatically generate new token signing and token decryption certificates, before hello old ones expire.</span></span>

<span data-ttu-id="c75d0-170">**2. hello AD FS 페더레이션 메타 데이터는 공개적으로 액세스할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="c75d0-170">**2. hello AD FS federation metadata is publicly accessible.**</span></span> <span data-ttu-id="c75d0-171">Toohello 이동 하 여 페더레이션 메타 데이터에 공개적으로 액세스할 수 있는지 확인 하십시오 (hello 회사 네트워크)에서 공용 인터넷 hello URL에는 컴퓨터에서 나오는에:</span><span class="sxs-lookup"><span data-stu-id="c75d0-171">Check that your federation metadata is publicly accessible by navigating toohello following URL from a computer on hello public internet (off of hello corporate network):</span></span>

<span data-ttu-id="c75d0-172">https://(your_FS_name)/federationmetadata/2007-06/federationmetadata.xml</span><span class="sxs-lookup"><span data-stu-id="c75d0-172">https://(your_FS_name)/federationmetadata/2007-06/federationmetadata.xml</span></span>

<span data-ttu-id="c75d0-173">여기서 `(your_FS_name) `fs.contoso.com과 같이 조직을 사용 하는 hello 페더레이션 서비스 호스트 이름으로 대체 됩니다.  두 tooverify 수 있다면 이러한 설정에 성공적으로 없는 toodo 다른 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-173">where `(your_FS_name) `is replaced with hello federation service host name your organization uses, such as fs.contoso.com.  If you are able tooverify both of these settings successfully, you do not have toodo anything else.</span></span>  

<span data-ttu-id="c75d0-174">예: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml</span><span class="sxs-lookup"><span data-stu-id="c75d0-174">Example: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml</span></span>

## <span data-ttu-id="c75d0-175">Hello 토큰 서명 인증서를 수동으로 갱신<a name="manualrenew"></a></span><span class="sxs-lookup"><span data-stu-id="c75d0-175">Renew hello token signing certificate manually <a name="manualrenew"></a></span></span>
<span data-ttu-id="c75d0-176">선택할 수 있습니다 toorenew hello 토큰 서명 인증서 수동으로.</span><span class="sxs-lookup"><span data-stu-id="c75d0-176">You may choose toorenew hello token signing certificates manually.</span></span> <span data-ttu-id="c75d0-177">예를 들어 hello 다음과 같은 시나리오에 더 적합할 수 수동 갱신 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-177">For example, hello following scenarios might work better for manual renewal:</span></span>

* <span data-ttu-id="c75d0-178">토큰 서명 인증서는 자체 서명된 인증서가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-178">Token signing certificates are not self-signed certificates.</span></span> <span data-ttu-id="c75d0-179">hello 가장 일반적인 이유는 조직의 AD FS 인증서는 조직의 인증 기관에서 등록을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-179">hello most common reason for this is that your organization manages AD FS certificates enrolled from an organizational certificate authority.</span></span>
* <span data-ttu-id="c75d0-180">네트워크 보안에는 hello 페더레이션 메타 데이터 toobe 공개적으로 사용할 수 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-180">Network security does not allow hello federation metadata toobe publicly available.</span></span>

<span data-ttu-id="c75d0-181">이러한 시나리오에서는 hello 토큰 서명 인증서를 업데이트할 때마다도 업데이트 해야 Office 365 도메인 Update-msolfederateddomain hello PowerShell 명령을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-181">In these scenarios, every time you update hello token signing certificates, you must also update your Office 365 domain by using hello PowerShell command, Update-MsolFederatedDomain.</span></span>

### <a name="step-1-ensure-that-ad-fs-has-new-token-signing-certificates"></a><span data-ttu-id="c75d0-182">1단계: AD FS에 새 토큰 서명 인증서가 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="c75d0-182">Step 1: Ensure that AD FS has new token signing certificates</span></span>
<span data-ttu-id="c75d0-183">**기본이 아닌 구성**</span><span class="sxs-lookup"><span data-stu-id="c75d0-183">**Non-default configuration**</span></span>

<span data-ttu-id="c75d0-184">AD FS의 기본 구성이 사용 하는 경우 (여기서 **AutoCertificateRollover** 너무 설정**False**), 사용자 지정 인증서 (자체 서명 되지 않았습니다)을 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-184">If you are using a non-default configuration of AD FS (where **AutoCertificateRollover** is set too**False**), you are probably using custom certificates (not self-signed).</span></span> <span data-ttu-id="c75d0-185">어떻게 toorenew hello AD FS 토큰 서명 인증서에 대 한 자세한 내용은 참조 [자체 서명 인증서를 AD FS를 사용 하지 않는 고객에 대 한 지침](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert)합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-185">For more information about how toorenew hello AD FS token signing certificates, see [Guidance for customers not using AD FS self-signed certificates](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert).</span></span>

<span data-ttu-id="c75d0-186">**페더레이션 메타데이터를 공개적으로 사용할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="c75d0-186">**Federation metadata is not publicly available**</span></span>

<span data-ttu-id="c75d0-187">경우에 다른 손을 hello **AutoCertificateRollover** 너무 설정 되어**True**, 페더레이션 메타 데이터를 공개적으로 액세스할 수 없는 경우, 먼저 새 토큰 서명 인증서 AD에서 생성 하 고 있는지 확인 하지만 FS 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-187">On hello other hand, if **AutoCertificateRollover** is set too**True**, but your federation metadata is not publicly accessible, first make sure that new token signing certificates have been generated by AD FS.</span></span> <span data-ttu-id="c75d0-188">새 토큰 서명 인증서 라인 hello 단계를 수행 하 여 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-188">Confirm you have new token signing certificates by taking hello following steps:</span></span>

1. <span data-ttu-id="c75d0-189">Toohello 기본 AD FS 서버에 로그온 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-189">Verify that you are logged on toohello primary AD FS server.</span></span>
2. <span data-ttu-id="c75d0-190">PowerShell 명령 창을 열고 다음 명령을 hello를 실행 하 여 AD FS에서 hello 현재 서명 인증서를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-190">Check hello current signing certificates in AD FS by opening a PowerShell command window, and running hello following command:</span></span>

    <span data-ttu-id="c75d0-191">PS C:\>Get-ADFSCertificate –CertificateType token-signing</span><span class="sxs-lookup"><span data-stu-id="c75d0-191">PS C:\>Get-ADFSCertificate –CertificateType token-signing</span></span>

   > [!NOTE]
   > <span data-ttu-id="c75d0-192">AD FS 2.0을 사용하는 경우 Add-Pssnapin Microsoft.Adfs.Powershell을 먼저 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-192">If you are using AD FS 2.0, you should run Add-Pssnapin Microsoft.Adfs.Powershell first.</span></span>
   >
   >
3. <span data-ttu-id="c75d0-193">나열 된 모든 인증서에 hello 명령 출력을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-193">Look at hello command output at any certificates listed.</span></span> <span data-ttu-id="c75d0-194">AD FS가 새 인증서를 생성 하는 경우에 hello 출력에 두 개의 인증서 표시 됩니다: 어떤 hello에 대 한 **IsPrimary** 값은 **True** 및 hello **NotAfter** 날짜는 개와 5 일 내 **IsPrimary** 은 **False** 및 **NotAfter** hello 나중에 1 년에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-194">If AD FS has generated a new certificate, you should see two certificates in hello output: one for which hello **IsPrimary** value is **True** and hello **NotAfter** date is within 5 days, and one for which **IsPrimary** is **False** and **NotAfter** is about a year in hello future.</span></span>
4. <span data-ttu-id="c75d0-195">만 인증서 1 개를 참조 하 고 hello **NotAfter** 날짜 5 일 이내는 toogenerate 새 인증서를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-195">If you only see one certificate, and hello **NotAfter** date is within 5 days, you need toogenerate a new certificate.</span></span>
5. <span data-ttu-id="c75d0-196">새 인증서를 toogenerate hello 다음 PowerShell 명령 프롬프트에서 명령을 실행: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-196">toogenerate a new certificate, execute hello following command at a PowerShell command prompt: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`.</span></span>
6. <span data-ttu-id="c75d0-197">다음 명령을 다시 hello를 실행 하 여 hello 업데이트 확인: PS c:\>Get ADFSCertificate – CertificateType 토큰 서명</span><span class="sxs-lookup"><span data-stu-id="c75d0-197">Verify hello update by running hello following command again: PS C:\>Get-ADFSCertificate –CertificateType token-signing</span></span>

<span data-ttu-id="c75d0-198">이제 두 개의 인증서 표시 됩니다, 그 중 하나에 **NotAfter** hello 미래에 어떤 hello에 대 한 약 1 년의 날짜 **IsPrimary** 값은 **False**합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-198">Two certificates should be listed now, one of which has a **NotAfter** date of approximately one year in hello future, and for which hello **IsPrimary** value is **False**.</span></span>

### <a name="step-2-update-hello-new-token-signing-certificates-for-hello-office-365-trust"></a><span data-ttu-id="c75d0-199">2 단계: hello 새 토큰 서명 인증서 hello Office 365 신뢰에 대 한 업데이트</span><span class="sxs-lookup"><span data-stu-id="c75d0-199">Step 2: Update hello new token signing certificates for hello Office 365 trust</span></span>
<span data-ttu-id="c75d0-200">Hello 새 토큰 서명 인증서 toobe 다음과 같이 hello 트러스트에 대 한 사용으로 Office 365를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-200">Update Office 365 with hello new token signing certificates toobe used for hello trust, as follows.</span></span>

1. <span data-ttu-id="c75d0-201">Hello Microsoft Azure Active Directory 모듈에 대 한 Windows PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-201">Open hello Microsoft Azure Active Directory Module for Windows PowerShell.</span></span>
2. <span data-ttu-id="c75d0-202">$cred=Get-Credential을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-202">Run $cred=Get-Credential.</span></span> <span data-ttu-id="c75d0-203">이 cmdlet에서 자격 증명을 물어보면 클라우드 서비스 관리자 계정 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-203">When this cmdlet prompts you for credentials, type your cloud service administrator account credentials.</span></span>
3. <span data-ttu-id="c75d0-204">Connect-MsolService –Credential $cred를 실행합니다. 이 cmdlet toohello 클라우드 서비스를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-204">Run Connect-MsolService –Credential $cred. This cmdlet connects you toohello cloud service.</span></span> <span data-ttu-id="c75d0-205">Hello 도구를 통해 설치 하는 hello 추가 cmdlet을 실행 하기 전에 필요 toohello 클라우드 서비스에 연결 하는 컨텍스트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-205">Creating a context that connects you toohello cloud service is required before running any of hello additional cmdlets installed by hello tool.</span></span>
4. <span data-ttu-id="c75d0-206">AD FS hello 기본 페더레이션 서버가 아닌 컴퓨터에 이러한 명령은 실행 하는 경우 실행 Set-msoladfscontext-컴퓨터 <AD FS primary server>여기서 <AD FS primary server> hello hello 기본 AD FS 서버의 내부 FQDN 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-206">If you are running these commands on a computer that is not hello AD FS primary federation server, run Set-MSOLAdfscontext -Computer <AD FS primary server>, where <AD FS primary server> is hello internal FQDN name of hello primary AD FS server.</span></span> <span data-ttu-id="c75d0-207">이 cmdlet은 tooAD FS 연결 하는 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-207">This cmdlet creates a context that connects you tooAD FS.</span></span>
5. <span data-ttu-id="c75d0-208">Update-MSOLFederatedDomain –DomainName <domain>을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-208">Run Update-MSOLFederatedDomain –DomainName <domain>.</span></span> <span data-ttu-id="c75d0-209">이 cmdlet hello 클라우드 서비스에 AD FS의 hello 설정을 업데이트 하 고 hello 2 간의 hello 트러스트 관계를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-209">This cmdlet updates hello settings from AD FS into hello cloud service, and configures hello trust relationship between hello two.</span></span>

> [!NOTE]
> <span data-ttu-id="c75d0-210">Hello를 사용 해야 toosupport contoso.com, fabrikam.com 등의 여러 최상위 도메인을 필요한 경우 **SupportMultipleDomain** 모든 cmdlet으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-210">If you need toosupport multiple top-level domains, such as contoso.com and fabrikam.com, you must use hello **SupportMultipleDomain** switch with any cmdlets.</span></span> <span data-ttu-id="c75d0-211">자세한 내용은 [여러 최상위 도메인에 대한 지원](active-directory-aadconnect-multiple-domains.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c75d0-211">For more information, see [Support for Multiple Top Level Domains](active-directory-aadconnect-multiple-domains.md).</span></span>
>
>

## <span data-ttu-id="c75d0-212">Azure AD Connect를 사용하여 Azure AD 트러스트 복구 <a name="connectrenew"></a></span><span class="sxs-lookup"><span data-stu-id="c75d0-212">Repair Azure AD trust by using Azure AD Connect <a name="connectrenew"></a></span></span>
<span data-ttu-id="c75d0-213">Azure AD Connect를 사용 하 여 AD FS 팜 및 Azure AD 트러스트를 구성 하는 경우에 토큰 서명 인증서에 대 한 tootake 조치가 필요한 경우 Azure AD Connect toodetect를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-213">If you configured your AD FS farm and Azure AD trust by using Azure AD Connect, you can use Azure AD Connect toodetect if you need tootake any action for your token signing certificates.</span></span> <span data-ttu-id="c75d0-214">Toorenew hello 인증서 해야 할 경우 Azure AD Connect toodo를 지금 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-214">If you need toorenew hello certificates, you can use Azure AD Connect toodo so.</span></span>

<span data-ttu-id="c75d0-215">자세한 내용은 참조 [hello 신뢰 복구](active-directory-aadconnect-federation-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c75d0-215">For more information, see [Repairing hello trust](active-directory-aadconnect-federation-management.md).</span></span>
