---
title: "Azure API Management 인증 정책 | Microsoft Docs"
description: "Azure API Management에 사용할 수 있는 인증 정책에 대해 알아봅니다."
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
ms.openlocfilehash: 63ef20a56ab7721f9ecc7025d05963cc4b0c27a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="6ea71-103">API Management 인증 정책</span><span class="sxs-lookup"><span data-stu-id="6ea71-103">API Management authentication policies</span></span>
<span data-ttu-id="6ea71-104">이 토픽에서는 다음 API Management 정책에 대한 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea71-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="6ea71-105">정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ea71-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="6ea71-106"><a name="AuthenticationPolicies"></a> 인증 정책</span><span class="sxs-lookup"><span data-stu-id="6ea71-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="6ea71-107">[기본 사용 인증](api-management-authentication-policies.md#Basic) - 기본 인증을 사용하여 백 엔드 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea71-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="6ea71-108">[클라이언트 인증서 사용 인증](api-management-authentication-policies.md#ClientCertificate) - 클라이언트 인증서를 사용하여 백 엔드 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea71-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="6ea71-109"><a name="Basic"></a> 기본 사용 인증</span><span class="sxs-lookup"><span data-stu-id="6ea71-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="6ea71-110">`authentication-basic` 정책을 사용하여 기본 인증을 사용하는 백 엔드 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea71-110">Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="6ea71-111">이 정책은 HTTP 권한 부여 헤더를 정책에서 제공한 자격 증명에 해당하는 값으로 효과적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea71-111">This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="6ea71-112">정책 명령문</span><span class="sxs-lookup"><span data-stu-id="6ea71-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="6ea71-113">예</span><span class="sxs-lookup"><span data-stu-id="6ea71-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="6ea71-114">요소</span><span class="sxs-lookup"><span data-stu-id="6ea71-114">Elements</span></span>  
  
|<span data-ttu-id="6ea71-115">이름</span><span class="sxs-lookup"><span data-stu-id="6ea71-115">Name</span></span>|<span data-ttu-id="6ea71-116">설명</span><span class="sxs-lookup"><span data-stu-id="6ea71-116">Description</span></span>|<span data-ttu-id="6ea71-117">필수</span><span class="sxs-lookup"><span data-stu-id="6ea71-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="6ea71-118">인증-기본</span><span class="sxs-lookup"><span data-stu-id="6ea71-118">authentication-basic</span></span>|<span data-ttu-id="6ea71-119">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea71-119">Root element.</span></span>|<span data-ttu-id="6ea71-120">예</span><span class="sxs-lookup"><span data-stu-id="6ea71-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="6ea71-121">특성</span><span class="sxs-lookup"><span data-stu-id="6ea71-121">Attributes</span></span>  
  
|<span data-ttu-id="6ea71-122">이름</span><span class="sxs-lookup"><span data-stu-id="6ea71-122">Name</span></span>|<span data-ttu-id="6ea71-123">설명</span><span class="sxs-lookup"><span data-stu-id="6ea71-123">Description</span></span>|<span data-ttu-id="6ea71-124">필수</span><span class="sxs-lookup"><span data-stu-id="6ea71-124">Required</span></span>|<span data-ttu-id="6ea71-125">기본값</span><span class="sxs-lookup"><span data-stu-id="6ea71-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="6ea71-126">username</span><span class="sxs-lookup"><span data-stu-id="6ea71-126">username</span></span>|<span data-ttu-id="6ea71-127">기본 자격 증명의 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea71-127">Specifies the username of the Basic credential.</span></span>|<span data-ttu-id="6ea71-128">예</span><span class="sxs-lookup"><span data-stu-id="6ea71-128">Yes</span></span>|<span data-ttu-id="6ea71-129">해당 없음</span><span class="sxs-lookup"><span data-stu-id="6ea71-129">N/A</span></span>|  
|<span data-ttu-id="6ea71-130">password</span><span class="sxs-lookup"><span data-stu-id="6ea71-130">password</span></span>|<span data-ttu-id="6ea71-131">기본 자격 증명의 비밀번호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea71-131">Specifies the password of the Basic credential.</span></span>|<span data-ttu-id="6ea71-132">예</span><span class="sxs-lookup"><span data-stu-id="6ea71-132">Yes</span></span>|<span data-ttu-id="6ea71-133">해당 없음</span><span class="sxs-lookup"><span data-stu-id="6ea71-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="6ea71-134">사용 현황</span><span class="sxs-lookup"><span data-stu-id="6ea71-134">Usage</span></span>  
 <span data-ttu-id="6ea71-135">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea71-135">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="6ea71-136">**정책 섹션:** 인바운드</span><span class="sxs-lookup"><span data-stu-id="6ea71-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="6ea71-137">**정책 범위:** API</span><span class="sxs-lookup"><span data-stu-id="6ea71-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="6ea71-138"><a name="ClientCertificate"></a> 클라이언트 인증서 사용 인증</span><span class="sxs-lookup"><span data-stu-id="6ea71-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="6ea71-139">`authentication-certificate` 정책을 사용하여 클라이언트 인증서를 사용하는 백 엔드 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea71-139">Use the `authentication-certificate` policy to authenticate with a backend service using client certificate.</span></span> <span data-ttu-id="6ea71-140">먼저 인증서를 [API Management에 설치](http://go.microsoft.com/fwlink/?LinkID=511599)하고 지문으로 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea71-140">The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="6ea71-141">정책 명령문</span><span class="sxs-lookup"><span data-stu-id="6ea71-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="6ea71-142">예</span><span class="sxs-lookup"><span data-stu-id="6ea71-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="6ea71-143">요소</span><span class="sxs-lookup"><span data-stu-id="6ea71-143">Elements</span></span>  
  
|<span data-ttu-id="6ea71-144">이름</span><span class="sxs-lookup"><span data-stu-id="6ea71-144">Name</span></span>|<span data-ttu-id="6ea71-145">설명</span><span class="sxs-lookup"><span data-stu-id="6ea71-145">Description</span></span>|<span data-ttu-id="6ea71-146">필수</span><span class="sxs-lookup"><span data-stu-id="6ea71-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="6ea71-147">인증-인증서</span><span class="sxs-lookup"><span data-stu-id="6ea71-147">authentication-certificate</span></span>|<span data-ttu-id="6ea71-148">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea71-148">Root element.</span></span>|<span data-ttu-id="6ea71-149">예</span><span class="sxs-lookup"><span data-stu-id="6ea71-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="6ea71-150">특성</span><span class="sxs-lookup"><span data-stu-id="6ea71-150">Attributes</span></span>  
  
|<span data-ttu-id="6ea71-151">이름</span><span class="sxs-lookup"><span data-stu-id="6ea71-151">Name</span></span>|<span data-ttu-id="6ea71-152">설명</span><span class="sxs-lookup"><span data-stu-id="6ea71-152">Description</span></span>|<span data-ttu-id="6ea71-153">필수</span><span class="sxs-lookup"><span data-stu-id="6ea71-153">Required</span></span>|<span data-ttu-id="6ea71-154">기본값</span><span class="sxs-lookup"><span data-stu-id="6ea71-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="6ea71-155">thumbprint</span><span class="sxs-lookup"><span data-stu-id="6ea71-155">thumbprint</span></span>|<span data-ttu-id="6ea71-156">클라이언트 인증서에 대한 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea71-156">The thumbprint for the client certificate.</span></span>|<span data-ttu-id="6ea71-157">예</span><span class="sxs-lookup"><span data-stu-id="6ea71-157">Yes</span></span>|<span data-ttu-id="6ea71-158">해당 없음</span><span class="sxs-lookup"><span data-stu-id="6ea71-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="6ea71-159">사용 현황</span><span class="sxs-lookup"><span data-stu-id="6ea71-159">Usage</span></span>  
 <span data-ttu-id="6ea71-160">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea71-160">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="6ea71-161">**정책 섹션:** 인바운드</span><span class="sxs-lookup"><span data-stu-id="6ea71-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="6ea71-162">**정책 범위:** API</span><span class="sxs-lookup"><span data-stu-id="6ea71-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="6ea71-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ea71-163">Next steps</span></span>
<span data-ttu-id="6ea71-164">정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ea71-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  