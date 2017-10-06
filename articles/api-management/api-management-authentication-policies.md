---
title: "API 관리 인증 정책 aaaAzure | Microsoft Docs"
description: "Azure API 관리에 사용할 수 있는 hello 인증 정책에 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="99878-103">API Management 인증 정책</span><span class="sxs-lookup"><span data-stu-id="99878-103">API Management authentication policies</span></span>
<span data-ttu-id="99878-104">이 항목에서는 다음 API 관리 정책 hello에 대 한 대 한 참조를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="99878-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="99878-105">정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="99878-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="99878-106"><a name="AuthenticationPolicies"></a> 인증 정책</span><span class="sxs-lookup"><span data-stu-id="99878-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="99878-107">[기본 사용 인증](api-management-authentication-policies.md#Basic) - 기본 인증을 사용하여 백 엔드 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="99878-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="99878-108">[클라이언트 인증서 사용 인증](api-management-authentication-policies.md#ClientCertificate) - 클라이언트 인증서를 사용하여 백 엔드 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="99878-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="99878-109"><a name="Basic"></a> 기본 사용 인증</span><span class="sxs-lookup"><span data-stu-id="99878-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="99878-110">사용 하 여 hello `authentication-basic` 기본 인증을 사용 하 여 백 엔드 서비스와 정책 tooauthenticate 합니다.</span><span class="sxs-lookup"><span data-stu-id="99878-110">Use hello `authentication-basic` policy tooauthenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="99878-111">이 정책은 효과적으로 hello HTTP 권한 부여 헤더 toohello hello 정책에 제공 된 값 해당 toohello 자격을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="99878-111">This policy effectively sets hello HTTP Authorization header toohello value corresponding toohello credentials provided in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="99878-112">정책 문</span><span class="sxs-lookup"><span data-stu-id="99878-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="99878-113">예</span><span class="sxs-lookup"><span data-stu-id="99878-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="99878-114">요소</span><span class="sxs-lookup"><span data-stu-id="99878-114">Elements</span></span>  
  
|<span data-ttu-id="99878-115">이름</span><span class="sxs-lookup"><span data-stu-id="99878-115">Name</span></span>|<span data-ttu-id="99878-116">설명</span><span class="sxs-lookup"><span data-stu-id="99878-116">Description</span></span>|<span data-ttu-id="99878-117">필수</span><span class="sxs-lookup"><span data-stu-id="99878-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="99878-118">인증-기본</span><span class="sxs-lookup"><span data-stu-id="99878-118">authentication-basic</span></span>|<span data-ttu-id="99878-119">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="99878-119">Root element.</span></span>|<span data-ttu-id="99878-120">예</span><span class="sxs-lookup"><span data-stu-id="99878-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="99878-121">특성</span><span class="sxs-lookup"><span data-stu-id="99878-121">Attributes</span></span>  
  
|<span data-ttu-id="99878-122">이름</span><span class="sxs-lookup"><span data-stu-id="99878-122">Name</span></span>|<span data-ttu-id="99878-123">설명</span><span class="sxs-lookup"><span data-stu-id="99878-123">Description</span></span>|<span data-ttu-id="99878-124">필수</span><span class="sxs-lookup"><span data-stu-id="99878-124">Required</span></span>|<span data-ttu-id="99878-125">기본값</span><span class="sxs-lookup"><span data-stu-id="99878-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="99878-126">username</span><span class="sxs-lookup"><span data-stu-id="99878-126">username</span></span>|<span data-ttu-id="99878-127">Hello 기본 자격 증명의 hello 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="99878-127">Specifies hello username of hello Basic credential.</span></span>|<span data-ttu-id="99878-128">예</span><span class="sxs-lookup"><span data-stu-id="99878-128">Yes</span></span>|<span data-ttu-id="99878-129">해당 없음</span><span class="sxs-lookup"><span data-stu-id="99878-129">N/A</span></span>|  
|<span data-ttu-id="99878-130">암호</span><span class="sxs-lookup"><span data-stu-id="99878-130">password</span></span>|<span data-ttu-id="99878-131">Hello 기본 자격 증명의 hello 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="99878-131">Specifies hello password of hello Basic credential.</span></span>|<span data-ttu-id="99878-132">예</span><span class="sxs-lookup"><span data-stu-id="99878-132">Yes</span></span>|<span data-ttu-id="99878-133">해당 없음</span><span class="sxs-lookup"><span data-stu-id="99878-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="99878-134">사용</span><span class="sxs-lookup"><span data-stu-id="99878-134">Usage</span></span>  
 <span data-ttu-id="99878-135">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="99878-135">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="99878-136">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="99878-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="99878-137">**정책 범위:** API</span><span class="sxs-lookup"><span data-stu-id="99878-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="99878-138"><a name="ClientCertificate"></a> 클라이언트 인증서 사용 인증</span><span class="sxs-lookup"><span data-stu-id="99878-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="99878-139">사용 하 여 hello `authentication-certificate` 클라이언트 인증서를 사용 하 여 백 엔드 서비스와 정책 tooauthenticate 합니다.</span><span class="sxs-lookup"><span data-stu-id="99878-139">Use hello `authentication-certificate` policy tooauthenticate with a backend service using client certificate.</span></span> <span data-ttu-id="99878-140">hello 인증서 필요 toobe [API 관리에 설치](http://go.microsoft.com/fwlink/?LinkID=511599) 첫 번째 지 문으로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99878-140">hello certificate needs toobe [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="99878-141">정책 문</span><span class="sxs-lookup"><span data-stu-id="99878-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="99878-142">예</span><span class="sxs-lookup"><span data-stu-id="99878-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="99878-143">요소</span><span class="sxs-lookup"><span data-stu-id="99878-143">Elements</span></span>  
  
|<span data-ttu-id="99878-144">이름</span><span class="sxs-lookup"><span data-stu-id="99878-144">Name</span></span>|<span data-ttu-id="99878-145">설명</span><span class="sxs-lookup"><span data-stu-id="99878-145">Description</span></span>|<span data-ttu-id="99878-146">필수</span><span class="sxs-lookup"><span data-stu-id="99878-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="99878-147">인증-인증서</span><span class="sxs-lookup"><span data-stu-id="99878-147">authentication-certificate</span></span>|<span data-ttu-id="99878-148">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="99878-148">Root element.</span></span>|<span data-ttu-id="99878-149">예</span><span class="sxs-lookup"><span data-stu-id="99878-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="99878-150">특성</span><span class="sxs-lookup"><span data-stu-id="99878-150">Attributes</span></span>  
  
|<span data-ttu-id="99878-151">이름</span><span class="sxs-lookup"><span data-stu-id="99878-151">Name</span></span>|<span data-ttu-id="99878-152">설명</span><span class="sxs-lookup"><span data-stu-id="99878-152">Description</span></span>|<span data-ttu-id="99878-153">필수</span><span class="sxs-lookup"><span data-stu-id="99878-153">Required</span></span>|<span data-ttu-id="99878-154">기본값</span><span class="sxs-lookup"><span data-stu-id="99878-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="99878-155">thumbprint</span><span class="sxs-lookup"><span data-stu-id="99878-155">thumbprint</span></span>|<span data-ttu-id="99878-156">hello 클라이언트 인증서에 대 한 hello 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="99878-156">hello thumbprint for hello client certificate.</span></span>|<span data-ttu-id="99878-157">예</span><span class="sxs-lookup"><span data-stu-id="99878-157">Yes</span></span>|<span data-ttu-id="99878-158">해당 없음</span><span class="sxs-lookup"><span data-stu-id="99878-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="99878-159">사용</span><span class="sxs-lookup"><span data-stu-id="99878-159">Usage</span></span>  
 <span data-ttu-id="99878-160">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="99878-160">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="99878-161">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="99878-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="99878-162">**정책 범위:** API</span><span class="sxs-lookup"><span data-stu-id="99878-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="99878-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="99878-163">Next steps</span></span>
<span data-ttu-id="99878-164">정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="99878-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  