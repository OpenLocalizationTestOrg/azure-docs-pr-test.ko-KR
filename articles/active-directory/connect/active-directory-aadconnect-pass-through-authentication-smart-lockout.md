---
title: "Azure AD Connect: 통과 인증 - 스마트 잠금 | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory (Azure AD) 통과 인증 온-프레미스 계정 hello 클라우드에서 무차별 암호 대입 공격에서 보호 하는 방법을 설명 합니다."
services: active-directory
keywords: "Azure AD Connect 통과 인증, Active Directory 설치, Azure AD에 대한 필수 구성 요소, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a>Azure Active Directory 통과 인증: 스마트 잠금

## <a name="overview"></a>개요

Azure AD는 무차별 암호 대입 공격으로부터 보호하고 실제 사용자가 Office 365 및 SaaS 응용 프로그램에서 잠기지 않게 차단합니다. 이 기능을 **스마트 잠금**이라고 하며 로그인 방법으로 통과 인증을 사용할 때 지원됩니다. 스마트 잠금은 기본적으로 모든 테 넌 트에 대 한 사용 및 보호 하는 사용자 계정을 항상 hello; 없는 필요 tooturn는에 있습니다.

스마트 잠금은 실패한 모든 로그인 시도를 추적하며 특정 **잠금 임계값** 이후 **잠금 기간**을 시작하는 방식으로 작동합니다. Hello 잠금 기간 동안 hello 공격자의 로그인 시도 거부 됩니다. Hello 공격 계속 되 면 hello 후속 실패 한 로그인 시도 hello 잠금 기간이 긴 잠금 기간에서 결과 종료 된 후입니다.

>[!NOTE]
>hello 미리 잠금 임계값의 기본값이 10 실패 한 시도 및 hello 기본 잠금 기간은 60 초입니다.

또한 스마트 잠금 로그인 정품 사용자 로부터 및 공격자 로부터 및 대부분의 경우에서 hello 공격자가 유일한 잠급니다를 구분합니다. 이 기능은 공격자가 악의적으로 실제 사용자를 잠그지 못하게 차단합니다. 로그인 동작을 사용자의 장치 및 브라우저 및 기타 신호 toodistinguish 정품 사용자와 공격자 간의 과거 사용합니다. 이 알고리즘은 지속적으로 개선 중입니다.

통과 인증 온-프레미스 Active Directory (AD)에 암호 유효성 검사 요청을 전달 하기 때문에 AD 사용자의 계정을 잠그는 tooprevent 공격자가 필요 합니다. 사용자 고유의 AD 계정 잠금 정책이 있으므로 (특히 [ **계정 잠금 임계값** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) 및 [ **재설정 계정 잠금 카운터 후 정책** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), Azure AD의 tooconfigure 잠금 임계값 필요한 및 온-프레미스에 도달 하기 전에 잠금 기간 값 hello 클라우드에서 공격 아웃 toofilter 적절 하 게 AD 합니다.

>[!NOTE]
>hello 스마트 잠금 기능은 무료 이며 _에_ 모든 고객에 대해 기본적으로 합니다. 그러나 Azure AD의 잠금 임계값 및 Graph API를 사용 하 여 잠금 기간 값 수정 테 넌 트 toohave 하나 이상의 Azure AD Premium P2 라이선스가 필요 합니다. Azure AD Premium P2 라이선스가 필요 하지 않는 _사용자 당_ tooget hello 스마트 잠금 기능 통과 인증을 사용 합니다.

사용자의 온-프레미스 AD 계정 tooensure 잘 보호, tooensure 해야입니다.

1.  Azure AD의 잠금 임계값은 AD의 계정 잠금 임계값보다 _작아야_ 합니다. AD의 계정 잠금 임계값은 적어도 두 개 또는 3 배 미리 잠금 임계값의 Azure AD의 hello 값을 설정 하는 것이 좋습니다.
2.  Azure AD의 잠금 기간(초 단위)이 AD의 다음 시간 이후 계정 잠금 재설정(분 단위)보다 _길어야_ 합니다.

## <a name="verify-your-ad-account-lockout-policies"></a>AD 계정 잠금 정책 확인

다음 지침 tooverify hello AD 계정 잠금 정책을 사용 합니다.

1.  Hello 그룹 정책 관리 도구를 엽니다.
2.  Hello 그룹 정책이 적용 된 tooall 사용자 예를 들어 hello 기본 도메인 정책을 편집 합니다.
3.  구성 설정 \ 보안 \ 계정 잠금 정책 tooComputer 이동 합니다.
4.  계정 잠금 임계값 및 다음 이후 계정 잠금 카운터 재설정 값을 확인합니다.

![AD 계정 잠금 정책](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a>스마트 잠금 값 테 넌 트의 Graph API toomanage hello를 사용 하 여

>[!IMPORTANT]
>그래픽 API를 사용하여 Azure AD의 잠금 임계값 및 잠금 기간을 수정하는 것은 Azure AD Premium P2 기능입니다.  또한, toobe 테 넌 트에 대 한 전역 관리자를 필요합니다.

사용할 수 있습니다 [그래프 탐색기](https://developer.microsoft.com/graph/graph-explorer) tooread, 설정 및 Azure AD의 스마트 잠금 값을 업데이트 합니다. 하지만 이러한 작업을 프로그래밍 방식으로 수행할 수도 있습니다.

### <a name="read-smart-lockout-values"></a>스마트 잠금 값 읽기

이러한 단계 tooread 테 넌 트의 스마트 잠금 값을 따릅니다.

1. Graph 탐색기에 테넌트의 전역 관리자로 로그인합니다. 메시지가 표시 되 면 hello에 대 한 액세스 권한 부여 사용 권한을 요청 합니다.
2. "사용 권한 수정"을 클릭 하 고 hello "Directory.ReadWrite.All" 권한을 선택 합니다.
3. Hello Graph API 요청을 다음과 같이 구성: 집합 버전 너무 "BETA" 요청 유형을 너무 "GET" 및 URL 너무`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`합니다.
4. "실행할 쿼리" toosee 테 넌 트의 스마트 잠금 값을 클릭 합니다. 앞서 테넌트의 값을 설정하지 않은 경우 빈 집합이 표시됩니다.

### <a name="set-smart-lockout-values"></a>스마트 잠금 값 설정

이러한 단계 tooset 테 넌 트의 스마트 잠금 값 (최초 구매 시에만 입력 hello)를 수행 합니다.

1. Graph 탐색기에 테넌트의 전역 관리자로 로그인합니다. 메시지가 표시 되 면 hello에 대 한 액세스 권한 부여 사용 권한을 요청 합니다.
2. "사용 권한 수정"을 클릭 하 고 hello "Directory.ReadWrite.All" 권한을 선택 합니다.
3. Hello Graph API 요청을 다음과 같이 구성: 집합 버전 너무 "BETA" 요청 유형을 너무 "POST" 및 URL 너무`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`합니다.
4. 복사한 hello JSON 요청 hello "요청 본문" 필드에 다음을 붙여 넣습니다. 적절 하 게 hello 스마트 잠금 값을 변경 하 고에 대 한 임의 GUID를 사용 하 여 `templateId`합니다.
5. "실행할 쿼리" tooset 테 넌 트의 스마트 잠금 값을 클릭 합니다.

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
>사용 하지 않는 경우에 hello을 둘 수 있습니다 **BannedPasswordList** 및 **EnableBannedPasswordCheck** 값이 비어 있는 것으로 ("") 및 "false" 각각.

[이 단계](#read-smart-lockout-values)를 사용하여 테넌트의 스마트 잠금 값을 올바르게 설정했는지 확인합니다.

### <a name="update-smart-lockout-values"></a>스마트 잠금 값 업데이트

값 뒤에 이러한 단계 tooupdate 테 넌 트의 스마트 잠금 (이미 설정한 경우 이전):

1. Graph 탐색기에 테넌트의 전역 관리자로 로그인합니다. 메시지가 표시 되 면 hello에 대 한 액세스 권한 부여 사용 권한을 요청 합니다.
2. "사용 권한 수정"을 클릭 하 고 hello "Directory.ReadWrite.All" 권한을 선택 합니다.
3. [이러한 단계 tooread 테 넌 트의 스마트 잠금 값에 따라](#read-smart-lockout-values)합니다. 복사 hello `id` "displayName" "PasswordRuleSettings"로 된 hello 항목의 값 (GUID)입니다.
4. Hello Graph API 요청을 다음과 같이 구성: 너무 버전 설정 "BETA" 너무 요청 유형 "패치" 및 URL 너무`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -사용 하 여 GUID에 대 한 3 단계부터에서 hello `<id>`합니다.
5. 복사한 hello JSON 요청 hello "요청 본문" 필드에 다음을 붙여 넣습니다. 적절 하 게 hello 스마트 잠금 값을 변경 합니다.
6. "실행할 쿼리" tooupdate 테 넌 트의 스마트 잠금 값을 클릭 합니다.

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

[이 단계](#read-smart-lockout-values)를 사용하여 테넌트의 스마트 잠금 값을 올바르게 업데이트했는지 확인합니다.

## <a name="next-steps"></a>다음 단계
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.
