---
title: "하이브리드 Azure Active Directory 가입 장치 구성 방법 | Microsoft Docs"
description: "하이브리드 Azure Active Directory 가입 장치를 구성하는 방법에 대해 알아봅니다."
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
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 4580075df9fce74664b22aa24065ba1885692384
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-hybrid-azure-active-directory-joined-devices"></a><span data-ttu-id="06d3f-103">하이브리드 Azure Active Directory 가입 장치를 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="06d3f-103">How to configure hybrid Azure Active Directory joined devices</span></span>

<span data-ttu-id="06d3f-104">Azure AD(Active Directory)의 장치 관리를 사용하면 보안 및 규정 준수에 대한 표준을 충족하는 장치에서 사용자 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-104">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> <span data-ttu-id="06d3f-105">자세한 내용은 [Azure Active Directory의 장치 관리 소개](device-management-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06d3f-105">For more details, see [Introduction to device management in Azure Active Directory](device-management-introduction.md).</span></span>

<span data-ttu-id="06d3f-106">온-프레미스 Active Directory 환경을 사용하고, Azure AD에 도메인 가입 장치를 연결하려는 경우 하이브리드 Azure AD 가입 장치를 구성하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-106">If you have an on-premises Active Directory environment and you want to join your domain-joined devices to Azure AD, you can accomplish this by configuring hybrid Azure AD joined devices.</span></span> <span data-ttu-id="06d3f-107">토픽은 관련된 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-107">The topic provides you with the related steps.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="06d3f-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="06d3f-108">Before you begin</span></span>

<span data-ttu-id="06d3f-109">환경에서 하이브리드 Azure AD 가입 장치 구성을 시작하기 전에 지원되는 시나리오와 제약 조건을 숙지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-109">Before you start configuring hybrid Azure AD joined devices in your environment, you should familiarize yourself with the supported scenarios and the constraints.</span></span>  

<span data-ttu-id="06d3f-110">설명의 가독성을 높이기 위해 이 토픽에서는 다음 용어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-110">To improve the readability of the descriptions, this topic uses the following term:</span></span> 

- <span data-ttu-id="06d3f-111">**Windows 현재 장치** - 이 용어는 Windows 10 또는 Windows Server 2016을 실행하는 도메인에 가입 된 장치를 말합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-111">**Windows current devices** - This term refers to domain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="06d3f-112">**Windows 하위 수준 장치** - 이 용어는 Windows 10과 Windows Server 2016 중 어떤 것도 실행하지 않는 **지원되는** 도메인에 가입된 Windows 장치를 말합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-112">**Windows down-level devices** - This term refers to all **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="06d3f-113">Windows 현재 장치</span><span class="sxs-lookup"><span data-stu-id="06d3f-113">Windows current devices</span></span>

- <span data-ttu-id="06d3f-114">Windows 데스크톱 운영 체제를 실행하는 장치의 경우 Windows 10주년 업데이트(버전 1607) 이상을 사용할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-114">For devices running the Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="06d3f-115">Windows 현재 장치의 등록은 암호 해시 동기화 구성처럼 페더레이션되지 않은 환경에서 **지원됩니다**.</span><span class="sxs-lookup"><span data-stu-id="06d3f-115">The registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="06d3f-116">Windows 하위 수준 장치</span><span class="sxs-lookup"><span data-stu-id="06d3f-116">Windows down-level devices</span></span>

- <span data-ttu-id="06d3f-117">다음은 지원되는 Windows 하위 수준 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-117">The following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="06d3f-118">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="06d3f-118">Windows 8.1</span></span>
    - <span data-ttu-id="06d3f-119">Windows 7</span><span class="sxs-lookup"><span data-stu-id="06d3f-119">Windows 7</span></span>
    - <span data-ttu-id="06d3f-120">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="06d3f-120">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="06d3f-121">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="06d3f-121">Windows Server 2012</span></span>
    - <span data-ttu-id="06d3f-122">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="06d3f-122">Windows Server 2008 R2</span></span>
- <span data-ttu-id="06d3f-123">Windows 하위 수준 장치 등록은 원활한 Single Sign-On([Azure Active Directory 원활한 Single Sign-On](https://aka.ms/hybrid/sso))을 통해 페더레이션되지 않은 환경에서 **지원됩니다**.</span><span class="sxs-lookup"><span data-stu-id="06d3f-123">The registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="06d3f-124">로밍 프로필을 사용하는 장치에 대해서는 Windows 하위 수준 장치 등록이 지원되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="06d3f-124">The registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="06d3f-125">프로필 또는 설정 로밍을 사용하는 경우 Windows 10을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="06d3f-125">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="06d3f-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="06d3f-126">Prerequisites</span></span>

<span data-ttu-id="06d3f-127">조직에서 하이브리드 Azure AD 가입 장치를 사용하도록 설정하기 전에 최신 버전의 Azure AD 연결을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-127">Before you start enabling hybrid Azure AD joined devices in your organization, you need to make sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="06d3f-128">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="06d3f-128">Azure AD Connect:</span></span>

- <span data-ttu-id="06d3f-129">온-프레미스 AD(Active Directory)의 컴퓨터 계정과 Azure AD의 장치 개체 간 연결을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-129">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span></span> 
- <span data-ttu-id="06d3f-130">비즈니스용 Windows Hello 같은 기타 장치 관련 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-130">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="06d3f-131">구성 단계</span><span class="sxs-lookup"><span data-stu-id="06d3f-131">Configuration steps</span></span>

<span data-ttu-id="06d3f-132">다양한 형식의 Windows 장치 플랫폼에 대한 하이브리드 Azure AD 가입 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-132">You can configure hybrid Azure AD joined devices for various types of Windows device platforms.</span></span> <span data-ttu-id="06d3f-133">이 토픽에는 모든 일반 구성 시나리오에 필요한 단계가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-133">This topic includes the required steps for all typical configuration scenarios.</span></span>  

<span data-ttu-id="06d3f-134">다음 테이블을 사용하여 본인의 시나리오에 필요한 단계의 개요를 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="06d3f-134">Use the following table to get an overview of the steps that are required for your scenario:</span></span>  



| <span data-ttu-id="06d3f-135">단계</span><span class="sxs-lookup"><span data-stu-id="06d3f-135">Steps</span></span>                                      | <span data-ttu-id="06d3f-136">Windows 현재 및 암호 해시 동기화</span><span class="sxs-lookup"><span data-stu-id="06d3f-136">Windows current and password hash sync</span></span> | <span data-ttu-id="06d3f-137">Windows 현재 및 페더레이션</span><span class="sxs-lookup"><span data-stu-id="06d3f-137">Windows current and federation</span></span> | <span data-ttu-id="06d3f-138">Windows 하위 수준</span><span class="sxs-lookup"><span data-stu-id="06d3f-138">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="06d3f-139">1단계: 서비스 연결 지점 구성</span><span class="sxs-lookup"><span data-stu-id="06d3f-139">Step 1: Configure service connection point</span></span> | ![확인][1]                            | ![확인][1]                    | ![확인][1]        |
| <span data-ttu-id="06d3f-143">2단계: 클레임 발급 설정</span><span class="sxs-lookup"><span data-stu-id="06d3f-143">Step 2: Setup issuance of claims</span></span>           |                                        | ![확인][1]                    | ![확인][1]        |
| <span data-ttu-id="06d3f-146">3단계: 비-Windows 10 장치 활성화</span><span class="sxs-lookup"><span data-stu-id="06d3f-146">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![확인][1]        |
| <span data-ttu-id="06d3f-148">4단계: 배포 및 롤아웃 제어</span><span class="sxs-lookup"><span data-stu-id="06d3f-148">Step 4: Control deployment and rollout</span></span>     | ![확인][1]                            | ![확인][1]                    | ![확인][1]        |
| <span data-ttu-id="06d3f-152">5단계: 가입 장치 확인</span><span class="sxs-lookup"><span data-stu-id="06d3f-152">Step 5: Verify joined devices</span></span>          | ![확인][1]                            | ![확인][1]                    | ![확인][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="06d3f-156">1단계: 서비스 연결 지점 구성</span><span class="sxs-lookup"><span data-stu-id="06d3f-156">Step 1: Configure service connection point</span></span>

<span data-ttu-id="06d3f-157">SCP(서비스 연결 지점) 개체는 등록 중에 장치가 Azure AD 테넌트 정보를 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-157">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span></span> <span data-ttu-id="06d3f-158">온-프레미스 AD(Active Directory)에서, 하이브리드 Azure AD 가입 장치에 대한 SCP 개체는 컴퓨터 포리스트의 구성 명명 컨텍스트 파티션에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-158">In your on-premises Active Directory (AD), the SCP object for the hybrid Azure AD joined devices must exist in the configuration naming context partition of the computer's forest.</span></span> <span data-ttu-id="06d3f-159">포리스트당 하나의 구성 명명 컨텍스트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-159">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="06d3f-160">다중 포리스트 Active Directory 구성에서는 도메인에 가입된 컴퓨터를 포함하고 있는 모든 포리스트에 서비스 연결점이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-160">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="06d3f-161">[**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet을 사용하여 포리스트의 구성 명명 컨텍스트를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-161">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span></span>  

<span data-ttu-id="06d3f-162">Active Directory 도메인 이름이 *fabrikam.com*인 포리스트의 경우 구성 명명 컨텍스트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-162">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="06d3f-163">포리스트에서 도메인에 가입된 장치의 자동 등록을 위한 SCP 개체는 다음 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-163">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="06d3f-164">Azure AD Connect를 배포한 방법에 따라 SCP 개체가 이미 구성되었을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-164">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span></span>
<span data-ttu-id="06d3f-165">다음 Windows PowerShell 스크립트를 사용하여 개체의 존재를 확인하고 검색 값을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-165">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="06d3f-166">**$scp.Keywords** 출력은 Azure AD 테넌트 정보를 보여줍니다. 예:</span><span class="sxs-lookup"><span data-stu-id="06d3f-166">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="06d3f-167">서비스 연결 지점이 없는 경우 Azure AD Connect 서버에서 `Initialize-ADSyncDomainJoinedComputerSync` cmdlet을 실행하여 서비스 연결 지점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-167">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="06d3f-168">이 cmdlet을 실행하려면 엔터프라이즈 관리자 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-168">Enterprise admin credential is required to run this cmdlet.</span></span>  
<span data-ttu-id="06d3f-169">cmdlet:</span><span class="sxs-lookup"><span data-stu-id="06d3f-169">The cmdlet:</span></span>

- <span data-ttu-id="06d3f-170">Azure AD Connect가 연결된 Active Directory 포리스트에 서비스 연결 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-170">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="06d3f-171">`AdConnectorAccount` 매개 변수를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-171">Requires you to specify the `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="06d3f-172">Azure AD Connect에서 Active Directory 커넥터 계정으로 구성되는 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-172">This is the account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="06d3f-173">다음 스크립트는 cmdlet 사용에 대한 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-173">The following script shows an example for using the cmdlet.</span></span> <span data-ttu-id="06d3f-174">이 스크립트에서 `$aadAdminCred = Get-Credential`에는 사용자 이름을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-174">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span></span> <span data-ttu-id="06d3f-175">UPN(사용자 계정 이름) 형식(`user@example.com`)에 사용자 이름을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-175">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="06d3f-176">`Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="06d3f-176">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="06d3f-177">Active Directory PowerShell 모듈을 사용합니다. 이 모듈은 도메인 컨트롤러에서 실행되는 Active Directory Web Services를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-177">Uses the Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="06d3f-178">Active Directory Web Services는 Windows Server 2008 R2 이상을 실행하는 도메인 컨트롤러에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-178">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="06d3f-179">**MSOnline PowerShell 모듈 버전 1.1.166.0**에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-179">Is only supported by the **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="06d3f-180">이 모듈을 다운로드하려면 이 [링크](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-180">To download this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="06d3f-181">Windows Server 2008 이전 버전을 실행하는 도메인 컨트롤러의 경우 아래 스크립트를 사용하여 서비스 연결 지점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-181">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span></span>

<span data-ttu-id="06d3f-182">다중 포리스트 구성에서는 다음 스크립트를 사용하여 컴퓨터가 있는 각 포리스트에 서비스 연결 지점을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-182">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="06d3f-183">2단계: 클레임 발급 설정</span><span class="sxs-lookup"><span data-stu-id="06d3f-183">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="06d3f-184">페더레이션된 Azure AD 구성에서는 장치가 AD FS(Active Directory Federation Services) 또는 타사 온-프레미스 페더레이션 서비스를 사용하여 Azure AD를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-184">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span></span> <span data-ttu-id="06d3f-185">장치는 인증을 통해 Azure DRS(Azure Active Directory Device Registration Service)에 등록하는 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-185">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="06d3f-186">Windows 현재 장치는 Windows 통합 인증을 사용하여 온-프레미스 페더레이션 서비스에서 호스트하는 활성 WS-Trust 끝점(1.3 또는 2005 버전)에 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-186">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="06d3f-187">AD FS를 사용하는 경우 **adfs/services/trust/13/windowstransport** 또는 **adfs/services/trust/2005/windowstransport**를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-187">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="06d3f-188">또한 웹 인증 프록시를 사용하는 경우 이 끝점이 프록시를 통해 게시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-188">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span></span> <span data-ttu-id="06d3f-189">**서비스 > 끝점**에서 AD FS 관리 콘솔을 통해 어떤 끝점이 사용하도록 설정되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-189">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="06d3f-190">온-프레미스 페더레이션 서비스로 사용되는 AD FS가 없으면 공급업체의 지침에 따라 없다면 WS-Trust 1.3 또는 2005 버전이 지원되는지 확인하고 메타데이터 교환 파일(MEX)을 통해 게시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-190">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="06d3f-191">Azure DRS가 수신한 토큰에 다음 클레임이 있어야 장치 등록이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-191">The following claims must exist in the token received by Azure DRS for device registration to complete.</span></span> <span data-ttu-id="06d3f-192">Azure DRS는 이 정보 중 일부를 사용하여 Azure AD에 장치 개체를 만듭니다. 장치 개체는 Azure AD Connect가 새로 만들어진 장치 개체를 컴퓨터 계정 온-프레미스와 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-192">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="06d3f-193">확인된 도메인 이름이 두 개 이상인 경우 컴퓨터에 대한 다음 클레임을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-193">If you have more than one verified domain name, you need to provide the following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="06d3f-194">ImmutableID 클레임(예: 대체 로그인 ID)을 이미 발급 중인 경우 컴퓨터에 대한 해당 클레임 하나를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-194">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="06d3f-195">다음 섹션에서는 다음 항목에 대한 정보를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-195">In the following sections, you find information about:</span></span>
 
- <span data-ttu-id="06d3f-196">각 클레임에 필요한 값</span><span class="sxs-lookup"><span data-stu-id="06d3f-196">The values each claim should have</span></span>
- <span data-ttu-id="06d3f-197">AD FS에서 정의의 형식</span><span class="sxs-lookup"><span data-stu-id="06d3f-197">How a definition would look like in AD FS</span></span>

<span data-ttu-id="06d3f-198">정의는 값의 존재 여부 또는 값을 만들어야 하는지 여부를 확인하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-198">The definition helps you to verify whether the values are present or if you need to create them.</span></span>

> [!NOTE]
> <span data-ttu-id="06d3f-199">온-프레미스 페더레이션 서버에 사용되는 AD FS가 없는 경우 공급업체의 지침에 따라 이러한 클레임을 발급하는 적절한 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-199">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="06d3f-200">계정 유형 클레임 발급</span><span class="sxs-lookup"><span data-stu-id="06d3f-200">Issue account type claim</span></span>

<span data-ttu-id="06d3f-201">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - 이 클레임은 도메인에 가입된 컴퓨터로 장치를 식별하는 **DJ** 값을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-201">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span></span> <span data-ttu-id="06d3f-202">AD FS에서 다음과 같은 형식의 발급 변환 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-202">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-the-computer-account-on-premises"></a><span data-ttu-id="06d3f-203">컴퓨터 계정 온-프레미스의 objectGUID 발급</span><span class="sxs-lookup"><span data-stu-id="06d3f-203">Issue objectGUID of the computer account on-premises</span></span>

<span data-ttu-id="06d3f-204">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - 이 클레임은 온-프레미스 컴퓨터 계정의 **objectGUID** 값을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-204">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span></span> <span data-ttu-id="06d3f-205">AD FS에서 다음과 같은 형식의 발급 변환 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-205">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-the-computer-account-on-premises"></a><span data-ttu-id="06d3f-206">컴퓨터 계정 온-프레미스의 objectSID 발급</span><span class="sxs-lookup"><span data-stu-id="06d3f-206">Issue objectSID of the computer account on-premises</span></span>

<span data-ttu-id="06d3f-207">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - 이 클레임은 온-프레미스 컴퓨터 계정의 **objectSid** 값을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-207">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the the **objectSid** value of the on-premises computer account.</span></span> <span data-ttu-id="06d3f-208">AD FS에서 다음과 같은 형식의 발급 변환 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-208">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="06d3f-209">Azure AD에 확인된 도메인 이름이 여러 개 있는 경우 컴퓨터에 대한 issuerID 발급</span><span class="sxs-lookup"><span data-stu-id="06d3f-209">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="06d3f-210">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - 이 클레임의 식별자는 토큰을 발급하는 온-프레미스 페더레이션 서비스(AD FS 또는 타사)와 연결하는 확인된 도메인 이름의 URI(Uniform Resource Identifier)를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-210">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span></span> <span data-ttu-id="06d3f-211">AD FS에서 위와 같은 발급 변환 규칙을 추가한 후 아래와 같은 발급 변환 규칙을 그 순서대로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-211">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span></span> <span data-ttu-id="06d3f-212">사용자에 대한 규칙을 명시적으로 발급하는 규칙 하나가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-212">Please note that one rule to explicitly issue the rule for users is necessary.</span></span> <span data-ttu-id="06d3f-213">아래 규칙에서 사용자 및 컴퓨터 인증을 식별하는 첫 번째 규칙이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-213">In the rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with the value User when its not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
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


<span data-ttu-id="06d3f-214">위의 클레임에서</span><span class="sxs-lookup"><span data-stu-id="06d3f-214">In the claim above,</span></span>

- <span data-ttu-id="06d3f-215">`$<domain>`은 AD FS 서비스 URL</span><span class="sxs-lookup"><span data-stu-id="06d3f-215">`$<domain>` is the AD FS service URL</span></span>
- <span data-ttu-id="06d3f-216">`<verified-domain-name>`은 Azure AD에서 확인된 도메인 이름 중 하나로 교체해야 하는 자리 표시자</span><span class="sxs-lookup"><span data-stu-id="06d3f-216">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="06d3f-217">확인된 도메인 이름에 대한 자세한 내용은 [Azure Active Directory에 사용자 지정 도메인 이름 추가](active-directory-add-domain.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06d3f-217">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="06d3f-218">확인된 회사 도메인 목록을 보려면 the [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-218">To get a list of your verified company domains, you can use the [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="06d3f-220">사용자에 대한 ID가 있는 경우(예: 대체 로그인 ID가 설정된 경우) 컴퓨터에 대한 ImmutableID 발급</span><span class="sxs-lookup"><span data-stu-id="06d3f-220">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="06d3f-221">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - 이 클레임은 컴퓨터에 대한 유효한 값을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-221">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="06d3f-222">AD FS에서 다음과 같은 발급 변환 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-222">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-to-create-the-ad-fs-issuance-transform-rules"></a><span data-ttu-id="06d3f-223">AD FS 발급 변환 규칙을 만드는 도우미 스크립트</span><span class="sxs-lookup"><span data-stu-id="06d3f-223">Helper script to create the AD FS issuance transform rules</span></span>

<span data-ttu-id="06d3f-224">다음 스크립트는 위에서 설명한 발급 변환 규칙을 만드는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-224">The following script helps you with the creation of the issuance transform rules described above.</span></span>

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
    $rule4 = '@RuleName = "Issue account type with the value User when it is not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
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

### <a name="remarks"></a><span data-ttu-id="06d3f-225">설명</span><span class="sxs-lookup"><span data-stu-id="06d3f-225">Remarks</span></span> 

- <span data-ttu-id="06d3f-226">이 스크립트는 기존 규칙에 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-226">This script appends the rules to the existing rules.</span></span> <span data-ttu-id="06d3f-227">이 스크립트를 두 번 실행하면 규칙 집합이 두 번 추가되므로 두 번 실행하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="06d3f-227">Do not run the script twice because the set of rules would be added twice.</span></span> <span data-ttu-id="06d3f-228">스크립트를 다시 실행하기 전에 이러한 클레임에 해당하는 규칙이 없는지 확인(해당 조건에서)하세요.</span><span class="sxs-lookup"><span data-stu-id="06d3f-228">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span></span>

- <span data-ttu-id="06d3f-229">Azure AD 포털에서 또는 Get MsolDomains cmdlet을 통해 보여드린 것처럼 확인된 도메인 이름이 여러 개 있는 경우 스크립트에서 **$multipleVerifiedDomainNames** 값을 **$true**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-229">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span></span> <span data-ttu-id="06d3f-230">또한 Azure AD Connect 또는 다른 방법을 통해 만들어졌을 수 있는 기존 issuerid 클레임을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-230">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="06d3f-231">다음은 이 규칙에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-231">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="06d3f-232">사용자 계정에 대한 **ImmutableID** 클레임을 이미 발급한 경우 스크립트에서 **$immutableIDAlreadyIssuedforUsers** 값을 **$true**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-232">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$immutableIDAlreadyIssuedforUsers** in the script to **$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="06d3f-233">3단계: Windows 하위 수준 장치 설정</span><span class="sxs-lookup"><span data-stu-id="06d3f-233">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="06d3f-234">도메인에 가입된 장치 중 일부가 Windows 하위 수준 장치인 경우 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-234">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="06d3f-235">사용자가 장치를 등록할 수 있도록 Azure AD에 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-235">Set a policy in Azure AD to enable users to register devices.</span></span>
 
- <span data-ttu-id="06d3f-236">장치 등록에 **IWA(통합 Windows 인증)**를 지원하는 클레임을 발급하도록 온-프레미스 페더레이션 서비스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-236">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="06d3f-237">장치를 인증할 때 인증서 프롬프트가 나타나지 않도록 로컬 인트라넷 영역에 Azure AD 장치 인증 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-237">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span></span>

### <a name="set-policy-in-azure-ad-to-enable-users-to-register-devices"></a><span data-ttu-id="06d3f-238">사용자가 장치를 등록할 수 있도록 Azure AD에 정책 설정</span><span class="sxs-lookup"><span data-stu-id="06d3f-238">Set policy in Azure AD to enable users to register devices</span></span>

<span data-ttu-id="06d3f-239">Windows 하위 수준 장치를 등록하려면 사용자가 Azure AD에서 장치를 등록할 수 있도록 허용하는 설정을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-239">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span></span> <span data-ttu-id="06d3f-240">Azure Portal의 다음 위치에서 이러한 값을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-240">In the Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="06d3f-241">**사용자가 장치를 Azure AD에 등록할 수 있습니다.** 정책이 **모두**로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-241">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![장치 등록](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="06d3f-243">온-프레미스 페더레이션 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="06d3f-243">Configure on-premises federation service</span></span> 

<span data-ttu-id="06d3f-244">온-프레미스 페더레이션 서비스는 아래와 같이 인코딩된 값으로 resouce_params 매개 변수를 보유한 Azure AD 신뢰 당사자에 대한 인증 요청을 받으면 **authenticationmehod** 및 **wiaormultiauthn** 클레임 발급을 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-244">Your on-premises federation service must support issuing the **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="06d3f-245">이러한 요청이 오면 온-프레미스 페더레이션 서비스는 통합 Windows 인증을 사용하여 사용자를 인증해야 하며 인증이 완료되는 즉시 다음 두 클레임을 발급해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-245">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="06d3f-246">AD FS에서 인증 메서드를 통과하는 발급 변환 규칙을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-246">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span></span>  

<span data-ttu-id="06d3f-247">**이 규칙을 추가하려면:**</span><span class="sxs-lookup"><span data-stu-id="06d3f-247">**To add this rule:**</span></span>

1. <span data-ttu-id="06d3f-248">AD FS 관리 콘솔에서 `AD FS > Trust Relationships > Relying Party Trusts`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-248">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="06d3f-249">마우스 오른쪽 단추로 Microsoft Office 365 ID 플랫폼 신뢰 당사자 트러스트 개체를 클릭하고 **클레임 규칙 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-249">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="06d3f-250">**발급 변환 규칙** 탭에서 **규칙 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-250">On the **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="06d3f-251">**클레임 규칙** 템플릿 목록에서 **사용자 지정 규칙을 사용하여 클레임 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-251">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="06d3f-252">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-252">Select **Next**.</span></span>
6. <span data-ttu-id="06d3f-253">**클레임 규칙 이름** 상자에 **인증 방법 클레임 규칙**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-253">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="06d3f-254">**클레임 규칙** 상자에 다음 규칙을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-254">In the **Claim rule** box, type the following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="06d3f-255">페더레이션 서버에서 **\<RPObjectName\>**을 Azure AD 신뢰 당사자 트러스트 개체의 신뢰 당사자 개체 이름으로 바꾼 후 아래의 PowerShell 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-255">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="06d3f-256">일반적으로 이 개체의 이름은 **Microsoft Office 365 ID 플랫폼**입니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-256">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-the-azure-ad-device-authentication-end-point-to-the-local-intranet-zones"></a><span data-ttu-id="06d3f-257">로컬 인트라넷 영역에 Azure AD 장치 인증 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="06d3f-257">Add the Azure AD device authentication end-point to the Local Intranet zones</span></span>

<span data-ttu-id="06d3f-258">등록 장치의 사용자가 Azure AD에 인증할 때 인증서 프롬프트를 표시하지 않으려는 경우 Internet Explorer의 로컬 인트라넷 영역에 다음 URL을 추가하도록 도메인에 가입된 장치에 정책을 푸시하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-258">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="06d3f-259">4단계: 배포 및 롤아웃 제어</span><span class="sxs-lookup"><span data-stu-id="06d3f-259">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="06d3f-260">필요한 단계를 완료하면 도메인에 가입된 장치는 Azure AD에 자동으로 가입할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-260">When you have completed the required steps, domain-joined devices are ready to automatically join Azure AD:</span></span>

- <span data-ttu-id="06d3f-261">Windows 10 1주년 업데이트 및 Windows Server 2016을 실행하는 모든 도메인에 가입된 장치는 장치를 다시 시작하거나 사용자가 로그인할 때 자동으로 Azure AD에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-261">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> 

- <span data-ttu-id="06d3f-262">새 장치는 도메인 가입 작업이 완료된 후 장치를 다시 시작할 때 Azure AD에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-262">New devices register with Azure AD when the device restarts after the domain join operation is completed.</span></span>

- <span data-ttu-id="06d3f-263">이전에 Azure AD에 등록된 장치(예: Intune)는 “*도메인 가입, AAD 등록*”으로 전환됩니다. 그러나 도메인 및 사용자 활동의 정상 흐름으로 인해 이 프로세스가 모든 장치에서 완료되려면 다소 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-263">Devices that were previously Azure AD registered (for example, for Intune) transition to “*Domain Joined, AAD Registered*”; however it takes some time for this process to complete across all devices due to the normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="06d3f-264">설명</span><span class="sxs-lookup"><span data-stu-id="06d3f-264">Remarks</span></span>

- <span data-ttu-id="06d3f-265">그룹 정책 개체를 사용하면 Windows 10 및 Windows Server 2016 도메인 가입 컴퓨터의 자동 등록 롤아웃을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-265">You can use a Group Policy object to control the rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="06d3f-266">Windows 10 2015년 11월 업데이트는 롤아웃 그룹 정책 개체가 설정된 **경우에만** Azure AD에 자동으로 가입됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-266">Windows 10 November 2015 Update automatically joins with Azure AD **only** if the rollout Group Policy object is set.</span></span>

- <span data-ttu-id="06d3f-267">Windows 하위 수준 컴퓨터를 롤아웃하려면 선택한 컴퓨터에 [Windows Installer 패키지](#windows-installer-packages-for-non-windows-10-computers)를 배포하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-267">To rollout of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to computers that you select.</span></span>

- <span data-ttu-id="06d3f-268">Windows 8.1 도메인 가입 장치에 그룹 정책 개체를 푸시하면 가입이 시도됩니다. 그러나 [Windows Installer 패키지](#windows-installer-packages-for-non-windows-10-computers)를 사용하여 모든 Windows 하위 수준 장치를 가입하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-268">If you push the Group Policy object to Windows 8.1 domain-joined devices, a join is attempted; however it is recommended that you use the [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to join all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="06d3f-269">그룹 정책 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="06d3f-269">Create a Group Policy object</span></span> 

<span data-ttu-id="06d3f-270">Windows 현재 컴퓨터의 롤아웃을 제어하려면 등록하려는 장치에 **도메인 가입 컴퓨터를 장치로 등록** 그룹 정책 개체를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-270">To control the rollout of Windows current computers, you should deploy the **Register domain-joined computers as devices** Group Policy object to the devices you want to register.</span></span> <span data-ttu-id="06d3f-271">예를 들어 조직 구성 단위 또는 보안 그룹에 정책을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-271">For example, you can deploy the policy to an organizational unit or to a security group.</span></span>

<span data-ttu-id="06d3f-272">**정책을 설정하려면:**</span><span class="sxs-lookup"><span data-stu-id="06d3f-272">**To set the policy:**</span></span>

1. <span data-ttu-id="06d3f-273">**서버 관리자**를 열고 `Tools > Group Policy Management`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-273">Open **Server Manager**, and then go to `Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="06d3f-274">Windows 현재 컴퓨터의 자동 등록을 활성화하려는 도메인에 해당하는 도메인 노드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-274">Go to the domain node that corresponds to the domain where you want to activate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="06d3f-275">**그룹 정책 개체**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-275">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="06d3f-276">그룹 정책 개체의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-276">Type a name for your Group Policy object.</span></span> <span data-ttu-id="06d3f-277">예를 들어 *하이브리드 Azure AD 가입입니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-277">For example, *Hybrid Azure AD join.</span></span> 
5. <span data-ttu-id="06d3f-278">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-278">Click **OK**.</span></span>
6. <span data-ttu-id="06d3f-279">마우스 오른쪽 단추로 새 그룹 정책 개체를 클릭한 다음 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-279">Right-click your new Group Policy object, and then select **Edit**.</span></span>
7. <span data-ttu-id="06d3f-280">**컴퓨터 구성** > **정책** > **관리 템플릿** > **Windows 구성 요소** > **장치 등록**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-280">Go to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> 
8. <span data-ttu-id="06d3f-281">마우스 오른쪽 단추로 **도메인 가입 컴퓨터를 장치로 등록**을 클릭한 다음 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-281">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="06d3f-282">이 그룹 정책 템플릿 이름은 이전 버전의 그룹 정책 관리 콘솔에서 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-282">This Group Policy template has been renamed from earlier versions of the Group Policy Management console.</span></span> <span data-ttu-id="06d3f-283">이전 버전의 콘솔을 사용하는 경우 `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-283">If you are using an earlier version of the console, go to `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="06d3f-284">**사용**을 선택하고 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-284">Select **Enabled**, and then click **Apply**.</span></span>
8. <span data-ttu-id="06d3f-285">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-285">Click **OK**.</span></span>
9. <span data-ttu-id="06d3f-286">그룹 정책 개체를 선택한 위치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-286">Link the Group Policy object to a location of your choice.</span></span> <span data-ttu-id="06d3f-287">예를 들어 특정 조직 구성 단위에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-287">For example, you can link it to a specific organizational unit.</span></span> <span data-ttu-id="06d3f-288">또한 Azure AD에 자동으로 가입되는 컴퓨터의 특정 보안 그룹에 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-288">You also could link it to a specific security group of computers that automatically join with Azure AD.</span></span> <span data-ttu-id="06d3f-289">조직의 모든 Windows 10 및 Windows Server 2016 도메인 가입 컴퓨터에 대해 이 정책을 사용하도록 설정하려면 그룹 정책 개체를 해당 도메인에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-289">To set this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link the Group Policy object to the domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="06d3f-290">비 Windows 10 컴퓨터용 Windows Installer 패키지</span><span class="sxs-lookup"><span data-stu-id="06d3f-290">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="06d3f-291">페더레이션된 환경에서 도메인에 가입된 Windows 하위 수준 컴퓨터를 가입하려면 [비-Windows 10 컴퓨터의 Microsoft 작업 공간 연결](https://www.microsoft.com/en-us/download/details.aspx?id=53554) 페이지의 다운로드 센터에서 Windows Installer 패키지(.msi)를 다운로드하여 설치하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-291">To join domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="06d3f-292">System Center Configuration Manager 같은 소프트웨어 배포 시스템을 사용하여 패키지를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-292">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="06d3f-293">이 패키지는 *quiet* 매개 변수를 사용하여 표준 자동 설치 옵션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-293">The package supports the standard silent install options with the *quiet* parameter.</span></span> <span data-ttu-id="06d3f-294">System Center Configuration Manager Current Branch는 완료된 등록을 추적하는 기능과 같은 이전 버전의 이점이 추가로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-294">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span></span> <span data-ttu-id="06d3f-295">자세한 내용은 [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06d3f-295">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="06d3f-296">설치 관리자에서는 사용자 컨텍스트에서 실행되도록 예약된 작업을 시스템에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-296">The installer creates a scheduled task on the system that runs in the user’s context.</span></span> <span data-ttu-id="06d3f-297">사용자가 Windows에 로그인할 때 이 작업이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-297">The task is triggered when the user signs in to Windows.</span></span> <span data-ttu-id="06d3f-298">이 작업은 통합 Windows 인증을 사용하여 인증한 후 사용자 자격 증명을 사용하여 장치를 Azure AD에 자동으로 가입합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-298">The task silently joins the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="06d3f-299">예약된 작업을 보려면 장치에서 **Microsoft** > **작업 공간 연결**, 작업 스케줄러 라이브러리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-299">To see the scheduled task, in the device, go to **Microsoft** > **Workplace Join**, and then go to the Task Scheduler library.</span></span>

## <a name="step-5-verify-joined-devices"></a><span data-ttu-id="06d3f-300">5단계: 가입 장치 확인</span><span class="sxs-lookup"><span data-stu-id="06d3f-300">Step 5: Verify joined devices</span></span>

<span data-ttu-id="06d3f-301">[Azure Active Directory PowerShell 모듈](/powershell/azure/install-msonlinev1?view=azureadps-2.0)에서 [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet을 사용하여 조직에 성공적으로 가입된 장치를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-301">You can check successful joined devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="06d3f-302">이 cmdlet의 출력은 Azure AD로 등록 및 가입된 장치를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-302">The output of this cmdlet shows devices that are registered and joined with Azure AD.</span></span> <span data-ttu-id="06d3f-303">모든 장치를 가져오려면 **-All** 매개 변수를 사용한 다음 **deviceTrustType** 속성을 사용하여 장치를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-303">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span></span> <span data-ttu-id="06d3f-304">도메인에 가입된 장치는 **도메인 가입** 값을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="06d3f-304">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06d3f-305">다음 단계</span><span class="sxs-lookup"><span data-stu-id="06d3f-305">Next steps</span></span>

* [<span data-ttu-id="06d3f-306">Azure Active Directory의 장치 관리 소개</span><span class="sxs-lookup"><span data-stu-id="06d3f-306">Introduction to device management in Azure Active Directory</span></span>](device-management-introduction.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
