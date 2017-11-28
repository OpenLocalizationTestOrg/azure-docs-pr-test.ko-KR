---
title: "Microsoft 클라우드 독일의 Azure AD Connect"
description: "Azure AD Connect는 온-프레미스 디렉터리와 Azure Active Directory를 통합니다. 이렇게 하면 Azure AD와 통합된 Office 365, Azure, 및 SaaS 응용 프로그램에 대한 공통 ID를 제공할 수 있습니다."
keywords: "Azure AD Connect 소개, Azure AD Connect 개요, Azure AD Connect 정의, Active Directory 설치, 독일, Black Forest"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4c55b116c0dc080ae316caca873a7b693caa793b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="06cfc-105">Microsoft 클라우드 독일의 Azure AD Connect - 공개 미리 보기</span><span class="sxs-lookup"><span data-stu-id="06cfc-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="06cfc-106">소개</span><span class="sxs-lookup"><span data-stu-id="06cfc-106">Introduction</span></span>
<span data-ttu-id="06cfc-107">Azure AD Connect는 온-프레미스 Active Directory와 Azure Active Directory 간의 동기화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="06cfc-108">현재 [Microsoft 클라우드 독일](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) 에 있는 대부분의 시나리오는 연산자에 의해 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-108">Currently, many of the scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by the operator.</span></span> <span data-ttu-id="06cfc-109">Microsoft 클라우드 독일을 사용할 경우 다음을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-109">When using Microsoft Cloud Germany, you must be aware of the following:</span></span>

* <span data-ttu-id="06cfc-110">동기화가 성공적으로 수행되려면 다음 URL은 프록시 서버에 대해 열려 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-110">The following URLs must be opened on a proxy server for synchronization to occur successfully:</span></span>
  
  * <span data-ttu-id="06cfc-111">*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="06cfc-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="06cfc-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="06cfc-112">*.windows.net</span></span>
  * * <span data-ttu-id="06cfc-113">인증서 해지 목록</span><span class="sxs-lookup"><span data-stu-id="06cfc-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="06cfc-114">Azure AD 디렉터리에 로그인할 경우 onmicrosoft.de 도메인의 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-114">When you sign in to your Azure AD directory, you must use an account in the onmicrosoft.de domain.</span></span>
* <span data-ttu-id="06cfc-115">사용할 수 없는 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-115">The following features are not available:</span></span>
  * <span data-ttu-id="06cfc-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="06cfc-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="06cfc-117">자동 업데이트</span><span class="sxs-lookup"><span data-stu-id="06cfc-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="06cfc-118">다운로드</span><span class="sxs-lookup"><span data-stu-id="06cfc-118">Download</span></span>
<span data-ttu-id="06cfc-119">포털 내의 Azure AD Connect 블레이드에서 Azure AD Connect를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-119">You can download Azure AD Connect from the Azure AD Connect blade within the portal.</span></span>  <span data-ttu-id="06cfc-120">아래 지침을 사용하여 Azure AD Connect 블레이드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-120">Use the instructions below to locate the Azure AD Connect blade.</span></span>

### <a name="the-azure-ad-connect-blade"></a><span data-ttu-id="06cfc-121">Azure AD Connect 블레이드</span><span class="sxs-lookup"><span data-stu-id="06cfc-121">The Azure AD Connect Blade</span></span>
<span data-ttu-id="06cfc-122">Azure Portal에 로그인하면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-122">Once you have signed in to the Azure portal, do the following:</span></span>

1. <span data-ttu-id="06cfc-123">찾아보기로 이동</span><span class="sxs-lookup"><span data-stu-id="06cfc-123">Go to Browse</span></span>
2. <span data-ttu-id="06cfc-124">Azure Active Directory 선택</span><span class="sxs-lookup"><span data-stu-id="06cfc-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="06cfc-125">그런 다음 Azure AD Connect 선택</span><span class="sxs-lookup"><span data-stu-id="06cfc-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="06cfc-126">다음이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-126">You should see the following:</span></span>

![Azure AD Connect 블레이드](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="06cfc-128">다음 테이블에서는 블레이드에 표시된 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-128">The following table describes the features shown in the blade.</span></span>

| <span data-ttu-id="06cfc-129">제목</span><span class="sxs-lookup"><span data-stu-id="06cfc-129">Title</span></span> | <span data-ttu-id="06cfc-130">설명</span><span class="sxs-lookup"><span data-stu-id="06cfc-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="06cfc-131">동기화 상태</span><span class="sxs-lookup"><span data-stu-id="06cfc-131">SYNC STATUS</span></span> |<span data-ttu-id="06cfc-132">동기화가 활성화되었는지 아니면 비활성화되었는지 여부를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="06cfc-133">최신 동기화</span><span class="sxs-lookup"><span data-stu-id="06cfc-133">LAST SYNC</span></span> |<span data-ttu-id="06cfc-134">마지막으로 성공한 동기화가 완료된 시점입니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-134">The last time a successful sync completed.</span></span> |
| <span data-ttu-id="06cfc-135">페더레이션된 도메인</span><span class="sxs-lookup"><span data-stu-id="06cfc-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="06cfc-136">현재 구성된 페더레이션된 도메인의 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-136">Shows the number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="06cfc-137">설치</span><span class="sxs-lookup"><span data-stu-id="06cfc-137">Installation</span></span>
<span data-ttu-id="06cfc-138">Azure AD Connect를 설치하려면 [여기](active-directory-aadconnect.md#install-azure-ad-connect)에서 설명서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-138">To install Azure AD Connect, you can use the documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="06cfc-139">고급 기능 및 추가 정보</span><span class="sxs-lookup"><span data-stu-id="06cfc-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="06cfc-140">사용자 지정 설정이나 고급 구성에 대한 추가 정보 및 지침은 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="06cfc-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="06cfc-141">이 페이지는 추가 지침에 대한 정보 및 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="06cfc-141">This page provides information and links to additional guidance.</span></span>

