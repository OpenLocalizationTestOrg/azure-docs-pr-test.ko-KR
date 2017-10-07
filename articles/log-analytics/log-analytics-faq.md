---
title: "aaaLog 분석 FAQ | Microsoft Docs"
description: "Hello Azure 로그 분석 서비스에 대 한 질문과 대답 toofrequently 합니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ad536ff7-2c60-4850-a46d-230bc9e1ab45
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 25931f521cbb6ec840184221c6c1a5794b3445f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-faq"></a>Log Analytics FAQ
Microsoft FAQ는 Microsoft Operations Management Suite(OMS)의 Log Analytics에 대해 자주 묻는 질문의 목록입니다. 로그 분석에 대 한 추가 질문이 있으면 이동 toohello [토론 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) 여 질문을 게시 합니다. 자주 묻는 질문 하는 경우 추가 것 toothis 문서 빠르고 쉽게 찾을 수 있도록 합니다.

## <a name="general"></a>일반

### <a name="q-does-log-analytics-use-hello-same-agent-as-azure-security-center"></a>Q. 로그 분석 hello 사용할 Azure 보안 센터와 동일한 에이전트?

A. 초기 6 월 2017 Azure 보안 센터 hello Microsoft Monitoring Agent toocollect 및 저장소 데이터를 사용 하 여 시작 되었습니다. toolearn 더 참조 [Azure 보안 센터 플랫폼 마이그레이션 FAQ](../security-center/security-center-platform-migration-faq.md)합니다.

### <a name="q-what-checks-are-performed-by-hello-ad-and-sql-assessment-solutions"></a>Q. 어떤 검사를 수행 하 여 hello AD 및 SQL 평가 솔루션으로?

A. hello 다음 쿼리는 현재 수행 하는 모든 검사에 대 한 설명을

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

hello 결과 수 추가 검토를 위해 내보낸된 tooExcel 합니다.

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a>Q: System Center Operations Manager 콘솔에서 *OMS*와 다르게 표시되는 이유는 무엇입니까?

A: 사용 중인 Operations Manager의 업데이트 롤업에 따라 *System Center Advisor*, *Operational Insights* 또는 *Log Analytics*에 대한 노드가 표시될 수 있습니다.

텍스트 문자열 업데이트가 너무 hello*OMS* 수동으로 가져올 toobe는 관리 팩에 포함 됩니다. toosee hello 현재 텍스트와 기능을 hello 최신 System Center Operations Manager 업데이트 롤업 기술 자료 문서 및 새로 고침 hello 콘솔에 hello 지침을 따릅니다.

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a>Q: Log Analytics의 *온-프레미스* 버전이 있나요?

A: 아니요. Log Analytics에서 대량의 데이터를 처리하고 저장합니다. 클라우드 서비스로 로그 분석 수 tooscale 접속 필요한 경우 이며 모든 성능 영향 tooyour 환경 방지 합니다.

추가 이점은 다음과 같습니다.
- Microsoft은 hello 로그 분석 인프라 비용을 절감 실행
- 정규 기능 배포는 업데이트되고 수정됩니다.

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a>Q. Log Analytics에서 더 이상 데이터를 수집하지 않는 문제를 어떻게 해결하나요?

A: 경우 hello 무료 가격 책정 계층에 하 고 하루에서 이상 500MB의 데이터를 보낸 hello 일의 hello 나머지 부분에 대 한 데이터 수집 중지 됩니다. 표시할 toobe 데이터 또는 hello 일일 제한에 도달 함 로그 분석 데이터 수집을 중지 하는 일반적인 이유는 없습니다.

Log Analytics는 데이터 수집을 시작하고 중지할 때 *Operation* 형식의 이벤트를 만듭니다. 

Hello hello 일일 한도 도달 하 고 누락 된 데이터는 경우에 다음 검색 toocheck에서 쿼리를 실행 합니다.`Type=Operation OperationCategory="Data Collection Status"`

데이터 수집을 중지할 시기를 hello *OperationStatus* 은 **경고**합니다. 데이터 수집 시작 되 면 hello *OperationStatus* 은 **Succeeded**합니다. 

hello 다음 표에서 데이터 수집을 중지 하는 이유 및 제안된 하는 조치 tooresume 데이터 수집:

| 데이터 수집 중지 이유                       | tooresume 데이터 수집 |
| -------------------------------------------------- | ----------------  |
| 무료 데이터의 일일 한도 도달<sup>1</sup>       | Hello 다음 날에 게 컬렉션 tooautomatically 다시 시작 될 때까지 대기 또는<br> 변경 tooa 유료 가격 책정 계층 |
| Azure 구독이 다음으로 인해 일시 중단된 상태: <br> 평가판 종료 <br> Azure 암호 만료 <br> 월별 지출 한도 도달(예: MSDN 또는 Visual Studio 구독에서)                          | Tooa 유료 구독으로 변환 <br> Tooa 유료 구독으로 변환 <br> 한도 제거 또는 한도가 재설정될 때까지 대기 |

<sup>1</sup> 을 hello 무료 가격 책정 계층에서 작업 영역을 하는 경우 제한 된 toosending 500MB의 데이터 일 toohello 서비스 당 합니다. Hello 일일 한도 도달 하면 hello 다음 날까지 데이터 수집을 중지 합니다. 데이터 수집이 중지되는 동안 전송된 데이터가 인덱싱되지 않으며 검색에 사용할 수 없습니다. 데이터 수집이 다시 시작되면 전송된 새 데이터에 대해서만 프로세스가 발생합니다. 

Log Analytics는 UTC 시간을 사용하고 매일 UTC 자정에 시작됩니다. Hello 작업 영역 hello 일일 한도 도달 하면 처리가 hello UTC 다음날 hello의 첫 번째 시간 동안 다시 시작 됩니다.

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a>Q. 데이터 수집이 중지될 때 알림을 받을 수 있는 방법은 무엇인가요?

A:에서 설명 하는 hello 단계를 사용 하 여 [경고 규칙을 생성할](log-analytics-alerts-creating.md#create-an-alert-rule) toobe 데이터 수집이 중지 될 때 알림을 합니다.

데이터 수집을 중지 하는 것에 대 한 hello 경고를 만들 때 설정 된:
- **이름** 너무*데이터 수집 중지*
- **심각도** 너무*경고*
- **검색 쿼리** 너무`Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`
- **시간 창** 너무*2 시간*합니다.
- **경고 빈도** toobe 1 시간 이후 hello 사용 현황 데이터는 시간당 한 번만 업데이트 합니다.
- **경고에 따라 생성** toobe *결과의 수*
- **결과 수가** toobe *0 보다 큰*

에 설명 된 hello 단계를 사용 하 여 [동작 tooalert 규칙 추가](log-analytics-alerts-actions.md) hello 경고 규칙에 대 한 전자 메일, webhook, 또는 runbook 작업을 구성 합니다.


## <a name="configuration"></a>구성
### <a name="q-can-i-change-hello-name-of-hello-tableblob-container-used-tooread-from-azure-diagnostics-wad"></a>Q. 변경 테이블/blob 사용 되는 컨테이너 tooread hello의 hello 이름에서 WAD (Azure 진단)?

A. 아니요, 현재는 가능 tooread 임의의 테이블 또는 컨테이너에에서 없는 Azure 저장소입니다.

### <a name="q-what-ip-addresses-does-hello-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-toohello-log-analytics-service"></a>Q. IP 주소 로그 분석 서비스 사용 하 여 hello가? 방화벽만 트래픽 toohello 로그 분석 서비스를 허용 하는지 확인?

A. hello 로그 분석 서비스는 Azure를 기반으로 빌드됩니다. 로그 분석 IP 주소는 hello [Microsoft Azure 데이터 센터 IP 범위](http://www.microsoft.com/download/details.aspx?id=41653)합니다.

서비스 배포는 hello hello 로그 분석 서비스의 실제 IP 주소가 변경 합니다. 방화벽을 통해 DNS 이름을 tooallow hello에 정리 되어 [로그 분석에서 프록시 및 방화벽 설정을 구성할](log-analytics-proxy-firewall.md)합니다.

### <a name="q-i-use-expressroute-for-connecting-tooazure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a>Q. TooAzure 연결 하기 위한 ExpressRoute 사용 하 여 합니다. Log Analytics 트래픽이 내 ExpressRoute 연결을 사용하나요?

A. hello 다양 한 유형의 express 경로 트래픽이 hello에 설명 되어 [express 경로 설명서](../expressroute/expressroute-faqs.md#supported-services)합니다.

트래픽 tooLog 분석 hello 공용 피어 링 express 경로 회로 사용합니다.

### <a name="q-is-there-a-simple-and-easy-way-toomove-an-existing-log-analytics-workspace-tooanother-log-analytics-workspaceazure-subscription"></a>Q. 쉽고 간단한 방법이 toomove 기존 로그 분석 작업 영역 tooanother 로그 분석 작업 영역/Azure 구독 무엇입니까?

A. hello `Move-AzureRmResource` cmdlet을 사용 하면 로그 분석 작업 영역 및 자동화 계정에서 하나의 Azure 구독 tooanother 이동할 수 있습니다. 자세한 내용은 [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx)를 참조하세요.

이 변경 hello Azure 포털에서에서 만들 수도 있습니다.

한 로그 분석 작업 영역 tooanother에서 데이터를 이동 하거나 로그 분석 데이터에 저장 되어 있는 hello 지역을 변경할 수 없습니다.

### <a name="q-how-do-i-add-log-analytics-toosystem-center-operations-manager"></a>Q: 로그 분석 tooSystem Center Operations Manager 추가 어떻게 해야 합니까?

A: toohello 최신 업데이트 롤업으로 업데이트 하 고 관리 팩을 가져오는 사용 하면 Operations Manager tooLog tooconnect 분석 합니다.

>[!NOTE]
>Operations Manager 연결 tooLog hello 분석은 System Center Operations Manager 2012 SP1 이상에 사용할 수 있습니다.

### <a name="q-how-can-i-confirm-that-an-agent-is-able-toocommunicate-with-log-analytics"></a>Q: 에이전트와 로그 분석 수 toocommunicate 인지 확인할 수는 어떻게

A: tooensure hello 에이전트가 OMS와 통신할 수로 이동: 제어판, 보안 및 설정, **Microsoft Monitoring Agent**합니다.

Hello에서 **Azure 로그 분석 (OMS)** 탭에서 녹색 확인 표시를 찾으세요. 녹색 확인 표시 아이콘이 hello 에이전트가 OMS 서비스 hello로 수 toocommunicate을 확인 합니다.

노란색 경고 아이콘은 hello 에이전트가 OMS와 통신 문제는 데 의미 합니다. 일반적인 이유 중 하나는 hello Microsoft Monitoring Agent 서비스가 중지 되었습니다. 서비스 제어 관리자 toorestart hello 서비스를 사용 합니다.

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a>Q: 에이전트가 Log Analytics와의 통신을 중지하도록 하려면 어떻게 하나요?

A: System Center Operations Manager에서 hello 관리자 관리 되는 컴퓨터 목록에서 hello 컴퓨터를 제거 합니다. Operations Manager 업데이트 hello hello 에이전트 toono 긴 보고서 tooLog 분석의 구성 합니다. 에이전트 tooLog 분석에 직접 연결에 대 한를 통해 통신할 중지할 수 있습니다: 제어판, 보안 및 설정, **Microsoft Monitoring Agent**합니다.
**Azure Log Analytics(OMS)**아래에서 나열된 모든 작업 영역을 제거합니다.

### <a name="q-why-am-i-getting-an-error-when-i-try-toomove-my-workspace-from-one-azure-subscription-tooanother"></a>Q 하는 동안 오류가 발생 하면 toomove 내 작업 영역에서 Azure 구독 하나 tooanother?

A: hello Azure 포털을 사용 하는 경우 hello 이동에 대 한만 hello 작업 영역을 선택 하는 확인 합니다. Hello 솔루션을 선택 하지 마십시오-hello 작업 영역 이동 되 면 자동으로 이동 됩니다. 

두 Azure 구독에서 권한을 갖는지 확인합니다.

## <a name="agent-data"></a>에이전트 데이터
### <a name="q-how-much-data-can-i-send-through-hello-agent-toolog-analytics-is-there-a-maximum-amount-of-data-per-customer"></a>Q. Hello 에이전트 tooLog 분석을 통해 보낼 수 있는 데이터의 크기는 있습니까? 고객 한 명당 최대 데이터 용량이 있나요?
A. hello 무료 계획 작업 영역당 500MB의 일일 한도가 설정합니다. hello 표준 및 프리미엄 계획 hello 업로드 된 데이터 크기 제한이 없습니다. 로그 분석은 설계 된 클라우드 서비스로 tooautomatically 수직 확장 toohandle hello 볼륨 1 일당 수 테라바이트가 되더라도 고객 으로부터 제공 될 예정입니다.

hello 로그 분석 에이전트에서이 공간이 작도록 설계 된 tooensure. 한 고객 hello에 대해 수행한 테스트 되었으면 그 결과 얼마나 만족 한은 에이전트에 대 한 블로그를 썼습니다. hello 데이터 볼륨을 사용 하도록 설정 하면 hello 솔루션에 따라 다릅니다. Hello 별 hello에 솔루션에 의해 참조와 hello 데이터 볼륨에 대 한 자세한 정보를 찾을 수 [사용](log-analytics-usage.md) 페이지.

자세한 내용은 참조는 [고객 블로그](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) hello hello OMS 에이전트의 작은 사용 공간에 대 한 합니다.

### <a name="q-how-much-network-bandwidth-is-used-by-hello-microsoft-management-agent-mma-when-sending-data-toolog-analytics"></a>Q. 얼마나 많은 네트워크 대역폭 사용 되는 Microsoft Management Agent (MMA) hello 하 여 데이터 tooLog 분석에 보낼 때

A. 대역폭은 전송 된 데이터의 hello 금액에는 함수입니다. 데이터는 hello 네트워크를 통해 전송 될 때 압축 됩니다.

### <a name="q-how-much-data-is-sent-per-agent"></a>Q. 에이전트당 얼마나 많은 데이터가 전송되나요?

A. hello 에이전트당 전송 되는 데이터에 따라 달라 집니다.

* 설정한 hello 솔루션
* 로그 및 성능 카운터 수집 되 고 hello 수
* hello 로그에서 데이터의 hello 볼륨

hello 무료 가격 책정 계층은 좋은 방법 tooonboard 여러 서버 및 hello 일반적인 데이터 볼륨을 측정 합니다. Hello에 사용량이 표시 되는 전반적인 [사용](log-analytics-usage.md) 페이지.

컴퓨터 수 toorun hello WireData 에이전트에 대해 얼마나 많은 데이터가 전송 되는 쿼리 toosee 다음 hello를 사용 합니다.

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a>다음 단계
* [로그 분석 작업 시작](log-analytics-get-started.md) toolearn 로그 분석 및 분 단위로 실행할에 대 한 자세한 합니다.
