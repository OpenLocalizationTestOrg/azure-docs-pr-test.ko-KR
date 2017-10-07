---
title: "Active Directory Id 보호 플레이 북 aaaAzure | Microsoft Docs"
description: "Azure AD Identity Protection을 통해 방법을 공격자가 tooexploit 노출된 된 id의 toolimit hello 능력 또는 장치와 toosecure id 또는 장치 의심 되는 또는 알려진 toobe를 이전에 손상에 대해 알아봅니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 클라우드 앱 검색, 응용 프로그램 관리, 보안, 위험, 위험 수준, 취약점, 보안 정책"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a>Azure Active Directory ID 보호 플레이 북
이 플레이 북은 다음 작업을 수행하는 데 도움이 됩니다.

* 위험 이벤트 시뮬레이션 및 취약성 여 hello Id 보호 환경에서 데이터를 채울
* 위험 기반 조건부 액세스 정책을 설정 및 테스트 이러한 정책의 hello 영향

## <a name="simulating-risk-events"></a>위험 이벤트 시뮬레이션
이 섹션에서는 위험 이벤트 유형만 hello를 시뮬레이트하기 위한 단계를 제공 합니다.

* 익명 IP 주소에서 로그인(초급)
* 잘 모르는 위치에서 로그인(중급)
* 이동 불가능 tooatypical 위치 (어려운)

안전한 방법으로 다른 위험 이벤트를 시뮬레이션할 수 없습니다.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>익명 IP 주소에서 로그인
이 위험 이벤트 유형은 익명 프록시 IP 주소로 식별된 IP 주소에서 시도하여 성공적으로 로그인한 사용자를 식별합니다. 이러한 프록시는 원하는 toohide 사람에 의해 해당 장치의 IP 주소를 사용 하 고 악의적인 의도에 사용할 수 있습니다.

**익명 IP에서 로그인에 toosimulate 수행할 단계를 수행 하는 hello**:

1. Hello 다운로드 [Tor 브라우저](https://www.torproject.org/projects/torbrowser.html.en)합니다.
2. Hello Tor 브라우저를 사용 하 여 이동 너무[https://myapps.microsoft.com](https://myapps.microsoft.com)합니다.   
3. Hello에 tooappear hello 계정 hello 자격 증명을 입력 **익명 IP 주소에서 로그인** 보고서입니다.

hello에 대 한 로그인에 표시 됩니다 hello Id 보호 대시보드 5 분 이내입니다. 

### <a name="sign-ins-from-unfamiliar-locations"></a>알 수 없는 위치에서 로그인
hello 생소 한 위치 위험은 로그인 위치 지난 간주 하는 실시간 로그인 평가 메커니즘 (IP, 위도 / 경도 및 ASN) toodetermine 새 / 생소 한 위치입니다. hello 시스템 저장 이전 ip 주소로 위도 / 경도 및 사용자의 Asn 이러한 toobe 친숙 한 위치 않은 것으로 간주 합니다. 로그인 위치 hello 로그인 위치와 일치 하지 않으면 hello 기존 친숙 한 위치에 익숙하지 않은 간주 됩니다.

Azure Active Directory ID 보호:  

* 새로운 위치를 알 수 없는 위치의 플래그로 지정하지 않는 14일의 초기 학습 기간이 있습니다.
* 친숙 한 장치 및 위치를 지리적으로 닫기 tooan 기존 친숙 한 위치에서 로그인을 무시 합니다.

toosimulate 생소 한 위치를가지고 toosign 위치와 hello 계정에 로그인 하지에서 하기 전에 장치에서 합니다. 

**로그인 생소 한 위치에서 toosimulate 수행할 단계를 수행 하는 hello**:

1. 적어도 14일의 로그인 기록이 있는 계정을 선택합니다. 
2. 다음 중 하나를 수행합니다.
   
   a. VPN을 사용 하는 동안 이동 너무[https://myapps.microsoft.com](https://myapps.microsoft.com) toosimulate hello 위험 이벤트에 대 한 hello 계정 hello 자격 증명을 입력 합니다.
   
   b. (권장 하지 않음) hello 계정의 자격 증명을 사용 하 여 다른 위치 toosign에서 동료에 게 요청 합니다.

hello에 대 한 로그인에 표시 됩니다 hello Id 보호 대시보드 5 분 이내입니다.

### <a name="impossible-travel-tooatypical-location"></a>이동 불가능 tooatypical 위치
Hello 알고리즘 거짓 긍정 hello 디렉터리에 다른 사용자가 사용 되는 Vpn에서 로그인 등 친숙 한 장치에서 이동 불가능으로 컴퓨터 학습 tooweed 사용 하기 때문에 hello 이동 불가능 조건을 시뮬레이션 하는 것은 어렵습니다. 또한 hello 알고리즘 위험 이벤트 생성을 시작 하기 전에 3 too14 일 로그인 기록을 hello 사용자에 대 한 필요 합니다.

**toosimulate 이동 불가능 tooatypical 위치를 사용 하는 단계를 수행 하는 hello 수행**:

1. 표준 브라우저를 사용 하 여 이동 너무[https://myapps.microsoft.com](https://myapps.microsoft.com)합니다.  
2. Toogenerate에 대 한 이동 불가능 위험 이벤트를 원하는 hello 계정의 hello 자격 증명을 입력 합니다.
3. 사용자 에이전트를 변경합니다. 사용자 에이전트 전환기 추가 기능을 사용하여 개발자 도구에서 Internet Explorer의 사용자 에이전트를 변경하거나 Firefox 또는 Chrome에서 사용자 에이전트를 변경할 수 있습니다.
4. 사용자의 IP 주소를 변경합니다. VPN, Tor 추가 기능을 사용하거나 다른 데이터 센터의 Azure에서 새 컴퓨터를 스핀업하여 사용자의 IP 주소를 변경할 수 있습니다.
5. 로그인 너무[https://myapps.microsoft.com](https://myapps.microsoft.com) 이전 처럼 및 hello 이전 로그인 후 몇 분 내에 동일한 자격 증명을 hello를 사용 하 여 합니다.

hello에 대 한 로그인에에서 표시 됩니다 hello Id 보호 대시보드 2-4 시간 이내입니다.<br>
학습 모델에 관련 된 복잡 한 컴퓨터 hello 인해 하도록 선택 하지 됩니다 것 가능성이 높습니다.<br> 여러 Azure AD 계정에 대 한 tooreplicate 다음이 단계를 할 수 있습니다.

## <a name="simulating-vulnerabilities"></a>취약점 시뮬레이션
취약점은 잘못된 행위자에 의해 악용될 수 있는 Azure AD 환경의 단점입니다. 현재 3가지 유형의 취약점은 Azure AD의 다른 기능을 활용하는 Azure AD ID 보호에 표시됩니다. 이러한 취약점 나타납니다 hello Identity Protection 대시보드에서 자동으로 이러한 기능이 설정 되 면 합니다.

* Azure AD [Multi-Factor Authentication이란?](../multi-factor-authentication/multi-factor-authentication.md)
* Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).
* Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="user-compromise-risk"></a>사용자 손상 위험
**사용자 손상 위험 tootest 수행할 단계를 수행 하는 hello**:

1. 로그인 너무[https://portal.azure.com](https://portal.azure.com) 테 넌 트에 대 한 전역 관리자 자격 증명을 사용 합니다.
2. 너무 이동**Id 보호**합니다. 
3. 주 hello에 **Azure AD Identity Protection** 블레이드에서 클릭 **설정을**합니다. 
4. Hello에 **포털 설정** 블레이드 아래 **보안 규칙**, 클릭 **사용자 손상 위험**합니다. 
5. Hello에 **위험에 로그인** 블레이드에서 설정 **사용 규칙이** 있는데 클릭 **저장** 설정 합니다.
6. 지정된 사용자 계정의 경우 알 수 없는 위치 또는 익명 IP 위험 이벤트를 시뮬레이션합니다. 이 권한 상승 해당 사용자에 대 한 hello 사용자 위험 수준을 너무**보통**합니다.
7. 몇 분 정도 기다린 후에 사용자에 대한 해당 사용자 수준이 **보통**인지 확인합니다.
8. Toohello 이동 **포털 설정** 블레이드입니다.
9. Hello에 **사용자 손상 위험** 블레이드 아래 **사용 규칙이**선택, **에** 합니다. 
10. Hello 다음 옵션 중 하나를 선택 합니다.
    
    a. tooblock, **보통** 아래 **블록 로그인**합니다.
    
    b. 선택 tooenforce 보안 된 암호 변경 **보통** 아래 **multi-factor authentication 필요**합니다.
11. **Save**를 클릭합니다.
12. 이제 위험 수준이 상승한 사용자로 로그인하여 위험 기반 조건부 액세스를 테스트할 수 있습니다. Hello 사용자 위험 중간 이면 hello 구성 정책에 따라 사용자 로그인이 차단 하거나 또는 toochange 강제 암호입니다. 
    <br><br>
    ![플레이 북](./media/active-directory-identityprotection-playbook/201.png "플레이 북")
    <br>

## <a name="sign-in-risk"></a>로그인 위험
**tootest 위험 로그인 hello 다음 단계를 수행 합니다.**

1. 로그인 너무[https://portal.azure.com ](https://portal.azure.com) 테 넌 트에 대 한 전역 관리자 자격 증명을 사용 합니다.
2. 너무 이동**Id 보호**합니다.
3. 주 hello에 **Azure AD Identity Protection** 블레이드에서 클릭 **설정을**합니다. 
4. Hello에 **포털 설정** 블레이드 아래 **보안 규칙**, 클릭 **위험 로그인**합니다.
5. Hello에 * * 위험 로그인 * * 블레이드를 **에** 아래 **사용 규칙이**합니다. 
6. Hello 다음 옵션 중 하나를 선택 합니다.
   
   a. tooblock, **보통** 아래 **블록에 로그인**
   
   b. 선택 tooenforce 보안 된 암호 변경 **보통** 아래 **multi-factor authentication 필요**합니다.
7. tooblock, 블록 아래 선택 중간에 로그인 합니다.
8. tooenforce multi-factor authentication을 선택 **보통** 아래 **multi-factor authentication 필요**합니다.
9. **Save**를 클릭합니다.
10. 이제 hello 생소 한 위치를 시뮬레이션 하 여 위험을 기준으로 조건부 액세스를 테스트할 수 있습니다 또는 둘 다 되기 때문에 익명 IP 위험 이벤트 **보통** 이벤트 위험 합니다.


![플레이 북](./media/active-directory-identityprotection-playbook/200.png "플레이 북")


## <a name="see-also"></a>참고 항목
* [Azure Active Directory ID 보호](active-directory-identityprotection.md)

