---
title: "Azure Active Directory B2C: 사용자 지정 정책 문제 해결 | Microsoft Docs"
description: "Azure Active Directory에서 사용자 지정 정책을 사용하는 경우 오류를 해결하는 방법을 알아봅니다."
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: joroja
ms.openlocfilehash: 023390ba36a74217503ff8b3076ad17978fe3fb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-ad-b2c-custom-policies-and-identity-experience-framework"></a><span data-ttu-id="e328e-103">Azure AD B2C 사용자 지정 정책 및 Identity Experience Framework 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e328e-103">Troubleshoot Azure AD B2C custom policies and Identity Experience Framework</span></span>

<span data-ttu-id="e328e-104">Azure AD B2C(Azure Active Directory B2C) 사용자 지정 정책을 사용하는 경우 정책 언어 XML 형식으로 Identity Experience Framework를 설정하는 동안 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-104">If you use Azure Active Directory B2C (Azure AD B2C) custom policies, you might experience challenges setting up the Identity Experience Framework in its policy language XML format.</span></span>  <span data-ttu-id="e328e-105">사용자 지정 정책을 작성하는 방법은 새로운 언어를 배우는 것과 유사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-105">Learning to write custom policies can be like learning a new language.</span></span> <span data-ttu-id="e328e-106">이 문서에서는 문제를 신속하게 검색하고 해결하는 데 유용한 도구와 팁을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-106">In this article, we describe tools and tips that can help you quickly discover and resolve issues.</span></span> 

> [!NOTE]
> <span data-ttu-id="e328e-107">이 문서에서는 Azure AD B2C 사용자 지정 정책 구성의 문제 해결을 중점적으로 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-107">This article focuses on troubleshooting your Azure AD B2C custom policy configuration.</span></span> <span data-ttu-id="e328e-108">신뢰 당사자 응용 프로그램 또는 ID 라이브러리는 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-108">It doesn't address the relying party application or its identity library.</span></span>

## <a name="xml-editing"></a><span data-ttu-id="e328e-109">XML 편집</span><span class="sxs-lookup"><span data-stu-id="e328e-109">XML editing</span></span>

<span data-ttu-id="e328e-110">사용자 지정 정책 설정에서 가장 일반적인 오류는 형식이 잘못 지정된 XML입니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-110">The most common error in setting up custom policies is improperly formatted XML.</span></span> <span data-ttu-id="e328e-111">좋은 XML 편집기가 거의 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-111">A good XML editor is nearly essential.</span></span> <span data-ttu-id="e328e-112">좋은 XML 편집기는 XML을 기본적으로 표시하고, 콘텐츠를 색상으로 구분하며, 일반적인 용어를 미리 채우고, XML 요소를 인덱싱된 상태로 유지하며, 스키마로 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-112">A good XML editor displays XML natively, color-codes content, prefills common terms, keeps XML elements indexed, and can validate with schema.</span></span> <span data-ttu-id="e328e-113">다음은 권장되는 두 XML 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-113">Here are two of our favorite XML editors:</span></span>

* [<span data-ttu-id="e328e-114">Contact.java</span><span class="sxs-lookup"><span data-stu-id="e328e-114">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* [<span data-ttu-id="e328e-115">메모장++</span><span class="sxs-lookup"><span data-stu-id="e328e-115">Notepad++</span></span>](https://notepad-plus-plus.org/)

<span data-ttu-id="e328e-116">XML 파일을 업로드하기 전에 XML 스키마 유효성 검사가 오류를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-116">XML schema validation identifies errors before you upload your XML file.</span></span> <span data-ttu-id="e328e-117">시작 팩의 루트 폴더에서 XML 스키마 정의 TrustFrameworkPolicy_0.3.0.0.xsd를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-117">In the root folder of the starter pack, get the XML schema definition TrustFrameworkPolicy_0.3.0.0.xsd.</span></span> <span data-ttu-id="e328e-118">자세한 내용을 보려면 XML 편집기 문서에서 *XML 도구* 및 *XML 유효성 검사*를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-118">For more information, in the documentation of your XML editor, look for *XML tools* and *XML validation*.</span></span>

<span data-ttu-id="e328e-119">XML 규칙 검토가 도움이 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-119">You might find a review of XML rules helpful.</span></span> <span data-ttu-id="e328e-120">Azure AD B2C는 검색된 XML 형식 오류를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-120">Azure AD B2C rejects any XML formatting errors that it detects.</span></span> <span data-ttu-id="e328e-121">경우에 따라 형식이 잘못된 XML로 인해 잘못된 오류 메시지가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-121">Occasionally, incorrectly formatted XML might cause error messages that are misleading.</span></span>

## <a name="upload-policies-and-policy-validation"></a><span data-ttu-id="e328e-122">정책 업로드 및 정책 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e328e-122">Upload policies and policy validation</span></span>

 <span data-ttu-id="e328e-123">XML 파일 업로드 유효성 검사는 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-123">XML file upload validation is automatic.</span></span> <span data-ttu-id="e328e-124">대부분의 오류로 인해 업로드가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-124">Most errors cause the upload to fail.</span></span> <span data-ttu-id="e328e-125">유효성 검사에는 업로드하는 정책 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-125">Validation includes the policy file that you are uploading.</span></span> <span data-ttu-id="e328e-126">또한 업로드 파일에서 참조하는 파일 체인(신뢰 당사자 정책 파일, 확장 파일 및 기본 파일)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-126">It also includes the chain of files the upload file refers to (the relying party policy file, the extensions file, and the base file).</span></span> 
 
 <span data-ttu-id="e328e-127">일반적인 유효성 검사 오류는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-127">Common validation errors include the following.</span></span>

<span data-ttu-id="e328e-128">오류 코드 조각: `... makes a reference to ClaimType with id "displaName" but neither the policy nor any of its base policies contain such an element`</span><span class="sxs-lookup"><span data-stu-id="e328e-128">Error snippet: `... makes a reference to ClaimType with id "displaName" but neither the policy nor any of its base policies contain such an element`</span></span>
* <span data-ttu-id="e328e-129">ClaimType 값의 철자가 틀렸거나 ClaimType 값이 스키마에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-129">The ClaimType value might be misspelled, or does not exist in the schema.</span></span>
* <span data-ttu-id="e328e-130">ClaimType 값이 정책 파일 중 하나 이상에 정의되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-130">ClaimType values must be defined in at least one of the files in the policy.</span></span> 
    <span data-ttu-id="e328e-131">예: ` <ClaimType Id="socialIdpUserId">`</span><span class="sxs-lookup"><span data-stu-id="e328e-131">For example: ` <ClaimType Id="socialIdpUserId">`</span></span>
* <span data-ttu-id="e328e-132">ClaimType이 확장 파일에 정의되어 있지만 기본 파일의 TechnicalProfile 값에도 사용된 경우 기본 파일을 업로드하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-132">If ClaimType is defined in the extensions file, but it's also used in a TechnicalProfile value in the base file, uploading the base file results in an error.</span></span>

<span data-ttu-id="e328e-133">오류 코드 조각: `...makes a reference to a ClaimsTransformation with id...`</span><span class="sxs-lookup"><span data-stu-id="e328e-133">Error snippet: `...makes a reference to a ClaimsTransformation with id...`</span></span>
* <span data-ttu-id="e328e-134">오류의 원인은 ClaimType 오류와 동일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-134">The causes for the error might be the same as for the ClaimType error.</span></span>

<span data-ttu-id="e328e-135">오류 코드 조각: `Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order to manage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`</span><span class="sxs-lookup"><span data-stu-id="e328e-135">Error snippet: `Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order to manage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`</span></span>
* <span data-ttu-id="e328e-136">**\<TrustFrameworkPolicy\>** 및 **\<BasePolicy\>** 요소의 TenantId 값이 대상 Azure AD B2C 테넌트와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-136">Check that the TenantId value in the **\<TrustFrameworkPolicy\>** and **\<BasePolicy\>** elements match your target Azure AD B2C tenant.</span></span>  

## <a name="troubleshoot-the-runtime"></a><span data-ttu-id="e328e-137">런타임 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e328e-137">Troubleshoot the runtime</span></span>

* <span data-ttu-id="e328e-138">`Run Now` 및 `https://jwt.io`를 사용하여 웹 또는 모바일 응용 프로그램과 별도로 정책을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-138">Use `Run Now` and `https://jwt.io` to test your policies independently of your web or mobile application.</span></span> <span data-ttu-id="e328e-139">이 웹 사이트는 신뢰 당사자 응용 프로그램처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-139">This website acts like a relying party application.</span></span> <span data-ttu-id="e328e-140">Azure AD B2C 정책에 의해 생성된 JWT(JSON Web Token)의 내용을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-140">It displays the contents of the JSON Web Token (JWT) that is generated by your Azure AD B2C policy.</span></span> <span data-ttu-id="e328e-141">Identity Experience Framework에서 테스트 응용 프로그램을 만들려면 다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-141">To create a test application in Identity Experience Framework, use the following values:</span></span>
    * <span data-ttu-id="e328e-142">이름: TestApp</span><span class="sxs-lookup"><span data-stu-id="e328e-142">Name: TestApp</span></span>
    * <span data-ttu-id="e328e-143">웹앱/Web API: 아니요</span><span class="sxs-lookup"><span data-stu-id="e328e-143">Web App/Web API: No</span></span>
    * <span data-ttu-id="e328e-144">네이티브 클라이언트: 아니요</span><span class="sxs-lookup"><span data-stu-id="e328e-144">Native client: No</span></span>

* <span data-ttu-id="e328e-145">클라이언트 브라우저와 Azure AD B2C 간의 메시지 교환을 추적하려면 [Fiddler](http://www.telerik.com/fiddler)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-145">To trace the exchange of messages between your client browser and Azure AD B2C, use [Fiddler](http://www.telerik.com/fiddler).</span></span> <span data-ttu-id="e328e-146">오케스트레이션 단계에서 사용자 환경이 실패한 위치를 확인하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-146">It can help you get an indication of where your user journey is failing in your orchestration steps.</span></span>

* <span data-ttu-id="e328e-147">**개발 모드**에서 **Application Insights**를 사용하여 Identity Experience Framework 사용자 환경의 활동을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-147">In **Development mode**, use **Application Insights** to trace the activity of your Identity Experience Framework user journey.</span></span> <span data-ttu-id="e328e-148">**개발 모드**에서는 Identity Experience Framework와 기술 프로필에서 정의된 다양한 클레임 공급자(예: ID 공급자, API 기반 서비스, Azure AD B2C 사용자 디렉터리 및 Azure Multi-Factor-Authentication과 같은 기타 서비스) 간의 클레임 교환을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-148">In **Development mode**, you can observe the exchange of claims between the Identity Experience Framework and the various claims providers that are defined by technical profiles, such as identity providers, API-based services, the Azure AD B2C user directory, and other services, like Azure Multi-Factor-Authentication.</span></span>  

## <a name="recommended-practices"></a><span data-ttu-id="e328e-149">권장 사례</span><span class="sxs-lookup"><span data-stu-id="e328e-149">Recommended practices</span></span>

<span data-ttu-id="e328e-150">**여러 버전의 시나리오를 유지하고 응용 프로그램과 함께 프로젝트에 그룹화합니다.**</span><span class="sxs-lookup"><span data-stu-id="e328e-150">**Keep multiple versions of your scenarios. Group them in a project with your application.**</span></span> <span data-ttu-id="e328e-151">기본, 확장 및 신뢰 당사자 파일은 서로 직접 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-151">The base, extensions, and relying party files are directly dependent on each other.</span></span> <span data-ttu-id="e328e-152">그룹으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-152">Save them as a group.</span></span> <span data-ttu-id="e328e-153">새로운 기능이 정책에 추가되면 별도 작업 버전을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-153">As new features are added to your policies, keep separate working versions.</span></span> <span data-ttu-id="e328e-154">상호 작용하는 응용 프로그램 코드를 사용하여 사용자 고유의 파일 시스템에 작업 버전을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-154">Stage working versions in your own file system with the application code they interact with.</span></span>  <span data-ttu-id="e328e-155">응용 프로그램은 테넌트의 여러 다른 신뢰 당사자 정책을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-155">Your applications might invoke many different relying party policies in a tenant.</span></span> <span data-ttu-id="e328e-156">Azure AD B2C 정책에서 예상하는 클레임에 종속될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-156">They might become dependent on the claims that they expect from your Azure AD B2C policies.</span></span>

<span data-ttu-id="e328e-157">**알려진 사용자 환경으로 기술 프로필을 개발 및 테스트합니다.**</span><span class="sxs-lookup"><span data-stu-id="e328e-157">**Develop and test technical profiles with known user journeys.**</span></span> <span data-ttu-id="e328e-158">테스트된 시작 팩 정책을 사용하여 기술 프로파일을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-158">Use tested starter pack policies to set up your technical profiles.</span></span> <span data-ttu-id="e328e-159">고유한 사용자 환경에 통합하기 전에 개별적으로 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-159">Test them separately before you incorporate them into your own user journeys.</span></span>

<span data-ttu-id="e328e-160">**테스트된 기술 프로필을 통해 사용자 환경을 개발 및 테스트합니다.**</span><span class="sxs-lookup"><span data-stu-id="e328e-160">**Develop and test user journeys with tested technical profiles.**</span></span> <span data-ttu-id="e328e-161">사용자 환경의 오케스트레이션 단계를 증분 방식으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-161">Change the orchestration steps of a user journey incrementally.</span></span> <span data-ttu-id="e328e-162">의도한 시나리오를 점진적으로 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-162">Progressively build your intended scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e328e-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e328e-163">Next steps</span></span>

* <span data-ttu-id="e328e-164">GitHub에서 [active-directory-b2c-custom-policy-starterpack](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) .zip 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e328e-164">In GitHub, download the [active-directory-b2c-custom-policy-starterpack] (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) .zip file.</span></span>
