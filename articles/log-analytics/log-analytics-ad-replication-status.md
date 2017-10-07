---
title: "Azure 로그 분석 함께 Active Directory 복제 상태 aaaMonitor | Microsoft Docs"
description: "정기적으로 Active Directory 복제 상태 솔루션 팩 hello는 모든 복제 오류에 대 한 Active Directory 환경 모니터링 하 고 OMS 대시보드 hello 결과 보고 합니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 1b988972-8e01-4f83-a7f4-87f62778f91d
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 235e4f7a066ea50b79f681398182b22c91fb6d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-active-directory-replication-status-with-log-analytics"></a>Log Analytics를 사용하여 Active Directory 복제 상태 모니터링

![AD 복제 상태 기호](./media/log-analytics-ad-replication-status/ad-replication-status-symbol.png)

Active Directory는 엔터프라이즈 IT 환경의 핵심 구성 요소입니다. tooensure 고가용성 및 높은 성능을 각 도메인 컨트롤러에 hello Active Directory 데이터베이스의 자체 복사본이 있습니다. 도메인 컨트롤러를 서로 hello 기업 전체에 걸쳐 변경 내용의 적용 순서 toopropagate 복제 됩니다. 이 복제 프로세스에서 발생 한 실패 hello 기업 전체에 걸쳐 다양 한 문제를 발생할 수 있습니다.

AD 복제 상태 솔루션 팩 hello는 정기적으로 모니터링 하는 모든 복제 오류에 대 한 Active Directory 환경 하 고 OMS 대시보드 hello 결과 보고 합니다.

## <a name="installing-and-configuring-hello-solution"></a>설치 하 고 hello 솔루션 구성
다음 정보 tooinstall hello를 사용 하 고 hello 솔루션을 구성 합니다.

* Hello 도메인 toobe 평가의 구성원 인 도메인 컨트롤러에서 에이전트를 설치 해야 합니다. 또는 구성원 서버에 에이전트를 설치 하 고 hello 에이전트 toosend AD 복제 데이터 tooOMS 구성 해야 합니다. Windows 컴퓨터 tooOMS tooconnect 참조 toounderstand [연결 Windows 컴퓨터 tooLog 분석](log-analytics-windows-agents.md)합니다. 도메인 컨트롤러가 이미 tooconnect tooOMS 원하는 기존 System Center Operations Manager 환경의 일부인 경우 참조 [Operations Manager 연결 tooLog 분석](log-analytics-om-agents.md)합니다.
* Hello 프로세스를 사용 하 여 OMS 작업 영역에서 설명 하는 hello Active Directory 복제 상태 솔루션 tooyour 추가 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.  추가 구성은 필요 없습니다.

## <a name="ad-replication-status-data-collection-details"></a>AD 복제 상태 데이터 컬렉션 세부 정보
hello 다음 표에서 데이터 수집 방법과 AD 복제 상태에 대 한 데이터 수집 방법에 대 한 기타 세부 정보입니다.

| 플랫폼 | 직접 에이전트 | SCOM 에이전트 | Azure 저장소 | SCOM 필요? | 관리 그룹을 통해 전송되는 SCOM 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |5일마다 |

## <a name="optionally-enable-a-non-domain-controller-toosend-ad-data-toooms"></a>필요에 따라 도메인 컨트롤러가 아닌 toosend AD 데이터 tooOMS 사용 하도록 설정
않으려면 tooconnect 도메인 컨트롤러 중 하나가 직접 tooOMS, 사용자 도메인 toocollect hello AD 복제 상태 솔루션에 대 한 데이터 압축 및 hello 데이터를 보낼 수도에서 OMS에 연결 된 다른 컴퓨터를 사용할 수 있습니다.

### <a name="tooenable-a-non-domain-controller-toosend-ad-data-toooms"></a>도메인 컨트롤러가 아닌 toosend AD 데이터 tooOMS tooenable
1. 해당 hello 컴퓨터가 toomonitor hello AD 복제 상태 솔루션을 사용 하 여 원하는 hello 도메인의 구성원을 확인 합니다.
2. [Windows 컴퓨터 tooOMS hello 연결](log-analytics-windows-agents.md) 또는 [에 기존 Operations Manager 환경 tooOMS를 사용 하 여 연결](log-analytics-om-agents.md)이미 연결 되어 있지 않으면, 합니다.
3. 해당 컴퓨터에서 다음 레지스트리 키 hello를 설정 합니다.

   * 키: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**
   * 값: **IsTarget**
   * 값 데이터: **true**

   > [!NOTE]
   > 이러한 변경 내용은 프로그램 다시 시작 hello Microsoft Monitoring Agent 서비스 (HealthService.exe) 될 때까지 적용 되지 않습니다.
   >
   >

## <a name="understanding-replication-errors"></a>복제 오류 이해
AD 복제 상태 데이터 전송 tooOMS를 만든 후 hello OMS 대시보드에 현재 복제 오류를 나타내는 이미지를 다음 타일 유사한 toohello를 표시 됩니다.  
![AD 복제 상태 타일](./media/log-analytics-ad-replication-status/oms-ad-replication-tile.png)

**중요 한 복제 오류** hello의 75% 이상 오류가 [삭제 표시 수명](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) Active Directory 포리스트에 대 한 합니다.

Hello 타일을 클릭할 때 hello 오류에 대 한 자세한 정보를 볼 수 있습니다.
![AD 복제 상태 대시보드](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)

### <a name="destination-server-status-and-source-server-status"></a>대상 서버 상태 및 원본 서버 상태
이러한 열에는 hello 상태는 복제 오류를 발생 하는 원본 서버와 대상 서버를 보여 줍니다. 각 도메인 컨트롤러 이름은 다음 hello 숫자는 해당 도메인 컨트롤러에서 복제 오류 hello 수를 나타냅니다.

대상 서버와 원본 서버에 대 한 hello 오류는 몇 가지 문제는 hello 원본 서버 관점에서 보다 쉽게 tootroubleshoot hello 대상 서버의 관점에서 다른 사용자에 표시 됩니다.

이 예제에서는 나타나면 많은 대상 서버가 대략가 동일한 오류 수, hello 이지만 모든 hello 보다 더 많은 오류 많은 다른 사용자가 하나의 원본 서버 (ADDC35). Toofail toosend 데이터 tooits 복제 파트너 없게 ADDC35에 문제가 있다고 가능성이 높습니다. ADDC35에서 hello 문제를 수정한 다양 한 hello 대상 서버 영역에 표시 되는 hello 오류를 해결할 수 있습니다.

### <a name="replication-error-types"></a>복제 오류 유형
이 영역은 hello 유형의 엔터프라이즈 전체에서 발견 된 오류에 대 한 정보를 제공 합니다. 각 오류에는 고유 숫자 코드와 hello 오류의 hello 근본 원인을 확인 하는 데 도움이 되는 메시지입니다.

hello 위쪽 hello 도넛을 통해 오류가 표시는 점점 더 적은 자주 사용자 환경.

표시 하면 여러 도메인 컨트롤러 발생할 hello 동일한 복제 오류가 있습니다. 이 경우 있습니다 있습니다 수 toodiscover 또는 한 도메인 컨트롤러에서 솔루션을 식별 후 다시 설치 해야 다른 도메인 컨트롤러에 영향을 받는 hello 동일한 반복 오류입니다.

### <a name="tombstone-lifetime"></a>삭제 표시 수명
hello 삭제 표시 수명 삭제 된 개체 기간 결정, tooas 삭제 표시 참조, hello Active Directory 데이터베이스에 유지 됩니다. 삭제 된 개체를 전달 hello 삭제 표시 수명, 가비지 수집 프로세스를 자동으로에서 제거 hello Active Directory 데이터베이스입니다.

hello 삭제 표시 수명 기본값은 180 일의 Windows에서 최신 버전에 대 한 있지만 60 일 이전 버전에 대 한 Active Directory 관리자가 명시적으로 변경할 수 있습니다.

Hello 삭제 표시 수명 지난에 도달 하는 복제 오류를 발생 하는 경우 중요 한 tooknow입니다. Hello 삭제 표시 기간을 지 나 계속 되 면 복제 오류가 발생 하는 두 명의 도메인 컨트롤러, 기본 복제 오류 hello 고정 된 경우에 이러한 두 도메인 컨트롤러 간의 복제 비활성화 됩니다.

hello 삭제 표시 수명 영역에는 사용할 수 없는 복제 문제가 발생할 위험에 여기서는 위치를 확인할 수 있습니다. Hello의 각 오류 **100%를 초과 TSL** 범주에는 복제 되지 않은에 대 한 해당 원본 및 대상 서버 간에 hello 포리스트에 대 한 hello 삭제 표시 수명을 최소화 하는 파티션을 나타냅니다.

이 경우 단순히 hello 복제 오류를 수정 되지 않습니다 충분 합니다. 여기에 최소한 toomanually 필요한 tooidentify 조사 하 고 복제를 다시 시작할 수 있습니다 느린 개체가 정리 합니다. Toodecommission 도메인 컨트롤러도 할 수 있습니다.

또한 tooidentifying hello 삭제 표시 수명 지난 유지 않은 모든 복제 오류 시겠습니까 toopay 주의 tooany 오류 hello에 속하는 **50-75 %TSL** 또는 **75 100 %TSL** 범주입니다.

이들은 하므로, 가능성이 개입 tooresolve은 명확 하 게 느린, 일시적인 오류입니다. hello 좋은 소식은 아직 도달 하지 hello 삭제 표시 수명입니다. 이러한 문제를 신속 하 게 수정 하는 경우 및 *전에* hello 삭제 표시 기간에 도달 하기, 복제 수동 개입을 최소한으로 다시 시작할 수 있습니다.

Hello AD 복제 상태 솔루션에 대 한 hello 대시보드 타일 표시 hello 수가 앞에서 설명한 대로 *중요* (포함 하는 삭제 표시 수명의 75% 이상 있는 오류로 정의 된 사용자 환경에서 복제 오류 오류 TSL의 100%를 넘는)입니다. 이 숫자 0에서 tookeep를 위해 노력 합니다.

> [!NOTE]
> 해당 백분율 정확 하 게 설정 하는 사용자 지정 삭제 표시 기간 값이 있는 경우에 신뢰할 수 있는 모든 hello 삭제 표시 수명 백분율 계산 Active Directory 포리스트를 위해 hello 실제 삭제 표시 수명에 따라 됩니다.
>
>

### <a name="ad-replication-status-details"></a>AD 복제 상태 세부 정보
Hello 목록 중 하나에서 항목을 클릭 하면 로그 검색을 사용 하 여 관련 된 세부 정보 표시 됩니다. hello 결과 필터링 된 tooshow 유일한 hello 오류 관련된 toothat 항목입니다. 예를 들어 클릭할 경우 첫 번째 도메인 컨트롤러 hello 아래에 나열 **대상 서버 상태 (ADDC02)**, 검색 결과 필터링 tooshow 오류 hello 대상 서버로 나열 된 해당 도메인 컨트롤러를 참조 하십시오.

![검색 결과에서 AD 복제 상태 오류](./media/log-analytics-ad-replication-status/oms-ad-replication-search-details.png)

여기에서 추가 필터링, hello 검색 쿼리를 수정 및 등 수 있습니다. Hello 로그 검색을 사용 하는 방법에 대 한 자세한 내용은 참조 [검색 로그](log-analytics-log-searches.md)합니다.

hello **HelpLink** 필드 해당 특정 오류에 대 한 추가 정보가 있는 TechNet 페이지의 hello URL을 표시 합니다. 복사 하 여 브라우저 창 toosee 문제 해결 및 hello 오류를 해결 하는 방법에 대 한 정보에이 링크를 붙여 수 있습니다.

클릭할 수도 있습니다 **내보내기** tooexport hello tooExcel 결과입니다. Hello 데이터 내보내기 원하는 어떤 방식으로든 복제 오류 데이터를 시각화할 수 있습니다.

![Excel에서 내보낸 AD 복제 상태 오류](./media/log-analytics-ad-replication-status/oms-ad-replication-export.png)

## <a name="ad-replication-status-faq"></a>AD 복제 상태 FAQ
**Q: AD 복제 상태 데이터는 얼마나 자주 업데이트되나요?**
A: hello 정보에는 5 일 마다 업데이트 됩니다.

**Q: 얼마나 자주이 데이터가 업데이트 되는 방식으로 tooconfigure는 무엇입니까?**
A: 지금은 없습니다.

**Q: 필요한 tooadd 내 도메인 컨트롤러 toomy OMS 작업 영역 순서 toosee 복제 상태에서의 모든?**
A: 아니요, 단일 도메인 컨트롤러만 추가되어야 합니다. OMS 작업 영역에서 도메인 컨트롤러가 여러 개 있는 경우 모든 데이터 tooOMS 전송 됩니다.

**Q: 않으려면 tooadd 모든 도메인 컨트롤러 toomy OMS 작업 영역입니다. 여전히 hello 솔루션 AD 복제 상태를 사용할 수 있습니까?**
A: 예. 레지스트리 키 tooenable의 hello 값을 설정할 수 것입니다. 참조 [tooenable 도메인 컨트롤러가 아닌 toosend AD 데이터 tooOMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms)합니다.

**Q: 데이터 수집을 hello는 hello 프로세스의 hello 이름은 무엇입니까?**
A: AdvisorAssessment.exe

**Q: 않습니다 소요 데이터 toobe 수집에 대 한?**
A: 데이터 수집 시간 hello Active Directory 환경에서의 hello 크기에 따라 달라 지지만 대개 15 분 미만입니다.

**Q: 어떤 유형의 데이터를 수집하나요?**
A: 복제 정보는 LDAP를 통해 수집됩니다.

**Q:가 데이터를 수집 하는 경우 방식으로 tooconfigure 있습니까?**
A: 지금은 없습니다.

**Q: 권한 수행할 toocollect 데이터 필요 합니까?**
A: 일반 사용자 권한 tooActive 디렉터리 만으로도 충분 합니다.

## <a name="troubleshoot-data-collection-problems"></a>데이터 수집 문제 해결
주문 toocollect 데이터 hello AD 복제 상태 솔루션 팩 하나 이상 도메인 컨트롤러 연결 toobe tooyour OMS 작업 영역을 필요합니다. 도메인 컨트롤러에 연결할 때까지 **데이터가 여전히 수집되고 있다고** 표시하는 메시지가 표시됩니다.

도메인 컨트롤러 중 하나가 연결 도움이 필요 하면에서 설명서를 볼 수 있습니다 [연결 Windows 컴퓨터 tooLog 분석](log-analytics-windows-agents.md)합니다. 또는 도메인 컨트롤러가 이미 연결 된 tooan 기존 System Center Operations Manager 환경 경우 설명서에서 볼 수 [System Center Operations Manager 연결 tooLog 분석](log-analytics-om-agents.md)합니다.

않으려면 tooconnect 도메인 컨트롤러 중 하나가 tooOMS 또는 tooSCOM, 참조 직접 [tooenable 도메인 컨트롤러가 아닌 toosend AD 데이터 tooOMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms)합니다.

## <a name="next-steps"></a>다음 단계
* 사용 하 여 [로그 분석 검색 로그인](log-analytics-log-searches.md) tooview Active Directory 복제 상태 데이터를 자세히 설명 합니다.
