---
title: "Azure AD에서 자격 증명 aaaCertificate | Microsoft Docs"
description: "이 문서에서는 hello 등록 및 응용 프로그램 인증 인증서 자격 증명 사용"
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
ms.openlocfilehash: 3508803112ac06268d553db86ab74812aa53e455
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="64ad1-103">응용 프로그램 인증을 위한 인증서 자격 증명</span><span class="sxs-lookup"><span data-stu-id="64ad1-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="64ad1-104">Azure Active Directory에서는 응용 프로그램 toouse는 자신의 자격 증명 인증에 대 한 예를 들어의 hello OAuth 2.0 클라이언트 자격 증명 부여 흐름 및 hello에 대신-흐름 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-104">Azure Active Directory allows an application toouse its own credentials for authentication, for example, in hello OAuth 2.0 Client Credentials Grant flow and hello On-Behalf-Of flow.</span></span>
<span data-ttu-id="64ad1-105">사용할 수 있는 자격 증명의 한 가지 형태는 JSON 웹 Token(JWT) 어설션 hello 응용 프로그램을 소유 하는 인증서로 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that hello application owns.</span></span>

## <a name="format-of-hello-assertion"></a><span data-ttu-id="64ad1-106">Hello 어설션 형식</span><span class="sxs-lookup"><span data-stu-id="64ad1-106">Format of hello assertion</span></span>
<span data-ttu-id="64ad1-107">toocompute hello 어설션 싶을 toouse hello 중 많은 [JSON 웹 토큰](https://jwt.io/) 라이브러리 hello 언어를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-107">toocompute hello assertion, you probably want toouse one of hello many [JSON Web Token](https://jwt.io/) libraries in hello language of your choice.</span></span> <span data-ttu-id="64ad1-108">hello 토큰 얻어진 hello 정보가입니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-108">hello information carried by hello token is:</span></span>

#### <a name="header"></a><span data-ttu-id="64ad1-109">헤더</span><span class="sxs-lookup"><span data-stu-id="64ad1-109">Header</span></span>

| <span data-ttu-id="64ad1-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="64ad1-110">Parameter</span></span> |  <span data-ttu-id="64ad1-111">설명</span><span class="sxs-lookup"><span data-stu-id="64ad1-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="64ad1-112">**RS256**이어야 함</span><span class="sxs-lookup"><span data-stu-id="64ad1-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="64ad1-113">**JWT**여야 함</span><span class="sxs-lookup"><span data-stu-id="64ad1-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="64ad1-114">Hello X.509 인증서 s h A-1 지문 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-114">Should be hello X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="64ad1-115">클레임(페이로드)</span><span class="sxs-lookup"><span data-stu-id="64ad1-115">Claims (Payload)</span></span>

| <span data-ttu-id="64ad1-116">매개 변수</span><span class="sxs-lookup"><span data-stu-id="64ad1-116">Parameter</span></span> |  <span data-ttu-id="64ad1-117">설명</span><span class="sxs-lookup"><span data-stu-id="64ad1-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="64ad1-118">대상: **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**이어야 함</span><span class="sxs-lookup"><span data-stu-id="64ad1-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="64ad1-119">만료 날짜: hello 토큰이 만료 되는 hello 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-119">Expiration date: hello date when hello token expires.</span></span> <span data-ttu-id="64ad1-120">hello 시간 1970 년 1 월 1 일에서 hello 시간 (초)로 표시 됩니다 (1970-01-01T0:0:0Z) hello 시간 hello 토큰 유효 만료 될 때까지 UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-120">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token validity expires.</span></span>|
| `iss` | <span data-ttu-id="64ad1-121">발급자: hello client_id (hello client 서비스의 응용 프로그램 Id) 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-121">Issuer: should be hello client_id (Application Id of hello client service)</span></span> |
| `jti` | <span data-ttu-id="64ad1-122">GUID: hello JWT ID</span><span class="sxs-lookup"><span data-stu-id="64ad1-122">GUID: hello JWT ID</span></span> |
| `nbf` | <span data-ttu-id="64ad1-123">날짜부터: hello 날짜는 hello 하기 전에 토큰을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-123">Not Before: hello date before which hello token cannot be used.</span></span> <span data-ttu-id="64ad1-124">hello 시간 1970 년 1 월 1 일에서 hello 시간 (초)로 표시 됩니다 (1970-01-01T0:0:0Z) hello 시간 hello 토큰이 발급 된 될 때까지 UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-124">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token was issued.</span></span> |
| `sub` | <span data-ttu-id="64ad1-125">제목:에 대 한 `iss`, hello client_id (hello client 서비스의 응용 프로그램 Id) 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-125">Subject: As for `iss`, should be hello client_id (Application Id of hello client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="64ad1-126">서명</span><span class="sxs-lookup"><span data-stu-id="64ad1-126">Signature</span></span>
<span data-ttu-id="64ad1-127">hello에 설명 된 대로 hello 인증서 적용 hello 서명을 계산 [JSON 웹 토큰 RFC7519 사양](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="64ad1-127">hello signature is computed applying hello certificate as described in hello [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="64ad1-128">디코딩된 JWT 어설션 예제</span><span class="sxs-lookup"><span data-stu-id="64ad1-128">Example of a decoded JWT assertion</span></span>
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

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="64ad1-129">인코딩된 JWT 어설션 예제</span><span class="sxs-lookup"><span data-stu-id="64ad1-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="64ad1-130">다음 문자열 hello는 인코딩된 어설션의 예시입니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-130">hello following string is an example of encoded assertion.</span></span> <span data-ttu-id="64ad1-131">자세히 살펴보면 세 개의 섹션이 점(.)으로 구분된 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="64ad1-132">hello 첫 번째 섹션 hello 헤더로, 두 번째 hello 페이로드 hello 인코딩하고 hello 마지막는 hello 처음 두 섹션의 내용을 사용 hello hello 인증서로 계산 하는 hello 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-132">hello first section encodes hello header, hello second hello payload, and hello last is hello signature computed with hello certificates from hello content of hello first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="64ad1-133">Azure AD에 인증서 등록</span><span class="sxs-lookup"><span data-stu-id="64ad1-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="64ad1-134">tooassociate hello 인증서 자격 증명은 Azure AD에서 hello 클라이언트 응용 프로그램, tooedit hello 응용 프로그램 매니페스트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-134">tooassociate hello certificate credential with hello client application in Azure AD, you need tooedit hello application manifest.</span></span>
<span data-ttu-id="64ad1-135">Toocompute를 인증서의 보류는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-135">Having hold of a certificate, you need toocompute:</span></span>
- <span data-ttu-id="64ad1-136">`$base64Thumbprint`해시 hello 인증서의 base64 인코딩을 hello가 있는</span><span class="sxs-lookup"><span data-stu-id="64ad1-136">`$base64Thumbprint`, which is hello base64 encoding of hello certificate Hash</span></span>
- <span data-ttu-id="64ad1-137">`$base64Value`hello 인증서 원시 데이터의 base64 인코딩입니다 hello가 있는</span><span class="sxs-lookup"><span data-stu-id="64ad1-137">`$base64Value`, which is hello base64 encoding of hello certificate raw data</span></span>

<span data-ttu-id="64ad1-138">또한 tooprovide hello 응용 프로그램 매니페스트에서 GUID tooidentify hello 키 해야 (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="64ad1-138">you also need tooprovide a GUID tooidentify hello key in hello application manifest (`$keyId`)</span></span>

<span data-ttu-id="64ad1-139">Hello 응용 프로그램 매니페스트를 열고 hello 바꿉니다 hello hello 클라이언트 응용 프로그램에 대 한 Azure 응용 프로그램 등록에에서 *keyCredentials* 스키마를 따르는 hello를 사용 하 여 새 인증서 정보를 사용 하 여 속성:</span><span class="sxs-lookup"><span data-stu-id="64ad1-139">In hello Azure app registration for hello client application, open hello application manifest, and replace hello *keyCredentials* property with your new certificate information using hello following schema:</span></span>
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

<span data-ttu-id="64ad1-140">Hello 편집 toohello 응용 프로그램 매니페스트를 저장 하 고 AD tooAzure를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-140">Save hello edits toohello application manifest, and upload tooAzure AD.</span></span> <span data-ttu-id="64ad1-141">hello keyCredentials 속성 다중 값 이므로 다양 한 키 관리에 대 한 여러 인증서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64ad1-141">hello keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
