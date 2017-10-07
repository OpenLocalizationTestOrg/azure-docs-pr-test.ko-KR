---
title: "Operations Management Suite 보안 및 감사 솔루션을 시작 하는 aaaGetting | Microsoft Docs"
description: "이 문서를 사용 하면 있습니다 tooget 시작 Operations Management Suite 보안 및 감사 솔루션 기능 toomonitor 하이브리드 클라우드."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 754796ef-a43e-468a-86c9-04a2eda55b5b
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: get-started-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 5cb3e5dbb3e60f9702a34c9413ddc1bf2b14b411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-operations-management-suite-security-and-audit-solution"></a>Operations Management Suite 보안 및 감사 솔루션 시작
이 문서는 각 옵션을 안내하여 OMS(Operations Management Suite) 보안 및 감사 솔루션 기능을 빠르게 시작할 수 있도록 도와줍니다.

## <a name="what-is-oms"></a>OMS란?
OMS(Microsoft Operations Management Suite)는 온-프레미스 및 클라우드 인프라를 관리 및 보호하도록 도와주는 Microsoft의 클라우드 기반 IT 관리 솔루션입니다. OMS에 대 한 자세한 내용은 hello 문서를 읽어 보세요. [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)합니다.

## <a name="oms-security-and-audit-dashboard"></a>OMS 보안 및 감사 대시보드
OMS 보안 및 감사 솔루션 hello 제공 한 포괄적인 뷰를 조직의 IT 보안 상태에는 주의가 필요한 주요 문제에 대 한 기본 제공 검색 쿼리. hello **보안 및 감사** 대시보드는 모든 항목에 대 한 홈 화면 hello 관련 OMS에서 toosecurity 합니다. 컴퓨터의 hello 보안 상태에 대 한 개략적인 정보를 제공합니다. 지난 24 시간, 7 일 hello에서 모든 이벤트 또는 다른 사용자 지정 시간 프레임 hello 기능 tooview도 있습니다. tooaccess hello **보안 및 감사** 대시보드를 다음이 단계를 수행 합니다.

1. Hello에 **Microsoft Operations Management Suite** 기본 대시보드 클릭 **설정을** 타일 hello 왼쪽에 있습니다.
2. Hello에 **설정** 블레이드 아래 **솔루션** 클릭 **보안 및 감사** 옵션입니다.
3. hello **보안 및 감사** 대시보드가 표시 됩니다.
   
    ![OMS 보안 및 감사 대시보드](./media/oms-security-getting-started/oms-getting-started-fig1-ga.png)

에 액세스 하는 hello에 대 한이 대시보드 처음으로 하는 경우 OMS에서 모니터링 하는 장치 없는 hello 에이전트에서 가져온 데이터로 hello 타일 되지 채워집니다. Hello 에이전트를 설치한 다음 몇 시간 toopopulate 걸릴 수 있습니다, 그리고 따라서 나타나는 처음 수 일부 데이터가 없을 수 있고 toohello 클라우드 업로드할 여전히 대로 합니다.  이 경우 정상적인 toosee 일부 유형의 정보 없이 바둑판식으로 표시 됩니다. 읽기 [Windows 컴퓨터 연결 tooOMS 직접](https://technet.microsoft.com/library/mt484108.aspx) 방법에 대 한 자세한 내용은 Windows 시스템에 tooinstall OMS 에이전트 및 [연결 Linux 컴퓨터 tooOMS](https://technet.microsoft.com/library/mt622052.aspx) 방법에 대 한 자세한 내용은 tooperform이이 작업 에 Linux 시스템입니다.

> [!NOTE]
> hello 에이전트 hello 현재 이벤트를 기반으로 설정 된 컴퓨터 이름, IP 주소와 사용자 이름 예를 들어 hello 정보를 수집 합니다. 그러나 문서/파일, 데이터베이스 이름 또는 개인 데이터가 수집되지 않습니다.   
> 
> 

솔루션은 주요 고객 과제를 해결하는 논리, 시각화 및 데이터 취득 규칙의 모음입니다. 보안 및 감사는 하나의 솔루션이며 다른 솔루션은 별도로 추가할 수 있습니다. Hello 문서 읽기 [솔루션 추가](https://technet.microsoft.com/library/mt674635.aspx) 방법에 대 한 자세한 내용은 tooadd 새 솔루션입니다.

hello OMS 보안 및 감사 대시보드는 4 개의 주요 범주로 구성 되어 있습니다.

* **보안 도메인**:이 영역의 수 toofurther 됩니다 시간에 따른 보안 레코드를 탐색, 맬웨어 평가 액세스, 보안 이벤트를 평가, 네트워크 보안, id 및 액세스 정보, 컴퓨터를 업데이트, 빠르게 tooAzure 보안 센터 대시보드에 액세스 합니다.
* **주목할 만한 문제**:이 옵션을 하면 tooquickly hello 수가 활성 문제를 식별 하 고 이러한 문제의 심각도 hello 합니다.
* **검색 (미리 보기)**: 사용자 리소스에 대해 수행 하는 대로 보안 경고를 시각화 하 여 tooidentify 공격 패턴 수 있도록 합니다.
* **위협 인텔리전스**: 아웃 바운드 악성 IP 트래픽이, hello 악의적인 위협 유형입니다. 이러한 Ip에서 생성 되는 위치를 보여 주는 지도와 서버 hello 총 수를 시각화 하 여 tooidentify 공격 패턴 수 있도록 합니다. 
* **일반적인 보안 쿼리**:이 옵션은 사용할 수 있는 toomonitor 환경 쿼리 있습니다 hello 가장 일반적인 보안의 목록을 제공 합니다. 이러한 쿼리 중 하나에 클릭 hello 열립니다 **검색** 블레이드 hello 결과 함께 해당 쿼리에 대 한 합니다.

> [!NOTE]
> OMS가 데이터를 안전하게 유지하는 방식을 자세히 알아보려면 OMS가 데이터를 보호하는 방식을 참조하세요.
> 
> 

## <a name="security-domains"></a>보안 도메인
리소스를 모니터링 하는 경우 중요 한 toobe 수 tooquickly 액세스 hello 현재 환경의 상태는 합니다. 그러나 중요 한 toobe 수 tootrack 백 발생 한 이벤트를 지난에서 일어나는 특정 지점에서 사용자 환경에서 시간을 보다 잘 이해 tooa 시킬 수 있는 hello 이기도 합니다. 

> [!NOTE]
> 데이터 보존 toohello OMS 가격 계획을 따르는 것입니다. 자세한 내용은 방문 hello [Microsoft Operations Management Suite](https://www.microsoft.com/server-cloud/operations-management-suite/pricing.aspx) 가격 책정 페이지입니다.
> 
> 

인시던트 응답 및 법정 조사 시나리오 직접 hello에서 사용할 수 있는 hello 결과에서 이익을 얻을 **시간에 따른 보안 레코드** 바둑판식으로 배열입니다.

![시간별 보안 기록](./media/oms-security-getting-started/oms-getting-started-fig2.JPG)

이 타일을 클릭할 때 hello **검색** 블레이드가 열리고에 대 한 쿼리 결과 보여 주는 **보안 이벤트** (유형 = SecurityEvents)에 따라 hello 지난 7 일, 아래와 같이 데이터:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![시간별 보안 기록](./media/oms-security-getting-started/oms-getting-started-fig3.JPG)

hello 검색 결과로 두 창에 나누어져: hello 왼쪽된 창에 발견 된 hello 컴퓨터는 이러한 이벤트가 발견 된 이러한 컴퓨터에서 검색 된 계정의 hello 수와 hello 유형의 보안 이벤트 hello 수에 대 한 분석을 제공 작업을 합니다. hello 오른쪽 창에는 총 결과 hello 및 hello 컴퓨터의 이름 및 이벤트 활동을 포함 하는 hello 보안 이벤트의 시간 보기 제공합니다. 클릭할 수도 있습니다 **자세히 표시** tooview hello 이벤트 데이터, hello 이벤트 ID 등 hello 이벤트 원본이이 이벤트에 대 한 더 자세히 설명 합니다.

> [!NOTE]
> OMS 검색 쿼리에 대한 자세한 내용은 [OMS 검색 참조](https://technet.microsoft.com/library/mt450427.aspx)를 읽으세요.
> 
> 

### <a name="antimalware-assessment"></a>맬웨어 방지 평가
이 옵션에서는 있습니다 tooquickly 맬웨어에 의해 손상 된 컴퓨터와 보호 수준이 부족 한 컴퓨터를 식별 합니다. 맬웨어 평가 읽은 다음 데이터를 hello 상태 및 모니터링 하는 hello 서버에서 검색 된 위협 요소에는 처리를 위해 클라우드의 hello에 toohello OMS 서비스로 전송 됩니다. 위협이 발견된 된 서버 및 보호가 부족 한 서버 hello에서 클릭 한 후 액세스할 수 있는 hello 맬웨어 평가 대시보드에 표시 됩니다 **맬웨어 방지 평가** 바둑판식으로 배열입니다. 

![맬웨어 평가](./media/oms-security-getting-started/oms-getting-started-fig4-ga.png)

모든 다른 라이브 타일이 OMS 대시보드의에서 사용할 수 있는 것 처럼를 클릭할 때 hello **검색** hello 쿼리 결과 함께 블레이드가 열립니다. Hello에서 클릭 하는 경우이 옵션에 대 한 **을 보고 하지 않은** 옵션에서 **보호 상태**, hello 쿼리 결과와 hello 컴퓨터의 이름 및 차수를 포함 하는이 단일 항목을 보여 주는 갖습니다. 다음과 같습니다.

![검색 결과](./media/oms-security-getting-started/oms-getting-started-fig5.png)

> [!NOTE]
> *순위* 의 hello 보호 tooreflect hello 상태를 제공 하는 등급은 (, off, 업데이트 등) 및 발견 된 위협입니다. 숫자는 데 도움이 됩니다 toomake 집계를 보유.
> 
> 

Hello 컴퓨터의 이름을 클릭 한 경우이 컴퓨터에 대 한 hello 보호 상태의 hello 시간 보기를 해야 합니다. Hello 맬웨어 방지가 설치 하 고 특정 시점에 제거 toounderstand 필요한 시나리오에 매우 유용 합니다.   

### <a name="update-assessment"></a>업데이트 평가
이 옵션에서는 있습니다 tooquickly 결정 hello 전체 노출을 toopotential 보안 문제를 여부와 이러한 업데이트는 사용자 환경에 대 한 중요도 또는 합니다. OMS 보안 및 감사 솔루션만 이러한 업데이트의 hello 시각화를 제공, hello 실제 데이터를 [업데이트 관리 솔루션](oms-solution-update-management.md), OMS 내에서 다른 모듈은입니다. 여기 hello 업데이트의 예:

![시스템 업데이트](./media/oms-security-getting-started/oms-getting-started-fig6-new.png)

> [!NOTE]
> 업데이트 관리 솔루션에 대한 자세한 내용은 [OMS의 업데이트 관리 솔루션](oms-solution-update-management.md)을 참조하세요.
> 
> 

### <a name="identity-and-access"></a>ID 및 액세스
Id는 hello 제어 여야 합니다. 평면 id 보호를 사용 하 여 엔터프라이즈에 대 한 최상위 우선 되어야 합니다. 지난 hello에 있는 조직 주위의 경계 값과 해당 경계 않은 hello 기본 방어 경계 중 하나, 이제 더 많은 데이터와 더 많은 앱 toohello 클라우드 이동 hello identity가 hello 새 경계입니다. 

> [!NOTE]
> 현재 hello 데이터는 hello 이후 office 365 로그인에서 보안 이벤트 로그인 데이터 (이벤트 ID 4624)만 기반 하 고 Azure AD 데이터 포함 됩니다.
> 
> 

Id 작업을 모니터링 하 여 인시던트 사후 동작 toostop 공격 시도 또는 전체를 수행 하기 전에 수 tootake 사전 조치 하면 됩니다. hello **Id 및 액세스** 대시보드 제공 된 잠겨 있거나, 계정 재전송 시도 하는 동안 사용 된 hello 사용자의 계정에 실패 한 시도 toolog의 hello 번호를 포함 하 여 identity 상태에 대 한 개요 계정을 변경 또는 암호와 현재 로그인 되어 있는 계정의 수를 다시 설정 합니다. 

Hello에서을 클릭 하면 **Id 및 액세스** 타일 대시보드 다음 hello 표시 됩니다.

![ID 및 액세스](./media/oms-security-getting-started/oms-getting-started-fig7-ga.png)

이 대시보드에서 사용할 수 있는 hello 정보는 잠재적으로 의심 스러운 활동 tooidentify 즉시 도움이 됩니다. 예를 들어, 338 시도 toolog에 없는으로 **관리자** 100% 이러한 시도에 실패 했습니다. 원인은 이 계정에 대한 무차별 공격 때문일 수 있습니다. 이 계정에 대해 클릭이 잠재적인 공격에 대 한 toodetermine hello 대상 리소스 활용할 수 있는 자세한 정보 획득 합니다.

![검색 결과](./media/oms-security-getting-started/oms-getting-started-fig8.JPG)

hello 자세한 כ ַ ׁ이 이벤트에 대 한 중요 한 정보 포함: hello 대상 컴퓨터, 로그온 (이 경우 네트워크 로그온), (이 경우 이벤트에서 4625) hello 활동의 hello 유형 및 각 시도의 포괄적인 타임 라인입니다. 

### <a name="computers"></a>컴퓨터
이 타일 tooaccess 사용 되는 보안 이벤트를 능동적으로 되어 있는 모든 컴퓨터 일 수 있습니다. 이 타일에 클릭할 때 각 컴퓨터에서 보안 이벤트와 이벤트 hello 수 있는 컴퓨터의 hello 목록이 나타납니다.

![컴퓨터](./media/oms-security-getting-started/oms-getting-started-fig9.JPG)

각 컴퓨터에서를 클릭 하 여 조사를 계속 한 플래그가 지정 된 hello 보안 이벤트를 검토 합니다.

### <a name="threat-intelligence"></a>위협 인텔리전스

OMS 보안 및 감사에서 사용할 수 있는 hello 위협 인텔리전스 옵션을 사용 하 여 IT 관리자가 예를 들어 hello 환경에 대 한 보안 위협을 식별, 특정 컴퓨터 봇 네트의 일부인 경우를 식별할 수 있습니다. 공격자가 불법 비밀리이 컴퓨터 toohello 명령 및 제어를 연결 하는 맬웨어를 설치할 때 컴퓨터에서 봇 네트에서 노드를 될 수 있습니다. darknet 같은 지하 통신 채널에서 오는 잠재적 위협도 식별할 수 있습니다. 에 대 한 자세한 위협 인텔리전스 읽어 [Operations Management Suite 보안 및 감사 솔루션에서 경고를 모니터링 및 응답 toosecurity](oms-security-responding-alerts.md) 문서.

일부 시나리오에서는 모니터링되는 한 컴퓨터에서 잠재적인 악성 IP에 액세스한 것을 확인할 수 있습니다.

![위협 인텔리전스 맵](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

이 경고 및 기타 내 동일한 범주 hello, 활용 하 여 OMS 보안을 통해 생성 된 [Microsoft 위협 인텔리전스](https://youtu.be/O4WtxgUrDc8)합니다. hello 위협 인텔리전스 데이터는 Microsoft에서 수집한으로 업계 선두 위협 인텔리전스 공급 업체에서 구입 합니다. 이 데이터 자주 업데이트 되 고 위협 toofast 이동를 채택 합니다. Tooits 특성 인해 것 ठ ा 하는 동안 보안 정보의 다른 소스와 [조사](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) 보안 경고가 있습니다. 

### <a name="baseline-assessment"></a>기준 평가

전 세계 산업 및 정부 조직과 함께 Microsoft에서는 보안 수준이 높은 서버 배포를 나타내는 Windows 구성을 정의합니다. 이 구성은 일련의 레지스트리 키, 감사 정책 설정 및 이러한 설정에 대한 Microsoft의 권장된 값과 함께 보안 정책 설정을 설명합니다. 이러한 규칙 집합을 보안 기준이라고 합니다. 이 옵션에 대한 자세한 내용은 [Operations Management Suite 보안 및 감사 솔루션의 기준 평가](oms-security-baseline.md)를 참조하세요.

### <a name="azure-security-center"></a>Azure 보안 센터
이 타일은 기본적으로 바로 가기 tooaccess Azure 보안 센터 대시보드에. 이 솔루션에 대한 자세한 내용은 [Azure Security Center 시작](../security-center/security-center-get-started.md)을 참조하세요.

## <a name="notable-issues"></a>주목할 만한 문제
옵션의이 그룹의 주 목적은 hello tooprovide 위험, 경고 및 정보에서 분류 하 여 사용자 환경에서 사용 하는 hello 문제에 대 한 빠른 보기 것입니다. 이러한 문제를 시각화는 활성 문제 유형 타일 hello 하지만,에 대 한 세부 정보 tooexplore 수 하지 않습니다 toouse hello 개체 수 있었습니다 (개수) 이렇게 hello 문제 (이름)의 hello 이름이이 타일의 아래 부분에 대 한 필요 하 고 중요도 (심각도)를 합니다.

![주목할 만한 문제](./media/oms-security-getting-started/oms-getting-started-fig10.JPG)

이러한 문제 hello의 다양 한 영역에서 이미 검사 된 것을 확인할 수 있습니다 **보안 도메인** 그룹이이 보기의 hello 의도 도움이 되도록: hello 한 곳에서 사용자 환경에서 가장 중요 한 문제를 시각화 합니다.

## <a name="detections-preview"></a>감지(미리 보기)
hello이 옵션의 주요 목적은 tooallow IT를 통해 잠재적 위협 tootheir 환경 및이 위협을 hello 심각도 tooquickly 식별 합니다.

![위협 인텔리전스](./media/oms-security-getting-started/oms-getting-started-fig12.png)

하는 동안이 옵션을 사용할 수도 있습니다는 [사고 대응 조사](https://blogs.msdn.microsoft.com/azuresecurity/2016/11/30/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) tooperform 평가 hello 및 hello 공격에 대 한 자세한 정보를 가져옵니다.

> [!NOTE]
> 방법에 대 한 자세한 내용은이 비디오를 시청 하는 인시던트 응답에 대 한 OMS toouse: [tooLeverage 인시던트 응답에 대 한 Azure 보안 센터 & Microsoft Operations Management Suite을 hello 어떻게](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703)합니다.
> 
> 

## <a name="threat-intelligence"></a>위협 인텔리전스
새로운 위협 인텔리전스 섹션 hello 보안 및 감사 솔루션의 여러 가지 방법으로 hello 가능한 공격 패턴 시각화 hello: hello 총 아웃 바운드 악성 IP 트래픽이 있는 서버 수, 악성 위협 유형 및 위치를 보여 주는 지도 hello 이러한 Ip 제공 될 예정입니다. Hello 지도와 상호 작용을 hello Ip에 대 한 자세한 내용은 클릭할 수 있습니다.

Hello 지도에 노란색 압정 악성 Ip에서 들어오는 트래픽을 지정합니다. 도 드물지 않습니다 상태인 서버의 toohello 인터넷 toosee 들어오는, 악의적인 트래픽을 노출 되지만 이러한 시도 toomake 성공적으로 그 중 있는지 검토 하는 것이 좋습니다. 이러한 표시는 IIS 로그, WireData 및 Windows 방화벽 로그를 기반으로 합니다.  

![위협 인텔리전스](./media/oms-security-getting-started/oms-getting-started-fig11-ga.png)

## <a name="common-security-queries"></a>일반적 보안 쿼리
사용할 수 있는 일반적인 보안 쿼리 hello 목록 있습니다 toorapidly 액세스 리소스의 정보는 데 유용 하 고 사용자 환경 요구 사항에 따라 사용자 지정할 수 합니다. 이러한 일반적 쿼리는 다음과 같습니다.

* 모든 보안 활동
* Hello 컴퓨터 \ "computer01.contoso.com\" (사용자 컴퓨터 이름으로 대체)에서 수행 된 보안 활동
* Hello 컴퓨터 \ "computer01.contoso.com\" (고유한 컴퓨터 이름과 계정 이름으로 대체) "관리자" 계정에 대 한에서 수행 된 보안 활동
* 컴퓨터별 로그온 활동
* 임의 컴퓨터에서 Microsoft 맬웨어 방지 프로그램을 종료한 계정
* Hello Microsoft 맬웨어 방지 프로세스가 종료 된 컴퓨터
* "hash.exe"를 실행한 컴퓨터(다른 프로세스 이름으로 대체)
* 실행된 모든 프로세스 이름
* 계정별 로그온 활동
* Hello 컴퓨터 \ "computer01.contoso.com\" (사용자 컴퓨터 이름으로 대체)에서 원격으로 로그온 한 계정

## <a name="see-also"></a>참고 항목
이 문서에 도입 된 보안 및 감사 솔루션 tooOMS 있었습니다. OMS 보안에 대해 자세히 toolearn hello 다음 문서 참조:

* [OMS(Operations Management Suite) 개요](operations-management-suite-overview.md)
* [모니터링 및 Operations Management Suite 보안 및 감사 솔루션에 응답 중 tooSecurity 경고](oms-security-responding-alerts.md)
* [Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링](oms-security-monitoring-resources.md)

