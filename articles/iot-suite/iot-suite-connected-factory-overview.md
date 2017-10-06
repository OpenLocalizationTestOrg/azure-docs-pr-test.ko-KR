---
title: "aaaAzure IoT Suite 연결 팩터리 개요 | Microsoft Docs"
description: "Hello Azure IoT Suite에 대 한 설명을 팩터리 미리 구성 된 솔루션을 연결 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a>연결 된 hello 미리 구성 하는 팩터리 솔루션 시작

Azure IoT Suite [솔루션 미리 구성 된] [ lnk-preconfigured-solutions] 일반적인 IoT 비즈니스 시나리오를 구현 하는 여러 Azure IoT 서비스 toodeliver 종단 간 솔루션을 결합 합니다. hello *연결 된 팩터리* 미리 구성 된 솔루션 tooand 모니터 산업 장치를 연결 합니다. 장치 및 toodrive operational 생산성 및 수익에서 데이터의 hello 솔루션 tooanalyze hello 스트림을 사용할 수 있습니다.

이 자습서에서는 tooprovision hello 팩터리를 연결 하는 방법을 솔루션 미리 구성 합니다. 또한 안내 합니다 hello hello 미리 구성 된 솔루션의 기본 기능입니다. 이러한 기능 중 대부분 hello 솔루션에서 액세스할 수 있습니다 *대시보드* hello 미리 구성 된 솔루션의 일부로 배포 하는:

![연결된 공장 미리 구성된 솔루션 대시보드][img-cf-home]

toocomplete이이 자습서에서는 활성 Azure 구독이 필요 합니다.

> [!NOTE]
> 계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 평가판][lnk_free_trial]을 참조하세요.
> 
> 

## <a name="provision-hello-solution"></a>프로 비전 hello 솔루션

1. Azure 계정 자격 증명을 사용 하 여 tooazureiotsuite.com에 로그인 하 고 클릭 "**+**" toocreate 솔루션입니다.
2. 클릭 **선택** hello에 **연결 된 팩터리** 바둑판식으로 배열입니다.
3. 미리 구성된 연결된 팩터리 솔루션에 대한 **솔루션 이름**을 입력합니다.
4. 선택 hello **구독** 및 **지역** toouse tooprovision hello 솔루션을 원할 수 있습니다.
5. 클릭 **솔루션 만들기** toobegin hello를 프로 비전 프로세스입니다. 이 프로세스는 일반적으로 몇 분 toorun을 걸립니다.

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a>프로비저닝 프로세스 toocomplete hello를 기다리는 동안

1. 솔루션에 hello 타일을 클릭 **프로 비전** 상태입니다.
2. 공지 hello **상태를 프로 비전** Azure 구독에서 Azure 서비스 배포 됩니다.
3. 프로 비전이 완료 되 면 hello 상태가 변경 될 너무**준비**합니다.
4. Hello 오른쪽 창에 솔루션의 hello 타일 toosee hello 자세히를 클릭 합니다.

> [!NOTE]
> Hello 미리 구성 된 솔루션을 배포 하는 문제가 발생 하는 경우 검토 [hello azureiotsuite.com 사이트에 대 한 권한을] [ lnk-permissions] 및 hello [팩터리 FAQ 연결](iot-suite-faq-cf.md)합니다. Hello 문제가 지속 되 면 hello에 서비스 티켓을 만들 [포털][lnk-portal]합니다.

솔루션에 대 한 목록에 없는 세부 정보 toosee 예상할 수 있습니까? [사용자 의견](https://feedback.azure.com/forums/321918-azure-iot)에 기능 제안을 보내주세요.

## <a name="scenario-overview"></a>시나리오 개요

연결 하는 hello를 배포할 때 팩터리 솔루션 미리 구성 된, toostep 일반적인 산업 시나리오를 통해 사용할 수 있는 리소스와 미리 채워져 합니다. 이 시나리오에서는 여러 팩터리 연결 hello 데이터 값을 필요한 toocompute toohello 솔루션 보고서 전반적인 장비 효율성 (OEE) 및 핵심 성과 지표 (Kpi). hello 다음 섹션에서는 방법을 보여 줍니다에:

* 팩터리, 생산 라인, 스테이션 OEE 및 KPI 값 모니터링
* Azure 시간 시계열 Insights를 사용 하 여 이러한 장치에서 생성 된 hello 원격 분석 데이터를 분석 합니다.
* 작업을 수행할 경고 toofix 문제

이 시나리오의 주요 기능은 수행할 수 있다는 이러한 모든 동작 원격으로 hello 솔루션 대시보드에서입니다. 물리적 액세스 toohello 장치 필요가 없습니다.

## <a name="view-hello-solution-dashboard"></a>Hello 솔루션 대시보드 보기

hello 솔루션 대시보드 toomanage 배포 된 hello 솔루션이 있습니다. 전역 팩터리 구성의 계층적 표현입니다. 예를 들어 OEE 및 KPI를 보고, 원격 분석 및 작업 경고에 대한 새 노드를 게시할 수 있습니다.

1. Hello 프로 비전이 완료 된 시점과 미리 구성 된 솔루션에 대 한 hello 타일 나타냅니다 **준비**, 선택 **시작** tooopen 새 탭에서 연결 된 팩터리 솔루션 포털입니다.

    ![미리 구성 하는 hello 솔루션 시작][img-launch-solution]

1. 기본적으로 hello 솔루션 포털 표시 hello *대시보드*합니다. hello 포털의 toonavigate tooother 영역 hello hello 페이지의 왼쪽에 hello 메뉴를 사용 합니다.

    ![연결된 공장 미리 구성된 솔루션 대시보드][cf-img-menu]

hello 대시보드 hello를 다음 정보를 표시 합니다.

* A **팩터리 목록** hello 솔루션의 hello 상태, 위치 및 현재 프로덕션 구성을 보여 주는 패널입니다. Hello 솔루션을 처음 실행할 때의 시뮬레이션 된 장치는 여러 가지가 있습니다. hello 생산 라인 시뮬레이션 3 명의 실제 OPC UA 생산 라인 당 시뮬레이션 된 작업을 수행 하 고는 서버 데이터를 공유로 구성 됩니다. OPC UA에 대 한 자세한 내용은 참조 hello [팩터리 FAQ 연결](iot-suite-faq-cf.md)합니다.
* A **지도** 각 장치의 표시 hello 위치 toohello 솔루션 연결 있는지 합니다. hello 솔루션 hello 맵에 hello Bing Maps API tooplot 정보를 사용할 수 있습니다. 구독이 Bing Maps Enterprise API에 대해 설정된 경우 이 기능이 자동으로 사용됩니다. 그렇지 않은 경우 참조 hello [FAQ] [ lnk-faq] toolearn 어떻게 toomake hello 맵 동적입니다.
* 원격 분석 또는 OEE/KPI 값이 특정 임계값을 초과할 때 생성되는 경고를 표시하는 **경고** 패널.
* **전반적인 장비 효율성** hello 전체 기업 또는 hello 공장/프로덕션에 대 한 hello OEE 값 선/있습니다 스테이션 표시 보고 패널입니다. 이 값은 hello 스테이션 보기 toohello 엔터프라이즈 수준에서 집계 됩니다. hello OEE 그림 및 구성 요소의 추가로 분석할 수 있습니다.
* **핵심 성과 지표** 생성 된 단위 및 에너지 hello 전체 기업 또는 hello 공장/생산 라인에서 사용 하는 hello 수를 표시 하면 스테이션이 / 패널 보고 합니다. 이러한 값은 스테이션 보기 toohello 엔터프라이즈 수준에서 집계 됩니다.

## <a name="view-factories"></a>공장 보기

hello *팩터리* 패널 hello 솔루션, 상태 및 현재 프로덕션 구성에서 모든 hello 팩터리의 지리적 위치 hello 보여 줍니다. Hello 위치 목록에서 toohello hello 솔루션 계층 구조의 다른 수준을 탐색할 수 있습니다. hello 행 hello 목록에서 해당 위치의 hello에서는 생산 라인의 세부 정보를 연결 하는 하이퍼링크가 됩니다. 그런 다음 가능한 toodrill hello 생산 라인 세부 정보를 및 toohello 스테이션에 대 한 개요 정보 중단 됩니다. 필터 toohello 목록도 적용할 수 있습니다.

![연결된 공장 미리 구성된 공장][cf-img-factories] 

1. hello **팩터리 패널** 표시 hello이 솔루션에 대 한 팩터리 목록입니다.

2. hello 팩터리 목록에는 처음 6 팩터리 hello를 프로 비전 프로세스에서 만든 표시 됩니다. 추가 시뮬레이션 및 물리적 장치 toohello 솔루션을 추가할 수 있습니다.

3. tooview hello 세부 정보는 팩터리의 hello 팩터리 목록의 hello 행을 클릭 합니다.

4. 생산 라인의 tooview hello 세부 정보는 hello 목록의 hello 행을 클릭 합니다.

5. tooview hello 게시 hello 생산 라인에서 스테이션의 OPC UA 노드, hello 목록 hello 행을 클릭 합니다.

6. hello 스테이션에 특정 노드에서 tooview 세부 정보는 hello 목록의 hello 행을 클릭 합니다. 이 작업 시간 시계열 Insights 시각화가 포함 된 hello 컨텍스트 패널을 시작합니다. Hello 시간 계열 Insights 탐색기 환경에서 이러한 그래프 toodo 추가 분석을 클릭 합니다.

## <a name="view-map"></a>지도 보기

구독 액세스 toohello Bing Maps API 있으면 hello *팩터리* 지도 보면 hello 지리적 위치 및 모든 hello 팩터리의 상태 hello 솔루션에 있습니다. hello 위치 세부 정보로 toodrill hello 지도에 표시 하는 hello 위치를 클릭 합니다.

![연결된 공장 미리 구성된 솔루션 지도][cf-img-map]

## <a name="view-alerts"></a>경고 보기

hello **경고** 패널 표시 인해 생성 된 경고 tooa 값 또는 구성 된 임계값을 초과 하는 계산 된 OEE/KPI 값을 보고 합니다. Hello 스테이션 개요 toohello 전역 보기에서 hello 계층의 각 수준에서이 패널에 경고가 표시 됩니다. hello 경고 hello 경고, 날짜, 시간, 위치 및 발생 수에 대 한 설명을 포함 합니다. Hello 시간 시계열 인 사이트 데이터를 사용 하 여 hello 경고를 발생 시킨 toohello 데이터에서 통찰력을 얻을 수 있습니다. hello 시간 계열 Insights에서 데이터를 시각화할 해당 되는 경고를 hello 합니다. 관리자 인 경우 hello 경고와 같은 기본 작업을 수행할 수 있습니다.

* 닫기 hello 경고입니다.
* Hello 경고를 확인 합니다.

필요에 따라 좀 더 복잡한 작업을 수행할 수 있습니다. 예를 들어 hello 어셈블리의 압력 OPC UA 노드 hello에 대 한 있습니다 수행할 수 있습니다.

* 새 브라우저 창에서 웹 페이지에 지원 정보를 표시합니다.
* Hello 장치에서 OPC UA 메서드를 호출 하 여 hello 경고의 원인 hello를 완화 합니다.
* Hello 기본 작업의 hello 사용 가능성을 표시 합니다.

    ![연결된 공장 미리 구성된 솔루션 경고][cf-img-alerts]

> [!NOTE]
> 이러한 경고는 hello 미리 구성 된 솔루션의 구성 파일에 지정 된 규칙에 의해 생성 됩니다. Hello OEE 또는 KPI 수치 또는 OPC UA 노드 값은 해당 구성 된 임계값을 초과 하는 경우 이러한 규칙에서 경고를 생성할 수 있습니다.

1. hello **경고 패널** 이 솔루션에서 생성 된 경고를 hello 보여 줍니다.

2. tooview hello 세부 정보는 경고의 hello 경고 패널에서 hello 경고를 클릭 합니다.

3. toofurther는 hello 경고 데이터를 분석, hello 경고 패널 tooopen hello 시간 계열 Insights 탐색기 환경에서 hello 그래프를 클릭 합니다.

4. tooaddress hello 경고, hello 경고 패널에서 사용할 수 있는 몇 가지 작업이 있습니다. Hello 적절 한 옵션을 선택 하 고 hello 클릭 동작 명령 단추를 실행 합니다.

## <a name="view-overall-equipment-efficiency"></a>설비 종합 효율 보기

OEE 세요 hello를 주요 제작과 관련 된 작업 매개 변수를 사용 하 여 hello 제조 프로세스의 효율성입니다. OEE는 산업 표준 측정값 hello 가용성, 성능 급여 및 품질 비율을 곱하여 계산: OEE 가용성 x 성능 품질 x = 합니다.

![연결된 공장 미리 구성된 솔루션 OEE][cf-img-oee]

1. tooview OEE hello 계층의 모든 수준에 대 한 필요한 toohello 특정 보기를 이동 합니다. 해당 보기에 대 한 hello OEE 각 hello OEE 백분율을 구성 하는 hello 요소와 함께 hello 패널에 표시 됩니다.

2. toofurther는 hello OEE hello 계층 구조 데이터의 모든 수준에 대 한 분석 hello OEE, 가용성, 성능 또는 품질 백분율을 클릭 합니다. 시간 시계열 Insights hello 지난 시간, 지난 24 시간 및 지난 7 일간의에서 데이터를 표시 하는 저전력된 시각화 컨텍스트 창이 나타납니다.

    ![연결된 공장 미리 구성된 솔루션 TSI 시각화][cf-img-tsi-visualization]

3. toofurther는 hello 경고 데이터를 분석, hello 경고 패널에서 hello 그래프를 클릭 합니다. Hello 시간 계열 Insights 탐색기 환경을 열립니다.

    ![연결된 공장 미리 구성된 솔루션 TSI 탐색기][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a>핵심 성과 지표 보기

hello 솔루션은 두 가지 핵심 성과 지표를 제공 */h* 및 *에너지 소비량 kwh에서*합니다.

![연결된 공장 미리 구성된 솔루션 KPI][cf-img-kpi]

1. 매 시간 마다 또는 hello 계층의 모든 수준에 사용 되는 에너지 tooview 단위 필요한 toohello 특정 보기를 이동 합니다. 시간 및 에너지 당 hello 단위가 hello 패널에서 표시를 사용 합니다.

2. 매 시간 마다 또는 또한 hello 계층의 모든 수준에 사용 되는 에너지 tooanalyze 단위 클릭 hello 계기 hello에 **핵심 성과 지표** 패널입니다. Tooview 데이터 hello 지난 시간, 지난 24 시간 및 지난 7 일 동안 hello에서 사용 하면 전원이 시간 시계열 Insights 시각화는 상황에 맞는 창이 나타납니다.

## <a name="scenario-review"></a>시나리오 검토

이 시나리오에서는 팩터리 OEE 및 Kpi 값을 하 여 hello 대시보드에 모니터링합니다. 그런 다음 사용 시간 시계열 Insights tooprovide 자세한 정보 toohelp 드릴 추가로 hello 원격 분석 데이터에 비정상 탐지 된 toohelp OEE 및 Kpi에 대 한 했습니다. 또한 프로그램 팩터리와 함께 hello 경고 패널 tooview 문제를 사용 하 고 hello 작업 사용 가능한 tooyou tooresolve hello 경고를 사용 합니다.

## <a name="other-features"></a>기타 기능

다음 섹션 hello hello 이전 시나리오에서 설명 되지 않은 연결 hello 팩터리 솔루션의 일부의 기능을 설명 합니다.

## <a name="apply-filters"></a>필터 적용

1. Hello 클릭 **펼침** toodisplay hello 팩터리 위치 패널 또는 hello 경고 패널에서 사용 가능한 필터 목록입니다.

2. 사용자에 대 한 hello 필터 패널이 표시 됩니다. 

    ![연결된 공장 미리 구성된 솔루션 필터][cf-img-alert-filter]

3. 필요한 hello 필터를 선택 합니다. Hello 필터 필드에 가능한 tootype 자유 텍스트 이기도합니다.

4. hello 필터를 적용 됩니다. hello 필터 상태가 hello 팩터리를 표시 하 고 테이블을 경고 하는 깔때기형 통해 hello 대시보드에 표시 됩니다.

    ![연결된 공장 미리 구성된 솔루션 필터][cf-img-alert-filter-funnel]

    > [!NOTE]
    > 활성 필터 표시 hello OEE 및 KPI 값에는 영향을 주지 hello 내용만 필터링 합니다.

5. 필터를 tooclear는 hello 깔때기형을 클릭 하 고 hello 필터 컨텍스트 창에서 필터를 클릭 합니다. 텍스트 hello **모든** hello 팩터리에 표시 되 고 테이블의 경고를 보냅니다.

## <a name="browse-an-opc-ua-server"></a>OPC UA 서버 찾아보기

Hello 미리 구성 된 솔루션을 배포 하면 자동으로 서버를 프로 비전 시뮬레이션 OPC UA hello 솔루션 브라우저를 통해 찾을 수 있습니다. 이러한 서버는 *시뮬레이션된 OPC UA 서버*입니다. 시뮬레이션 된 서버에 더 쉽게 있습니다 tooexperiment hello 필요 toodeploy real, 물리적 서버 없이 hello 미리 구성 된 솔루션입니다. 실제 OPC UA 서버 toohello 솔루션 tooconnect 않으려면 참조 hello [OPC UA 장치 연결 toohello 미리 구성 하는 팩터리 솔루션 연결] [ lnk-connect-cf] 자습서입니다.

1. Hello 클릭 **팩터리 아이콘** hello 대시보드 탐색 모음에서 합니다.

    ![연결된 공장 미리 구성된 솔루션 서버 브라우저][cf-img-server-browser]

2. Hello 미리 구성 된 목록에서 hello 서버 중 하나를 선택 합니다. 이 목록은 미리 구성 하는 hello 솔루션에서 사용자에 대 한 배포 된 hello 서버입니다.

    ![연결된 공장 미리 구성된 솔루션 서버 선택][cf-img-server-choice]

3. **연결**을 클릭하면 보안 대화 상자가 표시됩니다. Hello 시뮬레이션 것이 안전 tooclick **진행**

4. tooexpand hello hello 서버 트리의 노드 중 하나를 클릭 합니다. 원격 분석을 게시하는 노드 옆에는 눈금 표시가 있습니다.

    ![연결된 공장 미리 구성된 솔루션 서버 트리][cf-img-server-tree]

5. 항목 tooread를 마우스 오른쪽 단추로 클릭, 작성, 게시, 또는 해당 노드를 호출 합니다. hello 동작 사용 가능한 tooyou 사용 권한 및 hello 노드의 hello 특성에 따라 다릅니다. hello 옵션 toodisplays hello 특정 노드의 hello 값을 보여 주는 컨텍스트 패널을 읽습니다. hello 새 값을 입력할 수 있는 상황에 맞는 패널 옵션 표시를 작성 합니다. hello 통화 옵션 hello 호출에 대 한 hello 매개 변수를 입력할 수 있는 노드를 표시 합니다.

## <a name="publish-a-node"></a>노드 게시

검색할 때는 *시뮬레이션된 OPC UA 서버*를 선택할 수도 있습니다 toopublish 새 노드. Hello 솔루션의 이러한 노드 모두에서 hello 원격 분석을 분석할 수 있습니다. 이러한 *OPC UA 서버 시뮬레이션* real, 물리적 장치를 배포 하지 않고 쉽게 tooexperiment hello 미리 구성 된 솔루션을 확인 합니다.

1. OPC UA 서버 브라우저 트리에서 toopublish 한다고 hello에서 tooa 노드를 찾습니다.

2. Hello 노드를 마우스 오른쪽 단추로 클릭 합니다.

3. **게시**를 선택합니다.

    ![연결된 공장 노드 게시][cf-img-publish-node]

4. 상황에 맞는 패널 표시 게시 하면 hello 지시 성공 했습니다. hello 노드 옆에 확인 표시가 있는 hello 스테이션 수준 보기에 나타납니다.

    ![연결된 공장 미리 구성된 솔루션 게시 성공][cf-img-publish-success]

## <a name="command-and-control"></a>명령 및 컨트롤

연결 된 팩터리 hello 명령 및 hello 클라우드에서 직접 업계 장치를 사용 하 여 제어할 수 있습니다. 이 기능은 toorespond tooalerts hello 장치 생성을 사용할 수 있습니다. 예를 들어 hello 클라우드에서 명령 toohello 장치를 보낼 수 있습니다. Hello에서 사용할 수 있는 명령 hello를 찾을 수 **StationCommands** hello OPC UA 서버 브라우저 트리에서에서 노드. 이 시나리오에서는 생산 라인 뮌헨에 hello 어셈블리 스테이션에 압력 릴리스 밸브를 열 수 있습니다. toouse hello 명령 및 제어 기능에에서 있어야 hello **관리자** hello에 대 한 역할 미리 솔루션 배포를 구성 합니다.

1. Toohello 찾아보기 **StationCommands** hello OPC UA 서버 브라우저 트리에서에서 노드.

2. 사용 하 여 원하는 hello 명령을 선택 합니다.

3. Hello 노드를 마우스 오른쪽 단추로 클릭 합니다.

4. **호출**을 선택합니다.

    ![연결된 공장 미리 구성된 솔루션 명령 호출][cf-img-call-command]

5. 상황에 맞는 패널 toocall에 대 한 중인 방법을 알려주는 및 적용 가능한 모든 매개 변수 세부 정보는 나타납니다.

6. **호출**을 선택합니다.

    ![연결된 공장 미리 구성된 솔루션 호출 컨텍스트][cf-img-call-context]

7. hello 컨텍스트 패널은 업데이트 된 tooinform hello 메서드를 호출 하면 성공 합니다. Hello 호출의 결과로 업데이트는 hello 압력 노드의 hello 값을 읽어 성공 hello 호출을 확인할 수 있습니다.

    ![연결된 공장 미리 구성된 솔루션 호출 성공][cf-img-call-success]


## <a name="behind-hello-scenes"></a>Hello 백그라운드

미리 구성 된 솔루션을 배포 하면 hello 배포 프로세스 hello 선택한 Azure 구독에서에서 여러 리소스를 만듭니다. Hello Azure에서에서 이러한 리소스를 볼 수 있습니다 [포털][lnk-portal]합니다. hello 배포 프로세스 생성 한 **리소스 그룹** 미리 구성 된 솔루션에 대해 선택한 hello 이름을 기반으로 하는 이름의:

![Hello Azure 포털에서에서 미리 구성 된 솔루션][img-cf-portal]

Hello hello 리소스 그룹의 리소스 목록에서 선택 하 여 각 리소스의 hello 설정을 볼 수 있습니다.

미리 구성 하는 hello 솔루션에 대 한 hello 소스 코드를 볼 수 있습니다. hello 미리 구성 하는 연결 된 팩터리 솔루션 소스 코드는에 hello [azure iot-연결-공장] [ lnk-cfgithub] GitHub 리포지토리:

완료 되 면 hello에 Azure 구독에서 미리 구성 하는 hello 솔루션을 삭제할 수 있습니다 [azureiotsuite.com] [ lnk-azureiotsuite] 사이트입니다. 이 사이트 tooeasily 삭제를 hello 미리 구성 된 솔루션을 만든 경우 프로 비전 된 리소스를 hello 모두 있습니다.

> [!NOTE]
> 모든 항목을 삭제 하는 tooensure 관련 toohello 미리 구성 된 솔루션, hello에 삭제 [azureiotsuite.com] [ lnk-azureiotsuite] 사이트입니다. Hello 포털에서 hello 리소스 그룹을 삭제 하지 마십시오.

## <a name="next-steps"></a>다음 단계

미리 구성 된 솔루션을 배포한 했으므로 hello 다음 문서를 참조 하 여 IoT Suite 시작을 진행할 수 있습니다.

* [연결된 공장 미리 구성된 솔루션 연습][lnk-rm-walkthrough]
* [장치 toohello 미리 구성 하는 연결 된 팩터리 솔루션 연결][lnk-connect-cf]
* [Hello azureiotsuite.com 사이트에 대 한 권한][lnk-permissions]

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md