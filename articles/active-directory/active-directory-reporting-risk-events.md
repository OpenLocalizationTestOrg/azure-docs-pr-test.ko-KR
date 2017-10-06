---
title: "Active Directory 위험 이벤트 aaaAzure | Microsoft Docs"
description: "이 항목에서는 위험 이벤트의 자세한 개요를 제공합니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 보안, 위험, 위험 이벤트, 취약점, 보안 정책"
author: MarkusVi
manager: femila
ms.assetid: fa2c8b51-d43d-4349-8308-97e87665400b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d771c1f43707744aac728c4f72000d855cbd6e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-risk-events"></a>Azure Active Directory 위험 이벤트

공격자는 사용자의 id를 도용 하 여 액세스 tooan 환경 수 hello 포함 된 대부분의 보안 위반 걸릴 놓습니다. 손상된 ID를 검색하는 것은 쉬운 작업이 아닙니다. Azure Active Directory 적응 컴퓨터 학습 알고리즘 및 추론 toodetect 의심 스러운 동작을 관련된 tooyour 사용자 계정을 사용 합니다. 검색된 각 의심스러운 동작은 *위험 이벤트*라는 레코드에 저장됩니다.

현재, Azure Active Directory는 6가지 유형의 위험 이벤트를 검색합니다.

- [자격 증명이 손실된 사용자](#leaked-credentials) 
- [익명 IP 주소에서 로그인](#sign-ins-from-anonymous-ip-addresses) 
- [이동 불가능 tooatypical 위치](#impossible-travel-to-atypical-locations) 
- [알 수 없는 위치에서 로그인](#sign-in-from-unfamiliar-locations)
- [감염된 장치에서 로그인](#sign-ins-from-infected-devices) 
- [의심스러운 작업이 있는 IP 주소에서 로그인](#sign-ins-from-ip-addresses-with-suspicious-activity) 


![위험 이벤트](./media/active-directory-reporting-risk-events/91.png)

이 항목에서는 위험 이벤트의 자세한 개요는 하 고 사용 하는 방법으로 tooprotect Azure AD id 제공 합니다.


## <a name="risk-event-types"></a>위험 이벤트 유형

hello 위험 이벤트 유형 속성은 hello 의심 스러운 동작 위험 이벤트 레코드에 대 한 식별자에 대해 만들었습니다.  
Microsoft의 지속적인 투자 hello 검색 프로세스를 사항이 되었습니다.

- 기존 위험 이벤트의 toohello 검색 정확도 향상 
- Hello 앞에 추가 될 새 위험 이벤트 유형

### <a name="leaked-credentials"></a>유출된 자격 증명

사이버 범죄자 들 손상 합법적인 사용자의 유효한 암호 때 hello 범죄자는 종종 해당 자격 증명을 공유 합니다. 이 게시 함으로써 공개적으로 hello 어두운 붙여넣기 또는 웹 사이트 또는에 거래 또는 hello 자격 증명 hello 검정 시장에 판매 하 여 일반적으로 수행 됩니다. hello Microsoft 유출 자격 증명 서비스 획득 사용자 이름 / 암호 쌍을 사용 하 여 및 어두운 및 공용 웹 사이트를 모니터링 하 여:

- 연구원
- 사법 기관
- Microsoft 보안 팀
- 신뢰할 수 있는 기타 소스 

Hello 서비스 사용자 이름을 획득 하는 경우 / 암호 쌍은 대해 검사 하 여 AAD 사용자의 현재 유효한 자격 증명입니다. 일치하면 사용자의 암호가 손상된 것이며 *누출된 자격 증명 위험 이벤트*가 만들어집니다.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>익명 IP 주소에서 로그인

이 위험 이벤트 유형은 익명 프록시 IP 주소로 식별된 IP 주소에서 시도하여 성공적으로 로그인한 사용자를 식별합니다. 이러한 프록시는 원하는 toohide 사람에 의해 해당 장치의 IP 주소를 사용 하 고 악의적인 공격에 사용할 수 있습니다.


### <a name="impossible-travel-tooatypical-locations"></a>이동 불가능 tooatypical 위치

이 위험 이벤트 유형 식별 2 회의 로그인 동작 과거 여기서 hello 위치 중 하나 이상을 수도 있습니다 hello 사용자에 대 한 불규칙, 지리적으로 멀리 떨어진 위치에서 발생 합니다. 또한 hello 두 로그인 간 hello 시간은 것이 소요 되었을 hello 사용자 tootravel hello 첫 번째 위치 toohello에서 두 번째 hello 시간 미만, 동일 hello 다른 사용자가 사용 되 고 있는지를 나타내는 자격 증명입니다. 

이 확실 한 무시 하는 기계 학습 알고리즘 "*거짓 긍정*" Vpn 및 hello 조직의 다른 사용자가 정기적으로 사용 되는 위치와 같은 toohello 이동 불가능 조건 기여 합니다.  hello 시스템 14 일은 새 사용자의 로그인 동작을 파악 하는 초기 학습 기간을 있습니다.

### <a name="sign-in-from-unfamiliar-locations"></a>잘 모르는 위치에서 로그인

로그인 위치 지난 고려이 위험 이벤트 유형 (IP, 위도 / 경도 및 ASN) toodetermine 새 / 생소 한 위치입니다. hello 시스템 사용자가 사용 되는 이전 위치에 대 한 정보를 저장 하 고 이러한 "친숙 한" 위치를 고려 합니다. hello 위험 이벤트는 hello 로그인 hello 위치 목록에 친숙 하지 않은 위치에서 발생 하는 경우에 트리거됩니다. hello 시스템에 없는 것 표시 하지 않습니다 새 위치를 잘 모르는 위치로 30 일의 초기 학습 기간에는 있습니다. hello 시스템도 친숙 한 장치에서 로그인을 무시 하 고 있는 지리적 위치 tooa 친숙 한 위치를 닫습니다. 

### <a name="sign-ins-from-infected-devices"></a>감염된 장치에서 로그인

이 위험 이벤트 유형을 알려진 tooactively 봇 서버와 통신 하는 맬웨어에 감염 된 장치에서 로그인을 식별 합니다. 이 작업은 봇 서버와 접촉 되어 있는 IP 주소에 대 한 hello 사용자의 장치의 IP 주소를 상호 연결 하 여 결정 됩니다. 

### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>의심스러운 작업이 있는 IP 주소에서 로그인
이 위험 이벤트 유형은 짧은 기간 동안에 여러 사용자 계정에서 실패한 로그인 시도가 많이 확인되는 IP 주소를 식별합니다. 이 공격자의 목표가 사용 되는 IP 주소의 트래픽 패턴 일치 하며 된 계정 중 하나는 이미 파일이 나 toobe 손상에 대 한 강한 지표. 이 확실 한 무시 하는 기계 학습 알고리즘 "*거짓 긍정*"와 같은 IP 주소에 정기적으로 hello 조직의 다른 사용자가 사용 됩니다.  hello 시스템에 있는 새 사용자와 새 테 넌 트의 hello 로그인 동작을 파악 초기 학습 기간이 14 일입니다.


## <a name="detection-type"></a>검색 유형

hello 검색 type 속성은 표시기 (실시간 또는 오프 라인)는 위험 이벤트의 hello 검색 기간에 대 한 합니다.  
현재 대부분 위험 이벤트는 오프 라인 상태로 확인 후 처리 작업에서 hello 위험 이벤트 발생 후 합니다.

다음 표에서 hello hello 기간 차지 검색 유형 tooshow에 대 한 관련된 보고서에 나와 있습니다.

| 검색 유형 | 보고 대기 시간 |
| --- | --- |
| 실시간 | too10 5 분 |
| 오프라인 | 2 too4 시간 |


Azure Active Directory 검색 hello 위험 이벤트 유형, hello 검색 유형은 다음과 같습니다.

| 위험 이벤트 유형 | 검색 유형 |
| :-- | --- | 
| [자격 증명이 손실된 사용자](#leaked-credentials) | 오프라인 |
| [익명 IP 주소에서 로그인](#sign-ins-from-anonymous-ip-addresses) | 실시간 |
| [이동 불가능 tooatypical 위치](#impossible-travel-to-atypical-locations) | 오프라인 |
| [알 수 없는 위치에서 로그인](#sign-in-from-unfamiliar-locations) | 실시간 |
| [감염된 장치에서 로그인](#sign-ins-from-infected-devices) | 오프라인 |
| [의심스러운 작업이 있는 IP 주소에서 로그인](#sign-ins-from-ip-addresses-with-suspicious-activity) | 오프라인|


## <a name="risk-level"></a>위험 수준

위험 이벤트의 hello 위험 수준 속성은 hello 심각도 및 위험 이벤트의 hello 신뢰성에 대 한 표시기 (높음, 중간 또는 낮음)입니다. 이 속성을 사용 tooprioritize hello 작업을 수행 해야 하면 있습니다. 

hello 위험 이벤트의 심각도 hello identity 손상의 예측 hello 신호의 hello 강도를 나타냅니다.  
hello 신뢰도의 거짓 긍정 hello 가능성에 대 한 표시기입니다. 

예를 들면 다음과 같습니다. 

* **높음**: 신뢰도 및 심각도가 높은 위험 이벤트입니다. 이러한 이벤트는 강력한 표시기 hello 사용자의 id가 손상 된 및 영향을 받는 모든 사용자 계정에 즉시 재구성 해야 합니다.

* **보통**: 심각도가 높지만 신뢰도가 낮은 위험 이벤트 또는 그 반대의 경우입니다. 이러한 이벤트는 잠재적으로 위험하며 영향을 받는 사용자 계정은 수정되어야 합니다.

* **낮음**: 신뢰도 및 심각도가 낮은 위험 이벤트입니다. 이 이벤트 즉각적 조치가 필요 하지 않을 수 있지만 다른 위험 이벤트와 함께 사용 하면 identity hello는 손상 된를 제공할 수 있습니다.

![위험 수준](./media/active-directory-reporting-risk-events/01.png)

### <a name="leaked-credentials"></a>유출된 자격 증명

위험 이벤트로 분류 된 자격 증명을 유출는 **높은**뚜렷한 hello 사용자 이름 및 암호는 사용할 수 있는 tooan 공격자를 제공 하므로 합니다.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>익명 IP 주소에서 로그인

이 위험 이벤트 유형에 대 한 hello 위험 수준이 **보통** 익명 IP 주소는 계정 손상의 강력한 표시 없기 때문에 있습니다.  
익명 IP 주소 사용 중인 경우 hello 사용자 tooverify 즉시 문의 하는 것이 좋습니다.


### <a name="impossible-travel-tooatypical-locations"></a>이동 불가능 tooatypical 위치

이동 불가능는 일반적으로 해커가 수 toosuccessfully 로그인 했음을 나타내는 좋은 지표로 합니다. 그러나 거짓 긍정 hello 조직의 다른 사용자가 일반적으로 사용 되지 않는 VPN 또는 새 장치를 사용 하 여 사용자가 이동 중 발생할 수 있습니다. 거짓 긍정의 다른 소스는 클라이언트 hello 모양을 초래할 수 있는 Ip로 올바르게 서버 Ip를 전달 하는 응용 프로그램 로그인 수행 하 고 여기서 해당 응용 프로그램의 백 엔드 hello 데이터 센터에서 호스팅되는 (종종 이들은 Microsoft 데이터 센터 hello 모양을 제공 될 수 있습니다 하는 로그인의 IP 주소를 소유 microsoft에서 수행). 이 위험 이벤트에 대 한 hello 위험 수준을 이러한 거짓 긍정의 결과로 **보통**합니다.

> [!TIP]
> 구성 하 여이 위험 이벤트 유형에 대 한 보고 된 false positves hello 양을 줄일 수 있습니다 [명명 된 위치](active-directory-named-locations.md)합니다. 

### <a name="sign-in-from-unfamiliar-locations"></a>잘 모르는 위치에서 로그인

생소 한 위치 수 toouse id를 도난 당한 경우 공격자가 임을 나타냅니다를 제공할 수 있습니다. 가양성은 사용자가 이동하거나, 새 장치를 사용하거나, 새 VPN을 사용할 때 발생할 수 있습니다. 이 종류의 이벤트에 대 한 hello 위험 수준을 이러한 가양성 결과로 **보통**합니다.

### <a name="sign-ins-from-infected-devices"></a>감염된 장치에서 로그인

이 위험 이벤트는 사용자 장치가 아닌 IP 주소를 식별합니다. 경우는 단일 IP 주소를 뒤에 여러 장치가 고 일부는에 의해 제어 bot 네트워크에서 다른 장치에서 로그인 트리거 내이 이벤트 불필요 하 게이 위험 이벤트를 분류 하기 위한 hello 이유 변수인으로 **낮은**합니다.  

Hello 사용자에 게 문의 한 모든 hello 사용자의 장치를 검색 하는 것이 좋습니다. 사용자의 개인 장치에 감염 되었거나 hello에서 감염 된 장치에 사용 된 하 다른 사람 앞에서 설명한 것 처럼 동일한 IP 주소 hello 사용자로 수 이기도 합니다. 감염 된 장치는 바이러스 백신 소프트웨어에서 아직 확인 되지 않은 및 감염 hello 장치 toobecome를 일으킬 수 있는 잘못 된 사용자 습관으로 나타낼 수도 있습니다는 맬웨어에 감염 경우가 많습니다.

방법에 대 한 자세한 내용은 tooaddress 맬웨어 감염 참조 hello [맬웨어 보호 센터](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409)합니다.


### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>의심스러운 작업이 있는 IP 주소에서 로그인

로그인 한 경우 이러한 실제로 의심으로 표시 된 IP 주소에서 사용자 tooverify hello를 문의 하는 것이 좋습니다. 이 종류의 이벤트에 대 한 hello 위험 수준이 "**보통**" hello 뒤 여러 장치에 있을 수 있으므로 hello 의심 스러운 활동에 대 한 책임 수 있지만 일부의 동일한 IP 주소입니다. 


 
## <a name="next-steps"></a>다음 단계

위험 이벤트는 사용자 Azure AD id 보호 하기 위한 hello foundation입니다. Azure AD는 현재 여섯 가지 위험 이벤트를 감지할 수 있습니다. 


| 위험 이벤트 유형 | 위험 수준 | 검색 유형 |
| :-- | --- | --- |
| [자격 증명이 손실된 사용자](#leaked-credentials) | 높음 | 오프라인 |
| [익명 IP 주소에서 로그인](#sign-ins-from-anonymous-ip-addresses) | 중간 | 실시간 |
| [이동 불가능 tooatypical 위치](#impossible-travel-to-atypical-locations) | 중간 | 오프라인 |
| [알 수 없는 위치에서 로그인](#sign-in-from-unfamiliar-locations) | 중간 | 실시간 |
| [감염된 장치에서 로그인](#sign-ins-from-infected-devices) | 낮음 | 오프라인 |
| [의심스러운 작업이 있는 IP 주소에서 로그인](#sign-ins-from-ip-addresses-with-suspicious-activity) | 중간 | 오프라인|

사용자는 어디 hello 사용자 환경에서 검색 된 위험 이벤트?
두 곳에서 보고된 위험 이벤트를 검토할 수 있습니다.

 - **Azure AD 보고** - 위험 이벤트는 Azure AD의 보안 보고서의 일부입니다. 자세한 내용은 참조 hello [위험 보안 보고서에 사용자가](active-directory-reporting-security-user-at-risk.md) hello 및 [위험한 로그인 보안 보고서](active-directory-reporting-security-risky-sign-ins.md)합니다.

 - **Azure AD ID 보호** - 위험 이벤트는 [Azure Active Directory ID 보호](active-directory-identityprotection.md) 보고 기능의 일부입니다.
    

Hello 검색 하는 위험 이벤트 이미 id를 보호 하는 중요 한 측면을 나타내는 동안 hello 옵션 tooeither를 수동으로 해결할 또는 조건부 액세스 정책을 구성 하 여 자동화 된 응답을 구현할 수도 있습니다. 자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.
 
