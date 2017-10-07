---
title: "Api aaaSecure API 관리-Azure API 관리에서에서 클라이언트 인증서 인증을 사용 하 여 | Microsoft Docs"
description: "Toosecure tooAPIs 클라이언트 인증서를 사용 하 여 액세스 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 6ff78bda3d429829da79d0dc4d652f19669cc919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a>Toosecure Api 클라이언트를 사용 하 여 인증서의 인증 방법 API 관리

API 관리 제공 hello 기능 toosecure 액세스 tooAPIs (즉, 클라이언트 tooAPI 관리) 클라이언트 인증서를 사용 하 여 합니다. 현재, 원하는 값에 대 한 클라이언트 인증서의 지문 hello를 확인할 수 있습니다. 기존 인증서에 대 한 지문 안녕하세요 업로드 tooAPI 관리 확인할 수 있습니다.  

클라이언트 인증서 (즉, API 관리 tooback 엔드)를 사용 하 여 api 액세스 toohello 백 엔드 서비스를 보안에 대 한 정보를 참조 하십시오. [클라이언트를 사용 하 여 toosecure 백 엔드 서비스 인증 인증서 하는 방법](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)

## <a name="checking-hello-expiration-date"></a>Hello 만료 날짜를 확인 하는 중

정책 아래 수 구성된 toocheck hello 인증서가 만료 된 경우:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a>Hello 발급자 및 주체를 확인합니다.

구성 된 toocheck hello 발급자 및 클라이언트 인증서의 주체 정책을 아래 될 수 있습니다.

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a>Hello 지문을 확인 하는 중

정책 아래 구성된 toocheck hello 지문 클라이언트 인증서의 하나일 수 있습니다.

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a>업로드 된 tooAPI 관리 인증서에 대 한 지문을 확인 하는 중

hello 다음 예제는 인증서에 대 한 클라이언트 인증서의 toocheck hello 지문을 tooAPI 관리를 업로드 하는 방법. 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a>다음 단계

*  [클라이언트를 사용 하 여 toosecure 백 엔드 서비스 인증 인증서 하는 방법](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [어떻게 tooupload 인증서](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

