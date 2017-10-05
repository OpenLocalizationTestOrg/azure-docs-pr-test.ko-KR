---
title: "인증서와 함께 Azure AD Reporting API를 사용하여 데이터 가져오기 | Microsoft Docs"
description: "인증서 자격 증명과 함께 Azure AD Reporting API를 사용하여 사용자 개입 없이 디렉터리에서 데이터를 가져오는 방법에 대해 설명합니다."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: c1345dcda6e52267a8037ffd7207e6bc3b0d3b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-data-using-the-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="68c1b-103">인증서와 함께 Azure AD Reporting API를 사용하여 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="68c1b-103">Get data using the Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="68c1b-104">이 문서에서는 인증서 자격 증명과 함께 Azure AD Reporting API를 사용하여 사용자 개입 없이 디렉터리에서 데이터를 가져오는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-104">This article discusses how to use the Azure AD Reporting API with certificate credentials to get data from directories without user intervention.</span></span> 

## <a name="use-the-azure-ad-reporting-api"></a><span data-ttu-id="68c1b-105">Azure AD Reporting API 사용</span><span class="sxs-lookup"><span data-stu-id="68c1b-105">Use the Azure AD Reporting API</span></span> 
<span data-ttu-id="68c1b-106">Azure AD Reporting API은 다음 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-106">Azure AD Reporting API requires that you complete the following steps:</span></span>
 *  <span data-ttu-id="68c1b-107">필수 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="68c1b-107">Install prerequisites</span></span>
 *  <span data-ttu-id="68c1b-108">앱에서 인증서 설정</span><span class="sxs-lookup"><span data-stu-id="68c1b-108">Set the certificate in your app</span></span>
 *  <span data-ttu-id="68c1b-109">액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="68c1b-109">Get an access token</span></span>
 *  <span data-ttu-id="68c1b-110">액세스 토큰을 사용하여 Graph API 호출</span><span class="sxs-lookup"><span data-stu-id="68c1b-110">Use the access token to call the Graph API</span></span>

<span data-ttu-id="68c1b-111">원본 코드에 대한 정보는 [보고서 API 모듈 활용](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68c1b-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="68c1b-112">필수 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="68c1b-112">Install prerequisites</span></span>
<span data-ttu-id="68c1b-113">Azure AD PowerShell V2 및 AzureADUtils 모듈을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-113">You will need to have Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="68c1b-114">[Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md)의 지침에 따라 Azure AD Powershell V2를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-114">Download and install Azure AD Powershell V2, following the instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="68c1b-115">[AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1)에서 Azure AD 유틸리티 모듈을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-115">Download the Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="68c1b-116">이 모듈에서는 다음을 비롯한 몇 가지 유틸리티 cmdlet을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="68c1b-117">NuGet을 사용하는 최신 버전의 ADAL</span><span class="sxs-lookup"><span data-stu-id="68c1b-117">The latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="68c1b-118">ADAL을 사용하는 사용자, 응용 프로그램 키 및 인증서의 액세스 토큰</span><span class="sxs-lookup"><span data-stu-id="68c1b-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="68c1b-119">Graph API를 처리하는 페이지 단위의 결과</span><span class="sxs-lookup"><span data-stu-id="68c1b-119">Graph API handling paged results</span></span>

<span data-ttu-id="68c1b-120">**Azure AD 유틸리티 모듈을 설치하려면:**</span><span class="sxs-lookup"><span data-stu-id="68c1b-120">**To install the Azure AD Utils module:**</span></span>

1. <span data-ttu-id="68c1b-121">디렉터리를 만들어서 유틸리티 모듈(예: c:\azureAD)을 저장하고 GitHub에서 모듈을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-121">Create a directory to save the utilities module (for example, c:\azureAD) and download the module from GitHub.</span></span>
2. <span data-ttu-id="68c1b-122">PowerShell 세션을 열고 방금 만든 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-122">Open a PowerShell session, and go to the directory you just created.</span></span> 
3. <span data-ttu-id="68c1b-123">모듈을 가져오고 Install-AzureADUtilsModule cmdlet을 사용하여 PowerShell 모듈 경로에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-123">Import the module, and install it in the PowerShell module path using the Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="68c1b-124">세션은 이 화면과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-124">The session should look similar to this screen:</span></span>

  ![Windows PowerShell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-the-certificate-in-your-app"></a><span data-ttu-id="68c1b-126">앱에서 인증서 설정</span><span class="sxs-lookup"><span data-stu-id="68c1b-126">Set the certificate in your app</span></span>
1. <span data-ttu-id="68c1b-127">앱이 이미 있는 경우 Azure Portal에서 개체 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-127">If you already have an app, get its Object ID from the Azure Portal.</span></span> 

  ![Azure 포털](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="68c1b-129">PowerShell 세션을 열고 Connect-AzureAD cmdlet을 사용하여 Azure AD에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-129">Open a PowerShell session and connect to Azure AD using the Connect-AzureAD cmdlet.</span></span>

  ![Azure 포털](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="68c1b-131">AzureADUtils에서 New-AzureADApplicationCertificateCredential cmdlet을 사용하여 여기에 인증서 자격 증명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-131">Use the New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils to add a certificate credential to it.</span></span> 

>[!Note]
><span data-ttu-id="68c1b-132">인증서 개체뿐만 아니라 이전에 캡처한 응용 프로그램 개체 ID를 제공해야 합니다(Cert: 드라이브를 사용하여 가져옴).</span><span class="sxs-lookup"><span data-stu-id="68c1b-132">You need to provide the application Object ID that you captured earlier, as well as the certificate object (get this using the Cert: drive).</span></span>
>


  ![Azure 포털](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="68c1b-134">액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="68c1b-134">Get an access token</span></span>

<span data-ttu-id="68c1b-135">액세스 토큰을 가져오려면 AzureADUtils에서 Get-AzureADGraphAPIAccessTokenFromCert cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-135">To get an access token, use the Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="68c1b-136">마지막 섹션에서 사용한 개체 ID가 아닌 응용 프로그램 ID를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-136">You need to use the Application ID instead of the Object ID that you used in the last section.</span></span>
>

 ![Azure 포털](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-the-access-token-to-call-the-graph-api"></a><span data-ttu-id="68c1b-138">액세스 토큰을 사용하여 Graph API 호출</span><span class="sxs-lookup"><span data-stu-id="68c1b-138">Use the access token to call the Graph API</span></span>

<span data-ttu-id="68c1b-139">이제 스크립트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-139">Now you can create the script.</span></span> <span data-ttu-id="68c1b-140">다음은 AzureADUtils에서 Invoke-AzureADGraphAPIQuery cmdlet을 사용하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-140">Below is an example using the Invoke-AzureADGraphAPIQuery cmdlet from the AzureADUtils.</span></span> <span data-ttu-id="68c1b-141">이 cmdlet은 여러 페이지 단위의 결과를 처리한 다음 PowerShell 파이프라인에 해당 결과를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-141">This cmdlet handles multi-paged results, and then sends those results to the PowerShell pipeline.</span></span> 

 ![Azure 포털](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="68c1b-143">이제 CSV로 내보내고 SIEM 시스템에 저장할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-143">You are now ready to export to a CSV and save to a SIEM system.</span></span> <span data-ttu-id="68c1b-144">예약된 태스크에서 스크립트를 래핑하여 원본 코드에서 응용 프로그램 키를 저장하지 않고 주기적으로 테넌트에서 Azure AD 데이터를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68c1b-144">You can also wrap your script in a scheduled task to get Azure AD data from your tenant periodically without having to store application keys in the source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="68c1b-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68c1b-145">Next steps</span></span>
[<span data-ttu-id="68c1b-146">Azure ID 관리의 기본 항목</span><span class="sxs-lookup"><span data-stu-id="68c1b-146">The fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



