---
title: "Azure AD Connect를 사용하여 Active Directory Federation Services 관리 및 사용자 지정 | Microsoft Docs"
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
ms.openlocfilehash: 14f03542a6553c5bb697192828368ffe6b96441c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="1929a-104">Azure AD Connect를 사용하여 Active Directory Federation Services 관리 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="1929a-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="1929a-105">이 문서에서는 Azure AD(Azure Active Directory) Connect를 사용하여 AD FS(Active Directory Federation Services)를 관리 및 사용자 지정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-105">This article describes how to manage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="1929a-106">또한 AD FS 팜의 완벽한 구성을 위해 수행해야 할 수 있는 다른 일반적인 AD FS 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-106">It also includes other common AD FS tasks that you might need to do for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="1929a-107">항목</span><span class="sxs-lookup"><span data-stu-id="1929a-107">Topic</span></span> | <span data-ttu-id="1929a-108">포함된 내용</span><span class="sxs-lookup"><span data-stu-id="1929a-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="1929a-109">**AD FS 관리**</span><span class="sxs-lookup"><span data-stu-id="1929a-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="1929a-110">트러스트 복구</span><span class="sxs-lookup"><span data-stu-id="1929a-110">Repair the trust</span></span>](#repairthetrust) |<span data-ttu-id="1929a-111">Office 365를 사용하여 페더레이션 트러스트를 복구하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-111">How to repair the federation trust with Office 365.</span></span> |
| [<span data-ttu-id="1929a-112">대체 로그인 ID를 사용하여 Azure AD와 페더레이션</span><span class="sxs-lookup"><span data-stu-id="1929a-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="1929a-113">대체 로그인 ID를 사용하여 페더레이션 구성</span><span class="sxs-lookup"><span data-stu-id="1929a-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="1929a-114">AD FS 서버 추가</span><span class="sxs-lookup"><span data-stu-id="1929a-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="1929a-115">추가 AD FS 서버를 사용하여 AD FS 팜을 확장하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-115">How to expand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="1929a-116">AD FS 웹 응용 프로그램 프록시 서버 추가</span><span class="sxs-lookup"><span data-stu-id="1929a-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="1929a-117">추가 WAP(웹 응용 프로그램 프록시) 서버를 사용하여 AD FS 팜을 확장하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-117">How to expand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="1929a-118">페더레이션된 도메인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="1929a-119">페더레이션된 도메인을 추가하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-119">How to add a federated domain.</span></span> |
| [<span data-ttu-id="1929a-120">SSL 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="1929a-120">Update the SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="1929a-121">AD FS 팜에 대한 SSL 인증서를 업데이트하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-121">How to update the SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="1929a-122">**AD FS 사용자 지정**</span><span class="sxs-lookup"><span data-stu-id="1929a-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="1929a-123">사용자 지정 회사 로고 또는 일러스트레이션 추가</span><span class="sxs-lookup"><span data-stu-id="1929a-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="1929a-124">회사 로고와 일러스트레이션을 사용하여 AD FS 로그인 페이지를 사용자 지정하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-124">How to customize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="1929a-125">로그인 설명 추가</span><span class="sxs-lookup"><span data-stu-id="1929a-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="1929a-126">로그인 페이지 설명을 추가하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-126">How to add a sign-in page description.</span></span> |
| [<span data-ttu-id="1929a-127">AD FS 클레임 규칙 수정</span><span class="sxs-lookup"><span data-stu-id="1929a-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="1929a-128">다양한 페더레이션 시나리오에 대한 AD FS 클레임을 수정하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-128">How to modify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="1929a-129">AD FS 관리</span><span class="sxs-lookup"><span data-stu-id="1929a-129">Manage AD FS</span></span>
<span data-ttu-id="1929a-130">Azure AD Connect 마법사를 사용하여 최소한의 사용자의 개입만으로 Azure AD Connect에서 다양한 AD FS 관련 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using the Azure AD Connect wizard.</span></span> <span data-ttu-id="1929a-131">마법사를 실행하여 Azure AD Connect 설치를 완료한 후 다시 마법사를 실행하여 추가 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-131">After you've finished installing Azure AD Connect by running the wizard, you can run the wizard again to perform additional tasks.</span></span>

## <span data-ttu-id="1929a-132">트러스트 복구 <a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="1929a-132">Repair the trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="1929a-133">Azure AD Connect를 사용하여 AD FS와 Azure AD 트러스트의 현재 상태를 확인하고 적절한 조치를 취하여 트러스트를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-133">You can use Azure AD Connect to check the current health of the AD FS and Azure AD trust and take appropriate actions to repair the trust.</span></span> <span data-ttu-id="1929a-134">이러한 단계에 따라 Azure AD 및 AD FS 트러스트를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-134">Follow these steps to repair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="1929a-135">추가 작업 목록에서 **AAD 및 ADFS 트러스트 복구** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-135">Select **Repair AAD and ADFS Trust** from the list of additional tasks.</span></span>
   <span data-ttu-id="1929a-136">![AAD 및 ADFS 트러스트 복구](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="1929a-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="1929a-137">**Azure AD에 연결** 페이지에서 Azure AD에 대한 전역 관리자 자격 증명을 제공하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-137">On the **Connect to Azure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="1929a-138">![Azure에 연결](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="1929a-138">![Connect to Azure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="1929a-139">**원격 액세스 자격 증명** 페이지에서 도메인 관리자에 대한 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-139">On the **Remote access credentials** page, enter the credentials for the domain administrator.</span></span>

   ![원격 액세스 자격 증명](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="1929a-141">**다음**을 클릭한 후 Azure AD Connect가 인증서 상태를 확인하고 문제를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![인증서의 상태](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="1929a-143">**구성 준비** 페이지는 트러스트를 복구하기 위해 수행할 작업 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-143">The **Ready to configure** page shows the list of actions that will be performed to repair the trust.</span></span>

    ![구성 준비](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="1929a-145">**설치** 를 클릭하여 트러스트를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-145">Click **Install** to repair the trust.</span></span>

> [!NOTE]
> <span data-ttu-id="1929a-146">Azure AD Connect는 자체 서명된 인증서에 대해서만 복구 또는 조치를 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="1929a-147">Azure AD Connect에서 타사 인증서를 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="1929a-148"><a name=alternateid></a>대체 ID를 사용하여 Azure AD와 페더레이션</span><span class="sxs-lookup"><span data-stu-id="1929a-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="1929a-149">온-프레미스 UPN(사용자 계정 이름) 및 클라우드 사용자 계정 이름을 동일하게 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-149">It is recommended that the on-premises User Principal Name(UPN) and the cloud User Principal Name are kept the same.</span></span> <span data-ttu-id="1929a-150">온-프레미스 UPN이 라우팅할 수 없는 도메인(예:</span><span class="sxs-lookup"><span data-stu-id="1929a-150">If the on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="1929a-151">Contoso.local)을 사용하거나 로컬 응용 프로그램 종속성으로 인해 변경될 수 없는 경우 대체 로그인 ID를 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-151">Contoso.local) or cannot be changed due to local application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="1929a-152">대체 로그인 ID를 사용하면 사용자가 UPN 이외의 특성(예: 메일)을 사용하여 로그인할 수 있는 로그인 환경을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-152">Alternate login ID allows you to configure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="1929a-153">Azure AD Connect에서 선택할 수 있는 기본 사용자 계정 이름은 Active Directory의 userPrincipalName 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-153">The choice for User Principal Name in Azure AD Connect defaults to the userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="1929a-154">사용자 계정 이름에 대해 다른 특성을 선택하고 AD FS를 사용하여 페더레이션할 경우 Azure AD Connect는 대체 로그인 ID에 맞게 AD FS를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="1929a-155">사용자 계정 이름으로 선택할 수 있는 다른 특성은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![대체 ID 특성 선택 항목](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="1929a-157">AD FS에 대한 대체 로그인 ID 구성은 크게 다음 두 단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="1929a-158">**올바른 발급 클레임 집합 구성**: Azure AD 신뢰 당사자 트러스트의 발급 클레임 규칙이 선택한 UserPrincipalName 특성을 사용자의 대체 ID로 사용하도록 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-158">**Configure the right set of issuance claims**: The issuance claim rules in the Azure AD relying party trust are modified to use the selected UserPrincipalName attribute as the alternate ID of the user.</span></span>
2. <span data-ttu-id="1929a-159">**AD FS 구성에서 대체 로그인 ID를 사용하도록 설정**: AD FS가 대체 ID를 사용하여 해당 포리스트에서 사용자를 조회할 수 있도록 AD FS 구성이 업데이트됩니다</span><span class="sxs-lookup"><span data-stu-id="1929a-159">**Enable alternate login ID in the AD FS configuration**: The AD FS configuration is updated so that AD FS can look up users in the appropriate forests using the alternate ID.</span></span> <span data-ttu-id="1929a-160">이 구성은 Windows Server 2012 R2(KB2919355) 이상의 AD FS에 대해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="1929a-161">AD FS 서버가 2012 R2인 경우 Azure AD Connect는 필요한 KB가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-161">If the AD FS servers are 2012 R2, Azure AD Connect checks for the presence of the required KB.</span></span> <span data-ttu-id="1929a-162">KB가 검색되지 않으면 구성이 완료된 후에 아래와 같이 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-162">If the KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![2012R2의 KB 누락에 대한 경고](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="1929a-164">KB가 누락된 경우 구성 문제를 수정하려면 필요한 [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590)를 설치한 다음 [AAD 및 AD FS 트러스트 복구](#repairthetrust)를 사용하여 트러스트를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-164">To rectify the configuration in case of missing KB, install the required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair the trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="1929a-165">alternateID 및 수동 구성 단계에 대한 자세한 내용은 [대체 로그인 ID 구성](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1929a-165">For more information on alternateID and steps to manually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="1929a-166">AD FS 서버 추가 <a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="1929a-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="1929a-167">AD FS 서버를 추가하려면 Azure AD Connect는 PFX 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-167">To add an AD FS server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="1929a-168">따라서 Azure AD Connect를 사용하여 AD FS 팜을 구성한 경우에만 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-168">Therefore, you can perform this operation only if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="1929a-169">**추가 페더레이션 서버 배포**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![추가 페더레이션 서버](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="1929a-171">**Azure AD에 연결** 페이지에서 Azure AD에 대한 전역 관리자 자격 증명을 입력하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-171">On the **Connect to Azure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Azure에 연결](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="1929a-173">도메인 관리자 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-173">Provide the domain administrator credentials.</span></span>

   ![도메인 관리자 자격 증명](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="1929a-175">Azure AD Connect는 Azure AD Connect를 사용하여 새 AD FS 팜을 구성하는 동안 제공한 PFX 파일의 암호를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-175">Azure AD Connect asks for the password of the PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="1929a-176">**암호 입력** 을 클릭하여 PFX 파일에 대한 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-176">Click **Enter Password** to provide the password for the PFX file.</span></span>

   ![인증서 암호](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![SSL 인증서 지정](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="1929a-179">**AD FS 서버** 페이지에서 AD FS 팜에 추가할 서버 이름 또는 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-179">On the **AD FS Servers** page, enter the server name or IP address to be added to the AD FS farm.</span></span>

   ![AD FS 서버](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="1929a-181">**다음**을 클릭하고 마지막 **구성** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-181">Click **Next**, and go through the final **Configure** page.</span></span> <span data-ttu-id="1929a-182">Azure AD Connect가 AD FS 팜에 서버 추가를 완료한 후 연결을 확인하는 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-182">After Azure AD Connect has finished adding the servers to the AD FS farm, you will be given the option to verify the connectivity.</span></span>

   ![구성 준비](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![설치 완료](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="1929a-185">AD FS WAP 서버 추가 <a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="1929a-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="1929a-186">WAP 서버를 추가하려면 Azure AD Connect는 PFX 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-186">To add a WAP server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="1929a-187">따라서 Azure AD Connect를 사용하여 AD FS 팜을 구성한 경우에만 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-187">Therefore, you can only perform this operation if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="1929a-188">사용 가능한 작업 목록에서 **웹 응용 프로그램 프록시 배포** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-188">Select **Deploy Web Application Proxy** from the list of available tasks.</span></span>

   ![웹 응용 프로그램 프록시 배포](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="1929a-190">Azure 전역 관리자 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-190">Provide the Azure global administrator credentials.</span></span>

   ![Azure에 연결](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="1929a-192">**SSL 인증서 지정** 페이지에서 Azure AD Connect를 사용하여 AD FS 팜을 구성했을 때 제공한 PFX 파일에 대한 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-192">On the **Specify SSL certificate** page, provide the password for the PFX file that you provided when you configured the AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="1929a-193">![인증서 암호](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="1929a-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![SSL 인증서 지정](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="1929a-195">WAP 서버로 추가할 서버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-195">Add the server to be added as a WAP server.</span></span> <span data-ttu-id="1929a-196">WAP 서버가 도메인에 가입되지 않을 수 있으므로 마법사가 추가 중인 서버에 대한 관리자 자격 증명을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-196">Because the WAP server might not be joined to the domain, the wizard asks for administrative credentials to the server being added.</span></span>

   ![관리 서버 자격 증명](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="1929a-198">**프록시 트러스트 자격 증명** 페이지에서 프록시 트러스트를 구성하고 AD FS 팜의 주 서버에 액세스하는 관리자 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-198">On the **Proxy trust credentials** page, provide administrative credentials to configure the proxy trust and access the primary server in the AD FS farm.</span></span>

   ![프록시 트러스트 자격 증명](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="1929a-200">**구성 준비** 페이지에서 마법사는 수행할 작업 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-200">On the **Ready to configure** page, the wizard shows the list of actions that will be performed.</span></span>

   ![구성 준비](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="1929a-202">**설치** 를 클릭하여 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-202">Click **Install** to finish the configuration.</span></span> <span data-ttu-id="1929a-203">구성이 완료되면 마법사에서 서버에 대한 연결을 확인하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-203">After the configuration is complete, the wizard gives you the option to verify the connectivity to the servers.</span></span> <span data-ttu-id="1929a-204">**확인** 을 클릭하여 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-204">Click **Verify** to check connectivity.</span></span>

   ![설치 완료](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="1929a-206">페더레이션된 도메인을 추가합니다. <a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="1929a-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="1929a-207">Azure AD Connect를 사용하면 Azure AD와 페더레이션될 도메인을 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-207">It's easy to add a domain to be federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="1929a-208">Azure AD Connect는 페더레이션에 대한 도메인을 추가하고 Azure AD와 페더레이션된 여러 도메인이 있는 경우 발급자를 올바르게 반영하기 위해 클레임 규칙을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-208">Azure AD Connect adds the domain for federation and modifies the claim rules to correctly reflect the issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="1929a-209">페더레이션된 도메인을 추가하려면 작업 **추가 Azure AD 도메인 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-209">To add a federated domain, select the task **Add an additional Azure AD domain**.</span></span>

   ![추가 Azure AD 도메인](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="1929a-211">마법사의 다음 페이지에서 Azure AD 전역 관리자 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-211">On the next page of the wizard, provide the global administrator credentials for Azure AD.</span></span>

   ![Azure에 연결](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="1929a-213">**원격 액세스 자격 증명** 페이지에서 도메인 관리자 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-213">On the **Remote access credentials** page, provide the domain administrator credentials.</span></span>

   ![원격 액세스 자격 증명](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="1929a-215">다음 페이지에서 마법사는 온-프레미스 디렉터리를 페더레이션할 수 있는 Azure AD 도메인 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-215">On the next page, the wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="1929a-216">목록에서 도메인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-216">Choose the domain from the list.</span></span>

   ![Azure AD 도메인](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="1929a-218">도메인을 선택하면 마법사는 마법사가 수행할 추가 작업 및 구성의 영향에 대한 적절한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-218">After you choose the domain, the wizard provides you with appropriate information about further actions that the wizard will take and the impact of the configuration.</span></span> <span data-ttu-id="1929a-219">경우에 따라 Azure AD에서 아직 확인되지 않은 도메인을 선택하는 경우 마법사는 도메인을 확인하는 데 유용한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-219">In some cases, if you select a domain that isn't yet verified in Azure AD, the wizard provides you with information to help you verify the domain.</span></span> <span data-ttu-id="1929a-220">자세한 내용은 [Azure Active Directory에 사용자 지정 도메인 이름 추가](../active-directory-add-domain.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1929a-220">See [Add your custom domain name to Azure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="1929a-221">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-221">Click **Next**.</span></span> <span data-ttu-id="1929a-222">**구성 준비** 페이지에 Azure AD Connect가 수행할 작업 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-222">The **Ready to configure** page shows the list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="1929a-223">**설치** 를 클릭하여 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-223">Click **Install** to finish the configuration.</span></span>

   ![구성 준비](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="1929a-225">추가 페더레이션된 도메인의 사용자는 Azure AD에 로그인하기 전에 동기화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-225">Users from the added federated domain must be synchronized before they will be able to login to Azure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="1929a-226">AD FS 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="1929a-226">AD FS customization</span></span>
<span data-ttu-id="1929a-227">다음 섹션에서는 AD FS 로그인 페이지를 사용자 지정할 때 수행해야 할 수 있는 일반적인 작업 중 일부에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-227">The following sections provide details about some of the common tasks that you might have to perform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="1929a-228">사용자 지정 회사 로고 또는 일러스트레이션 추가 <a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="1929a-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="1929a-229">**로그인** 페이지에 표시되는 회사의 로고를 변경하려면 다음 Windows PowerShell cmdlet 및 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-229">To change the logo of the company that's displayed on the **Sign-in** page, use the following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="1929a-230">로고의 권장 크기는 파일 크기가 10KB 이하인 96dpi에서 260x35입니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-230">The recommended dimensions for the logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="1929a-231">*TargetName* 매개 변수는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-231">The *TargetName* parameter is required.</span></span> <span data-ttu-id="1929a-232">AD FS와 함께 제공되는 기본 테마의 이름은 Default입니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-232">The default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="1929a-233">로그인 설명 추가 <a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="1929a-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="1929a-234">**로그인 페이지**에 로그인 페이지 설명을 추가하려면 다음 Windows PowerShell cmdlet 및 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-234">To add a sign-in page description to the **Sign-in page**, use the following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="1929a-235">AD FS 클레임 규칙 수정 <a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="1929a-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="1929a-236">AD FS는 사용자 지정 클레임 규칙을 만드는 데 사용할 수 있는 다양한 클레임 언어를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-236">AD FS supports a rich claim language that you can use to create custom claim rules.</span></span> <span data-ttu-id="1929a-237">자세한 내용은 [클레임 규칙 언어의 역할](https://technet.microsoft.com/library/dd807118.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1929a-237">For more information, see [The Role of the Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="1929a-238">다음 섹션에서는 Azure AD 및 AD FS 페더레이션에 관련된 몇 가지 시나리오에 대한 사용자 지정 규칙을 작성할 수 있는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-238">The following sections describe how you can write custom rules for some scenarios that relate to Azure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-the-attribute"></a><span data-ttu-id="1929a-239">특성에 나타나는 값에서 변경이 불가능한 ID 조건부</span><span class="sxs-lookup"><span data-stu-id="1929a-239">Immutable ID conditional on a value being present in the attribute</span></span>
<span data-ttu-id="1929a-240">Azure AD Connect에서는 개체가 Azure AD에 동기화되는 경우 원본 앵커로 사용할 특성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-240">Azure AD Connect lets you specify an attribute to be used as a source anchor when objects are synced to Azure AD.</span></span> <span data-ttu-id="1929a-241">사용자 지정 특성의 값이 비어 있지 않은 경우 변경이 불가능한 ID 클레임을 발급하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-241">If the value in the custom attribute is not empty, you might want to issue an immutable ID claim.</span></span>

<span data-ttu-id="1929a-242">예를 들어 원본 앵커의 특성으로 **ms-ds-consistencyguid**를 선택하고 특성이 해당 항목에 대한 값을 갖는 경우 **ms-ds-consistencyguid**로 **ImmutableID**를 발급할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-242">For example, you might select **ms-ds-consistencyguid** as the attribute for the source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case the attribute has a value against it.</span></span> <span data-ttu-id="1929a-243">특성에 대한 값이 없는 경우 변경이 불가능한 ID로 **objectGuid**를 발급합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-243">If there's no value against the attribute, issue **objectGuid** as the immutable ID.</span></span> <span data-ttu-id="1929a-244">다음 섹션에 설명된 대로 사용자 지정 클레임 규칙의 집합을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-244">You can construct the set of custom claim rules as described in the following section.</span></span>

<span data-ttu-id="1929a-245">**규칙 1: 쿼리 특성**</span><span class="sxs-lookup"><span data-stu-id="1929a-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="1929a-246">이 규칙에서는 Active Directory의 사용자에 대해 **ms-ds-consistencyguid** 및 **objectGuid**의 값을 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-246">In this rule, you're querying the values of **ms-ds-consistencyguid** and **objectGuid** for the user from Active Directory.</span></span> <span data-ttu-id="1929a-247">AD FS 배포에서 적절한 저장소 이름으로 저장소 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-247">Change the store name to an appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="1929a-248">또한 **objectGuid** 및 **ms-ds-consistencyguid**에 대해 정의된 대로 페더레이션에 대한 적절한 클레임 형식으로 클레임 형식을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-248">Also change the claims type to a proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="1929a-249">또한 **issue**가 아닌 **add**를 사용하여 엔터티에 대해 나가는 발급을 추가하지 않고 단지 중간 값으로 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for the entity, and can use the values as intermediate values.</span></span> <span data-ttu-id="1929a-250">변경이 불가능한 ID로 사용할 값을 설정한 후 이후 규칙에서 클레임을 발급합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-250">You will issue the claim in a later rule after you establish which value to use as the immutable ID.</span></span>

<span data-ttu-id="1929a-251">**규칙 2: 사용자에 대한 ms-ds-consistencyguid가 있는지 확인**</span><span class="sxs-lookup"><span data-stu-id="1929a-251">**Rule 2: Check if ms-ds-consistencyguid exists for the user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="1929a-252">이 규칙은 단순히 사용자에 대해 채워진 **ms-ds-consistencyguid**가 없는 경우 **useguid**로 설정된 **idflag**라는 임시 플래그를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-252">This rule defines a temporary flag called **idflag** that is set to **useguid** if there's no **ms-ds-consistencyguid** populated for the user.</span></span> <span data-ttu-id="1929a-253">이 이면에 숨겨진 논리는 AD FS가 빈 클레임을 허용하지 않는다는 사실입니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-253">The logic behind this is the fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="1929a-254">따라서 규칙 1에서 http://contoso.com/ws/2016/02/identity/claims/objectguid 및 http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid 클레임을 추가하면 사용자에 대해 값이 채워진 경우에만 **msdsconsistencyguid** 클레임을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if the value is populated for the user.</span></span> <span data-ttu-id="1929a-255">채워지지 않은 경우 AD FS는 빈 값을 갖는 것을 확인하고 즉시 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="1929a-256">모든 개체에는 **objectGuid**가 있으므로 규칙 1이 실행된 후 항상 클레임이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="1929a-257">**규칙 3: 있는 경우 변경이 불가능한 ID로 ms-ds-consistencyguid 발급**</span><span class="sxs-lookup"><span data-stu-id="1929a-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="1929a-258">이는 암시적 **Exist** 확인입니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="1929a-259">클레임에 대한 값이 있으면 변경이 불가능한 ID로 이를 발급합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-259">If the value for the claim exists, then issue that as the immutable ID.</span></span> <span data-ttu-id="1929a-260">이전 예제는 **nameidentifier** 클레임을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-260">The previous example uses the **nameidentifier** claim.</span></span> <span data-ttu-id="1929a-261">사용자 환경에서 변경이 불가능한 ID에 대한 적절한 클레임 유형으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-261">You'll have to change this to the appropriate claim type for the immutable ID in your environment.</span></span>

<span data-ttu-id="1929a-262">**규칙 4: ms-ds-consistencyGuid가 없는 경우 변경이 불가능한 ID로 objectGuid 발급**</span><span class="sxs-lookup"><span data-stu-id="1929a-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="1929a-263">이 규칙에서는 단순히 임시 플래그 **idflag**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-263">In this rule, you're simply checking the temporary flag **idflag**.</span></span> <span data-ttu-id="1929a-264">해당 값에 따라 클레임 발급 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-264">You decide whether to issue the claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="1929a-265">이러한 규칙 시퀀스는 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-265">The sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="1929a-266">하위 도메인 UPN을 사용한 SSO</span><span class="sxs-lookup"><span data-stu-id="1929a-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="1929a-267">[새 페더레이션된 도메인 추가](active-directory-aadconnect-federation-management.md#addfeddomain)에 설명된 대로 Azure AD Connect를 사용하여 페더레이션될 도메인을 둘 이상 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-267">You can add more than one domain to be federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="1929a-268">페더레이션된 루트 도메인이 자식도 포함하기 때문에 발급자 ID는 하위 도메인이 아닌 루트 도메인과 일치해야 하므로 UPN(사용자 계정 이름) 클레임을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-268">You must modify the user principal name (UPN) claim so that the issuer ID corresponds to the root domain and not the subdomain, because the federated root domain also covers the child.</span></span>

<span data-ttu-id="1929a-269">기본적으로 발급자 ID에 대한 클레임 규칙은 다음과 같이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-269">By default, the claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![기본 발급자 ID 클레임](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="1929a-271">기본 규칙은 UPN 접미사를 가져다가 발급자 ID 클레임에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-271">The default rule simply takes the UPN suffix and uses it in the issuer ID claim.</span></span> <span data-ttu-id="1929a-272">예를 들어 John은 sub.contoso.com의 사용자이고 contoso.com은 Azure AD를 사용하여 페더레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="1929a-273">John은 Azure AD에 로그인하는 동안 사용자 이름으로 john@sub.contoso.com을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-273">John enters john@sub.contoso.com as the username while signing in to Azure AD.</span></span> <span data-ttu-id="1929a-274">AD FS에서 기본 발급자 ID 클레임 규칙은 다음과 같은 방식으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-274">The default issuer ID claim rule in AD FS handles it in the following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="1929a-275">**클레임 값:** http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="1929a-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="1929a-276">발급자 클레임 값에 루트 도메인을 포함시키려면 다음과 일치하도록 클레임 규칙을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-276">To have only the root domain in the issuer claim value, change the claim rule to match the following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="1929a-277">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1929a-277">Next steps</span></span>
<span data-ttu-id="1929a-278">[사용자 로그인 옵션](active-directory-aadconnect-user-signin.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1929a-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
