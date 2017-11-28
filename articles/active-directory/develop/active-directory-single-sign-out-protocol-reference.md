---
title: "SAML 프로토콜 아웃 Single Sign aaaAzure | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory에서 Single Sign-Out SAML 프로토콜 hello 설명"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 0e4aa75d-d1ad-4bde-a94c-d8a41fb0abe6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 889c9b3397a601c16ba6971d2b15bfee305576de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# Single Sign-Out SAML 프로토콜
Azure Active Directory (Azure AD) 지원 hello SAML 2.0 웹 브라우저 single sign-out 프로필입니다. Single sign-out toowork에 대 한 hello 올바르게 **LogoutURL** 에 응용 프로그램 등록 시 Azure AD에 hello 응용 프로그램을 명시적으로 등록 되어야 합니다. Azure AD는 로그 아웃 후 hello LogoutURL tooredirect 사용자가 사용 합니다.

이 다이어그램에서는 hello Azure AD single sign-out 프로세스의 hello 워크플로를 보여 줍니다.

![Single Sign Out 워크플로](media/active-directory-single-sign-out-protocol-reference/active-directory-saml-single-sign-out-workflow.png)

## LogoutRequest
클라우드 서비스 보냅니다 hello는 `LogoutRequest` 메시지 tooAzure AD tooindicate는 세션이 종료 되었습니다. hello 발췌 한 다음 예제를 보여 줍니다 `LogoutRequest` 요소입니다.

```
<samlp:LogoutRequest xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="idaa6ebe6839094fe4abc4ebd5281ec780" Version="2.0" IssueInstant="2013-03-28T07:10:49.6004822Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.workaad.com</Issuer>
  <NameID xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
</samlp:LogoutRequest>
```

### LogoutRequest
hello `LogoutRequest` 전송 요소 tooAzure AD 특성 뒤 hello 필요:

* `ID`:이 hello 로그 아웃 요청을 식별합니다. 값을 hello `ID` 숫자로 시작할 수 없습니다. hello 일반적인 방법은 tooappend **id** GUID의 문자열 표현을 toohello 합니다.
* `Version`:이 요소의 hello 값을 너무 설정**2.0**합니다. 이 값은 필수입니다.
* `IssueInstant` : UTC(Coordinate Universal Time) 값과 [라운드 트립 형식("o")](https://msdn.microsoft.com/library/az4se3k1.aspx)을 포함하는 `DateTime` 문자열입니다. Azure AD에는 이 형식의 값이 필요하지만 강제 적용하지는 않습니다.

### 발급자
hello `Issuer` 요소에는 `LogoutRequest` hello 중 하나에 정확히 일치 해야 **ServicePrincipalNames** hello 클라우드 서비스에 Azure AD. 일반적으로이 설정은 toohello **앱 ID URI** 응용 프로그램 등록 시 지정 된 합니다.

### NameID
값의 hello hello `NameID` 요소 hello와 정확히 일치 해야 `NameID` 는 로그 아웃 하는 hello 사용자의 합니다.

## LogoutResponse
Azure AD 보냅니다는 `LogoutResponse` 응답 tooa에 `LogoutRequest` 요소입니다. hello 발췌 한 다음 예제를 보여 줍니다 `LogoutResponse`합니다.

```
<samlp:LogoutResponse ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
</samlp:LogoutResponse>
```

### LogoutResponse
Hello를 설정 하는 azure AD `ID`, `Version` 및 `IssueInstant` hello 값 `LogoutResponse` 요소입니다. 또한 hello 설정 `InResponseTo` hello 요소 toohello 값 `ID` hello 특성 `LogoutRequest` hello 응답을 요청한 합니다.

### 발급자
Azure AD 설정이 값이 너무`https://login.microsoftonline.com/<TenantIdGUID>/` 여기서 <TenantIdGUID> hello Azure AD 테 넌 트의 hello 테 넌 트 ID입니다.

hello tooevaluate hello 값 `Issuer` 요소를 사용 하 여 hello 값 hello **앱 ID URI** 응용 프로그램 등록 중에 제공 합니다.

### 가동 상태
Azure AD hello를 사용 하 여 `StatusCode` 요소 hello에 `Status` 요소 tooindicate hello 성공 또는 실패의 로그 아웃 합니다. Hello 로그 아웃 시도가 실패 한 경우, hello `StatusCode` 요소 사용자 지정 오류 메시지를 포함할 수도 있습니다.
