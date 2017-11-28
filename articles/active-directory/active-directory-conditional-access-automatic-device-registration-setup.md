---
title: "Windows Azure Active directory 도메인에 가입 된 장치 aaaHow tooconfigure 자동 등록 | Microsoft Docs"
description: "설정 하면 도메인에 가입 된 Windows 장치 tooregister 자동으로 Azure Active Directory와 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="c308c-103">어떻게 tooconfigure 자동 등록의 Windows 도메인에 가입 된 장치의 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="c308c-103">How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="c308c-104">toouse [Azure Active Directory 장치 기반 조건부 액세스](active-directory-conditional-access-azure-portal.md), Azure Active Directory (Azure AD)에 컴퓨터를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-104">toouse [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c308c-105">Hello를 사용 하 여 조직에서 등록 된 장치 목록을 가져올 수 있습니다 [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet hello에 [Azure Active Directory PowerShell 모듈](/powershell/azure/install-msonlinev1?view=azureadps-2.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-105">You can get a list of registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="c308c-106">이 문서에서는 조직에서 Azure AD와 Windows 도메인에 가입 된 장치의 hello 자동 등록을 구성 하기 위한 hello 단계를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-106">This article provides you with hello steps for configuring hello automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="c308c-107">조건부 액세스에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="c308c-107">For more information about:</span></span>

- <span data-ttu-id="c308c-108">[Azure Active Directory 장치 기반 조건부 액세스](active-directory-conditional-access-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c308c-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="c308c-109">Hello 작업 공간 및 Azure AD에 등록할 때 향상 된 hello 환경에서 Windows 10 장치 참조 [hello 엔터프라이즈용 Windows 10: 업무에 장치 사용](active-directory-azureadjoin-windows10-devices-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-109">Windows 10 devices in hello workplace and hello enhanced experiences when registered with Azure AD, see [Windows 10 for hello enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="c308c-110">CSP의 Windows 10 Enterprise E3 참조 hello [CSP 개요에서 Windows 10 Enterprise E3](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-110">Windows 10 Enterprise E3 in CSP, see hello [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="c308c-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="c308c-111">Before you begin</span></span>

<span data-ttu-id="c308c-112">사용자 환경에서 Windows 도메인에 가입 된 장치의 hello 자동 등록을 구성을 시작 하기 전에 알아야 할 hello 지원 시나리오 및 hello 제약 조건에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-112">Before you start configuring hello automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="c308c-113">hello 설명의 tooimprove hello 가독성을이 항목에서는 다음 용어 hello 사용:</span><span class="sxs-lookup"><span data-stu-id="c308c-113">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="c308c-114">**Windows 현재 장치** -이 용어는 Windows 10 또는 Windows Server 2016을 실행 하는 toodomain에 가입 된 장치.</span><span class="sxs-lookup"><span data-stu-id="c308c-114">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="c308c-115">**Windows 하위 수준 장치** -이 용어는 tooall **지원** 실행 중인 Windows 10 및 아닌 Windows Server 2016 도메인에 가입 된 Windows 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-115">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="c308c-116">Windows 현재 장치</span><span class="sxs-lookup"><span data-stu-id="c308c-116">Windows current devices</span></span>

- <span data-ttu-id="c308c-117">Hello Windows 데스크톱 운영 체제를 실행 하는 장치에 대 한 Windows 10 Anniversary 업데이트 (버전 1607)를 사용 하 여 권장 이상.</span><span class="sxs-lookup"><span data-stu-id="c308c-117">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="c308c-118">현재 Windows 장치 등록 hello **은** 암호 해시 동기화 구성과 같은 페더레이션 되지 않은 환경에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-118">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="c308c-119">Windows 하위 수준 장치</span><span class="sxs-lookup"><span data-stu-id="c308c-119">Windows down-level devices</span></span>

- <span data-ttu-id="c308c-120">다음 하위 수준 장치 Windows hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-120">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="c308c-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="c308c-121">Windows 8.1</span></span>
    - <span data-ttu-id="c308c-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="c308c-122">Windows 7</span></span>
    - <span data-ttu-id="c308c-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c308c-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="c308c-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c308c-124">Windows Server 2012</span></span>
    - <span data-ttu-id="c308c-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="c308c-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="c308c-126">하위 수준 Windows 장치 등록 hello **은** 원활한 Single Sign On을 통해 페더레이션 되지 않은 환경에서 지원 [Azure Active Directory 원활한 Single Sign-on](https://aka.ms/hybrid/sso)합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-126">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="c308c-127">하위 수준 Windows 장치 등록 hello **않습니다** 로밍 프로필을 사용 하 여 장치에 대 한 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-127">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="c308c-128">프로필 또는 설정 로밍을 사용하는 경우 Windows 10을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="c308c-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="c308c-129">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c308c-129">Prerequisites</span></span>

<span data-ttu-id="c308c-130">Azure AD의 최신 버전이 실행 되 고 있는지 toomake 필요 hello 자동 등록 조직의 도메인에 가입 된 장치의 사용을 시작 하기 전에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-130">Before you start enabling hello auto-registration of domain-joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="c308c-131">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="c308c-131">Azure AD Connect:</span></span>

- <span data-ttu-id="c308c-132">온-프레미스 AD (Active Directory) 및 Azure AD에서 hello 장치 개체에 hello 컴퓨터 계정 간의 hello 연결을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-132">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="c308c-133">비즈니스용 Windows Hello 같은 기타 장치 관련 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="c308c-134">구성 단계</span><span class="sxs-lookup"><span data-stu-id="c308c-134">Configuration steps</span></span>

<span data-ttu-id="c308c-135">이 항목에는 모든 일반적인 구성 시나리오에 대 한 hello 필요한 단계 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-135">This topic includes hello required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="c308c-136">다음 테이블 tooget 시나리오에 필요한 hello 단계의 개요 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-136">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="c308c-137">단계</span><span class="sxs-lookup"><span data-stu-id="c308c-137">Steps</span></span>                                      | <span data-ttu-id="c308c-138">Windows 현재 및 암호 해시 동기화</span><span class="sxs-lookup"><span data-stu-id="c308c-138">Windows current and password hash sync</span></span> | <span data-ttu-id="c308c-139">Windows 현재 및 페더레이션</span><span class="sxs-lookup"><span data-stu-id="c308c-139">Windows current and federation</span></span> | <span data-ttu-id="c308c-140">Windows 하위 수준</span><span class="sxs-lookup"><span data-stu-id="c308c-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="c308c-141">1단계: 서비스 연결 지점 구성</span><span class="sxs-lookup"><span data-stu-id="c308c-141">Step 1: Configure service connection point</span></span> | ![확인][1]                            | ![확인][1]                    | ![확인][1]        |
| <span data-ttu-id="c308c-145">2단계: 클레임 발급 설정</span><span class="sxs-lookup"><span data-stu-id="c308c-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![확인][1]                    | ![확인][1]        |
| <span data-ttu-id="c308c-148">3단계: 비-Windows 10 장치 활성화</span><span class="sxs-lookup"><span data-stu-id="c308c-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![확인][1]        |
| <span data-ttu-id="c308c-150">4단계: 배포 및 롤아웃 제어</span><span class="sxs-lookup"><span data-stu-id="c308c-150">Step 4: Control deployment and rollout</span></span>     | ![확인][1]                            | ![확인][1]                    | ![확인][1]        |
| <span data-ttu-id="c308c-154">5단계: 등록된 장치 확인</span><span class="sxs-lookup"><span data-stu-id="c308c-154">Step 5: Verify registered devices</span></span>          | ![확인][1]                            | ![확인][1]                    | ![확인][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="c308c-158">1단계: 서비스 연결 지점 구성</span><span class="sxs-lookup"><span data-stu-id="c308c-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="c308c-159">hello 서비스 연결 지점 (SCP) 개체는 hello 등록 toodiscover Azure AD 테 넌 트 정보 중 장치에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-159">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="c308c-160">온-프레미스 Active Directory에서 AD (), hello 자동 등록의 도메인에 가입 된 장치에 대 한 hello SCP 개체 hello 컴퓨터 포리스트와의 hello 구성 명명 컨텍스트 부분에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-160">In your on-premises Active Directory (AD), hello SCP object for hello auto-registration of domain-joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="c308c-161">포리스트당 하나의 구성 명명 컨텍스트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="c308c-162">다중 포리스트 Active Directory 구성에서 서비스 연결 지점 hello 도메인에 가입 된 컴퓨터를 포함 하는 모든 포리스트에서 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-162">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="c308c-163">Hello를 사용할 수 있습니다 [ **Get ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello 구성 명명 컨텍스트 포리스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-163">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="c308c-164">Hello Active Directory 도메인 이름의 포리스트에 대 한 *fabrikam.com*, hello 구성 명명 컨텍스트가:</span><span class="sxs-lookup"><span data-stu-id="c308c-164">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="c308c-165">포리스트, 도메인에 가입 된 장치의 hello 자동 등록에 대 한 SCP hello 개체에 위치한:</span><span class="sxs-lookup"><span data-stu-id="c308c-165">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="c308c-166">Azure AD Connect, 배포 방법에 따라 hello SCP 개체 이미 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-166">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="c308c-167">Hello 개체의 hello 존재 여부를 확인 하 고 Windows PowerShell 스크립트 뒤 hello를 사용 하 여 hello 검색 값을 검색할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="c308c-167">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="c308c-168">hello **$scp 합니다. 키워드** 출력 예를 들어 hello Azure AD 테 넌 트 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-168">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="c308c-169">Hello 서비스 연결 지점 존재 하지 않는 경우 hello를 실행 하 여 만들 수 있습니다 `Initialize-ADSyncDomainJoinedComputerSync` Azure AD Connect 서버의 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c308c-169">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="c308c-170">엔터프라이즈 관리자 자격 증명이 필요한 toorun이이 cmdlet이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-170">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="c308c-171">hello cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c308c-171">hello cmdlet:</span></span>

- <span data-ttu-id="c308c-172">Hello Active Directory 포리스트에서 Azure AD Connect에 연결 된 hello 서비스 연결 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-172">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="c308c-173">Toospecify hello 해야 `AdConnectorAccount` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-173">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="c308c-174">Azure ad에서 커넥터 계정에 연결 하는 Active Directory로 구성 된 hello 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-174">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="c308c-175">hello 다음 스크립트 예를 보여 줍니다 hello cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-175">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="c308c-176">이 스크립트에서는 `$aadAdminCred = Get-Credential` tootype 사용자 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-176">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="c308c-177">Hello 사용자 계정 이름 (UPN) 형식에서 tooprovide hello 사용자 이름이 필요 (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="c308c-177">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="c308c-178">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c308c-178">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="c308c-179">도메인 컨트롤러에서 실행 되는 Active Directory 웹 서비스에 의존 하는 hello Active Directory PowerShell 모듈을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-179">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="c308c-180">Active Directory Web Services는 Windows Server 2008 R2 이상을 실행하는 도메인 컨트롤러에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="c308c-181">Hello을 통해서만 **MSOnline PowerShell 모듈 버전 1.1.166.0**합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-181">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="c308c-182">toodownload이이 단원에서는이 사용 하 여 [링크](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-182">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="c308c-183">Windows Server 2008 또는 이전 버전을 실행 하는 도메인 컨트롤러에 대 한 toocreate hello 서비스 연결 지점 아래 hello 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-183">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="c308c-184">다중 포리스트 구성에서 다음 스크립트 toocreate hello 서비스 연결 지점 컴퓨터 있는 각 포리스트에 hello를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-184">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="c308c-185">2단계: 클레임 발급 설정</span><span class="sxs-lookup"><span data-stu-id="c308c-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="c308c-186">페더레이션된 azure에서 AD 구성 장치 Active Directory Federation Services (AD FS)에 의존 하거나 타사 온-프레미스 페더레이션 서비스 tooauthenticate tooAzure AD 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="c308c-187">장치 tooget hello Azure Active Directory Device Registration Service (Azure DRS)를 사용 하는 액세스 토큰 tooregister를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-187">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="c308c-188">Windows 현재 장치 Windows 통합 인증 tooan 활성 WS-트러스트 (버전 1.3 또는 2005)에서 호스팅된 끝점 hello 온-프레미스 페더레이션 서비스를 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-188">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="c308c-189">AD FS를 사용하는 경우 **adfs/services/trust/13/windowstransport** 또는 **adfs/services/trust/2005/windowstransport**를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="c308c-190">Hello 웹 인증 프록시를 사용 하는 경우 또한 hello 프록시를 통해이 끝점이 게시 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-190">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="c308c-191">어떤 끝점이 모두에서 hello AD FS 관리 콘솔을 통해 사용 하도록 설정 되어 볼 수 있습니다 **서비스 > 끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-191">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="c308c-192">AD FS 온-프레미스 페더레이션 서비스로 없다면 Ws-trust 1.3 또는 2005 끝점 및 hello 메타 데이터 교환 파일 (MEX)을 통해 게시 된 이러한을 지원 하는지 프로그램 공급 업체 toomake의 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-192">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="c308c-193">hello 다음 클레임에에서 있는 장치 등록 toocomplete에 대 한 Azure DRS에서 수신 하는 hello 토큰.</span><span class="sxs-lookup"><span data-stu-id="c308c-193">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="c308c-194">Azure DRS는 다음 hello 컴퓨터 계정 온-프레미스와 Azure AD Connect tooassociate 새로 만든 hello 장치 개체에 사용 되는이 정보 중 일부와 Azure AD의 장치 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="c308c-195">확인 된 도메인 이름이 둘 이상 있는 경우 컴퓨터에 대 한 클레임을 따라 tooprovide hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-195">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="c308c-196">이미 ImmutableID 클레임 (예: 대체 로그인 ID)를 발급 하는 컴퓨터에 대 한 한 해당 클레임 tooprovide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="c308c-197">다음 섹션 hello,에서는 대 한 정보를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-197">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="c308c-198">각 클레임에 포함 해야 hello 값</span><span class="sxs-lookup"><span data-stu-id="c308c-198">hello values each claim should have</span></span>
- <span data-ttu-id="c308c-199">AD FS에서 정의의 형식</span><span class="sxs-lookup"><span data-stu-id="c308c-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="c308c-200">hello 정의 사용 하면 tooverify hello 값이 있는지 또는 toocreate 해야 하는 경우 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-200">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="c308c-201">온-프레미스 페더레이션 서버에 대 한 AD FS를 사용 하지 않는 경우 이러한 클레임이 해당 공급 업체의 지침 toocreate hello 적절 한 구성 tooissue 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="c308c-202">계정 유형 클레임 발급</span><span class="sxs-lookup"><span data-stu-id="c308c-202">Issue account type claim</span></span>

<span data-ttu-id="c308c-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-이 클레임의 값이 있어야 합니다. **DJ**, hello 장치는 도메인에 가입 된 컴퓨터를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="c308c-204">AD FS에서 다음과 같은 형식의 발급 변환 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="c308c-205">문제 objectGUID hello 컴퓨터 계정 온-프레미스의</span><span class="sxs-lookup"><span data-stu-id="c308c-205">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="c308c-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-이 클레임 hello 있어야 **objectGUID** hello 값 온-프레미스 컴퓨터 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="c308c-207">AD FS에서 다음과 같은 형식의 발급 변환 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="c308c-208">문제 objectSID hello 컴퓨터 계정 온-프레미스의</span><span class="sxs-lookup"><span data-stu-id="c308c-208">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="c308c-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-이 클레임 hello hello 있어야 **objectSid** hello 값 온-프레미스 컴퓨터 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="c308c-210">AD FS에서 다음과 같은 형식의 발급 변환 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="c308c-211">Azure AD에 확인된 도메인 이름이 여러 개 있는 경우 컴퓨터에 대한 issuerID 발급</span><span class="sxs-lookup"><span data-stu-id="c308c-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="c308c-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-이 클레임 식별자 URI (Uniform Resource) hello 중 아무 메서드나 확인할 도메인 이름을 hello로 연결 하는 온-프레미스 페더레이션 서비스 (AD FS 또는 타사) hello 토큰을 발급 하는 hello를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="c308c-213">AD FS에서 hello는 스토리 아래 후 특정 순서 hello는 스토리 위의 한다는 점에서 처럼 보이지만 발급 변환 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-213">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="c308c-214">사용자가 필요한 하나의 규칙 tooexplicitly 문제 hello 규칙을 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c308c-214">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="c308c-215">아래의 hello 규칙에서 식별 되는 사용자 컴퓨터 인증에 대 한 첫 번째 규칙 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-215">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with hello value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


<span data-ttu-id="c308c-216">위의 hello 클레임에</span><span class="sxs-lookup"><span data-stu-id="c308c-216">In hello claim above,</span></span>

- <span data-ttu-id="c308c-217">`$<domain>`hello AD FS 서비스 URL</span><span class="sxs-lookup"><span data-stu-id="c308c-217">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="c308c-218">`<verified-domain-name>`Azure AD에서 확인 된 도메인 이름 중 하나를 통해 tooreplace 필요한 자리 표시자</span><span class="sxs-lookup"><span data-stu-id="c308c-218">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="c308c-219">확인 된 도메인 이름에 대 한 자세한 내용은 참조 하십시오. [추가 사용자 지정 도메인 이름을 tooAzure Active Directory](active-directory-add-domain.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-219">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="c308c-220">확인 된 회사 도메인 목록을 tooget hello를 사용할 수 있습니다 [Get-msoldomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c308c-220">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="c308c-222">사용자에 대한 ID가 있는 경우(예: 대체 로그인 ID가 설정된 경우) 컴퓨터에 대한 ImmutableID 발급</span><span class="sxs-lookup"><span data-stu-id="c308c-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="c308c-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - 이 클레임은 컴퓨터에 대한 유효한 값을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="c308c-224">AD FS에서 다음과 같은 발급 변환 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="c308c-225">도우미 스크립트 toocreate hello AD FS 발급 변환 규칙</span><span class="sxs-lookup"><span data-stu-id="c308c-225">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="c308c-226">hello 다음 스크립트를 사용 하면 hello 작성 hello 발급 변환 규칙 위에서 설명한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-226">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a><span data-ttu-id="c308c-227">설명</span><span class="sxs-lookup"><span data-stu-id="c308c-227">Remarks</span></span> 

- <span data-ttu-id="c308c-228">이 스크립트는 hello 규칙 toohello 기존 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-228">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="c308c-229">Hello 스크립트를 실행 하지 마십시오 두 번 hello 규칙의 설정 때문에 두 번 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-229">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="c308c-230">Hello 스크립트를 다시 실행 하기 전에 이러한 클레임 (조건 하에서 hello 해당)에 대 한 해당 규칙이 존재 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-230">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="c308c-231">여러 확인 된 도메인 이름 (같이 hello Azure AD 포털 또는 hello MsolDomains Get cmdlet을 통해)의 hello 값을 설정할 수 있으면 **$multipleVerifiedDomainNames** 너무 hello 스크립트**$true**합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-231">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="c308c-232">또한 Azure AD Connect 또는 다른 방법을 통해 만들어졌을 수 있는 기존 issuerid 클레임을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="c308c-233">다음은 이 규칙에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="c308c-234">이미 실행 한 경우에 **ImmutableID** 사용자 계정에 대 한 클레임 값으로 설정 hello의 **$immutableIDAlreadyIssuedforUsers** 너무 hello 스크립트**$true**합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-234">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="c308c-235">3단계: Windows 하위 수준 장치 설정</span><span class="sxs-lookup"><span data-stu-id="c308c-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="c308c-236">도메인에 가입된 장치 중 일부가 Windows 하위 수준 장치인 경우 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="c308c-237">사용자가 tooregister 장치에서 Azure AD tooenable 정책을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-237">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="c308c-238">온-프레미스 페더레이션 서비스 tooissue 클레임 toosupport 구성 **통합 IWA (Windows 인증)** 장치 등록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-238">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="c308c-239">Hello Azure AD 장치 인증 끝점 toohello 로컬 인트라넷 영역 tooavoid 인증서 hello 장치를 인증할 때 메시지 표시를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-239">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="c308c-240">사용자 tooregister 장치에서 Azure AD tooenable 정책을 설정합니다</span><span class="sxs-lookup"><span data-stu-id="c308c-240">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="c308c-241">tooregister Windows 하위 수준 장치를 Azure AD에서 tooallow 사용자 tooregister 장치를 설정 하는 hello 설정 되어 있는지 toomake를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-241">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="c308c-242">Hello Azure 포털에서에서이 설정을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-242">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="c308c-243">hello 다음 정책을 설정 해야 너무**모든**: **Azure ad 사용자가 장치를 등록할 수 있습니다**</span><span class="sxs-lookup"><span data-stu-id="c308c-243">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![장치 등록](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="c308c-245">온-프레미스 페더레이션 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="c308c-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="c308c-246">온-프레미스 페더레이션 서비스에서 발급 hello를 지원 해야 **authenticationmehod** 및 **wiaormultiauthn** 클레임 인증을 받을 때 요청 보유 toohello Azure AD 신뢰 당사자는 resouce_params 매개 변수 표시 된 대로 인코딩된 값 아래:</span><span class="sxs-lookup"><span data-stu-id="c308c-246">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="c308c-247">이러한 요청 되 면 hello 온-프레미스 페더레이션 서비스에서 Windows 통합 인증을 사용 하 여 hello 사용자를 인증 해야 하 고 요청이 성공 하면 다음 두 개의 클레임 hello를 실행 해야 하기:</span><span class="sxs-lookup"><span data-stu-id="c308c-247">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="c308c-248">AD FS에서 발급 변환 규칙을 통해 전달 hello 해당 인증 방법을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-248">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="c308c-249">**tooadd이이 규칙:**</span><span class="sxs-lookup"><span data-stu-id="c308c-249">**tooadd this rule:**</span></span>

1. <span data-ttu-id="c308c-250">Hello AD FS 관리 콘솔에서 이동 너무`AD FS > Trust Relationships > Relying Party Trusts`합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-250">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="c308c-251">Hello Microsoft Office 365 Id 플랫폼 신뢰 당사자 트러스트 개체를 마우스 오른쪽 단추로 클릭 한 다음 선택 **클레임 규칙 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-251">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="c308c-252">Hello에 **발급 변환 규칙** 탭에서 **규칙 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-252">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="c308c-253">Hello에 **클레임 규칙** 템플릿 목록 **사용자 지정 규칙을 사용 하 여 클레임 보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-253">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="c308c-254">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-254">Select **Next**.</span></span>
6. <span data-ttu-id="c308c-255">Hello에 **클레임 규칙 이름** 상자에서 입력 **인증 방법 클레임 규칙**합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-255">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="c308c-256">Hello에 **클레임 규칙** 상자, 규칙을 따르는 형식 hello:</span><span class="sxs-lookup"><span data-stu-id="c308c-256">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="c308c-257">페더레이션 서버에서 아래의 PowerShell 명령 hello 대체 한 다음 입력 ** \<RPObjectName\> ** 하면 Azure AD 신뢰 당사자 트러스트 개체에 대 한 hello 신뢰 당사자 개체 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-257">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="c308c-258">일반적으로 이 개체의 이름은 **Microsoft Office 365 ID 플랫폼**입니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="c308c-259">Hello Azure AD 장치 인증 끝점 toohello 로컬 인트라넷 영역 추가</span><span class="sxs-lookup"><span data-stu-id="c308c-259">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="c308c-260">tooavoid 인증서 레지스터 장치의 사용자가 Internet Explorer에서 URL toohello 로컬 인트라넷 영역에 따라 정책 tooyour 도메인에 가입 된 장치 tooadd hello 푸시할 수 있는 AD tooAzure 인증할 때 다음 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-260">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="c308c-261">4단계: 배포 및 롤아웃 제어</span><span class="sxs-lookup"><span data-stu-id="c308c-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="c308c-262">Hello 필요한 단계를 완료 한 도메인에 가입 된 장치를 Azure AD와 준비 tooautomatically 레지스터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-262">When you have completed hello required steps, domain-joined devices are ready tooautomatically register with Azure AD.</span></span> <span data-ttu-id="c308c-263">Windows 10 1주년 업데이트 및 Windows Server 2016을 실행하는 모든 도메인에 가입된 장치는 장치를 다시 시작하거나 사용자가 로그인할 때 자동으로 Azure AD에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="c308c-264">새 장치 hello 장치 다시 시작할 때 hello 도메인 가입 작업이 완료 된 후 Azure AD에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-264">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

<span data-ttu-id="c308c-265">그러나 된 장치에 (예를 들어 Intune에 대 한) 이전에 작업 공간 가입 tooAzure AD 전환 너무"*도메인에 가입 된, 등록 된 AAD*"toohello 보통 인해 모든 장치에서이 프로세스 toocomplete에 대 한 시간이 걸립니다; 도메인 및 사용자 활동의 흐름입니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-265">Devices that were previously workplace-joined tooAzure AD (for example for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="c308c-266">설명</span><span class="sxs-lookup"><span data-stu-id="c308c-266">Remarks</span></span>

- <span data-ttu-id="c308c-267">Windows 10 및 Windows Server 2016 도메인에 가입 된 컴퓨터의 자동 등록의 그룹 정책 개체 toocontrol hello 출시를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-267">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="c308c-268">Windows 10 2015 년 11 월 업데이트 자동으로 레지스터 Azure AD와 **만** hello 롤아웃 그룹 정책 개체를 설정 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="c308c-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="c308c-269">배포할 수 있습니다 Windows 하위 수준 컴퓨터의 toorollout hello의 자동 등록을 한 [Windows Installer 패키지](#windows-installer-packages-for-non-windows-10-computers) 선택한 toocomputers 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-269">toorollout hello automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="c308c-270">Hello 그룹 정책 개체 tooWindows 8.1 도메인 가입 장치를 푸시 등록 하려고 시도 합니다. 그러나 것이 좋습니다 hello를 사용 하는 [Windows Installer 패키지](#windows-installer-packages-for-non-windows-10-computers) tooregister 모든 Windows 하위 수준 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-270">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) tooregister all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="c308c-271">그룹 정책 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="c308c-271">Create a Group Policy object</span></span> 

<span data-ttu-id="c308c-272">Windows 현재 컴퓨터의 자동 등록의 toocontrol hello 롤아웃, hello를 배포 해야 **장치로 도메인에 가입 된 컴퓨터를 등록할** tooregister 원하는 그룹 정책 개체 toohello 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-272">toocontrol hello rollout of automatic registration of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="c308c-273">예를 들어 hello 정책 tooan 조직 구성 단위 또는 tooa 보안 그룹을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-273">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="c308c-274">**tooset hello 정책:**</span><span class="sxs-lookup"><span data-stu-id="c308c-274">**tooset hello policy:**</span></span>

1. <span data-ttu-id="c308c-275">열기 **서버 관리자**, 한 다음 너무 이동`Tools > Group Policy Management`합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-275">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="c308c-276">Toohello 도메인 Windows 현재 컴퓨터의 tooactivate 자동 등록 하려는 해당 하는 toohello 도메인 노드로 이동 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c308c-276">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="c308c-277">**그룹 정책 개체**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="c308c-278">그룹 정책 개체의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="c308c-279">예를 들어 *AD 자동 등록 tooAzure*합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-279">For example, *Automatic Registration tooAzure AD*.</span></span> <span data-ttu-id="c308c-280">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-280">Select **OK**.</span></span>
5. <span data-ttu-id="c308c-281">마우스 오른쪽 단추로 새 그룹 정책 개체를 클릭한 다음 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="c308c-282">너무 이동**컴퓨터 구성** > **정책** > **관리 템플릿** > **Windows 구성 요소** > **장치 등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-282">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="c308c-283">마우스 오른쪽 단추로 **도메인 가입 컴퓨터를 장치로 등록**을 클릭한 다음 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c308c-284">이전 버전의 hello 그룹 정책 관리 콘솔에서이 그룹 정책 템플릿 이름이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-284">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="c308c-285">이전 버전의 hello 콘솔을 사용 하는 경우 너무 이동`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-285">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="c308c-286">**사용**, **적용**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="c308c-287">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-287">Select **OK**.</span></span>
9. <span data-ttu-id="c308c-288">링크 hello 그룹 정책 개체 tooa 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-288">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="c308c-289">예를 들어 특정 조직 단위의 tooa 것 것을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-289">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="c308c-290">또한 연결할 수 있습니다이 자동으로 Azure AD에 등록 하는 컴퓨터의 tooa 특정 보안 그룹.</span><span class="sxs-lookup"><span data-stu-id="c308c-290">You also could link it tooa specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="c308c-291">tooset 도메인에 가입 된 Windows 10 및 Windows Server 2016의에서 모든 컴퓨터 조직 링크 hello 그룹 정책 개체 toohello 도메인에 대해이 정책을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-291">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="c308c-292">비 Windows 10 컴퓨터용 Windows Installer 패키지</span><span class="sxs-lookup"><span data-stu-id="c308c-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="c308c-293">tooregister 도메인에 가입 된 Windows 하위 수준 컴퓨터 연결된 된 환경에서 다운로드 하 고 수 hello에이 Windows Installer 패키지 (.msi) 다운로드 센터에서 설치 [비-Windows10컴퓨터에대한Microsoft작업공간연결](https://www.microsoft.com/en-us/download/details.aspx?id=53554) 페이지.</span><span class="sxs-lookup"><span data-stu-id="c308c-293">tooregister domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="c308c-294">System Center Configuration Manager 같은 소프트웨어 배포 시스템을 사용 하 여 hello 패키지를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-294">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="c308c-295">hello 패키지 hello 표준 자동 설치 옵션이 지원 hello로 *quiet* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-295">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="c308c-296">System Center Configuration Manager 현재 분기는 hello 기능 완료 tootrack 등록과 같은 이전 버전의 추가 혜택을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="c308c-297">자세한 내용은 [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c308c-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="c308c-298">hello installer hello 사용자의 컨텍스트에서 실행 하는 hello 시스템에서 예약 된 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-298">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="c308c-299">hello 작업 hello 사용자 tooWindows에 로그인 할 때 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-299">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="c308c-300">hello 작업은 자동으로 Windows 통합 인증을 사용 하 여 인증 한 후 hello 사용자 자격 증명으로 Azure AD와 hello 장치를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-300">hello task silently registers hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="c308c-301">hello 장치에 toosee hello 예약 된 작업, 너무 이동**Microsoft** > **작업 공간 연결**, toohello 작업 스케줄러 라이브러리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-301">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="c308c-302">5단계: 등록된 장치 확인</span><span class="sxs-lookup"><span data-stu-id="c308c-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="c308c-303">Hello를 사용 하 여 조직에서 성공적으로 등록 된 장치를 확인할 수 있습니다 [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet hello에 [Azure Active Directory PowerShell 모듈](/powershell/azure/install-msonlinev1?view=azureadps-2.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-303">You can check successful registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="c308c-304">이 cmdlet의 출력 hello Azure AD에 등록 된 장치를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-304">hello output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="c308c-305">tooget hello를 사용 하는 모든 장치 **-모든** 매개 변수 및 필터 hello를 통해 **deviceTrustType** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-305">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="c308c-306">도메인에 가입된 장치는 **도메인 가입** 값을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="c308c-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c308c-307">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c308c-307">Next steps</span></span>

* [<span data-ttu-id="c308c-308">자동 장치 등록 FAQ</span><span class="sxs-lookup"><span data-stu-id="c308c-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="c308c-309">가입 된 컴퓨터 tooAzure AD – Windows 10 및 Windows Server 2016 도메인의 자동 등록 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c308c-309">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="c308c-310">가입 된 컴퓨터 tooAzure AD – 비-Windows 10 도메인의 자동 등록 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c308c-310">Troubleshooting auto-registration of domain joined computers tooAzure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="c308c-311">Azure Active Directory 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="c308c-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
