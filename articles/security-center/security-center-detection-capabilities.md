---
title: "Azure 보안 센터의 aaaDetection 기능 | Microsoft Docs"
description: "이 문서 Azure 보안 센터 검색 기능이 작동 하는 방식 toounderstand 수 있습니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 4c5599cc-99a1-430f-895f-601615ef12a0
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: d8001cc2acdd0026bd9b3596bbdfec56f8874513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-detection-capabilities"></a>Azure 보안 센터 감지 기능
이 문서에서는 Microsoft Azure 리소스를 대상으로 하는 활성 위협이 통해 식별 하 고 hello insights 필요한 toorespond 신속 하 게 제공 하는 Azure 보안 센터의 고급 검색 기능을 설명 합니다.

> [!NOTE]
> 고급 검색 hello 표준 계층의 Azure 보안 센터에에서 표시 됩니다. 무료 60일 평가판을 사용할 수 있습니다. Hello hello에 선택한 가격 책정 계층에서에서 업그레이드할 수 [보안 정책](security-center-policies.md)합니다. 방문 [보안 센터 페이지](https://azure.microsoft.com/pricing/details/security-center/) toolearn 가격에 대 한 자세한 합니다. 
> 
> 

## <a name="responding-tootodays-threats"></a>Tootoday의 위협 응답
중요 한 변경 내용이 hello 위협 환경에서 hello를 통해 마지막 20 년입니다. 지난 hello, 회사 일반적으로 만으로는 tooworry 보는 "수 수행할" 관심이 대부분 이었던 개별 공격자가 변조 웹 사이트에 대 한 합니다. 오늘날의 공격자는 훨씬 더 정교하며 조직적입니다. 특정 금융 및 전략적 목표가 있는 경우가 많습니다. 더 많은 리소스가 사용 가능한 toothem도를 가집니다 대로 사막이 남 지역 상태 또는 조직 범죄 자금 될 수 있습니다.

이 방법은 tooan 매우 높은 수준을 hello 공격자가 순위의 전문성 되었습니다. 공격자는 더 이상 웹 손상에 관심이 없습니다. 특정 비즈니스, 정치적 또는 military 위치 hello 시장 또는 tooleverage toogenerate 현금 이제 가로채기 정보, 금융 계좌 및 사용할 수 있는 모든 개인 데이터에 관심이 있습니다. 이러한 공격자가 금융 목표와 hello 공격자가 네트워크 toodo 손해가 발생 tooinfrastructure와 사람 위반 것 보다 더 많은 관한 합니다.

에 대 한 응답 조직은 종종 알려진된 공격 서명을 검색 하 여 hello 기업 경계 또는 끝점 중 하나를 방어 하기에 집중 다양 한 지점 솔루션을 구축 합니다. 이러한 솔루션 toogenerate 보안 분석가 tootriage 필요 하 고 조사 하는 낮은 충실도 경고를 상당히 많은 경향이 있습니다. 대부분의 조직에서는 hello 시간 없고 필요한 기술력 toorespond toothese 경고 – 단점 채로 이동 합니다.  한편, 공격자가 발전 하 고 해당 메서드 toosubvert 많은 서명 기반의 방어 및 [toocloud 환경에 맞게 조정](https://azure.microsoft.com/blog/detecting-threats-with-azure-security-center/)합니다. 필요한 toomore에 신속 하 게는 새로운 접근 방법이 새로운 위협 식별 하 고 검색 하 고 응답을 촉진 합니다. 

## <a name="how-azure-security-center-detects-and-responds-toothreats"></a>Azure 보안 센터를 검색 하 고 toothreats 응답 하는 방법
Microsoft 보안 연구원 위협에 대 한 lookout hello에 지속적으로 있습니다. 액세스 tooan 과다 집합 hello 클라우드 및 온-프레미스 Microsoft의 글로벌 상태에서 확보 하는 원격 분석을 포함 합니다. 이 광범위 하 고 다양 한 컬렉션 데이터 집합의 온라인 서비스와 해당 온-프레미스 소비자 및 엔터프라이즈 제품에서 Microsoft toodiscover 새 공격 패턴 및 추세를 사용합니다. 결과적으로 보안 센터는 공격자가 새롭고 더욱 정교한 악용을 릴리스하는 동안 신속하게 해당 감지 알고리즘을 업데이트할 수 있습니다. 이 방법을 통해 빠르게 움직이는 위협 환경을 지속적으로 관리할 수 있습니다. 

보안 센터 위협 요소 탐지 자동으로 Azure 리소스, hello 네트워크와 연결 된 파트너 솔루션의 보안 정보를 수집 하 여 작동 합니다. 이 정보를 종종 tooidentify 위협 여러 소스의 정보 상관 관계를 분석 합니다. 보안 경고 사항 tooremediate 위협 hello 하는 방법에 대 한 권장 사항과 함께 보안 센터에 우선 순위입니다.

![보안 센터 데이터 수집 및 프레젠테이션](./media/security-center-detection-capabilities/security-center-detection-capabilities-fig1.png)

보안 센터는 서명 기반 방식을 뛰어 넘는 고급 보안 분석을 사용합니다. 빅 데이터의 문제를 해결 하면 및 [기계 학습](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) 기술이 사용된 tooevaluate 이벤트 하는 것이 불가능 한 tooidentify 수동 방법을 사용 하 고 hello를 예측 하는 위협을 감지 – hello 전체 클라우드 패브릭에서 공격 발전 합니다. 이러한 보안 분석은 다음과 같습니다. 

* **위협 인텔리전스 통합**: 검색, Microsoft 제품 및 서비스에서 글로벌 위협 인텔리전스를 활용 하 여 알려진된 믿지 못할 자 Microsoft Digital Crimes 단위 (DCU), hello에 대 한 hello Microsoft 보안 대응 센터 (MSRC), 및 외부 피드를 나타냅니다.
* **동작 분석**: 알려진된 패턴 toodiscover 악의적인 동작을 적용 합니다. 
* **이상 탐지**: toobuild 기록 기준선을 프로 파일링 통계 사용 합니다. 편차가 tooa 잠재적인 공격 벡터를 준수 하는 설정 된 기준에 게 알립니다.

### <a name="threat-intelligence"></a>위협 인텔리전스
Microsoft는 방대한 글로벌 위협 인텔리전스가 있습니다. 원격 분석의 흐름에서는 Azure와 같은 여러 원본에서 Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, hello Microsoft Digital Crimes 단위 (DCU) 및 Microsoft 보안 대응 센터 (MSRC). 또한 연구원은 주요 클라우드 서비스 공급자 간에 공유 되 고 제 3 자에서 toothreat intelligence 피드를 구독 하는 위협 인텔리전스 정보를 받습니다. Azure 보안 센터가 정보 tooalert צ ְ ײ 알려진된 믿지 못할 자에서 toothreats 있습니다. 일부 사례:

* **아웃 바운드 통신 tooa 악성 IP 주소로**: 아웃 바운드 트래픽을 tooa 봇 네트 또는 다크 넷 가능성이 알려진 리소스가 손상 된 하는 공격자가 tooexecute 시도 것에 있는 명령을 해당 시스템 또는 exfiltrate 데이터를 나타냅니다. Azure 보안 센터 네트워크 트래픽 tooMicrosoft 글로벌 위협 데이터베이스 비교 및 통신 tooa 악성 IP 주소를 검색 하는 경우 경고를 보냅니다.

## <a name="behavioral-analytics"></a>동작 분석
동작 분석은 분석 하 고 알려진된 패턴의 tooa 컬렉션 데이터를 비교 하는 기술입니다. 그러나 이러한 패턴은 단순한 서명이 아닙니다. 데이터 집합이 적용 된 toomassive는 복잡 한 기계 학습 알고리즘을 통해 결정 됩니다. 또한 전문 분석가가 악의적인 행동을 신중하게 분석하여 결정합니다. Azure 보안 센터 분석 로그 가상 컴퓨터, 가상 네트워크 장치 로그, 패브릭 로그, 크래시 덤프 및 기타 소스에 따라 동작 분석 tooidentify 손상 리소스를 사용할 수 있습니다. 

또한 광범위 한 캠페인의 증거를 지원 하기 위한 다른 신호 toocheck와의 상관 관계는 합니다. 이 상관 관계가 손상의 설정 된 표시기와 일치 하는 tooidentify 이벤트 수 있습니다. 일부 사례:

* **의심 스러운 프로세스 실행**: 공격자가 몰래 몇 가지 기술을 tooexecute 악성 소프트웨어를 사용 합니다. 예를 들어 공격자 수 제공 맬웨어 hello 승인 된 시스템 파일 이름이 같은 하지만 이러한 파일을 대체 위치에에서 배치, 매우 유사한 tooa 무해 파일 또는 true 마스크 hello 파일의 확장명 이름을 사용 합니다. 보안 센터 모델 프로세스 동작 및 모니터 같은 실행 toodetect 이상 값 처리합니다.  
* **맬웨어 및 악용 시도 숨겨진**: 정교한 맬웨어 수 tooevade 기존 맬웨어 방지 제품 toodisk 작성 되지 또는 디스크에 저장 하는 소프트웨어 구성 요소를 암호화 하는 것입니다.  그러나 이러한 맬웨어 수 감지할 수 메모리 분석을 사용 하 여 hello 맬웨어 순서 toofunction 메모리에 추적을 두어야 합니다. 소프트웨어 충돌, 크래시 덤프는 hello 충돌 hello 시 메모리의 일부를 캡처합니다.  Hello 크래시 덤프의 hello 메모리를 분석 하 여 Azure 보안 센터 수 tooexploit 취약점 소프트웨어에서 사용 하는 기술을 검색, 기밀 데이터를 액세스 및에 부정적 유지 hello 성능에 영향을 주지 않고 손상 된 컴퓨터 컴퓨터입니다.
* **내부 정찰 및 이동 하 여 측면**: 손상 된 네트워크 및 찾기/수집 중요 한 데이터에 toopersist, 종종 공격자가 손상 hello에서 가로로 toomove 컴퓨터 tooothers 내에서 동일한 네트워크 hello 합니다. 보안 센터 프로세스를 모니터링 하 고 순서 toodiscover의 로그인 활동 tooexpand 내에서 원격 명령 실행 네트워크 검색이 같은 hello 네트워크 및 계정 열거는 공격자의 발판을 마련 합니다.
* **PowerShell 스크립트를 악의적인**: 다양 한 용도로 PowerShell 대상 가상 컴퓨터에서 공격자가 tooexecute 악성 코드에서 사용 되 고 있습니다. 보안 센터는 의심스러운 활동의 증거에 대해 PowerShell 작업을 검사합니다. 
* **공격을 나가는**: 공격자는 종종 이러한 리소스 toomount 추가 공격을 사용 하 여 hello 목표를 사용 하 여 클라우드 리소스 대상입니다. 손상 된 가상 컴퓨터, 예를 들어 수 있습니다 다른 가상 컴퓨터에 대 한 무차별 암호 대입 공격 사용된 toolaunch 수, 스팸 메일을 보낼 또는 열린 포트를 검색 및 기타 장치에서 인터넷 hello 합니다. 컴퓨터를 적용 하 여 toonetwork 트래픽 학습, 보안 센터 감지할 수 아웃 바운드 네트워크 통신 hello norm를 초과 하는 경우. 스팸 hello 경우에서 보안 센터도 상관 관계가 비정상적인 전자 메일 트래픽 Office 365 toodetermine에서 정보를 바탕으로 hello 메일 가능성이 인지 불법 또는 올바른 전자 메일 캠페인의 hello 결과입니다.  

### <a name="anomaly-detection"></a>이상 감지
또한 azure 보안 센터 비정상 탐지 tooidentify 위협 요소를 사용합니다. (있음 큰 데이터 집합에서 파생 된 알려진된 패턴에 따라 다름) 대비 toobehavioral 분석에서 변칙 검색 더 "개인화 된" 및 특정 tooyour 배포 하는 기준에 중점을 둡니다. 기계 학습 배포에 대해 적용 된 toodetermine 정상적인 작업을 하 고 규칙은 보안 이벤트를 나타낼 수 있는 생성 된 toodefine 이상 값 조건을 합니다. 예를 들면 다음과 같습니다.

* **인바운드 RDP/SSH 무차별 대입 공격**: 배포에는 매일 로그인 사용량이 많은 가상 컴퓨터 및 로그인이 거의 없는 기타 가상 컴퓨터가 있을 수 있습니다. Azure 보안 센터 이러한 가상 컴퓨터에 대 한 초기 로그인 활동을 확인 하 고 일반 로그인 활동 외부에서 이란 컴퓨터 학습 toodefine를 사용 합니다. 로그인의 hello 숫자 또는 날짜 hello 로그인 또는 hello 위치는 hello에서 로그인, 요청 된의 hello 시간 또는 기타 로그인 관련 특성 hello 초기 계획에서 크게 다른 경우 경고가 생성 될 수 있습니다. 다시, 기계 학습은 무엇이 중요한지를 결정합니다.

## <a name="continuous-threat-intelligence-monitoring"></a>연속 위협 인텔리전스 모니터링
Azure 보안 센터 hello 위협 환경에서 변경 내용을 지속적으로 모니터링 하는 보안 연구 및 데이터 과학 팀 작동 합니다. 이 이니셔티브 다음 hello 포함 됩니다.

* **위협 인텔리전스 모니터링**: 위협 인텔리전스는 기존 또는 새로운 위협에 대한 메커니즘, 표시기, 영향 및 조치 가능한 조언을 포함합니다. 이 정보는 hello 보안 커뮤니티에서 공유 및 Microsoft 내부 및 외부 소스에서 위협 인텔리전스 피드를 지속적으로 모니터링 합니다.
* **신호 공유**: Microsoft의 클라우드 및 온-프레미스 서비스, 서버 및 클라이언트 끝점 장치의 광범위한 포트폴리오에 대한 보안 팀의 정보는 공유 및 분석됩니다. 
* **Microsoft 보안 전문가**: 과학 수사 및 웹 공격 감지와 같은 특수 보안 필드에서 활동하는 Microsoft 팀과의 지속적인 참여입니다.
* **검색 튜닝**: 알고리즘 실제 고객 데이터 집합에 대해 실행 되 고 보안 연구원 고객 toovalidate hello 결과 함께 작동 합니다. 여러 참과 거짓 긍정은 사용 되는 toorefine 기계 학습 알고리즘입니다.

이러한 결합 된 활동에서 즉시 얻을 수 있는 새로운 기능과 향상 된 검색에 누적 – tootake 있습니다에 대 한 작업이 없습니다.

## <a name="see-also"></a>참고 항목
이 문서에서는 tooAzure 보안 센터 검색 기능이 작동 하는 방법을 배웠습니다. 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure Security Center 계획 및 작업 가이드](security-center-planning-and-operations-guide.md)
* [관리 하 고 Azure 보안 센터에서 toosecurity 경고 응답](security-center-managing-and-responding-alerts.md)
* [Azure Security Center에서 유형별 보안 경고](security-center-alerts-type.md)
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.

