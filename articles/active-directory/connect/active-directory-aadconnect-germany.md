---
title: "AD aaaAzure Microsoft 클라우드 독일에 연결"
description: "Azure AD Connect는 온-프레미스 디렉터리와 Azure Active Directory를 통합니다. 이렇게 하면 tooprovide Office 365, Azure 및 SaaS 응용 프로그램에 대 한 일반 id를 Azure AD와 통합 되어 있습니다."
keywords: "소개 tooAzure AD Connect, Azure AD Connect 개요, Azure AD Connect 이란 active directory, 독일에 블랙 포리스트를 설치 합니다."
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
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="c8bcf-105">Microsoft 클라우드 독일의 Azure AD Connect - 공개 미리 보기</span><span class="sxs-lookup"><span data-stu-id="c8bcf-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="c8bcf-106">소개</span><span class="sxs-lookup"><span data-stu-id="c8bcf-106">Introduction</span></span>
<span data-ttu-id="c8bcf-107">Azure AD Connect는 온-프레미스 Active Directory와 Azure Active Directory 간의 동기화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="c8bcf-108">현재 대부분의 hello 시나리오의 [Microsoft 클라우드 독일](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) hello 연산자에서 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-108">Currently, many of hello scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by hello operator.</span></span> <span data-ttu-id="c8bcf-109">Microsoft 클라우드 독일을 사용할 때는 hello 다음 중 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-109">When using Microsoft Cloud Germany, you must be aware of hello following:</span></span>

* <span data-ttu-id="c8bcf-110">hello 성공적으로 다음 Url 동기화 toooccur에 프록시 서버에 열려 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-110">hello following URLs must be opened on a proxy server for synchronization toooccur successfully:</span></span>
  
  * <span data-ttu-id="c8bcf-111">*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="c8bcf-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="c8bcf-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="c8bcf-112">*.windows.net</span></span>
  * * <span data-ttu-id="c8bcf-113">인증서 해지 목록</span><span class="sxs-lookup"><span data-stu-id="c8bcf-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="c8bcf-114">Tooyour Azure AD 디렉터리에 로그인 할 때 hello onmicrosoft.de 도메인의 계정을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-114">When you sign in tooyour Azure AD directory, you must use an account in hello onmicrosoft.de domain.</span></span>
* <span data-ttu-id="c8bcf-115">같은 기능 hello 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-115">hello following features are not available:</span></span>
  * <span data-ttu-id="c8bcf-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="c8bcf-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="c8bcf-117">자동 업데이트</span><span class="sxs-lookup"><span data-stu-id="c8bcf-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="c8bcf-118">다운로드</span><span class="sxs-lookup"><span data-stu-id="c8bcf-118">Download</span></span>
<span data-ttu-id="c8bcf-119">Hello Azure AD Connect 블레이드 hello 포털 내에서 Azure AD Connect를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-119">You can download Azure AD Connect from hello Azure AD Connect blade within hello portal.</span></span>  <span data-ttu-id="c8bcf-120">Toolocate hello Azure AD Connect 블레이드 아래의 hello 지침을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-120">Use hello instructions below toolocate hello Azure AD Connect blade.</span></span>

### <a name="hello-azure-ad-connect-blade"></a><span data-ttu-id="c8bcf-121">Azure AD Connect 블레이드 hello</span><span class="sxs-lookup"><span data-stu-id="c8bcf-121">hello Azure AD Connect Blade</span></span>
<span data-ttu-id="c8bcf-122">Toohello Azure 포털에에서 로그인 하면 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-122">Once you have signed in toohello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="c8bcf-123">TooBrowse 이동</span><span class="sxs-lookup"><span data-stu-id="c8bcf-123">Go tooBrowse</span></span>
2. <span data-ttu-id="c8bcf-124">Azure Active Directory 선택</span><span class="sxs-lookup"><span data-stu-id="c8bcf-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="c8bcf-125">그런 다음 Azure AD Connect 선택</span><span class="sxs-lookup"><span data-stu-id="c8bcf-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="c8bcf-126">Hello 다음을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-126">You should see hello following:</span></span>

![Azure AD Connect 블레이드](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="c8bcf-128">hello 다음 설명 hello 블레이드에 표시 된 hello 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-128">hello following table describes hello features shown in hello blade.</span></span>

| <span data-ttu-id="c8bcf-129">제목</span><span class="sxs-lookup"><span data-stu-id="c8bcf-129">Title</span></span> | <span data-ttu-id="c8bcf-130">설명</span><span class="sxs-lookup"><span data-stu-id="c8bcf-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c8bcf-131">동기화 상태</span><span class="sxs-lookup"><span data-stu-id="c8bcf-131">SYNC STATUS</span></span> |<span data-ttu-id="c8bcf-132">동기화가 활성화되었는지 아니면 비활성화되었는지 여부를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="c8bcf-133">최신 동기화</span><span class="sxs-lookup"><span data-stu-id="c8bcf-133">LAST SYNC</span></span> |<span data-ttu-id="c8bcf-134">마지막으로 성공한 동기화가 완료 되었습니다 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-134">hello last time a successful sync completed.</span></span> |
| <span data-ttu-id="c8bcf-135">페더레이션된 도메인</span><span class="sxs-lookup"><span data-stu-id="c8bcf-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="c8bcf-136">현재 구성 된 페더레이션된 도메인 hello 수가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-136">Shows hello number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="c8bcf-137">설치</span><span class="sxs-lookup"><span data-stu-id="c8bcf-137">Installation</span></span>
<span data-ttu-id="c8bcf-138">Azure AD Connect tooinstall hello 설명서를 사용할 수 있습니다 [여기](active-directory-aadconnect.md#install-azure-ad-connect)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-138">tooinstall Azure AD Connect, you can use hello documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="c8bcf-139">고급 기능 및 추가 정보</span><span class="sxs-lookup"><span data-stu-id="c8bcf-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="c8bcf-140">사용자 지정 설정이나 고급 구성에 대한 추가 정보 및 지침은 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="c8bcf-141">이 페이지 tooadditional 지침 정보와 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8bcf-141">This page provides information and links tooadditional guidance.</span></span>

