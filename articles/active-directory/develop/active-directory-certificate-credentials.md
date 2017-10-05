---
title: "Azure AD의 인증서 자격 증명 | Microsoft Docs"
description: "이 문서에서는 응용 프로그램 인증을 위한 인증서 자격 증명의 등록 및 사용에 대해 설명합니다."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 88f0c64a-25f7-4974-aca2-2acadc9acbd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 08bb5140bb35bbd120aaa506afeab8ad247f81e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="1f2ff-103">응용 프로그램 인증을 위한 인증서 자격 증명</span><span class="sxs-lookup"><span data-stu-id="1f2ff-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="1f2ff-104">Azure Active Directory를 사용하면 응용 프로그램에서(예: OAuth 2.0 클라이언트 자격 증명 부여 흐름 및 On-Behalf-Of 흐름에서) 인증을 위해 자체의 자격 증명을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-104">Azure Active Directory allows an application to use its own credentials for authentication, for example, in the OAuth 2.0 Client Credentials Grant flow and the On-Behalf-Of flow.</span></span>
<span data-ttu-id="1f2ff-105">사용할 수 있는 자격 증명의 한 가지 형태는 응용 프로그램에서 소유한 인증서로 서명된 JWT(JSON Web Token) 어설션입니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that the application owns.</span></span>

## <a name="format-of-the-assertion"></a><span data-ttu-id="1f2ff-106">어설션 형식</span><span class="sxs-lookup"><span data-stu-id="1f2ff-106">Format of the assertion</span></span>
<span data-ttu-id="1f2ff-107">어설션을 계산하려면 선택한 언어로 많은 [JSON Web Token](https://jwt.io/)(영문) 라이브러리 중 하나를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-107">To compute the assertion, you probably want to use one of the many [JSON Web Token](https://jwt.io/) libraries in the language of your choice.</span></span> <span data-ttu-id="1f2ff-108">토큰에 의해 전달되는 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-108">The information carried by the token is:</span></span>

#### <a name="header"></a><span data-ttu-id="1f2ff-109">헤더</span><span class="sxs-lookup"><span data-stu-id="1f2ff-109">Header</span></span>

| <span data-ttu-id="1f2ff-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="1f2ff-110">Parameter</span></span> |  <span data-ttu-id="1f2ff-111">설명</span><span class="sxs-lookup"><span data-stu-id="1f2ff-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="1f2ff-112">**RS256**이어야 함</span><span class="sxs-lookup"><span data-stu-id="1f2ff-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="1f2ff-113">**JWT**여야 함</span><span class="sxs-lookup"><span data-stu-id="1f2ff-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="1f2ff-114">X.509 인증서 SHA-1 지문이어야 함</span><span class="sxs-lookup"><span data-stu-id="1f2ff-114">Should be the X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="1f2ff-115">클레임(페이로드)</span><span class="sxs-lookup"><span data-stu-id="1f2ff-115">Claims (Payload)</span></span>

| <span data-ttu-id="1f2ff-116">매개 변수</span><span class="sxs-lookup"><span data-stu-id="1f2ff-116">Parameter</span></span> |  <span data-ttu-id="1f2ff-117">설명</span><span class="sxs-lookup"><span data-stu-id="1f2ff-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="1f2ff-118">대상: **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**이어야 함</span><span class="sxs-lookup"><span data-stu-id="1f2ff-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="1f2ff-119">만료 날짜: 토큰이 만료되는 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-119">Expiration date: the date when the token expires.</span></span> <span data-ttu-id="1f2ff-120">시간은 1970년 1월 1일(1970-01-01T0:0:0Z) UTC부터 토큰의 유효 기간이 만료될 때까지의 시간(초)으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-120">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token validity expires.</span></span>|
| `iss` | <span data-ttu-id="1f2ff-121">발급자: client_id(클라이언트 서비스의 응용 프로그램 ID)여야 함</span><span class="sxs-lookup"><span data-stu-id="1f2ff-121">Issuer: should be the client_id (Application Id of the client service)</span></span> |
| `jti` | <span data-ttu-id="1f2ff-122">GUID: JWT ID</span><span class="sxs-lookup"><span data-stu-id="1f2ff-122">GUID: the JWT ID</span></span> |
| `nbf` | <span data-ttu-id="1f2ff-123">이전이 아님: 토큰을 사용할 수 없게 된 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-123">Not Before: the date before which the token cannot be used.</span></span> <span data-ttu-id="1f2ff-124">시간은 1970년 1월 1일(1970-01-01T0:0:0Z) UTC부터 토큰이 발급된 시간까지 기간(초)으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-124">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token was issued.</span></span> |
| `sub` | <span data-ttu-id="1f2ff-125">주체: `iss`의 경우 client_id(클라이언트 서비스의 응용 프로그램 ID)여야 함</span><span class="sxs-lookup"><span data-stu-id="1f2ff-125">Subject: As for `iss`, should be the client_id (Application Id of the client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="1f2ff-126">서명</span><span class="sxs-lookup"><span data-stu-id="1f2ff-126">Signature</span></span>
<span data-ttu-id="1f2ff-127">서명은 [JSON 웹 토큰 RFC7519 사양](https://tools.ietf.org/html/rfc7519)에 설명된 대로 인증서를 적용하여 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-127">The signature is computed applying the certificate as described in the [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="1f2ff-128">디코딩된 JWT 어설션 예제</span><span class="sxs-lookup"><span data-stu-id="1f2ff-128">Example of a decoded JWT assertion</span></span>
```
{
  "alg": "RS256",
  "typ": "JWT",
  "x5t": "gx8tGysyjcRqKjFPnd7RFwvwZI0"
}
.
{
  "aud": "https: //login.microsoftonline.com/contoso.onmicrosoft.com/oauth2/token",
  "exp": 1484593341,
  "iss": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05",
  "jti": "22b3bb26-e046-42df-9c96-65dbd72c1c81",
  "nbf": 1484592741,  
  "sub": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05"
}
.
"Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"

```

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="1f2ff-129">인코딩된 JWT 어설션 예제</span><span class="sxs-lookup"><span data-stu-id="1f2ff-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="1f2ff-130">다음 문자열은 인코딩된 어설션의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-130">The following string is an example of encoded assertion.</span></span> <span data-ttu-id="1f2ff-131">자세히 살펴보면 세 개의 섹션이 점(.)으로 구분된 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="1f2ff-132">첫 번째 섹션은 헤더를 인코딩하고, 두 번째는 페이로드를 인코딩하며, 마지막은 처음 두 섹션 콘텐츠의 인증서로 계산된 서명입니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-132">The first section encodes the header, the second the payload, and the last is the signature computed with the certificates from the content of the first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="1f2ff-133">Azure AD에 인증서 등록</span><span class="sxs-lookup"><span data-stu-id="1f2ff-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="1f2ff-134">인증서 자격 증명을 Azure AD의 클라이언트 응용 프로그램에 연결하려면 응용 프로그램 매니페스트를 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-134">To associate the certificate credential with the client application in Azure AD, you need to edit the application manifest.</span></span>
<span data-ttu-id="1f2ff-135">인증서가 있을 때 다음을 계산해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-135">Having hold of a certificate, you need to compute:</span></span>
- <span data-ttu-id="1f2ff-136">`$base64Thumbprint` - 인증서 해시의 base64 인코딩</span><span class="sxs-lookup"><span data-stu-id="1f2ff-136">`$base64Thumbprint`, which is the base64 encoding of the certificate Hash</span></span>
- <span data-ttu-id="1f2ff-137">`$base64Value` - 인증서 원시 데이터의 해시의 base64 인코딩</span><span class="sxs-lookup"><span data-stu-id="1f2ff-137">`$base64Value`, which is the base64 encoding of the certificate raw data</span></span>

<span data-ttu-id="1f2ff-138">응용 프로그램 매니페스트에서 키를 식별하는 GUID도 제공해야 합니다(`$keyId`).</span><span class="sxs-lookup"><span data-stu-id="1f2ff-138">you also need to provide a GUID to identify the key in the application manifest (`$keyId`)</span></span>

<span data-ttu-id="1f2ff-139">클라이언트 응용 프로그램에 대한 Azure 앱 등록에서 응용 프로그램 매니페스트를 열고, 다음 스키마를 사용하여 *keyCredentials* 속성을 새 인증서 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-139">In the Azure app registration for the client application, open the application manifest, and replace the *keyCredentials* property with your new certificate information using the following schema:</span></span>
```
"keyCredentials": [
    {
        "customKeyIdentifier": "$base64Thumbprint",
        "keyId": "$keyid",
        "type": "AsymmetricX509Cert",
        "usage": "Verify",
        "value":  "$base64Value"
    }
]
```

<span data-ttu-id="1f2ff-140">응용 프로그램 매니페스트에 편집 내용을 저장하고 Azure AD에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-140">Save the edits to the application manifest, and upload to Azure AD.</span></span> <span data-ttu-id="1f2ff-141">keycredentials 속성은 다중 값이므로 풍부한 키 관리를 위해 여러 인증서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f2ff-141">The keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
