---
title: "aaaActive Directory 페더레이션 서비스 관리 및 Azure AD Connect와 사용자 정의 | Microsoft Docs"
description: "Azure AD Connect를 사용한 AD FS 관리 및 Azure AD Connect와 PowerShell을 사용한 사용자 AD FS 로그인 환경의 사용자 지정입니다."
keywords: "AD FS, ADFS, AD FS 관리, AAD Connect, 연결, 로그인, AD FS 사용자 지정, 트러스트 복구, O365, 페더레이션, 신뢰 당사자"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="cff0b-104">Azure AD Connect를 사용하여 Active Directory Federation Services 관리 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="cff0b-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="cff0b-105">이 문서에서는 설명 방법을 toomanage 및 Azure Active Directory (Azure AD) 연결을 사용 하 여 Active Directory Federation Services (AD FS)를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-105">This article describes how toomanage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="cff0b-106">AD FS 팜 전체 구성에 대 한 toodo이 필요할 수 있습니다 다른 일반적인 AD FS 작업 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-106">It also includes other common AD FS tasks that you might need toodo for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="cff0b-107">항목</span><span class="sxs-lookup"><span data-stu-id="cff0b-107">Topic</span></span> | <span data-ttu-id="cff0b-108">포함된 내용</span><span class="sxs-lookup"><span data-stu-id="cff0b-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="cff0b-109">**AD FS 관리**</span><span class="sxs-lookup"><span data-stu-id="cff0b-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="cff0b-110">복구 hello 신뢰</span><span class="sxs-lookup"><span data-stu-id="cff0b-110">Repair hello trust</span></span>](#repairthetrust) |<span data-ttu-id="cff0b-111">어떻게 Office 365와 toorepair hello 페더레이션 신뢰 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-111">How toorepair hello federation trust with Office 365.</span></span> |
| [<span data-ttu-id="cff0b-112">대체 로그인 ID를 사용하여 Azure AD와 페더레이션</span><span class="sxs-lookup"><span data-stu-id="cff0b-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="cff0b-113">대체 로그인 ID를 사용하여 페더레이션 구성</span><span class="sxs-lookup"><span data-stu-id="cff0b-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="cff0b-114">AD FS 서버 추가</span><span class="sxs-lookup"><span data-stu-id="cff0b-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="cff0b-115">어떻게 추가 AD FS 서버가 있는 AD FS tooexpand 팜 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-115">How tooexpand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="cff0b-116">AD FS 웹 응용 프로그램 프록시 서버 추가</span><span class="sxs-lookup"><span data-stu-id="cff0b-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="cff0b-117">어떻게 추가 응용 프로그램 프록시 WAP (웹) 서버가 있는 AD FS tooexpand 팜 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-117">How tooexpand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="cff0b-118">페더레이션된 도메인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="cff0b-119">어떻게 tooadd 페더레이션된 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-119">How tooadd a federated domain.</span></span> |
| [<span data-ttu-id="cff0b-120">Hello SSL 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="cff0b-120">Update hello SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="cff0b-121">어떻게 tooupdate hello SSL 인증서는 AD FS 팜에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-121">How tooupdate hello SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="cff0b-122">**AD FS 사용자 지정**</span><span class="sxs-lookup"><span data-stu-id="cff0b-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="cff0b-123">사용자 지정 회사 로고 또는 일러스트레이션 추가</span><span class="sxs-lookup"><span data-stu-id="cff0b-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="cff0b-124">어떻게 toocustomize AD FS 로그인 페이지 회사 로고 및 일러스트레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-124">How toocustomize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="cff0b-125">로그인 설명 추가</span><span class="sxs-lookup"><span data-stu-id="cff0b-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="cff0b-126">어떻게 tooadd에 로그인 페이지 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-126">How tooadd a sign-in page description.</span></span> |
| [<span data-ttu-id="cff0b-127">AD FS 클레임 규칙 수정</span><span class="sxs-lookup"><span data-stu-id="cff0b-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="cff0b-128">어떻게 toomodify AD FS는 다양 한 페더레이션 시나리오에 대 한 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-128">How toomodify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="cff0b-129">AD FS 관리</span><span class="sxs-lookup"><span data-stu-id="cff0b-129">Manage AD FS</span></span>
<span data-ttu-id="cff0b-130">Hello Azure AD Connect 마법사를 사용 하 여 최소한의 사용자 개입으로 Azure AD Connect에서 다양 한 AD FS와 관련 된 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using hello Azure AD Connect wizard.</span></span> <span data-ttu-id="cff0b-131">Hello 마법사를 실행 하려면 hello 마법사를 실행 하 여 Azure AD Connect 설치를 마친 후 다시 tooperform 추가 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-131">After you've finished installing Azure AD Connect by running hello wizard, you can run hello wizard again tooperform additional tasks.</span></span>

## <span data-ttu-id="cff0b-132">복구 hello 신뢰<a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="cff0b-132">Repair hello trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="cff0b-133">Azure AD Connect toocheck hello hello AD FS의 현재 상태와 Azure AD 신뢰를 사용 하 여 수 있으며 toorepair hello 신뢰 적절 한 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-133">You can use Azure AD Connect toocheck hello current health of hello AD FS and Azure AD trust and take appropriate actions toorepair hello trust.</span></span> <span data-ttu-id="cff0b-134">따라 이러한 단계 toorepair Azure AD와 AD FS 신뢰 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-134">Follow these steps toorepair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="cff0b-135">선택 **복구 AAD와 ad FS를 신뢰** 추가 작업의 hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-135">Select **Repair AAD and ADFS Trust** from hello list of additional tasks.</span></span>
   <span data-ttu-id="cff0b-136">![AAD 및 ADFS 트러스트 복구](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="cff0b-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="cff0b-137">Hello에 **tooAzure AD 연결** 페이지 Azure AD에 대 한 전역 관리자 자격 증명을 제공 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-137">On hello **Connect tooAzure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="cff0b-138">![TooAzure AD 연결](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="cff0b-138">![Connect tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="cff0b-139">Hello에 **원격 액세스 자격 증명** 페이지에서 도메인 관리자에 게 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-139">On hello **Remote access credentials** page, enter hello credentials for hello domain administrator.</span></span>

   ![원격 액세스 자격 증명](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="cff0b-141">**다음**을 클릭한 후 Azure AD Connect가 인증서 상태를 확인하고 문제를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![인증서의 상태](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="cff0b-143">hello **준비 tooconfigure** 페이지 toorepair hello 신뢰를 수행할 수 있는 작업이 hello 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-143">hello **Ready tooconfigure** page shows hello list of actions that will be performed toorepair hello trust.</span></span>

    ![준비 tooconfigure](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="cff0b-145">클릭 **설치** toorepair hello 신뢰 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-145">Click **Install** toorepair hello trust.</span></span>

> [!NOTE]
> <span data-ttu-id="cff0b-146">Azure AD Connect는 자체 서명된 인증서에 대해서만 복구 또는 조치를 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="cff0b-147">Azure AD Connect에서 타사 인증서를 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="cff0b-148"><a name=alternateid></a>대체 ID를 사용하여 Azure AD와 페더레이션</span><span class="sxs-lookup"><span data-stu-id="cff0b-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="cff0b-149">Hello 온-프레미스 사용자 계정 Name(UPN) 및 동일한 사용자 계정 이름 유지 되는 hello 클라우드 hello는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-149">It is recommended that hello on-premises User Principal Name(UPN) and hello cloud User Principal Name are kept hello same.</span></span> <span data-ttu-id="cff0b-150">Hello 온-프레미스 UPN 사용 (예: 라우팅할 수 없는 도메인.</span><span class="sxs-lookup"><span data-stu-id="cff0b-150">If hello on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="cff0b-151">Contoso.local)을 변경할 수 없습니다 또는 toolocal 응용 프로그램 종속성 인해 좋습니다 대체 로그인 id입니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-151">Contoso.local) or cannot be changed due toolocal application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="cff0b-152">대체 로그인 ID는 로그인, 메일 등의 해당 UPN 이외의 특성으로 사용자가 로그인 수 있는 환경 tooconfigure가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-152">Alternate login ID allows you tooconfigure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="cff0b-153">Active Directory에서 Azure AD Connect 기본값 toohello userPrincipalName 특성의 사용자 계정 이름에 대 한 hello 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-153">hello choice for User Principal Name in Azure AD Connect defaults toohello userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="cff0b-154">사용자 계정 이름에 대해 다른 특성을 선택하고 AD FS를 사용하여 페더레이션할 경우 Azure AD Connect는 대체 로그인 ID에 맞게 AD FS를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="cff0b-155">사용자 계정 이름으로 선택할 수 있는 다른 특성은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![대체 ID 특성 선택 항목](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="cff0b-157">AD FS에 대한 대체 로그인 ID 구성은 크게 다음 두 단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="cff0b-158">**Hello 오른쪽 발급 클레임 집합이 구성**: hello Azure AD 신뢰 당사자에 hello 발급 클레임 규칙 수정된 toouse 선택한 hello UserPrincipalName 특성은 hello hello 사용자의 대체 ID를 신뢰 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-158">**Configure hello right set of issuance claims**: hello issuance claim rules in hello Azure AD relying party trust are modified toouse hello selected UserPrincipalName attribute as hello alternate ID of hello user.</span></span>
2. <span data-ttu-id="cff0b-159">**Hello AD FS 구성에 대체 로그인 ID를 사용 하도록 설정**: AD FS hello 대체 id입니다. 사용 하는 hello 적절 한 포리스트에 사용자가 조회할 수 있도록 hello AD FS 구성을 업데이트 됩니다</span><span class="sxs-lookup"><span data-stu-id="cff0b-159">**Enable alternate login ID in hello AD FS configuration**: hello AD FS configuration is updated so that AD FS can look up users in hello appropriate forests using hello alternate ID.</span></span> <span data-ttu-id="cff0b-160">이 구성은 Windows Server 2012 R2(KB2919355) 이상의 AD FS에 대해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="cff0b-161">Hello AD FS 서버는 2012 r 2 인 경우 hello hello 있는지 확인 합니다. Azure AD Connect KB이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-161">If hello AD FS servers are 2012 R2, Azure AD Connect checks for hello presence of hello required KB.</span></span> <span data-ttu-id="cff0b-162">Hello KB 검색 되지 않으면 경고가 나타납니다 구성이 완료 된 후 아래와 같이:</span><span class="sxs-lookup"><span data-stu-id="cff0b-162">If hello KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![2012R2의 KB 누락에 대한 경고](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="cff0b-164">누락 된 KB 발생할 경우 toorectify hello 구성 hello 필요한 설치 [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) hello 트러스트를 사용 하 여 다음 복구 및 [복구 AAD 및 AD FS 신뢰](#repairthetrust)합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-164">toorectify hello configuration in case of missing KB, install hello required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair hello trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="cff0b-165">Toomanually alternateID 및 단계에 대 한 자세한 내용은 구성, 읽기 [대체 로그인 ID 구성](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="cff0b-165">For more information on alternateID and steps toomanually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="cff0b-166">AD FS 서버 추가 <a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="cff0b-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="cff0b-167">tooadd AD FS 서버에 Azure AD Connect hello PFX 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-167">tooadd an AD FS server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="cff0b-168">따라서 Azure AD Connect를 사용 하 여 hello AD FS 팜을 구성 하는 경우에이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-168">Therefore, you can perform this operation only if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="cff0b-169">**추가 페더레이션 서버 배포**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![추가 페더레이션 서버](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="cff0b-171">Hello에 **tooAzure AD 연결** 페이지, Azure AD에 대 한 전역 관리자 자격 증명을 입력 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-171">On hello **Connect tooAzure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![TooAzure AD 연결](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="cff0b-173">Hello 도메인 관리자 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-173">Provide hello domain administrator credentials.</span></span>

   ![도메인 관리자 자격 증명](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="cff0b-175">Azure AD Connect Azure AD Connect를 사용 하 여 새 AD FS 팜을 구성 하는 동안 사용자가 제공한 hello PFX 파일의 hello 암호를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-175">Azure AD Connect asks for hello password of hello PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="cff0b-176">클릭 **암호 입력** tooprovide hello hello PFX 파일 암호를 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-176">Click **Enter Password** tooprovide hello password for hello PFX file.</span></span>

   ![인증서 암호](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![SSL 인증서 지정](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="cff0b-179">Hello에 **AD FS 서버** 페이지 hello 서버 이름 또는 IP 주소 toobe 추가 입력 toohello AD FS 팜을 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-179">On hello **AD FS Servers** page, enter hello server name or IP address toobe added toohello AD FS farm.</span></span>

   ![AD FS 서버](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="cff0b-181">클릭 **다음**, 이동 하 여 최종 hello **구성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="cff0b-181">Click **Next**, and go through hello final **Configure** page.</span></span> <span data-ttu-id="cff0b-182">Azure AD Connect hello 서버 toohello AD FS 팜에 추가 완료 되 면 hello 옵션 tooverify hello 연결을 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-182">After Azure AD Connect has finished adding hello servers toohello AD FS farm, you will be given hello option tooverify hello connectivity.</span></span>

   ![준비 tooconfigure](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![설치 완료](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="cff0b-185">AD FS WAP 서버 추가 <a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="cff0b-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="cff0b-186">WAP 서버 tooadd Azure AD Connect hello PFX 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-186">tooadd a WAP server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="cff0b-187">따라서 Azure AD Connect를 사용 하 여 hello AD FS 팜을 구성한 경우이 작업에 수행할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-187">Therefore, you can only perform this operation if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="cff0b-188">선택 **웹 응용 프로그램 프록시 배포** hello 사용 가능한 작업 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-188">Select **Deploy Web Application Proxy** from hello list of available tasks.</span></span>

   ![웹 응용 프로그램 프록시 배포](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="cff0b-190">Hello Azure 전역 관리자 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-190">Provide hello Azure global administrator credentials.</span></span>

   ![TooAzure AD 연결](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="cff0b-192">Hello에 **지정 SSL 인증서** 페이지에서 Azure AD Connect와 hello AD FS 팜을 구성할 때 사용자가 제공한 hello PFX 파일에 대 한 hello 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-192">On hello **Specify SSL certificate** page, provide hello password for hello PFX file that you provided when you configured hello AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="cff0b-193">![인증서 암호](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="cff0b-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![SSL 인증서 지정](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="cff0b-195">WAP 서버로 추가 하는 hello 서버 toobe를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-195">Add hello server toobe added as a WAP server.</span></span> <span data-ttu-id="cff0b-196">Hello WAP 서버는 도메인에 가입된 toohello 되지 않을 수 있습니다, 때문에 추가 되 고 관리자 자격 증명이 toohello 서버 hello 마법사 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-196">Because hello WAP server might not be joined toohello domain, hello wizard asks for administrative credentials toohello server being added.</span></span>

   ![관리 서버 자격 증명](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="cff0b-198">Hello에 **프록시 트러스트 자격 증명** 페이지 신뢰 및 액세스 hello 팜의 기본 서버로 hello AD FS 관리 자격 증명이 tooconfigure hello 프록시를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-198">On hello **Proxy trust credentials** page, provide administrative credentials tooconfigure hello proxy trust and access hello primary server in hello AD FS farm.</span></span>

   ![프록시 트러스트 자격 증명](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="cff0b-200">Hello에 **준비 tooconfigure** hello 마법사 페이지에서 수행 되는 작업 목록은 hello에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-200">On hello **Ready tooconfigure** page, hello wizard shows hello list of actions that will be performed.</span></span>

   ![준비 tooconfigure](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="cff0b-202">클릭 **설치** toofinish hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-202">Click **Install** toofinish hello configuration.</span></span> <span data-ttu-id="cff0b-203">Hello 구성이 완료 되 면 hello 마법사 제공 옵션 tooverify hello 연결 toohello 서버 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-203">After hello configuration is complete, hello wizard gives you hello option tooverify hello connectivity toohello servers.</span></span> <span data-ttu-id="cff0b-204">클릭 **확인** toocheck 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-204">Click **Verify** toocheck connectivity.</span></span>

   ![설치 완료](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="cff0b-206">페더레이션된 도메인을 추가합니다. <a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="cff0b-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="cff0b-207">것이 쉬운 tooadd 도메인 toobe Azure AD Connect를 사용 하 여 Azure AD와 페더레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-207">It's easy tooadd a domain toobe federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="cff0b-208">Azure AD Connect 페더레이션에 대 한 hello 도메인을 추가 하 고 Azure AD와 페더레이션 하는 여러 도메인이 있는 경우 규칙 toocorrectly hello 발급자를 반영 하는 hello 클레임을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-208">Azure AD Connect adds hello domain for federation and modifies hello claim rules toocorrectly reflect hello issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="cff0b-209">tooadd 페더레이션된 도메인으로 선택 hello 작업 **더 추가 Azure AD 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-209">tooadd a federated domain, select hello task **Add an additional Azure AD domain**.</span></span>

   ![추가 Azure AD 도메인](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="cff0b-211">Hello hello 마법사의 다음 페이지에서 Azure AD에 대 한 hello 전역 관리자 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-211">On hello next page of hello wizard, provide hello global administrator credentials for Azure AD.</span></span>

   ![TooAzure AD 연결](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="cff0b-213">Hello에 **원격 액세스 자격 증명** 페이지 hello 도메인 관리자 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-213">On hello **Remote access credentials** page, provide hello domain administrator credentials.</span></span>

   ![원격 액세스 자격 증명](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="cff0b-215">Hello 다음 페이지에서 hello 마법사는 온-프레미스 디렉터리와 페더레이션 할 수 있는 Azure AD 도메인의 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-215">On hello next page, hello wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="cff0b-216">Hello 도메인 hello 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-216">Choose hello domain from hello list.</span></span>

   ![Azure AD 도메인](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="cff0b-218">Hello 도메인을 선택한 후 hello 마법사 영향 hello 구성 hello를 가져와 됩니다 있습니다 마법사 hello 추가 작업에 대 한 적절 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-218">After you choose hello domain, hello wizard provides you with appropriate information about further actions that hello wizard will take and hello impact of hello configuration.</span></span> <span data-ttu-id="cff0b-219">경우에 따라 hello을 제공 합니다. 정보 toohelp Azure AD에서 확인 아직 하지 않는 도메인을 선택할 경우 hello 도메인을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-219">In some cases, if you select a domain that isn't yet verified in Azure AD, hello wizard provides you with information toohelp you verify hello domain.</span></span> <span data-ttu-id="cff0b-220">참조 [추가 사용자 지정 도메인 이름을 tooAzure Active Directory](../active-directory-add-domain.md) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-220">See [Add your custom domain name tooAzure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="cff0b-221">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-221">Click **Next**.</span></span> <span data-ttu-id="cff0b-222">hello **준비 tooconfigure** 페이지 hello Azure AD Connect를 수행 하는 작업 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-222">hello **Ready tooconfigure** page shows hello list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="cff0b-223">클릭 **설치** toofinish hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-223">Click **Install** toofinish hello configuration.</span></span>

   ![준비 tooconfigure](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="cff0b-225">Hello에서 사용자가 추가 수 toologin tooAzure AD 됩니다 전에 페더레이션된 도메인을 동기화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-225">Users from hello added federated domain must be synchronized before they will be able toologin tooAzure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="cff0b-226">AD FS 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="cff0b-226">AD FS customization</span></span>
<span data-ttu-id="cff0b-227">hello 다음 섹션에서는 hello 일반적인 작업 중 일부에 대 한 AD FS 로그인 페이지를 사용자 지정할 때 tooperform를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-227">hello following sections provide details about some of hello common tasks that you might have tooperform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="cff0b-228">사용자 지정 회사 로고 또는 일러스트레이션 추가 <a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="cff0b-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="cff0b-229">hello에 표시 되는 hello 회사의 toochange hello 로고 **로그인** 페이지에서 다음 Windows PowerShell cmdlet 및 구문을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-229">toochange hello logo of hello company that's displayed on hello **Sign-in** page, use hello following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="cff0b-230">hello hello 로고는 10KB 이내인 파일 크기는 96dpi에서 260 x 35에 크기를 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-230">hello recommended dimensions for hello logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="cff0b-231">hello *TargetName* 매개 변수는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-231">hello *TargetName* parameter is required.</span></span> <span data-ttu-id="cff0b-232">AD FS와 함께 제공 되는 hello 기본 테마의 기본을 이름은입니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-232">hello default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="cff0b-233">로그인 설명 추가 <a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="cff0b-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="cff0b-234">로그인 페이지 설명 toohello tooadd **로그인 페이지**, hello 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-234">tooadd a sign-in page description toohello **Sign-in page**, use hello following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="cff0b-235">AD FS 클레임 규칙 수정 <a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="cff0b-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="cff0b-236">AD FS에서 사용할 수 있는 풍부한 클레임 언어 원하는 toocreate 사용자 지정 클레임 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-236">AD FS supports a rich claim language that you can use toocreate custom claim rules.</span></span> <span data-ttu-id="cff0b-237">자세한 내용은 참조 [hello 클레임 규칙 언어의 역할 hello](https://technet.microsoft.com/library/dd807118.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-237">For more information, see [hello Role of hello Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="cff0b-238">hello 다음 단원에서는 tooAzure AD 및 AD FS 페더레이션 관련 된 일부 시나리오에 대 한 사용자 지정 규칙을 작성 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="cff0b-238">hello following sections describe how you can write custom rules for some scenarios that relate tooAzure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a><span data-ttu-id="cff0b-239">Hello 특성에 없는 값에 조건부 변경할 수 없는 ID</span><span class="sxs-lookup"><span data-stu-id="cff0b-239">Immutable ID conditional on a value being present in hello attribute</span></span>
<span data-ttu-id="cff0b-240">Azure AD Connect를 사용 하면 개체가 경우 원본 앵커 tooAzure AD 동기화로 사용 하는 특성 toobe를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-240">Azure AD Connect lets you specify an attribute toobe used as a source anchor when objects are synced tooAzure AD.</span></span> <span data-ttu-id="cff0b-241">Hello 값 hello 사용자 지정 특성에 비어 있지 않은 경우에 변경할 수 없는 ID 클레임 tooissue를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-241">If hello value in hello custom attribute is not empty, you might want tooissue an immutable ID claim.</span></span>

<span data-ttu-id="cff0b-242">예를 들어, 선택할 수 **ms-ds-consistencyguid** hello 원본 앵커 및 문제에 대 한 hello 특성으로 **ImmutableID** 으로 **ms-ds-consistencyguid** 사례 hello에 특성에 대 한 값을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-242">For example, you might select **ms-ds-consistencyguid** as hello attribute for hello source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case hello attribute has a value against it.</span></span> <span data-ttu-id="cff0b-243">Hello 특성에 대 한 값이 없는 경우 발급 **objectGuid** 대로 hello 변경할 수 없는 id입니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-243">If there's no value against hello attribute, issue **objectGuid** as hello immutable ID.</span></span> <span data-ttu-id="cff0b-244">사용자 지정 클레임 규칙 집합이 hello hello 다음 섹션에에서 설명 된 대로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-244">You can construct hello set of custom claim rules as described in hello following section.</span></span>

<span data-ttu-id="cff0b-245">**규칙 1: 쿼리 특성**</span><span class="sxs-lookup"><span data-stu-id="cff0b-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="cff0b-246">이 규칙에 hello 값을 쿼리 하는 **ms-ds-consistencyguid** 및 **objectGuid** Active Directory에서 사용자 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-246">In this rule, you're querying hello values of **ms-ds-consistencyguid** and **objectGuid** for hello user from Active Directory.</span></span> <span data-ttu-id="cff0b-247">AD FS 배포에서 hello 저장소 이름 tooan 적절 한 저장소 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-247">Change hello store name tooan appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="cff0b-248">에 대해 정의 된 대로 페더레이션에서는 hello 클레임 유형 tooa 적절 한 클레임 종류를 변경할 수도 **objectGuid** 및 **ms-ds-consistencyguid**합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-248">Also change hello claims type tooa proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="cff0b-249">또한를 사용 하 여 **추가** 아닌 **문제**, 나가는 문제 hello 엔터티에 대 한 추가 하지 않도록 하 고 hello 값 중간 값으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for hello entity, and can use hello values as intermediate values.</span></span> <span data-ttu-id="cff0b-250">변경할 수 없는 id입니다. hello으로 어떤 값 toouse를 설정한 후 이상 규칙에 hello 클레임을 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-250">You will issue hello claim in a later rule after you establish which value toouse as hello immutable ID.</span></span>

<span data-ttu-id="cff0b-251">**규칙 2: hello 사용자에 대 한 ms-ds-consistencyguid 있는지 확인**</span><span class="sxs-lookup"><span data-stu-id="cff0b-251">**Rule 2: Check if ms-ds-consistencyguid exists for hello user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="cff0b-252">이 규칙은 이라는 임시 플래그를 정의 **idflag** 너무 설정 된**useguid** 없는 경우 없는 **ms-ds-consistencyguid** hello 사용자에 대해 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-252">This rule defines a temporary flag called **idflag** that is set too**useguid** if there's no **ms-ds-consistencyguid** populated for hello user.</span></span> <span data-ttu-id="cff0b-253">이 뒤에 있는 hello 논리 hello 팩트 AD FS가 빈 클레임을 허용 하지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-253">hello logic behind this is hello fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="cff0b-254">규칙 1에 클레임 http://contoso.com/ws/2016/02/identity/claims/objectguid 및 http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid를 추가할 때 /fd 되므로 **msdsconsistencyguid** 경우에만 클레임 hello 사용자에 대 한 hello 값은 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if hello value is populated for hello user.</span></span> <span data-ttu-id="cff0b-255">채워지지 않은 경우 AD FS는 빈 값을 갖는 것을 확인하고 즉시 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="cff0b-256">모든 개체에는 **objectGuid**가 있으므로 규칙 1이 실행된 후 항상 클레임이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="cff0b-257">**규칙 3: 있는 경우 변경이 불가능한 ID로 ms-ds-consistencyguid 발급**</span><span class="sxs-lookup"><span data-stu-id="cff0b-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="cff0b-258">이는 암시적 **Exist** 확인입니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="cff0b-259">Hello 클레임에 대 한 hello 값이 있으면 그런 후 실행 하는 변경할 수 없는 hello로 id입니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-259">If hello value for hello claim exists, then issue that as hello immutable ID.</span></span> <span data-ttu-id="cff0b-260">hello를 사용 하 여 hello 이전 예제 **nameidentifier** 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-260">hello previous example uses hello **nameidentifier** claim.</span></span> <span data-ttu-id="cff0b-261">해야 toochange이 toohello 적절 한 클레임 유형을 변경할 수 없는 ID hello에 대 한 사용자 환경에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-261">You'll have toochange this toohello appropriate claim type for hello immutable ID in your environment.</span></span>

<span data-ttu-id="cff0b-262">**규칙 4: ms-ds-consistencyGuid가 없는 경우 변경이 불가능한 ID로 objectGuid 발급**</span><span class="sxs-lookup"><span data-stu-id="cff0b-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="cff0b-263">이 규칙에 단순히 hello 임시 플래그를 확인 하는지에 **idflag**합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-263">In this rule, you're simply checking hello temporary flag **idflag**.</span></span> <span data-ttu-id="cff0b-264">Tooissue hello 클레임 기반 하는지 여부를 결정할 값에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-264">You decide whether tooissue hello claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="cff0b-265">이러한 규칙의 hello 순서가 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-265">hello sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="cff0b-266">하위 도메인 UPN을 사용한 SSO</span><span class="sxs-lookup"><span data-stu-id="cff0b-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="cff0b-267">에 설명 된 대로 Azure AD Connect를 사용 하 여 페더레이션 도메인 toobe를 여러 개 추가할 수 있습니다 [새 페더레이션된 도메인을 추가](active-directory-aadconnect-federation-management.md#addfeddomain)합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-267">You can add more than one domain toobe federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="cff0b-268">수정 해야 hello 사용자 계정 이름 (UPN) 클레임 hello 발급자 ID toohello 루트 도메인 및 해당 hello 하위 도메인 되지 않도록 hello 자식 hello 페더레이션된 루트 도메인에 대해서도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-268">You must modify hello user principal name (UPN) claim so that hello issuer ID corresponds toohello root domain and not hello subdomain, because hello federated root domain also covers hello child.</span></span>

<span data-ttu-id="cff0b-269">기본적으로 hello 클레임 ID가로 설정 하는 발급자에 대 한 규칙:</span><span class="sxs-lookup"><span data-stu-id="cff0b-269">By default, hello claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![기본 발급자 ID 클레임](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="cff0b-271">hello 기본 규칙 hello UPN 접미사를 가져와서을 hello 발급자 ID 클레임에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-271">hello default rule simply takes hello UPN suffix and uses it in hello issuer ID claim.</span></span> <span data-ttu-id="cff0b-272">예를 들어 John은 sub.contoso.com의 사용자이고 contoso.com은 Azure AD를 사용하여 페더레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="cff0b-273">John 입력 john@sub.contoso.com tooAzure AD에에서 로그인 하는 동안 사용자 이름 hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-273">John enters john@sub.contoso.com as hello username while signing in tooAzure AD.</span></span> <span data-ttu-id="cff0b-274">AD FS의 hello 기본 발급자 ID 클레임 규칙 hello 방식으로 다음이 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-274">hello default issuer ID claim rule in AD FS handles it in hello following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="cff0b-275">**클레임 값:** http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="cff0b-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="cff0b-276">toohave 유일한 hello 루트 도메인의 hello 발급자 클레임 값 같이 hello 클레임 규칙 toomatch hello 다음 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-276">toohave only hello root domain in hello issuer claim value, change hello claim rule toomatch hello following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="cff0b-277">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cff0b-277">Next steps</span></span>
<span data-ttu-id="cff0b-278">[사용자 로그인 옵션](active-directory-aadconnect-user-signin.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cff0b-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
