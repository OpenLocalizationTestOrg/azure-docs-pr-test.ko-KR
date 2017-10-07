---
title: "분석 플랫폼: Apache Storm 비교 tooStream 분석 | Microsoft Docs"
description: "Apache Storm 비교 tooStream 분석을 사용 하 여 클라우드 분석 플랫폼을 선택 하는 지침을 알아봅니다. 기능 및 차이점을 이해하세요."
keywords: "분석 플랫폼, 클라우드 분석 플랫폼, storm 비교"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 5a0ec5b2439596f0da962f04b776472031660062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a>스트리밍 분석 플랫폼 선택: Apache Storm 및 Azure Stream Analytics 비교
Azure는 스트리밍 데이터 분석을 위해 [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) 및 [Azure HDInsight의 Apache Storm](https://azure.microsoft.com/services/hdinsight/apache-storm/)과 같은 여러 솔루션을 제공합니다. 분석 플랫폼은 모두 PaaS 솔루션의 hello 이점을 제공합니다. 하지만 hello 플랫폼도 구성 하 고 이러한 컴퓨터를 관리 하는 방법을 에서처럼의 기능에 따라 다릅니다. 

이 문서에서는 Apache Storm와 클라우드 분석 플랫폼으로 서 Azure 스트림 분석 중에서 선택할 기능 toohelp-나란히 비교 합니다. 

## <a name="general-features"></a>일반 기능

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>HDInsight의 Apache Storm</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>오픈 소스 여부</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
아니요. Azure Stream Analytics은 Microsoft 등록 제품입니다.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
예. Apache Storm은 Apache 라이선스가 허가된 기술입니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Microsoft 지원 여부</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
예 </p>
            </td>
            <td width="246" valign="top">
                <p>
예 </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>하드웨어 요구 사항</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
없음. Azure Stream Analytics은  인스턴스 Azure 서비스 입니다.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
없음. Apache Storm은 Azure 서비스입니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>최상위 단위</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
사용자가 스트리밍 작업을 배포 및 모니터링합니다.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
사용자는 다중 Storm 작업과 다른 워크로드(배치 포함)를 호스트할 수 있는 전체 클러스터를 배포하고 모니터링합니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>가격 책정</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
처리 된 데이터의 볼륨에 의해 가격이 책정 hello 스트리밍 단위 수가 필요한 시간당 작업 hello 있지만 실행 되 고 있습니다. 
                </p>
                    <p>자세한 내용은 <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics 가격</a>을 참조하세요.</p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
hello 단위 구입 클러스터 기반 이며 hello 클러스터가 실행 중인지, 배포 하는 작업의 독립적인 hello 시간에 따라 청구 됩니다.
                </p>
                <p>
자세한 내용은 <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight 가격</a>을 참조하세요.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a>작성

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>HDInsight의 Apache Storm</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>기능: SQL DSL 여부</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
예. Stream Analytics는 변환을 만들기 위해 SQL 유사 언어를 제공합니다.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
아니요. 사용자는 Java 또는 C#으로 코드를 작성하거나 Trident API를 사용합니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>기능: 임시 연산자 여부</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
기간 이동 집계 및 temporal 조인이 기본적으로 지원됩니다.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
임시 연산자는 hello 사용자에 의해 구현 되어야 합니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>개발 환경</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
사용자 만들 수, 디버깅 및 라이브 스트림을에서 파생 된 샘플 데이터를 사용 하 여 hello Azure 포털을 통해 작업을 모니터링 합니다.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
.NET을 사용하는 사용자는 Visual Studio를 통해 개발, 디버그 및 모니터할 수 있습니다. Java 또는 기타 언어를 사용 하 여 사용자가 선택한 IDE hello를 사용 수 있습니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>디버깅 지원</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
기본 작업 상태 및 작업 로그는 사용할 수 있는 toohelp 디버그 합니다. 스트림 분석 현재 수는 없습니다 사용자 지정 콘텐츠 또는 콘텐츠 hello 로그 (즉, 자세한 정보 표시 모드)에 포함 됩니다.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
자세한 로그를 사용할 수 있습니다. 사용자가 로그 toohello 클러스터를 로그인 하 고 hello 로그에 직접 액세스 하거나 Visual Studio에서 액세스할 수 있습니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>사용자 지정 코드를 사용하여 확장 가능 여부</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
JavaScript UDF에서 부분적으로 지원됩니다. 자세한 내용은 <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF 통합</a>을 참조하세요.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
예. 사용자는 C#, Java 또는 Storm에서 지원되는 다른 언어로 사용자 지정 코드를 작성할 수 있습니다.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a>데이터 원본(입력) 및 출력 ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>HDInsight의 Apache Storm</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                 <strong>입력 데이터 원본</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>Azure Event Hubs 및 Azure Blob Storage.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
커넥터는 Azure Event Hubs, Azure Service Bus, Kafka 등에 사용할 수 있습니다. 사용자는 사용자 지정 코드를 사용하여 추가 커넥터를 만들 수 있습니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>입력 데이터 형식</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Avro, JSON, CSV </p>
            </td>
            <td width="246" valign="top">
                <p>
사용자가 사용자 지정 코드를 사용하여 모든 형식을 구현할 수 있습니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>출력</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
스트리밍 작업은 여러 출력을 포함할 수 있습니다. 지원되는 출력은 Azure Event Hubs, Azure Blob Storage, Azure Table Storage, Azure SQL DB 및 Power BI입니다.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Storm에서는 토폴로지의 많은 출력을 지원하여 각 출력에는 다운스트림 처리에 대한 사용자 지정 논리가 있을 수 있습니다. Storm은 Power BI, Azure Event Hubs, Azure Blob Storage, Azure Cosmos DB, SQL 및 HBase에 대한 커넥터를 포함합니다. 사용자는 사용자 지정 코드를 사용하여 추가 커넥터를 만들 수 있습니다.    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>데이터 인코딩 형식</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
데이터는 UTF-8을 사용하여 형식이 지정되어야 합니다.
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
사용자가 사용자 지정 코드를 사용하여 모든 데이터 인코딩 형식을 구현할 수 있습니다.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a>관리 및 운영 ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>HDInsight의 Apache Storm</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>작업 배포 모델</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Azure Portal, PowerShell 및 REST API.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Azure Portal, PowerShell, Visual Studio 및 REST API.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>모니터링(통계, 카운터 등)</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
모니터링은 Azure Portal 및 REST API를 사용하여 구현됩니다. 사용자는 Azure 경고를 구성할 수도 있습니다.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
모니터링 스톰 UI hello 및 REST Api를 사용 하 여 구현 됩니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>확장성</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
확장성은 hello 스트리밍 단위 수가 (SUs) 각 작업에 의해 결정 됩니다. 최대 50 명의 단위와 m B/초를 too1를 처리 하는 각 스트리밍 단위 합니다. 자세한 내용은 참조 <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">배율 tooincrease 처리량</a>합니다.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
확장성은 hello hello HDInsight Storm 클러스터의에서 노드 수가 결정 됩니다. hello 상위 노드의 hello 수 제한은 15 hello 사용자의 Azure 할당량에 의해 정의 됩니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>데이터 처리 제한</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
사용자가 데이터 처리 늘리거나 증가 또는 감소 hello 개수 스트리밍 단위를 1 g B/초의 상한값을 적용 하 여 비용을 최적화 수입니다.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
사용자가 클러스터 크기를 확장 또는 축소할 수 있습니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>중지/다시 시작</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
중지한 후 중지된 마지막 위치에서 다시 시작 합니다.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
중지한 후 워터마크에 따라 중지된 마지막 위치에서 다시 시작 합니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>서비스 및 프레임워크 업데이트</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
가동 중지 시간 없이 자동 패치
                </p>
            </td>
            <td width="246" valign="top">
                <p>
가동 중지 시간 없이 자동 패치
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>보장된 SLA와 고가용 서비스를 통한 비즈니스 연속성</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li>SLA 가동 시간 99.9%</li>
                <li>오류에서 자동 복구</li>
                <li>temporal 상태 저장 연산자의 기본 제공 복구</li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
Hello Storm 클러스터의 99.9% 가동률의 SLA를 제공 합니다. 
                </p>
                <p>
Apache Storm는 내결함성이 있는 스트리밍 플랫폼입니다. 그러나는 스트리밍 작업이 실행 되는 중단 없이 hello 사용자의 책임 tooensure 되기 합니다.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a>고급 기능 ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>HDInsight의 Apache Storm</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>지연 도착 및 순서가 벗어난 이벤트 처리</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
기본 제공 구성 가능 정책으로 이벤트 순서 조정, 이벤트 드롭 또는 이벤트 시간 조정이 가능합니다.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
사용자가 논리 toohandle이이 시나리오를 구현 해야 합니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>참조 데이터</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
참조 데이터를 최대 100MB의 메모리 내 캐시가 있는 Azure Blob Storage에서 사용할 수 있습니다. 참조 데이터는 hello 서비스에서 새로 고쳐집니다.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
데이터 크기에 제한이 없습니다. 커넥터를 HBase, Azure Cosmos DB, SQL Server 및 Azure에 사용할 수 있습니다. 사용자는 사용자 지정 코드를 사용하여 추가 커넥터를 만들 수 있습니다. 참조 데이터는 사용자 지정 코드를 사용하여 새로 고쳐야 합니다.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Machine Learning과 통합</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
게시된 Azure Machine Learning 모델을 작업 생성 중에 함수로 구성할 수 있습니다. 자세한 내용은 <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Machine Learning 함수에 대한 크기 조정</a>을 참조하세요.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Storm Bolt를 통해 사용할 수 있습니다.
                </p>
            </td>
        </tr>
    </tbody>
</table>
