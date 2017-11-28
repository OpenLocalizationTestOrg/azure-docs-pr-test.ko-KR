---
title: "SAML 프로토콜에서 Single Sign aaaAzure | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory에서 Single Sign SAML 프로토콜 hello 설명"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: ad8437f5-b887-41ff-bd77-779ddafc33fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 435cfe0e7be3f2defd34e8b6f6b0f08596ee1f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# Single Sign-On SAML 프로토콜
이 문서에서는 hello SAML 2.0 인증 요청 및 응답에 Azure Active Directory (Azure AD)에 대 한 Single Sign-on 지원에 대해 설명 합니다.

아래 다이어그램 hello 프로토콜 hello 단일 로그온 시퀀스를 설명합니다. hello 클라우드 서비스 (hello 서비스 공급자) 사용 하 여 HTTP 리디렉션 바인딩을 toopass는 `AuthnRequest` (인증 요청) 요소 tooAzure AD (hello id 공급자). HTTP post 바인딩을 toopost을 사용 하 여 다음 azure AD는 `Response` 요소 toohello 클라우드 서비스입니다.

![Single Sign On 워크플로](media/active-directory-single-sign-on-protocol-reference/active-directory-saml-single-sign-on-workflow.png)

## AuthnRequest
사용자 인증 toorequest 클라우드 서비스 보내기는 `AuthnRequest` 요소 tooAzure AD 합니다. 샘플 SAML 2.0 `AuthnRequest` 는 다음과 같습니다.

```
<samlp:AuthnRequest
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="id6c1c178c166d486687be4aaf5e482730"
Version="2.0" IssueInstant="2013-03-18T03:28:54.1839884Z"
xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
</samlp:AuthnRequest>
```


| 매개 변수 |  | 설명 |
| --- | --- | --- |
| ID |필수 |Azure AD에서는이 특성 toopopulate hello `InResponseTo` 특성의 hello 응답을 반환 합니다. ID로 시작 해서는 안 숫자 일반적인 전략은 tooprepend "id" toohello 문자열 표현 guid와 같은 문자열입니다. 예를 들어 `id6c1c178c166d486687be4aaf5e482730` 은 유효한 ID입니다. |
| 버전 |필수 |**2.0**이어야 합니다. |
| IssueInstant |필수 |UTC 값과 [라운드 트립 형식("o")](https://msdn.microsoft.com/library/az4se3k1.aspx)을 포함하는 DateTime 문자열입니다. Azure AD는이 형식의 DateTime 값이 필요 하지만 평가 않거나 hello 값을 사용 합니다. |
| AssertionConsumerServiceUrl |선택 사항 |제공 된 경우에 hello 일치 해야이 `RedirectUri` hello 클라우드 서비스에서 Azure AD의 합니다. |
| ForceAuthn |선택 사항 | 부울 값입니다. 경우 true, 즉 해당 hello 사용자는 강제 toore-Azure AD와 올바른 세션 있는 경우에 인증 합니다. |
| IsPassive |선택 사항 |이것이 여부를 Azure AD 인증 해야 hello 사용자 자동으로 사용자 조작 없이도 있는 경우에 hello 세션 쿠키를 사용 하 여 지정 하는 부울 값입니다. True 이면 Azure AD는 hello 세션 쿠키를 사용 하 여 tooauthenticate hello 사용자를 시도 합니다. |

다른 모든 `AuthnRequest` 특성(예: Consent, Destination, AssertionConsumerServiceIndex, AttributeConsumerServiceIndex, ProviderName)은 **무시**됩니다.

Azure AD에서는 hello 무시 `Conditions` 요소 `AuthnRequest`합니다.

### 발급자
hello `Issuer` 요소에는 `AuthnRequest` hello 중 하나에 정확히 일치 해야 **ServicePrincipalNames** hello 클라우드 서비스에 Azure AD. 일반적으로이 설정은 toohello **앱 ID URI** 응용 프로그램 등록 시 지정 된 합니다.

Hello를 포함 하는 샘플 SAML 발췌문 `Issuer` 요소는 다음과 같습니다.

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
```

### NameIDPolicy
이 요소는 특정 이름 ID 형식 hello에 대 한 응답을 요청 하 고에서 선택 사항 `AuthnRequest` 전송 요소 tooAzure AD 합니다.

샘플 `NameIdPolicy` 요소는 다음과 같습니다.

```
<NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
```

`NameIDPolicy`가 제공된 경우 선택 사항인 `Format` 특성을 포함할 수 있습니다. hello `Format` hello 다음 값 중 하나에만; 다른 오류가 발생 값 특성이 있을 수 있습니다.

* `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`: Azure Active Directory는 쌍으로 된 식별자로 hello NameID 클레임을 발급합니다.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`: Azure Active Directory 전자 메일 주소 형식에서 hello NameID 클레임을 발급합니다.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`:이 값은 Azure Active Directory tooselect hello 클레임 형식을 허용합니다. Azure Active Directory는 쌍으로 된 식별자로 NameID hello를 발급합니다.
* `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`: Azure Active Directory 고유 toohello 현재 SSO 작업 임의로 생성 된 값으로 hello NameID 클레임을 발급 합니다. 즉, 임시 hello 값은 인증 중인 사용자를 사용 하는 tooidentify hello 수 수 없습니다.

Azure AD 무시 hello `AllowCreate` 특성입니다.

### RequestAuthnContext
hello `RequestedAuthnContext` 요소 hello 필요한 인증 방법을 지정 합니다. 에 선택 사항이 `AuthnRequest` 전송 요소 tooAzure AD 합니다. Azure AD는 하나의 `AuthnContextClassRef` 값 `urn:oasis:names:tc:SAML:2.0:ac:classes:Password`만 지원합니다.

### 범위 지정
hello `Scoping` id 공급자 목록이 포함 하는 요소는의 선택적 `AuthnRequest` 전송 요소 tooAzure AD 합니다.

제공 된 경우 hello를 넣지 마십시오 `ProxyCount` 특성 `IDPListOption` 또는 `RequesterID` 요소를은 지원 되지 않습니다.

### 서명
Azure AD에서는 서명된 인증 요청을 지원하지 않으므로 `AuthnRequest` 요소에 `Signature` 요소를 포함하지 마세요.

### 제목
Azure AD 무시 hello `Subject` 요소의 `AuthnRequest` 요소입니다.

## 응답
요청한 로그온 성공적으로 완료 되 면 Azure AD는 응답 toohello 클라우드 서비스를 게시 합니다. 샘플 응답 tooa 성공적인 로그온 시도 하는 다음과 같습니다.

```
<samlp:Response ID="_a4958bfd-e107-4e67-b06d-0d85ade2e76a" Version="2.0" IssueInstant="2013-03-18T07:38:15.144Z" Destination="https://contoso.com/identity/inboundsso.aspx" InResponseTo="id758d0ef385634593a77bdf7e632984b6" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
    ...
  </ds:Signature>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
  <Assertion ID="_bf9c623d-cc20-407a-9a59-c2d0aee84d12" IssueInstant="2013-03-18T07:38:15.144Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      ...
    </ds:Signature>
    <Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
  </Assertion>
</samlp:Response>
```

### 응답
hello `Response` 요소 hello 권한 부여 요청의 hello 결과 포함 합니다. Hello를 설정 하는 azure AD `ID`, `Version` 및 `IssueInstant` hello 값 `Response` 요소입니다. 또한 hello 다음 특성을 설정 합니다.

* `Destination`: 로그온 성공적으로 완료 되 면이 설정 됩니다 toohello `RedirectUri` hello 서비스 공급자 (클라우드 서비스)의 합니다.
* `InResponseTo`:이 설정은 toohello `ID` hello 특성 `AuthnRequest` hello 응답을 시작 하는 요소입니다.

### 발급자
Hello를 설정 하는 azure AD `Issuer` 요소 너무`https://login.microsoftonline.com/<TenantIDGUID>/` 여기서 <TenantIDGUID> hello Azure AD 테 넌 트의 hello 테 넌 트 ID입니다.

예를 들어 발급자 요소를 포함하는 샘플 응답은 다음과 같습니다.

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

### 가동 상태
hello `Status` 요소가 로그온의 hello 성공 또는 실패를 전달 합니다. Hello 포함 `StatusCode` 코드나 hello hello 요청 상태를 나타내는 중첩된 코드 집합을 포함 하는 요소입니다. 또한 hello 포함 `StatusMessage` hello 로그온 프로세스 중 생성 되는 사용자 정의 오류 메시지를 포함 하는 요소입니다.

<!-- TODO: Add a authentication protocol error reference -->

hello 다음은 SAML 응답 tooan 실패 한 로그온 시도 합니다.

```
<samlp:Response ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Requester">
      <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:RequestUnsupported" />
    </samlp:StatusCode>
    <samlp:StatusMessage>AADSTS75006: An error occurred while processing a SAML2 Authentication request. AADSTS90011: hello SAML authentication request property 'NameIdentifierPolicy/SPNameQualifier' is not supported.
Trace ID: 66febed4-e737-49ff-ac23-464ba090d57c
Timestamp: 2013-03-18 08:49:24Z</samlp:StatusMessage>
  </samlp:Status>
```

### 어설션
또한 toohello에서 `ID`, `IssueInstant` 및 `Version`, hello 요소 hello에 다음을 설정 하는 Azure AD `Assertion` hello 응답의 요소입니다.

#### 발급자
이 설정은 너무`https://sts.windows.net/<TenantIDGUID>/`여기서 <TenantIDGUID> 는 hello hello Azure AD 테 넌 트의 테 넌 트 ID입니다.

```
<Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

#### 서명
Azure AD 서명 hello 어설션이 응답 tooa 로그온에 성공 합니다. hello `Signature` 요소 hello 클라우드 서비스가 hello 어설션의 tooauthenticate hello 소스 tooverify hello 무결성 사용 하 여 디지털 서명을 포함 합니다.

이 디지털 서명으로 Azure AD를 사용 하 여 toogenerate hello hello에 대 한 서명 키 `IDPSSODescriptor` 의 메타 데이터 문서의 요소입니다.

```
<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      digital_signature_here
    </ds:Signature>
```

#### 제목
Hello 보안 주체 hello assertion에서 hello 문 hello 주체를 지정 합니다. 포함 된 `NameID` hello 인증 된 사용자를 나타내는 요소입니다. hello `NameID` 값은 대상인 hello hello 토큰에 대 한 유일한 toohello 방향이 지정 된 서비스 공급자는 대상이 지정 된 식별자입니다. 영구적이며 해지할 수 있지만 다시 할당되지는 않습니다. 이기도 불투명, 즉 hello 사용자에 대 한 정보도 노출 되지 않습니다 고 특성 쿼리의 식별자로 사용할 수 없습니다.

hello `Method` hello 특성 `SubjectConfirmation` 요소는 항상 너무 설정`urn:oasis:names:tc:SAML:2.0:cm:bearer`합니다.

```
<Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
</Subject>
```

#### 조건
이 요소는 SAML 어설션의 hello 허용을 정의 하는 조건 사용 하 여 지정 합니다.

```
<Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
</Conditions>
```

hello `NotBefore` 및 `NotOnOrAfter` 특성 hello는 hello 어설션이 유효한 간격을 지정 합니다.

* 값의 hello hello `NotBefore` 특성은 같은 tooor 약간 (1 초 미만)의 hello 값 보다 나중 `IssueInstant` hello의 특성 `Assertion` 요소입니다. Azure AD에서 자체와 hello 시간의 차이를 고려 하지 클라우드 서비스 (서비스 공급자) 및 버퍼 toothis 때마다 추가 하지 않습니다.
* 값의 hello hello `NotOnOrAfter` 특성은 70 분 후 hello hello 값 `NotBefore` 특성입니다.

#### 대상
대상 그룹을 식별하는 URI를 포함합니다. 이 요소 toohello 값의 hello 값을 설정 하는 azure AD `Issuer` hello 요소의 `AuthnRequest` hello 로그온를 초기화 합니다. tooevaluate hello `Audience` hello hello 값을 사용 하 여, 값 `App ID URI` 응용 프로그램 등록 중에 지정한 합니다.

```
<AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
</AudienceRestriction>
```

Hello 처럼 `Issuer` 값을 hello `Audience` 값 정확히 일치 해야 Azure AD에서 hello 클라우드 서비스를 나타내는 hello 서비스 사용자 이름 중 하나입니다. 그러나 hello 값의 hello `Issuer` 아니므로 URI 값 hello `Audience` hello에 대 한 응답 값은 hello `Issuer` 기수가 `spn:`합니다.

#### AttributeStatement
이 hello 주체 또는 사용자에 대 한 클레임을 포함합니다. hello 발췌 한 다음 예제가 포함 `AttributeStatement` 요소입니다. hello 줄임표가 나타냅니다 hello 요소에는 여러 특성 및 특성 값에 포함 될 수 있습니다.

```
<AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
</AttributeStatement>
```        

* **클레임을 이름** : hello 값 hello `Name` 특성 (`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`) 같은 hello hello 인증 된 사용자의 사용자 계정 이름입니다 `testuser@managedtenant.com`합니다.
* **ObjectIdentifier 클레임** : hello 값 hello `ObjectIdentifier` 특성 (`http://schemas.microsoft.com/identity/claims/objectidentifier`)는 hello `ObjectId` hello 나타내는 hello 디렉터리 개체의 Azure AD에서 사용자를 인증 합니다. `ObjectId`변경할 수 없는 전역적으로 고유 이며 hello의 안전 식별자 다시 사용 하 여 사용자를 인증 합니다.

#### AuthnStatement
이 요소는 해당 hello 어설션 주체가 특정 시간에 특정 수단으로 인증 되었음을 어설션 합니다.

* hello `AuthnInstant` 특성 Azure AD로 인증 hello 사용자 hello 시간을 지정 합니다.
* hello `AuthnContext` 요소 tooauthenticate hello 사용자를 사용 하는 hello 인증 컨텍스트를 지정 합니다.

```
<AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
</AuthnStatement>
```