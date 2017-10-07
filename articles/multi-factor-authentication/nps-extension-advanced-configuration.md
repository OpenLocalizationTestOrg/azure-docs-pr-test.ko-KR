---
title: "Azure MFA NPS 확장 aaaConfigure hello | Microsoft Docs"
description: "IP 허용 목록 및 UPN 대체와 같은 고급 구성에 대 한 hello NPS 확장을 설치한 후 다음이 단계를 사용 합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: c3aed077b23c95f874861eb00c8e6dca668329c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-options-for-hello-nps-extension-for-multi-factor-authentication"></a>고급 Multi-factor Authentication에 대 한 hello NPS 확장에 대 한 구성 옵션

hello 정책 서버 NPS (네트워크) 확장 온-프레미스 인프라에 클라우드 기반 Azure Multi-factor Authentication 기능을 확장합니다. 이 문서에서는 이미 확장명이 hello 설치 하 고 할 수 있습니다에 대 한 toocustomize hello 확장 요구 하는 방법을 tooknow 가정 합니다. 

## <a name="alternate-login-id"></a>대체 로그인 ID

온-프레미스 및 클라우드 hello NPS 확장 연결 tooboth 있으므로 디렉터리를 실행 하 여 온-프레미스 사용자 계정 이름 (Upn) hello 클라우드에서 hello 이름을 일치 하지 않는 문제가 발생할 수 있습니다. toosolve이이 문제를 사용 하 여 대체 로그인 id를 나열 합니다. 

Hello NPS 확장 내에서 Azure Multi-factor Authentication에 대 한 hello UPN 대신 사용 하는 Active Directory 특성 toobe를 지정할 수 있습니다. 그러면 tooprotect 하면 2 단계 인증을 사용 하 여 온-프레미스 리소스에 온-프레미스 Upn을 수정 하지 않고 있습니다. 

tooconfigure 대체 로그인 Id를 이동 너무`HKLM\SOFTWARE\Microsoft\AzureMfa` hello 다음 레지스트리 값을 편집 합니다.

| 이름 | 형식 | 기본값 | 설명 |
| ---- | ---- | ------------- | ----------- |
| LDAP_ALTERNATE_LOGINID_ATTRIBUTE | string | Empty | Hello toouse hello UPN 대신 Active Directory 특성 이름을 지정 합니다. 이 특성은 hello AlternateLoginId 특성으로 사용 됩니다. 이 레지스트리 값은 tooa를 설정 하는 경우 [유효한 Active Directory 특성](https://msdn.microsoft.com/library/ms675090.aspx) (예: 메일 또는 displayName)에 대해 다음 hello 특성의 값 hello 사용자의 UPN 대신 인증에 사용 됩니다. 이 레지스트리 값이 비어 구성 다음 AlternateLoginId 비활성화 되 고 UPN hello 사용자 인증에 사용 됩니다. |
| LDAP_FORCE_GLOBAL_CATALOG | 부울 | False | AlternateLoginId를 조회할 때 LDAP 검색을 위해 글로벌 카탈로그의 플래그 tooforce hello 사용이를 사용 합니다. Hello AlternateLoginId 특성 toohello 글로벌 카탈로그 추가 도메인 컨트롤러를 글로벌 카탈로그로 구성 하 고이 플래그를 설정 합니다. <br><br> LDAP_LOOKUP_FORESTS (비어 있지 않음), 구성 된 경우 **이 플래그를 true로 적용**hello hello 레지스트리 설정 값에 관계 없이 합니다. 이 경우 NPS 확장 hello hello 글로벌 카탈로그 toobe 각 포리스트에 대 한 hello AlternateLoginId 특성을 사용 하 여 구성 해야 합니다. |
| LDAP_LOOKUP_FORESTS | string | Empty | 포리스트 toosearch의 세미콜론으로 구분 된 목록을 제공 합니다. 예를 들어 *contoso.com;foobar.com*과 같습니다. 이 레지스트리 값을 구성 하는 경우 hello NPS 확장 hello 순서 대로 나열 된 하 고 하 던 hello 첫 번째 성공적인 AlternateLoginId 값을 반환 모든 hello 포리스트에 반복적으로 검색 합니다. 이 레지스트리 값이 구성 되지 않은 경우 hello AlternateLoginId 조회 예외일된 toohello 현재 도메인입니다.|

tootroubleshoot 문제는 대체 로그인 Id 사용 하 여 단계를 권장 하는 hello [대체 로그인 ID 오류](multi-factor-authentication-nps-errors.md#alternate-login-id-errors)합니다.

## <a name="ip-exceptions"></a>IP 예외

Toomonitor 서버 가용성, 부하 분산 장치 작업 부하를 보내기 전에 실행 중인 서버를 확인 하는 경우 처럼 필요한 경우에 이러한 검사 toobe 확인 요청에 의해 차단 바람직하지 않습니다. 대신, 서비스 계정에서 사용되는 것으로 알고 있는 IP 주소의 목록을 만들고 해당 목록에 대한 Multi-Factor Authentication 요구 사항을 사용하지 않도록 설정합니다. 

IP 화이트 리스트 tooconfigure 너무 이동`HKLM\SOFTWARE\Microsoft\AzureMfa` hello 다음 레지스트리 값을 구성 합니다. 

| 이름 | 형식 | 기본값 | 설명 |
| ---- | ---- | ------------- | ----------- |
| IP_WHITELIST | string | Empty | IP 주소 목록을 세미콜론으로 구분된 형태로 제공합니다. 서비스 요청 발생 한 위치, NAS/VPN 서버 hello와 같은 컴퓨터의 hello IP 주소를 포함 합니다. IP 범위는 지원되지 않는 서브넷입니다. <br><br> 예: *10.0.0.1;10.0.0.2;10.0.0.3*.

Hello 허용 목록에 존재 하는 IP 주소에서 한 요청이 들어올 때 2 단계 인증을 건너뜁니다. hello IP 화이트 리스트는 hello에 제공 되는 IP 주소를 비교한 toohello *ratNASIPAddress* 특성 hello RADIUS 요청입니다. 다음 경고 hello 로깅됩니다 RADIUS 요청이 들어올 hello ratNASIPAddress 특성이 없는 경우: "P_WHITE_LIST_WARNING::IP 화이트 리스트 원본 IP가 NasIpAddress 특성에 RADIUS 요청에서 누락 되어 무시 되 고 됩니다."

## <a name="next-steps"></a>다음 단계

[Azure Multi-factor Authentication에 대 한 hello NPS 확장에서에서 오류 메시지를 해결 합니다.](multi-factor-authentication-nps-errors.md)
