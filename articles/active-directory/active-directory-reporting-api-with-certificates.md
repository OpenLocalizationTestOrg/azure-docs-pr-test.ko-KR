---
title: "인증서를 사용 하 여 Azure AD Reporting API hello aaaGet 데이터를 사용 하 여 | Microsoft Docs"
description: "Toouse 사용자 개입 없이 디렉터리에서 인증서 자격 증명 tooget 데이터를 사용 하 여 Azure AD Reporting API hello 하는 방법에 대해 설명 합니다."
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
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="389b3-103">인증서가 있는 hello Azure AD Reporting API를 사용 하 여 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="389b3-103">Get data using hello Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="389b3-104">이 문서에서는 toouse 사용자 개입 없이 디렉터리에서 인증서 자격 증명 tooget 데이터를 사용 하 여 Azure AD Reporting API hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-104">This article discusses how toouse hello Azure AD Reporting API with certificate credentials tooget data from directories without user intervention.</span></span> 

## <a name="use-hello-azure-ad-reporting-api"></a><span data-ttu-id="389b3-105">사용 하 여 Azure AD Reporting API hello</span><span class="sxs-lookup"><span data-stu-id="389b3-105">Use hello Azure AD Reporting API</span></span> 
<span data-ttu-id="389b3-106">Azure AD Reporting API 단계를 수행 하는 hello를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-106">Azure AD Reporting API requires that you complete hello following steps:</span></span>
 *  <span data-ttu-id="389b3-107">필수 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="389b3-107">Install prerequisites</span></span>
 *  <span data-ttu-id="389b3-108">응용 프로그램에서 hello 인증서를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-108">Set hello certificate in your app</span></span>
 *  <span data-ttu-id="389b3-109">액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="389b3-109">Get an access token</span></span>
 *  <span data-ttu-id="389b3-110">Hello 액세스 토큰 toocall hello Graph API를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="389b3-110">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="389b3-111">원본 코드에 대한 정보는 [보고서 API 모듈 활용](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="389b3-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="389b3-112">필수 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="389b3-112">Install prerequisites</span></span>
<span data-ttu-id="389b3-113">Azure AD PowerShell V2 toohave 및 AzureADUtils 모듈을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-113">You will need toohave Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="389b3-114">다운로드 하 여 Azure AD Powershell V2, hello 지침에 따라 설치 [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-114">Download and install Azure AD Powershell V2, following hello instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="389b3-115">hello Azure AD 유틸리티 모듈 다운로드 [azure Ad/azure-active directory powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1)합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-115">Download hello Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="389b3-116">이 모듈에서는 다음을 비롯한 몇 가지 유틸리티 cmdlet을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="389b3-117">hello Nuget을 사용 하 여 ADAL의 최신 버전</span><span class="sxs-lookup"><span data-stu-id="389b3-117">hello latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="389b3-118">ADAL을 사용하는 사용자, 응용 프로그램 키 및 인증서의 액세스 토큰</span><span class="sxs-lookup"><span data-stu-id="389b3-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="389b3-119">Graph API를 처리하는 페이지 단위의 결과</span><span class="sxs-lookup"><span data-stu-id="389b3-119">Graph API handling paged results</span></span>

<span data-ttu-id="389b3-120">**tooinstall hello Azure AD 유틸리티 모듈:**</span><span class="sxs-lookup"><span data-stu-id="389b3-120">**tooinstall hello Azure AD Utils module:**</span></span>

1. <span data-ttu-id="389b3-121">디렉터리 toosave hello 유틸리티 모듈 (예를 들어 c:\azureAD)을 만들고 GitHub에서 hello 모듈을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-121">Create a directory toosave hello utilities module (for example, c:\azureAD) and download hello module from GitHub.</span></span>
2. <span data-ttu-id="389b3-122">PowerShell 세션을 열고 방금 만든 toohello 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-122">Open a PowerShell session, and go toohello directory you just created.</span></span> 
3. <span data-ttu-id="389b3-123">Hello 모듈 가져오기 및 설치 AzureADUtilsModule hello cmdlet를 사용 하 여 hello PowerShell 모듈 경로에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-123">Import hello module, and install it in hello PowerShell module path using hello Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="389b3-124">hello 세션은 유사한 toothis 화면 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-124">hello session should look similar toothis screen:</span></span>

  ![Windows PowerShell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a><span data-ttu-id="389b3-126">응용 프로그램에서 hello 인증서를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-126">Set hello certificate in your app</span></span>
1. <span data-ttu-id="389b3-127">앱이 이미 있는 경우 hello Azure 포털에서에서 해당 개체 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-127">If you already have an app, get its Object ID from hello Azure Portal.</span></span> 

  ![Azure portal](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="389b3-129">PowerShell 세션을 열고 tooAzure AD 연결 hello 연결-azure Ad cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-129">Open a PowerShell session and connect tooAzure AD using hello Connect-AzureAD cmdlet.</span></span>

  ![Azure portal](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="389b3-131">AzureADUtils tooadd 인증서 자격 증명 tooit에서에서 hello 새로 AzureADApplicationCertificateCredential cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-131">Use hello New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils tooadd a certificate credential tooit.</span></span> 

>[!Note]
><span data-ttu-id="389b3-132">Tooprovide hello 응용 프로그램 개체 ID는 이전에 캡처한 필요한 것은 물론 있습니다 hello 인증서 개체 (이 사용 하 여 hello Cert: 드라이브).</span><span class="sxs-lookup"><span data-stu-id="389b3-132">You need tooprovide hello application Object ID that you captured earlier, as well as hello certificate object (get this using hello Cert: drive).</span></span>
>


  ![Azure portal](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="389b3-134">액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="389b3-134">Get an access token</span></span>

<span data-ttu-id="389b3-135">액세스 토큰을 tooget AzureADUtils에서 hello Get AzureADGraphAPIAccessTokenFromCert cmdlet를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-135">tooget an access token, use hello Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="389b3-136">Hello hello 마지막 섹션에서 사용한 개체 ID 대신 toouse hello 응용 프로그램 ID가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-136">You need toouse hello Application ID instead of hello Object ID that you used in hello last section.</span></span>
>

 ![Azure portal](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a><span data-ttu-id="389b3-138">Hello 액세스 토큰 toocall hello Graph API를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="389b3-138">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="389b3-139">이제 hello 스크립트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-139">Now you can create hello script.</span></span> <span data-ttu-id="389b3-140">다음은 hello AzureADUtils에서에서 Invoke AzureADGraphAPIQuery hello cmdlet을 사용 하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-140">Below is an example using hello Invoke-AzureADGraphAPIQuery cmdlet from hello AzureADUtils.</span></span> <span data-ttu-id="389b3-141">이 Cmdlet이 여러 페이지 단위 결과 처리 한 다음 해당 결과 toohello PowerShell 파이프라인을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-141">This cmdlet handles multi-paged results, and then sends those results toohello PowerShell pipeline.</span></span> 

 ![Azure portal](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="389b3-143">이제 CSV 준비 tooexport tooa 및 tooa SIEM 시스템을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-143">You are now ready tooexport tooa CSV and save tooa SIEM system.</span></span> <span data-ttu-id="389b3-144">또한에 래핑할 수 있습니다 스크립트 예약 된 작업 tooget Azure AD 데이터 테 넌 트 로부터 주기적으로 hello 소스 코드에서 toostore 응용 프로그램 키 필요 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="389b3-144">You can also wrap your script in a scheduled task tooget Azure AD data from your tenant periodically without having toostore application keys in hello source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="389b3-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="389b3-145">Next steps</span></span>
[<span data-ttu-id="389b3-146">hello Azure id 관리 기본 사항</span><span class="sxs-lookup"><span data-stu-id="389b3-146">hello fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



