---
title: "AD FS와 Azure AD Connect Health aaaUsing | Microsoft Docs"
description: "Hello Azure AD Connect Health 페이지를 어떻게 이것이 toomonitor 온-프레미스 AD FS 인프라입니다."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
editor: curtand
ms.assetid: dc0e53d8-403e-462a-9543-164eaa7dd8b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0cd26e8762be65e09d22e1f113e5165c4f131715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-ad-fs-using-azure-ad-connect-health"></a>Azure AD Connect Health를 사용하여 AD FS 모니터링
다음 설명서 hello 특정 toomonitoring Azure AD Connect Health를 AD FS 인프라는 합니다. Azure AD Connect Health와 함께 Azure AD Connect (동기화)를 모니터링하는 방법에 대한 정보는 [동기화를 위해 Azure AD Connect Health 사용](active-directory-aadconnect-health-sync.md)을 참조하세요. 또한 Azure AD Connect Health와 함께 Active Directory 도메인 서비스를 모니터링하는 방법에 대한 정보는 [AD DS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adds.md)을 참조하세요.

## <a name="alerts-for-ad-fs"></a>AD FS의 경고
Azure AD Connect Health 경고 섹션 hello 활성 경고 목록이 hello를 제공 합니다. 각 경고 관련 정보, 해결 단계 및 toorelated 설명서 링크를 포함합니다.

활성 또는 해결 된 경고, tooopen와 추가 정보는 새 블레이드가 두 번 클릭 수, 경고 및 링크 toorelevant 설명서 tooresolve 수행할 수 있는 단계 hello 합니다. 또한 hello 과거에 해결 된 경고에 기록 데이터를 볼 수 있습니다.

![Azure AD Connect Health 포털](./media/active-directory-aadconnect-health/alert2.png)

## <a name="usage-analytics-for-ad-fs"></a>AD FS의 사용량 분석
Azure AD Connect Health 사용 현황 분석은 페더레이션 서버 hello 인증 트래픽을 분석합니다. Hello 사용 현황 분석 상자 tooopen hello 사용 현황 분석 블레이드에서 여러 메트릭 및 그룹화 보여 주는 두 번 수 있습니다.

> [!NOTE]
> AD FS와 함께 사용 현황 분석 toouse 있어야 AD FS 감사가 설정 된 합니다. 자세한 내용은 [AD FS 감사 사용](active-directory-aadconnect-health-agent-install.md#enable-auditing-for-ad-fs)을 참조하십시오.
>
>

![Azure AD Connect Health 포털](./media/active-directory-aadconnect-health/report1.png)

tooselect 추가 메트릭을 toochange hello 그룹화 또는 시간 범위를 지정 하 고 hello 사용 현황 분석 차트를 마우스 오른쪽 단추로 클릭 차트 편집을 선택 합니다. 그런 다음 hello 시간 범위를 지정 하 고, 다른 메트릭을 선택 하 고, hello 그룹화 변경 수 있습니다. 서로 다른 "메트릭"에 따라 hello 인증 트래픽의 hello 배포를 볼 수 있고 hello 다음 섹션에에서 설명 된 관련 "그룹화 기준" 매개 변수를 사용 하 여 각 메트릭을 그룹화 됩니다.

**메트릭: 총 요청 수** - AD FS 서버에서 처리한 총 요청 수.

|그룹화 기준 | 어떤 hello 그룹화 방법 및 그것이 유용한 이유는? |
| --- | --- |
| 모두 | Hello 모든 AD FS 서버에서 처리의 총 수를 보여 줍니다.|
| 응용 프로그램 | 그룹에는 전체 요청을 대상으로 하는 hello 신뢰 당사자 hello 합니다. 이 그룹화는 유용한 toounderstand hello 총 트래픽 양을 백분율로 응용 프로그램을 수신 합니다. |
|  서버 |그룹 hello hello 요청을 처리 한 hello 서버 기반 총 요청 수입니다. 이 그룹화는 총 트래픽 hello 유용 toounderstand hello 부하 분산 합니다.
| 작업 공간 연결 |그룹에는 총 요청 된 작업 공간 연결 장치에서 생성 되는 여부에 따라 알려진 hello 합니다. 이 그룹화는 유용한 toounderstand는 알 수 없는 toohello id 인프라는 장치를 사용 하 여 리소스 액세스 되는 경우. |
|  인증 방법 | 그룹 hello 전체 요청을 인증에 사용 된 hello 인증 방법입니다. 이 그룹화는 유용한 toounderstand hello 공통 인증 방법을 인증에 사용 되는 합니다. 다음은 hello 가능한 인증 방법 <ol> <li>Windows 통합 인증(Windows)</li> <li>폼 기반 인증(양식)</li> <li>SSO(Single Sign On)</li> <li>X509 인증서 인증(인증서)</li> <br>Hello 페더레이션 서버가 SSO 쿠키를 사용 하 여 hello 요청을 받을 경우 해당 요청은 SSO (Single Sign On)로 계산 됩니다. 이러한 경우 hello 쿠키가 유효 하다 면 경우 hello 사용자 tooprovide 자격 증명을 요청 되지 않은 하 고 원활한 액세스 toohello 응용 프로그램을 가져옵니다. 이 동작은 hello 페더레이션 서버로 보호 되는 여러 신뢰 당사자를 설정한 경우에 일반적입니다. |
| 네트워크 위치 | 그룹 hello hello 사용자의 hello 네트워크 위치에 따라 총 요청 수입니다. 네트워크 위치는 인트라넷 또는 엑스트라넷이 될 수 있습니다. 이 그룹화는 hello 트래픽의 비율 hello 인트라넷 및 엑스트라넷에서 가져온 tooknow 유용 합니다. |


**메트릭: 총 실패 한 요청** -hello 페더레이션 서비스에서 처리 된 요청에 실패 한 hello 총 수입니다. (이 메트릭은 Windows Server 2012 R2용 AD FS에서만 사용할 수 있습니다.)

|그룹화 기준 | 어떤 hello 그룹화 방법 및 그것이 유용한 이유는? |
| --- | --- |
| 오류 유형 | 미리 정의 된 오류 형식에 기반 하 여 오류 hello 수가 표시 됩니다. 이 그룹화는 유용한 toounderstand hello 일반적인 유형의 오류입니다. <ul><li>잘못 된 사용자 이름 또는 암호가: tooincorrect 사용자 이름 또는 암호가 않아서 발생 한 오류입니다.</li> <li>"엑스트라넷 잠금을": 엑스트라넷에서 잠긴 사용자 로부터 받은 toohello 요청 인해 오류가 발생 했습니다. </li><li> "암호 만료": 만료 된 암호를 사용 하 여 toousers 로깅 인해 오류가 발생 했습니다.</li><li>"계정을 사용할 수 없게": toousers 로깅 사용할 수 없는 계정으로 인해 오류가 발생 했습니다.</li><li>"장치 인증": 장치 인증을 사용 하 여 실패 한 toousers tooauthenticate 인해 오류가 발생 했습니다.</li><li>"사용자 인증서 인증": 잘못 된 인증서로 인해 실패 한 toousers tooauthenticate 인해 오류가 발생 했습니다.</li><li>"MFA": Multi-factor Authentication을 사용 하 여 실패 한 toouser tooauthenticate 인해 오류가 발생 했습니다.</li><li>"다른 자격 증명": "발급 권한 부여": tooauthorization 오류 인해 오류가 발생 했습니다.</li><li>"발급 위임": tooissuance 위임 오류 인해 오류가 발생 했습니다.</li><li>"동의 토큰": 타사 Id 공급자 로부터 토큰 hello tooADFS 거부 인해 오류가 발생 했습니다.</li><li>"Protocol": tooprotocol 오류 때문에 실패 합니다.</li><li>"알 수 없음": 모두 Catch합니다. Hello에 적합 하지 않은 다른 모든 오류 범주를 정의 합니다.</li> |
| 서버 | 그룹 hello hello 서버에 기반 하 여 오류입니다. 이 그룹화는 서버에 대해 유용한 toounderstand hello 오류 분포입니다. 분포가 균일하지 않으면 특정 서버에 문제가 있음을 나타낼 수 있습니다. |
| 네트워크 위치 | 그룹 hello hello 요청 (인트라넷 및 엑스트라넷) hello 네트워크 위치에 기반 하 여 오류입니다. 이 그룹화는 유용한 toounderstand hello 형식의 실패 하는 요청입니다. |
|  응용 프로그램 | 그룹 hello hello 대상 응용 프로그램 (신뢰 당사자)에 따라 오류가 발생 했습니다. 이 그룹화는 유용한 toounderstand 대부분 오류 수를 보고 하는 대상된 응용 프로그램입니다. |

**메트릭: 사용자 수** - 적극적으로 AD FS를 사용하여 인증하는 평균 고유 사용자 수

|그룹화 기준 | 어떤 hello 그룹화 방법 및 그것이 유용한 이유는? |
| --- | --- |
|모두 |이 메트릭은 평균 hello 페더레이션 서비스를 사용 하 여 hello 선택한 시간 조각에는 사용자 수의 개수를 제공 합니다. hello 사용자 그룹화 되지 않습니다. <br>hello 평균 hello 시간 조각에서 선택에 따라 달라 집니다. |
| 응용 프로그램 |Hello에 따라 사용자의 그룹 hello 평균 수 (신뢰 당사자) 응용 프로그램을 대상으로 합니다. 이 그룹화는 유용한 toounderstand 사용자 수에 응용 프로그램을 사용 하는 합니다. |

## <a name="performance-monitoring-for-ad-fs"></a>AD FS의 모니터링 성능
Azure AD Connect Health 성능 모니터링은 메트릭에 대한 모니터링 정보를 제공합니다. Hello 모니터링 상자를 선택 하면, hello 메트릭에 대 한 자세한 정보는 새 블레이드가 열립니다.

![Azure AD Connect Health 포털](./media/active-directory-aadconnect-health/perf1.png)

Hello 블레이드의 hello 위쪽 hello 필터 옵션을 선택 하면 서버 toosee에서 개별 서버 메트릭을 필터링 할 수 있습니다. toochange 메트릭을 hello 모니터링 블레이드에서 모니터링 hello에서 차트를 마우스 오른쪽 단추로 클릭 하 고 차트 편집 (또는 차트 편집 단추 선택 hello)를 선택 합니다. 열리는 새 블레이드의 hello에서 hello 드롭다운 목록에서 추가 메트릭을 선택 하 고 hello 성능 데이터를 보기 위한 시간 범위를 지정할 수 있습니다.

## <a name="reports-for-ad-fs"></a>AD FS에 대한 보고서
Azure AD Connect Health는 AD FS의 활동 및 성능에 대한 보고서를 제공합니다. 이러한 보고서는 관리자가 AD FS 서버의 활동을 파악하는 데 도움이 됩니다.

### <a name="top-50-users-with-failed-usernamepassword-logins"></a>사용자 이름/암호 로그인이 실패한 상위 사용자 50명
AD FS 서버에서 실패 한 인증 요청에 대 한 hello 일반적인 이유 중 하나, 즉: 잘못 된 사용자 이름 또는 암호가 잘못 된 자격 증명으로는 요청입니다. 기한 toocomplex 암호, 암호를 잊어버리거나 또는 오타 toousers 일반적으로 발생 합니다.

예기치 않은 개수와 같은 AD FS 서버에 의해 처리 중인 요청이 발생할 수 있는 다른 이유는 하지만: 캐시 사용자 자격 증명 및 hello 자격 증명이 만료 되는 응용 프로그램 또는 악의적인 사용자는 일련의 계정으로 toosign 시도 잘 알려진 암호입니다. 다음 두 예제는 tooa 서 지 요청에서 발생할 수 있는 유효한 이유입니다.

Ad FS에 대 한 azure AD Connect Health tooinvalid 사용자 이름 또는 암호가 인해 실패 한 로그인 시도와 상위 50 사용자에 대 한 보고서를 제공합니다. 이 보고서는 hello 그룹에서 모든 hello AD FS 서버에 의해 생성 된 hello 감사 이벤트를 처리 하 여 달성 됩니다.

![Azure AD Connect Health 포털](./media/active-directory-aadconnect-health-adfs/report1a.png)

이 보고서 내에서 다음 정보를 쉽게 액세스할 수 있도록 toohello를 사용할 수 있습니다.

* Total # of hello 지난 30 일 이내에에서 잘못 된 사용자 이름/암호를 사용 하 여 실패 한 요청
* 잘못된 사용자 이름/암호로 로그인하여 실패한 일별 평균 사용자 수

이 부분을 클릭 하면 추가 세부 정보를 제공 하는 toohello 주 보고서 블레이드를 이동 합니다. 이 블레이드는 추세 toohelp 잘못 된 사용자 이름 또는 암호를 사용 하 여 요청에 대 한 기준선을 설정 하는 정보를 포함 하는 그래프를 포함 합니다. 또한 실패 한 시도의 hello 번호로 hello 상위 50 명의 사용자 목록을 제공합니다.

hello 그래프 hello를 다음 정보를 제공 합니다.

* total # tooa 잘못 된 사용자 이름/암호 매일으로 인해 실패 한 로그인의 hello 합니다.
* 실패 한 로그인 매일 별로 고유 사용자의 total #를 hello 합니다.
* 마지막 요청에 대한 클라이언트 IP 주소

![Azure AD Connect Health 포털](./media/active-directory-aadconnect-health-adfs/report3a.png)

hello 보고서 hello를 다음 정보를 제공 합니다.

| 보고서 항목 | 설명 |
| --- | --- |
| 사용자 ID |사용 된 hello 사용자 ID를 표시 합니다. 이 값은 어떤 hello 잘못 된 사용자 ID를 사용 하 고 hello는 일부 경우에는 사용자를 입력 합니다. |
| 실패한 시도 |에서는 특정 사용자 ID에 대 한 실패 한 시도의 total # hello hello 표는 대부분의 내림차순으로 정렬 하려고 했지만 실패 숫자 hello로 정렬 됩니다. |
| 마지막 실패 |Hello 마지막 실패가 발생 한 경우 hello 타임 스탬프를 보여 줍니다. |
| 마지막 실패 IP |Hello 최신 잘못 된 요청에서 hello 클라이언트 IP 주소를 보여 줍니다. |

> [!NOTE]
> 이 보고서는 해당 시간 내 hello로 2 시간 마다 새 정보 수집한 후 자동으로 업데이트 됩니다. 결과적으로, hello 마지막 2 시간 내에 로그인 시도 hello 보고서에 포함 되지 않을 수 있습니다.
>
>

## <a name="related-links"></a>관련 링크
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health Agent 설치](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health 작업](active-directory-aadconnect-health-operations.md)
* [동기화에 대한 Azure AD Connect Health 사용](active-directory-aadconnect-health-sync.md)
* [AD DS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health FAQ](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health 버전 내역](active-directory-aadconnect-health-version-history.md)