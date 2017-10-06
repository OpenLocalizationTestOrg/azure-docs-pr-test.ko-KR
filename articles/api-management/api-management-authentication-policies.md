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
# <a name="api-management-authentication-policies"></a>API Management 인증 정책
이 항목에서는 다음 API 관리 정책 hello에 대 한 대 한 참조를 제공 합니다. 정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.  
  
##  <a name="AuthenticationPolicies"></a> 인증 정책  
  
-   [기본 사용 인증](api-management-authentication-policies.md#Basic) - 기본 인증을 사용하여 백 엔드 서비스를 인증합니다.  
  
-   [클라이언트 인증서 사용 인증](api-management-authentication-policies.md#ClientCertificate) - 클라이언트 인증서를 사용하여 백 엔드 서비스를 인증합니다.  
  
##  <a name="Basic"></a> 기본 사용 인증  
 사용 하 여 hello `authentication-basic` 기본 인증을 사용 하 여 백 엔드 서비스와 정책 tooauthenticate 합니다. 이 정책은 효과적으로 hello HTTP 권한 부여 헤더 toohello hello 정책에 제공 된 값 해당 toohello 자격을 설정 합니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a>예  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|인증-기본|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|username|Hello 기본 자격 증명의 hello 사용자 이름을 지정합니다.|예|해당 없음|  
|암호|Hello 기본 자격 증명의 hello 암호를 지정합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound  
  
-   **정책 범위:** API  
  
##  <a name="ClientCertificate"></a> 클라이언트 인증서 사용 인증  
 사용 하 여 hello `authentication-certificate` 클라이언트 인증서를 사용 하 여 백 엔드 서비스와 정책 tooauthenticate 합니다. hello 인증서 필요 toobe [API 관리에 설치](http://go.microsoft.com/fwlink/?LinkID=511599) 첫 번째 지 문으로 식별 됩니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a>예  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|인증-인증서|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|thumbprint|hello 클라이언트 인증서에 대 한 hello 지문입니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound  
  
-   **정책 범위:** API  
  

## <a name="next-steps"></a>다음 단계
정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.  