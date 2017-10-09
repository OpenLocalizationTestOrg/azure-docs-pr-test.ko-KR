---
title: "Azure IoT Suite aaaCustomize 연결 팩터리 | Microsoft Docs"
description: "Hello의 toocustomize hello 동작 팩터리를 연결 하는 방법에 대 한 설명을 미리 솔루션을 구성 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a>Hello OPC UA는 서버에서 데이터를 표시 팩터리 솔루션에 연결 하는 방법을 사용자 지정

## <a name="introduction"></a>소개

hello 연결 된 팩터리 솔루션 집계 하 고 hello OPC UA 서버 연결 된 toohello 솔루션의에서 데이터를 표시 합니다. 찾아볼 수 있으며 명령을 toohello OPC UA 서버 솔루션에 보낼 수 있습니다. OPC UA에 대 한 자세한 내용은 참조 hello [팩터리 FAQ 연결](iot-suite-faq-cf.md)합니다.

Hello 솔루션의 집계 된 데이터의 예로 전체 장비 효율성 (OEE) hello 및 hello 팩터리, 선 및 스테이션 수준에서 hello 대시보드에서 볼 수 있는 핵심 성과 지표 (Kpi)이 있습니다. hello 다음 스크린샷은 hello에 대 한 hello OEE 및 KPI 값 **어셈블리** 스테이션에 **생산 라인 1**, hello에 **뮌헨** 팩터리:

![Hello 솔루션에서 OEE 및 KPI 값의 예][img-oee-kpi]

hello 솔루션 사용 하면 tooview 세부 정보에서 특정 데이터 항목에서 hello 서버 OPC UA 함 *스테이션*합니다. hello 다음 스크린샷은 차트가 hello 특정 스테이션에서 제조 된 항목 수 있습니다:

![제조된 항목 수 그림][img-manufactured-items]

Hello 그래프 중 하나를 클릭 하는 경우에 hello 데이터 시간 시계열 Insights (TSI)를 사용 하 여 자세히 탐색할 수 있습니다.

![Time Series Insights를 사용하여 데이터 탐색][img-tsi]

이 문서에서는 다음을 설명합니다.

- 어떻게 hello 데이터 toohello 사용할 수 있는 다양 한 보기를에서 이루어집니다 hello 솔루션.
- Hello 방식으로 hello 솔루션 사용자 지정할 수 hello 데이터가 표시 됩니다.

## <a name="data-sources"></a>데이터 원본

hello 연결 된 팩터리 솔루션 hello OPC UA 연결 된 서버 toohello 솔루션에서에서 데이터를 표시 합니다. hello 기본 설치는 공장 시뮬레이션을 실행 하는 여러 OPC UA 서버를 포함 합니다. 사용자 고유의 OPC UA 서버를 추가할 수 있는 [게이트웨이 통해 연결] [ lnk-connect-cf] tooyour 솔루션입니다.

연결된 된 OPC UA 서버 hello 대시보드에 tooyour 솔루션을 보낼 수 있음을 hello 데이터 항목을 찾아볼 수 있습니다.

1. Toohello 이동 **OPC UA 서버 선택** 보기:

    ![탐색 toohello OPC UA 서버 뷰 선택][img-select-server]

1. 서버를 선택하고 **연결**을 클릭합니다. 클릭 **진행** 때 hello 보안 경고가 나타납니다.

    > [!NOTE]
    > 이 경고는만 각 서버에 대해 한 번만 표시 하며 hello 솔루션 대시보드와 hello 서버 간에 트러스트 관계를 설정 합니다.

1. 서버 hello 찾아보기 hello 데이터 항목 toohello 솔루션을 보낼 수 이제 할 수 있습니다. Toohello 솔루션 전송 된 항목은 녹색 확인 표시:

    ![게시된 항목][img-published]

1. 있다면는 *관리자* hello 솔루션을 선택할 수 있습니다 toopublish 데이터 항목 toomake hello에서 사용할 수 있는 공장 솔루션 연결 합니다. 관리자는 데이터 항목의 hello 값을 변경 하 고 hello OPC UA 서버에서에서 메서드를 호출할 수도 있습니다.

## <a name="map-hello-data"></a>Hello 데이터 매핑

hello 팩터리 솔루션 지도 연결 하 고 집계 hello 게시 된 데이터 항목 hello OPC UA 서버 toohello에서에서 다양 한 뷰 hello 솔루션에서 키를 누릅니다. hello 연결 된 팩터리 솔루션 배포 tooyour Azure 계정 hello 솔루션을 프로 비전 할 때 합니다. JSON 파일에 연결 하는 Visual Studio 팩터리 솔루션 hello이 매핑 정보를 저장합니다. 보고 및 hello 연결 된 팩터리 Visual Studio 솔루션에서에서이 JSON 구성 파일을 수정할 수 있습니다. 변경을 수행한 후 hello 솔루션을 다시 배포할 수 있습니다.

Hello 구성 파일을 사용할 수 있습니다.

- Hello 기존 시뮬레이션 된 팩터리, 생산 라인 및 스테이션을 편집 합니다.
- Toohello 솔루션을 연결 하는 실제 OPC UA 서버에서 데이터를 매핑하십시오.

tooclone hello의 복사본을 공장 Visual Studio 솔루션을 사용 하 여 hello 다음 git 명령을 연결:

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

hello 파일 **ContosoTopologyDescription.json** hello hello OPC UA 서버 데이터에서에서 매핑 hello 연결 된 팩터리 솔루션 대시보드에 항목 toohello 뷰를 정의 합니다. Hello에서이 구성 파일을 찾을 수 있습니다 **Contoso\Topology** 폴더 hello에 **WebApp** hello Visual Studio 솔루션에서에서 프로젝트.

hello JSON 파일의 내용은 hello 팩터리, 생산 라인 및 스테이션 노드 계층으로 구성 됩니다. 이 계층 구조는 hello 연결 된 팩터리 대시보드에 hello 탐색 계층 구조를 정의합니다. Hello 계층의 각 노드에서 값 hello 대시보드에 표시 되는 hello 정보를 결정 합니다. 예를 들어 hello JSON 파일에는 hello를 다음 뮌헨 팩터리 hello에 대 한 값에 포함 되어 있습니다.

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

hello 이름, 설명 및 위치 hello 대시보드에서이 보기에 나타납니다.

![Hello 대시보드에 뮌헨 데이터][img-munich]

각 공장, 생산 라인 및 스테이션에는 이미지 속성이 있습니다. Hello에서 이러한 JPEG 파일을 찾을 수 있습니다 **Content\img** 폴더 hello에 **WebApp** 프로젝트. 이러한 이미지 파일 hello 연결 된 팩터리 대시보드에 표시 됩니다.

각 스테이션 hello OPC UA에서에서 데이터 항목의 매핑 hello를 정의 하는 몇 가지 자세한 속성을 포함 합니다. 이러한 속성은 hello 다음 섹션에에서 설명 되어 있습니다.

### <a name="opcuri"></a>OpcUri

hello **OpcUri** 는 hello OPC UA 응용 프로그램 URI hello OPC UA 서버를 고유 하 게 식별 하는 값입니다. 예를 들어 hello **OpcUri** hello 어셈블리 스테이션 뮌헨에 생산 라인 1에서 다음과 같은 hello에 대 한 값: **urn: scada2194:ua:munich:productionline0:assemblystation**합니다.

Uri의 연결 된 hello OPC UA 서버 hello hello 솔루션 대시보드에서 볼 수 있습니다.

![OPC UA 서버 URI 보기][img-server-uris]

### <a name="simulation"></a>시뮬레이션

hello에 대 한 정보를 hello **시뮬레이션** 노드는 특정 toohello 기본적으로 프로 비전 되는 OPC UA 서버 hello에서 실행 되는 OPC UA 시뮬레이션 합니다. 실제 OPC UA 서버에는 사용되지 않습니다.

### <a name="kpi1-and-kpi2"></a>Kpi1 및 Kpi2

이러한 노드는 hello 스테이션에서 데이터 hello 대시보드에 toohello 두 KPI 값을 제공 하는 방법을 설명 합니다. 기본 배포에서 이러한 KPI 값은 시간당 단위 및 시간당 kWh입니다. 스테이션의 hello 수준에서 KPI 값을 계산 하 고 hello 생산 라인 및 팩터리 수준에서이 집계 하는 hello 솔루션.

각 KPI에는 최소값, 최대값 및 대상 값이 있습니다. 각 KPI 값 팩터리 솔루션 tooperform 연결 hello에 대 한 경고 작업 정의할 수도 있습니다. hello 다음 코드 조각 정의 보여 줍니다 hello KPI hello 어셈블리 스테이션에 대 한 생산 라인 뮌헨에 1에서:

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

hello 다음 스크린샷은 hello KPI 데이터 hello 대시보드에.

![Hello 대시보드에서 KPI 정보][lnk-kpi]

### <a name="opcnodes"></a>OpcNodes

hello **OpcNodes** 노드 식별 hello hello OPC UA 서버에서에서 게시 된 데이터 항목 및 지정 방법을 tooprocess 해당 데이터입니다.

hello **NodeId** 값 식별 hello hello OPC UA 서버에서에서 특정 OPC UA NodeID 합니다. hello hello 어셈블리 스테이션에서 생산 라인 뮌헨에 1의 첫 번째 노드 값이 **ns = 2; i = 385**합니다. A **NodeId** 값 지정 OPC UA 서버 hello 및 hello에서 데이터 항목 tooread hello **심볼 이름** 해당 데이터에 대 한 hello 대시보드에 친숙 한 이름 toouse를 제공 합니다.

각 노드에 연결 된 다른 값은 다음 표에 hello에 요약 되어 있습니다.

| 값 | 설명 |
| ----- | ----------- |
| 관련성  | hello KPI 및 OEE 값이이 데이터에 기여합니다. |
| OpCode     | 어떻게 hello 데이터가 집계 됩니다. |
| Units      | hello 대시보드에 hello 단위 toouse 합니다.  |
| Visible    | 여부 toodisplay이 값에 hello 대시보드 합니다. 일부 값은 계산에 사용되지만 표시되지 않습니다.  |
| 최대    | hello 대시보드에 경고를 트리거하는 최대 값 hello입니다. |
| MaximumAlertActions | 응답 tooan 경고에서 작업 tootake 합니다. 예를 들어, 명령 tooa 스테이션을 보냅니다. |
| ConstValue | 계산에서 사용되는 상수 값입니다. |

## <a name="deploy-hello-changes"></a>Hello 변경 내용을 배포합니다

변경 내용을 toohello 만들기 완료 했을 때 **ContosoTopologyDescription.json** 파일을 다시 배포 해야 hello 팩터리 솔루션 tooyour Azure 계정을 연결 합니다.

hello **azure iot-연결-공장** 저장소에 포함 되어는 **build.ps1** PowerShell 스크립트 toorebuild를 사용 하 고 hello 솔루션을 배포할 수 있습니다.

## <a name="next-steps"></a>다음 단계

자세한 정보 hello 연결 된 팩터리 미리 구성 된 솔루션에 대 한 다음 문서를 읽는 hello 여:

* [연결된 공장 미리 구성된 솔루션 연습][lnk-rm-walkthrough]
* [연결된 공장에 대한 게이트웨이 배포][lnk-connect-cf]
* [Hello azureiotsuite.com 사이트에 대 한 권한][lnk-permissions]
* [연결된 팩터리 FAQ](iot-suite-faq-cf.md)
* [FAQ][lnk-faq]


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md