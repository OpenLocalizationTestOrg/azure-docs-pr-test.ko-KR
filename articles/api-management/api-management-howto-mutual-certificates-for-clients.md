---
title: "API Management에서 클라이언트 인증서 인증을 사용하여 API 보호 - Azure API Management | Microsoft Docs"
description: "클라이언트 인증서를 사용하여 API에 대한 액세스의 보안을 유지하는 방법을 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: apimpm
ms.openlocfilehash: d3d51d0575a6d2dacced931601d48eb1e51a4051
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="b72e7-103">API Management에서 클라이언트 인증서 인증을 사용하여 API를 보호하는 방법</span><span class="sxs-lookup"><span data-stu-id="b72e7-103">How to secure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="b72e7-104">API Management에서는 클라이언트 인증서를 사용하여 API에 대한 액세스(예: API Management에 대한 클라이언트)를 보호하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b72e7-104">API Management provides the capability to secure access to APIs (i.e., client to API Management) using client certificates.</span></span> <span data-ttu-id="b72e7-105">현재, 클라이언트 인증서의 지문을 원하는 값과 비교해서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b72e7-105">Currently, you can check the thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="b72e7-106">API Management에 업로드된 기존 인증서와 지문을 비교해서 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b72e7-106">You can also check the thumbprint against existing certificates uploaded to API Management.</span></span>  

<span data-ttu-id="b72e7-107">클라이언트 인증서를 사용하여 API의 백 엔드 서비스(예: 백 엔드에 대한 API Management)에 대한 액세스를 보호하는 방법에 대한 자세한 내용은 [클라이언트 인증서 인증을 사용하여 백 엔드 서비스를 보호하는 방법](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b72e7-107">For information about securing access to the back-end service of an API using client certificates (i.e., API Management to back-end), see [How to secure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-the-expiration-date"></a><span data-ttu-id="b72e7-108">만료 날짜 확인</span><span class="sxs-lookup"><span data-stu-id="b72e7-108">Checking the expiration date</span></span>

<span data-ttu-id="b72e7-109">인증서 만료 여부를 확인하도록 아래 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b72e7-109">Below policies can be configured to check if the certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-issuer-and-subject"></a><span data-ttu-id="b72e7-110">발급자 및 주체 확인</span><span class="sxs-lookup"><span data-stu-id="b72e7-110">Checking the issuer and subject</span></span>

<span data-ttu-id="b72e7-111">클라이언트 인증서의 발급자 및 주체를 확인하도록 아래 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b72e7-111">Below policies can be configured to check the issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-thumbprint"></a><span data-ttu-id="b72e7-112">지문 확인</span><span class="sxs-lookup"><span data-stu-id="b72e7-112">Checking the thumbprint</span></span>

<span data-ttu-id="b72e7-113">클라이언트 인증서의 지문을 확인하도록 아래 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b72e7-113">Below policies can be configured to check the thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-to-api-management"></a><span data-ttu-id="b72e7-114">API Management에 업로드된 인증서에 대해 지문 확인</span><span class="sxs-lookup"><span data-stu-id="b72e7-114">Checking a thumbprint against certificates uploaded to API Management</span></span>

<span data-ttu-id="b72e7-115">다음 예제에서는 API Management에 업로드된 인증서에 대해 클라이언트 인증서의 지문을 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b72e7-115">The following example shows how to check the thumbprint of a client certificate against certificates uploaded to API Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="b72e7-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b72e7-116">Next step</span></span>

*  [<span data-ttu-id="b72e7-117">클라이언트 인증서 인증을 사용하여 백 엔드 서비스를 보호하는 방법</span><span class="sxs-lookup"><span data-stu-id="b72e7-117">How to secure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="b72e7-118">인증서 업로드 방법</span><span class="sxs-lookup"><span data-stu-id="b72e7-118">How to upload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

