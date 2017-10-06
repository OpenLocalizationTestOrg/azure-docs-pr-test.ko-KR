---
title: "aaaConnected 팩터리 Azure IoT Suite 솔루션 연습 | Microsoft Docs"
description: "Hello 미리 구성 된 Azure IoT 솔루션에 대 한 설명을 팩터리 및 해당 아키텍처에 연결 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a>연결된 공장 미리 구성된 솔루션 연습

hello IoT Suite 연결 팩터리 [솔루션 미리 구성 된] [ lnk-preconfigured-solutions] 는 종단 간 산업 솔루션의 구현입니다:

* 시뮬레이션 된 팩터리에서는 생산 라인 실제 OPC UA 서버 장치 등에서 OPC UA 서버를 실행 하는 산업 tooboth 시뮬레이션 된 장치를 연결 합니다. OPC UA에 대 한 자세한 내용은 참조 hello [팩터리 FAQ 연결](iot-suite-faq-cf.md)합니다.
* 이러한 장치 및 생산 라인의 운영 KPI 및 OEE를 보여 줍니다.
* 방법을 클라우드 기반 응용 프로그램 사용된 toointeract OPC UA 서버 시스템과 수를 보여 줍니다.
* OPC UA 서버 장치를 tooconnect 있습니다를 수 있습니다.
* Toobrowse 있으며 hello OPC UA 서버 데이터를 수정 합니다.
* 사용자 지정 된 데이터 뷰를 hello OPC UA는 서버에서 Azure 시간 시계열 Insights (TSI) 서비스 tooprovide hello와 통합 됩니다.

사용자 고유의 구현에 대 한 시작 점으로 hello 솔루션을 사용할 수 있습니다 및 [사용자 지정] [ lnk-customize] 것 toomeet 특정 비즈니스 요구 사항입니다.

이 문서에서는 hello hello 연결 된 팩터리 솔루션 tooenable의 핵심 요소 중 일부를 통해 toounderstand 작동 방식입니다. 이 정보는 다음 항목을 도울 수 있습니다.

* Hello 솔루션의 문제를 해결 합니다.
* 계획 방법을 toocustomize toohello 솔루션 toomeet 특정 요구 사항입니다.
* Azure 서비스를 사용하는 고유한 IoT 솔루션을 디자인합니다.

자세한 내용은 참조 hello [팩터리 FAQ 연결](iot-suite-faq-cf.md)합니다.

## <a name="logical-architecture"></a>논리 아키텍처

다음 다이어그램 hello hello hello 미리 구성 된 솔루션의 논리적 구성 요소를 설명 합니다.

![연결된 공장 논리 아키텍처][connected-factory-logical]

## <a name="communication-patterns"></a>통신 패턴

hello 솔루션 hello를 사용 하 여 [UA Pub/Sub OPC 사양](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA 원격 분석 데이터 tooIoT 허브 JSON 형식에서입니다. hello 솔루션 hello를 사용 하 여 [OPC 게시자](https://github.com/Azure/iot-edge-opc-publisher) 이 목적을 위해 IoT 지 모듈입니다.

hello 솔루션에는 온-프레미스 OPC UA 서버와의 연결을 설정할 수 있는 웹 응용 프로그램에 통합 된 OPC UA 클라이언트가 있습니다. hello 클라이언트가 사용 하는 [역방향 프록시](https://wikipedia.org/wiki/Reverse_proxy) hello 온-프레미스 방화벽에서 포트 열기를 요구 하지 않고 IoT 허브 toomake hello 연결에서 도움말을 받습니다. 이 통신 패턴을 [서비스 지원 통신](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/)이라고 합니다. hello 솔루션 hello를 사용 하 여 [OPC 프록시](https://github.com/Azure/iot-edge-opc-proxy/) 이 목적을 위해 IoT 지 모듈입니다.


## <a name="simulation"></a>시뮬레이션

hello는 (MES) 시스템을 공장 생산 라인 구성 스테이션과 시뮬레이션 된 hello 제조 실행 시뮬레이션 합니다. hello 시뮬레이션 된 장치 및 hello OPC 게시자 모듈 기반 hello [OPC UA 표준.NET] [ lnk-OPC-UA-NET-Standard] hello OPC Foundation에서 게시 합니다.

hello OPC 프록시와 OPC 게시자는 모듈로 구현에 따라 [Azure IoT 가장자리][lnk-Azure-IoT-Gateway]합니다. 각 시뮬레이션된 생산 라인에는 지정된 게이트웨이가 연결되었습니다.

모든 시뮬레이션 구성 요소는 Azure Linux VM에서 호스팅되는 Docker 컨테이너에서 실행됩니다. hello 시뮬레이션은 구성 된 toorun 8 개의 시뮬레이션에서는 생산 라인 기본적으로입니다.

## <a name="simulated-production-line"></a>시뮬레이션된 생산 라인

생산 라인 제조 파트. 어셈블리 스테이션, 테스트 스테이션 및 패키징 스테이션과 같은 다른 스테이션으로 구성됩니다.

hello 시뮬레이션 실행 되 고 hello OPC UA 노드를 통해 노출 되는 hello 데이터를 업데이트 합니다. 모든 시뮬레이션된 생산 라인 스테이션 hello OPC UA 통해 MES에 의해 오케스트레이션 됩니다.

## <a name="simulated-manufacturing-execution-system"></a>시뮬레이션된 제조 실행 시스템

hello MES OPC UA toodetect 스테이션 상태 변경을 통해 hello 생산 라인의 각 스테이션을 모니터링합니다. OPC UA toocontrol hello 스테이션 메서드를 호출 하 고 제품에서에서 전달 한 스테이션 toohello 다음 완료 될 때까지 합니다.

## <a name="gateway-opc-publisher-module"></a>게이트웨이 OPC 게시자 모듈

OPC 게시자 모듈 toohello 스테이션 OPC UA 서버를 연결 하 고 toohello OPC 노드 toobe 게시를 구독 합니다. hello 모듈 hello 노드 데이터를 JSON 형식으로 변환 하 고, 암호화, OPC UA Pub/Sub 메시지로 tooIoT 허브 보냅니다.

hello OPC 게시자 모듈 아웃 바운드 https 포트 (443)만 걸리며 기존 엔터프라이즈 인프라를 작업할 수 있습니다.

## <a name="gateway-opc-proxy-module"></a>게이트웨이 OPC 프록시 모듈

hello 게이트웨이 OPC UA 프록시 모듈 터널링 이진 OPC UA 명령 및 제어 메시지 및 아웃 바운드 https 포트 (443)만 필요 합니다. 웹 프록시를 포함하여 기존 엔터프라이즈 인프라로 작업할 수 있습니다.

Hello 응용 프로그램 계층에서 IoT Hub 장치 메서드 packetized tootransfer TCP/IP 데이터를 사용 하며 따라서 끝점 신뢰, 데이터 암호화 및 SSL/TLS를 사용 하 여 무결성을 보장 합니다.

OPC UA 이진 프로토콜 헤더 블록이 릴레이 자체 hello 프록시를 통해 hello UA 인증 및 암호화를 사용 합니다.

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

게이트웨이 OPC 게시자 모듈 hello tooOPC UA 서버 노드 toodetect 값의 변경 내용이 hello 데이터를 구독합니다. Hello 노드 중 하나에서 데이터 변경 검색 된 경우이 모듈은 그런 다음 메시지 tooAzure IoT Hub 보냅니다.

IoT 허브는 이벤트 소스 tooAzure TSI를 제공합니다. 타임 스탬프에 따라 30 일에 대 한 데이터를 저장 TSI toohello 메시지 연결 합니다. 이 데이터에는 다음이 포함됩니다.

* OPC UA ApplicationUri
* OPC UA NodeId
* Hello 노드 값
* 원본 타임스탬프
* OPC UA DisplayName

현재 TSI 하지 못하도록 고객 tookeep hello 데이터에 대 한 원하는 toocustomize 시간입니다.

TSI는 SearchSpan(Time.From, Time.To)을 사용하여 노드 데이터에 대해 쿼리하고 OPC UA ApplicationUri 또는 OPC UA NodeId 또는 OPC UA DisplayName으로 집계합니다.

hello OEE 및 KPI 계기와 hello 시간 시계열 차트 데이터에 대 한 tooretrieve hello 데이터 이벤트, Sum, Avg, Min 및 Max 개수 별로 집계 됩니다.

hello 시계열을 다른 프로세스를 사용 하 여 빌드됩니다. OEE 및 Kpi 스테이션 기본 데이터에서 계산 되며 hello 토폴로지 (에서는 생산 라인, 팩터리, enterprise)에 대해 hello 응용 프로그램에 있게 됩니다.

또한 시계열 OEE 및 KPI 토폴로지에 대 한 표시 된 timespan가 준비 될 때마다 hello 응용 프로그램에서 계산 됩니다. 예를 들어 hello 일 보기에는 전체 1 시간 마다 업데이트 됩니다.

노드 데이터의 hello 타임 시계열 보기 timespan에 대 한 집계를 사용 하 여 TSI에서 직접 제공 됩니다.

## <a name="iot-hub"></a>IoT 허브
hello [IoT hub] [ lnk-IoT Hub] hello OPC 게시자 모듈 hello 클라우드로 전송 된 데이터를 수신 하 고 사용할 수 있는 toohello Azure TSI 서비스입니다. 

hello 솔루션에서 IoT Hub hello 또한:
- 모든 OPC 게시자 모듈 및 모든 OPC 프록시 모듈에 대 한 hello Id를 저장 하는 id 레지스트리에 유지 관리 합니다.
- Hello OPC 프록시 모듈의 양방향 통신에 대 한 전송 채널으로 사용 됩니다.

## <a name="azure-storage"></a>Azure 저장소
hello 솔루션 hello VM과 toostore 배포 데이터에 대 한 디스크 저장소로 Azure blob 저장소를 사용합니다.

## <a name="web-app"></a>웹앱
hello 웹 응용 프로그램 배포는 통합된 OPC UA 클라이언트, 처리 하는 경고 및 원격 분석 시각화 hello 미리 구성 된 솔루션의 일부로 구성 됩니다.

## <a name="next-steps"></a>다음 단계

Hello 다음 문서를 참조 하 여 IoT Suite를 시작 하기를 진행할 수 있습니다.

* [Hello azureiotsuite.com 사이트에 대 한 권한][lnk-permissions]
* [연결 된 hello 팩터리 미리 구성 된 솔루션에 대 한 Windows 또는 Linux에서 게이트웨이 배포](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
