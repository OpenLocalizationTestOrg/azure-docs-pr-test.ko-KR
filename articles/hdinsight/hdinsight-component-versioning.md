---
title: "aaaHadoop 구성 요소 및 버전-Azure HDInsight | Microsoft Docs"
description: "Hortonworks Data Platform의이 클라우드 배포에서 사용할 수 있는 HDInsight 및 hello 서비스 수준에서 버전의 hello Hadoop 구성 요소에 알아봅니다."
keywords: "hadoop 버전, hadoop 에코 시스템 구성 요소, hadoop 구성 요소가 어떻게 toocheck hadoop 버전"
services: hdinsight
editor: cgronlun
manager: asadk
author: bprakash
tags: azure-portal
documentationcenter: 
ms.assetid: 367b3f4a-f7d3-4e59-abd0-5dc59576f1ff
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: bprakash
ms.openlocfilehash: b661d901b0113458c3501ec06454fc8841189672
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-hadoop-components-and-versions-available-with-hdinsight"></a>Hello Hadoop 구성 요소 및 HDInsight를 사용할 수 있는 버전은 무엇입니까?

Standard 및 Premium 서비스 수준을 hello 뿐만 아니라 hello Apache Hadoop 에코 시스템 구성 요소 및 Microsoft Azure HDInsight의 버전에 알아봅니다. 또한 자세한 방법을 HDInsight의 Hadoop 구성 요소 버전 toocheck 합니다. 

각 HDInsight 버전은 클라우드 배포판의 HDP(Hortonworks Data Platform) 버전입니다.

## <a name="hadoop-components-available-with-different-hdinsight-versions"></a>각 HDInsight 버전에서 제공되는 Hadoop 구성 요소
Azure HDInsight는 언제든 배포할 수 있는 여러 Hadoop 클러스터 버전을 지원합니다. 각 버전 선택 사항을 hello HDP 배포의 특정 버전 및 해당 배포에 포함 된 구성 요소 집합을 만듭니다. 2017 년 2 월 17을 기준으로 Azure HDInsight에서 사용 하는 hello 기본 클러스터 버전은 3.5 및 HDP 2.5를 기반으로 합니다.

HDInsight 클러스터 버전이와 관련 된 hello 구성 요소 버전은 다음 표에 hello에 나열 됩니다. 

> [!NOTE]
> hello HDInsight 서비스에 대 한 hello 기본 버전은 예 고 없이 변경 될 수 있습니다. 버전 종속성을 설정한 경우 Azure PowerShell 및 Azure CLI를 통해.NET SDK hello로 클러스터를 만들 때 hello HDInsight 버전을 지정 합니다.

| 구성 요소 | HDInsight 3.6(기본값) | HDInsight 3.5 | HDInsight 3.4 | HDInsight 3.3 | HDInsight 3.2 | HDInsight 3.1 | HDInsight 3.0 |
| --- | --- | --- | --- | --- | --- | --- |--- |
| Hortonworks Data Platform |2.6 |2.5 |2.4 |2.3 |2.2 |2.1.7 |2.0 |
| Apache Hadoop 및 YARN |2.7.3 |2.7.3 |2.7.1 |2.7.1 |2.6.0 |2.4.0 |2.2.0 |
| Apache Tez |0.7.0 |0.7.0 |0.7.0 |0.7.0 |0.5.2 |0.4.0 |-|
| Apache Pig |0.16.0 |0.16.0 |0.15.0 |0.15.0 |0.14.0 |0.12.1 |0.12.0 |
| Apache Hive 및 HCatalog |1.2.1 |1.2.1 |1.2.1 |1.2.1 |0.14.0 |0.13.1 |0.12.0 |
| Apache Hive2 | 2.1.0 |-|-|-|-|-|-|
| Apache Tez Hive2 | 0.8.4 |-|-|-|-|-|-|
| Apache Ranger | 0.7.0 |0.6.0 |-|-|-|-|-|
| Apache HBase |1.1.2 |1.1.2 |1.1.2 |1.1.1 |0.98.4 |0.98.0 |-|
| Apache Sqoop |1.4.6 |1.4.6 |1.4.6 |1.4.6 |1.4.5 |1.4.4 |1.4.4 |
| Apache Oozie |4.2.0 |4.2.0 |4.2.0 |4.2.0 |4.1.0 |4.0.0 |4.0.0 |
| Apache Zookeeper |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.5 |3.4.5 |
| Apache Storm |1.1.0 |1.0.1 |0.10.0 |0.10.0 |0.9.3 |0.9.1 |-|
| Apache Mahout |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0 |0.9.0 |-|
| Apache Phoenix |4.7.0 |4.7.0 |4.4.0 |4.4.0 |4.2.0 |4.0.0.2.1.7.0-2162 |-|
| Apache Spark |2.1.0(Linux만 해당) |1.6.2 + 2.0(Linux만 해당) |1.6.0(Linux만 해당) |1.5.2(Linux 실험적 빌드만 해당) |1.3.1(Windows만 해당) |-|-|
| Apache Kafka | 0.10.0 | 0.10.0 | 0.9.0 |-|-|-|-|
| Apache Ambari | 2.5.0 | 2.4.0 | 2.2.1 | 2.1.0 |-|-|-|
| Apache Zeppelin | 0.7.0 |-|-|-|-|-|-|
| Mono |4.2.1 |4.2.1 |3.2.8 |-|-|-|

## <a name="check-for-current-hadoop-component-version-information"></a>현재 Hadoop 구성 요소 버전 정보 확인

HDInsight 클러스터 버전에 연결 된 hello Hadoop 에코 시스템 구성 요소 버전으로 업데이트 tooHDInsight 변경할 수 있습니다. toocheck hello Hadoop 구성 요소 및 버전을 사용 하는 클러스터에 사용 되 고 tooverify hello Ambari REST API를 사용 합니다. hello **GetComponentInformation** 명령은 서비스 구성 요소에 대 한 정보를 검색 합니다. 자세한 내용은 참조 hello [Ambari 설명서][ambari-docs]합니다.

Windows 클러스터에 대 한 또 다른 방법은 toocheck hello 구성 요소 버전은 toolog tooa 클러스터에 원격 데스크톱을 사용 하 여 하며 hello C:\apps\dist\ 디렉터리의 hello 내용을 검사 합니다.

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [HDInsight에서 Windows 사용 중지](#hdinsight-windows-retirement)를 참조하세요.

### <a name="release-notes"></a>릴리스 정보

참조 [HDInsight 릴리스 정보](hdinsight-release-notes.md) hello HDInsight의 최신 버전에서 추가 릴리스 정보에 대 한 합니다.

## <a name="supported-hdinsight-versions"></a>지원되는 HDInsight 버전
hello 다음 표에 hello 버전의 HDInsight은 hello Azure 포털에서 현재 사용할 수 있습니다. hello HDP 버전 tooeach HDInsight 버전을 해당 하는 hello 제품 출시 날짜와 함께 나열 되어 있습니다. 알려진 하는 경우 hello 지원 만료 및 사용 중지 날짜도 제공 됩니다.

> [!NOTE]
> 지원을 만료 되는 버전에 대 한 것 하지 못할 수도 있습니다 hello Microsoft Azure 클래식 포털을 통해. 그러나 클러스터 버전 계속 toobe hello를 사용 하 여 사용할 수 있는 `Version` hello Windows PowerShell의에서 매개 변수에 [새로 AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx) 명령 및.NET SDK hello 버전 사용 중지 날짜까지 hello 합니다.
> 
> 헤드 노드가 2개 있는 고가용성 클러스터는 기본적으로 HDInsight 버전 2.1 이상에 배포됩니다. HDInsight 버전 1.6 클러스터에서는 사용할 수 없습니다.

| HDInsight 버전 | HDP 버전 | VM OS | 고가용성 | 릴리스 날짜 | Hello Azure 포털에서 가용성 | 지원 만료 날짜 | 사용 중지 날짜 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| HDInsight 3.6 |HDP 2.6 |Ubuntu 16 |예 |2017년 4월 4일 |예 | | |
| HDInsight 3.5 |HDP 2.5 |Ubuntu 16 |예 |2016년 9월 30일 |예 |2017년 9월 5일 |2018년 5월 31일 |
| HDInsight 3.4 |HDP 2.4 |Ubuntu 14.0.4 LTS |예 |2016년 3월 29일 |예 |2016년 12월 29일 |2018년 1월 9일 |
| HDInsight 3.3 |HDP 2.3 |Windows Server 2012 R2 |예 |2015년 12월 2일 |예 |2016년 6월 27일 |2018년 7월 31일 |
| HDInsight 3.3 |HDP 2.3 |Ubuntu 14.0.4 LTS |예 |2015년 12월 2일 |예 |2016년 6월 27일 |2017년 7월 31일 |
| HDInsight 3.2 |HDP 2.2 |Ubuntu 12.04 LTS 또는 Windows Server 2012 R2 |예 |2015년 2월 18일 |아니요 |2016년 3월 1일 |2017년 4월 1일 |
| HDInsight 3.1 |HDP 2.1 |Windows Server 2012 R2 |예 |2014년 6월 24일 |아니요 |2015년 5월 18일 |2016년 6월 30일 |
| HDInsight 3.0 |HDP 2.0 |Windows Server 2012 R2 |예 |2014년 2월 11일 |아니요 |2014년 9월 17일 |2015년 6월 30일 |
| HDInsight 2.1 |HDP 1.3 |Windows Server 2012 R2 |예 |2013년 10월 28일 |아니요 |2014년 5월 12일 |2015년 5월 31일 |
| HDInsight 1.6 |HDP 1.1 | |아니요 |2013년 10월 28일 |아니요 |2014년 4월 26일 |2015년 5월 31일 |

## <a name="hdinsight-windows-retirement"></a>HDInsight Windows 사용 중지
Microsoft Azure HDInsight 버전 3.3 hello 마지막 버전의 Windows에서 HDInsight 했습니다. hello는 Windows에서 HDInsight에 대 한 사용 중지 날짜는 2018 년 7 월 31입니다. 또는 이전 버전의 Windows 3.3 하는 HDInsight 클러스터를 설정한 경우 2018 년 7 월 31, 하기 전에 Linux (HDInsight 버전 3.5 이상)에서 tooHDInsight 마이그레이션해야 합니다. Toohello Linux OS tooretain hello 기능 toocreate를 사용 하면 마이그레이션하거나 HDInsight 클러스터의 크기를 조정 합니다. Windows의 HDInsight 버전 3.3에 대한 지원은 2016년 6월 27일에 만료되었습니다.

HDInsight 버전 3.4 이상에서는 hello Linux 운영 체제에 대해서만 Microsoft HDInsight 출시 했습니다. 결과적으로, HDInsight 내 hello 구성 요소 중 일부가 Linux 용는 으로만 제공 됩니다. 여기에 Apache 레인저, Kafka, 대화형 하이브, Spark, HDInsight 응용 프로그램 및 hello 주 파일 시스템으로 Azure 데이터 레이크 저장소입니다. HDInsight의 이후 릴리스에서 hello Linux 운영 체제 에서만 사용할 수 있습니다. Windows HDInsight는 향후에 더 이상 릴리스되지 않습니다. 

## <a name="faqs"></a>FAQ

### <a name="what-is-hello-timeline-for-retiring-hdinsight-on-windows"></a>Windows에서 HDInsight를 사용 중지에 대 한 타임 라인 hello 이란?
Windows에서 HDInsight에 대 한 사용 중지 날짜는 hello 2018, 7 월 31입니다. 계획 된 hello 사용 중지 날짜는 해당 지역에 대 한 다른 면 별도로 알림을 받게 됩니다. 

### <a name="what-is-hello-impact-of-retiring-hdinsight-on-windows-for-existing-customers"></a>기존 고객을 위해 Windows에서 HDInsight를 사용 중지의 영향 hello 이란?
Windows HDInsight가 사용 중지된 후에 새로운 Windows HDInsight를 만들거나 기존 Windows HDInsight의 크기를 조정할 수 없습니다. Windows HDInsight 버전 3.3에 대한 지원은 2016년 6월 27일에 만료되었습니다. 따라서 HDInsight 3.3 이전 버전에 대한 지원이나 버그 수정은 없습니다. HDInsight의 이후 릴리스에서 hello Linux 운영 체제 에서만 사용할 수 있습니다. Windows HDInsight는 향후에 더 이상 릴리스되지 않습니다.
 
### <a name="which-versions-of-hdinsight-on-windows-are-affected"></a>영향을 받는 Windows HDInsight 버전은 무엇인가요?
Azure HDInsight 버전 3.3는 HDInsight에 대 한 windows hello 마지막 버전입니다. Windows의 HDInsight는 사용 중지 전에 모든 HDInsight Windows 클러스터 버전 3.3 또는 이전 버전 이어야 합니다는 Linux 버전 3.5 이상에서 tooHDInsight 마이그레이션됩니다. Linux 클러스터 tooHDInsight 프로그램 마이그레이션 기존 클러스터 크기를 조정 하거나 있습니다 tooretain hello 기능 toocreate 새 클러스터를 사용 합니다. 

### <a name="what-do-i-need-toodo"></a>수행할 작업 toodo 필요 합니까?
2018 년 7 월 31, 하기 전에 HDInsight Windows 클러스터 지원 tooa HDInsight Linux 클러스터를 마이그레이션하십시오. Hello에서 자세한 내용을 [HDInsight 마이그레이션 문서](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux)합니다. Azure HDInsight 버전에 대 한 자세한 참조 hello 목록이 [지원 되는 버전](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-component-versioning#supported-hdinsight-versions)합니다. 

### <a name="where-do-i-find-hello-cluster-os-type"></a>Hello 클러스터 운영 체제 종류는 어디서 찾을 수 있습니까?
Hello Azure 포털에서에서 toohello HDInsight 클러스터의 개요 페이지를 이동 하 고 찾을 **형식 클러스터** 아래 **Essentials**합니다. hello 클러스터 운영 체제 종류는 해당 페이지에 나열 됩니다. 

### <a name="i-cant-migrate-tooan-hdinsight-linux-cluster-by-july-31-2018-what-is-hello-impact-toomy-hdinsight-windows-cluster"></a>2018 년 7 월 31 여 tooan HDInsight Linux 클러스터를 마이그레이션할 수 없습니다 I. Hello 영향 toomy HDInsight Windows 클러스터는 무엇입니까?
hello HDInsight Windows 클러스터로 실행-이면 있지만 기존 HDInsight Windows 클러스터의 크기를 조정 하거나 새 HDInsight Windows 클러스터를 만들 수 없습니다. 

### <a name="my-cluster-has-a-net-dependency-how-do-i-resolve-this-dependency-on-linux"></a>내 클러스터에 .NET 종속성이 있습니다. Linux에서 이 종속성을 해결하려면 어떻게 하나요?
Linux 클러스터 종속성 hello를 사용 하 여 해결할 수 있습니다 [모노 프로젝트](http://www.mono-project.com/)합니다. 이 .NET의 오픈 소스 구현은 HDInsight Linux 클러스터에 사용할 수 있습니다. Hello에서 자세한 내용을 [HDInsight 마이그레이션 문서](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux)합니다. 

### <a name="im-a-new-customer-for-hdinsight-on-windows-how-can-i-create-an-hdinsight-windows-cluster"></a>사용자가 Windows HDInsight에 새 고객입니다. HDInsight Windows 클러스터를 만들려면 어떻게 할까요?
2017년 7월 3일을 기준으로 기존 HDInsight Windows 고객만이 새로운 HDInsight Windows 클러스터를 만들 수 있습니다. 신규 고객은 PowerShell 또는 hello SDK 사용 하 여 hello Azure 포털에서에서 HDInsight Windows 클러스터를 만들 수 없습니다. 신규 고객은 Linux HDInsight 클러스터를 만드는 것이 좋습니다. 기존 고객 HDInsight windows hello 사용 중지 날짜까지 새 HDInsight Windows 클러스터를 만들 수 있습니다. 

### <a name="is-there-a-pricing-impact-associated-with-moving-from-hdinsight-on-windows-toohdinsight-on-linux"></a>이 Windows tooHDInsight linux에서 HDInsight에서 이동과 관련 된 가격에 영향 있습니까?
아니요, hello 가격 책정은 hello 동일한 운영 체제 중 하나에 HDInsight에 대 한 합니다. 

### <a name="what-are-hello-customer-advantages-associated-with-hello-move-tooonly-using-hdinsight-on-linux"></a>Linux에서 HDInsight를 사용 하 여 tooonly 이동할 hello와 관련 된 hello 고객 이점 이란?
* 더 빠른 시간을 단축 hello HDInsight 서비스를 통해 오픈 소스 빅 데이터 기술에 대 한
* 지원을 위한 대규모 커뮤니티 및 에코시스템
* 기능 tooexercise 개발 hello 하 여 Hadoop 및 기타 빅 데이터 기술에 대 한 소스 커뮤니티를 열려면

### <a name="does-hdinsight-on-linux-provide-additional-functionality-beyond-what-is-available-in-hdinsight-on-windows"></a>Linux HDInsight는 Windows HDInsight에서 사용할 수 있는 기능 이외의 추가 기능을 제공하나요?
HDInsight 버전 3.4 이상에서는 hello Linux 운영 체제에 대해서만 Microsoft HDInsight 출시 했습니다. 결과적으로, HDInsight 내 hello 구성 요소 중 일부가 Linux 용는 으로만 제공 됩니다. 여기에 Apache 레인저, Kafka, 대화형 하이브, Spark, HDInsight 응용 프로그램 및 hello 주 파일 시스템으로 Azure 데이터 레이크 저장소입니다. 

## <a name="service-level-agreement-for-hdinsight-cluster-versions"></a>HDInsight 클러스터 버전의 서비스 수준 약정
hello 서비스 수준 계약 (SLA)의 측면에서 정의 되는 _지원 창의_합니다. hello 지원 창의 HDInsight 클러스터 버전이 Microsoft 고객 서비스 및 지원에서 지원 되는 시간의 hello 기간입니다. Hello 버전에는 _만료 날짜를 지원_ 경과 하는, hello 지원 기간을 벗어나도 hello HDInsight 클러스터는 합니다. 지원 되는 버전에 대 한 자세한 내용은 참조 hello 목록이 [지원 되는 HDInsight 클러스터 버전](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux)합니다. 지정 된 HDInsight 버전 (새 X + 1 버전을 사용할 수 있음) 한 후 X에 대 한 hello 지원 만료 날짜는 다음과 같이 나중의 hello 계산 됩니다.  

* 수식 1: hello HDInsight 클러스터 버전이 X 릴리스한 180 일 toohello 날짜를 추가 합니다.
* 수식 2: 때 hello HDInsight 클러스터 버전이 X + 1 Azure 포털에서 사용할 수는 90 일 동안 toohello 날짜를 추가 합니다.

hello _사용 중지 날짜_ 지나면 hello 클러스터 버전에 만들 수 없습니다 HDInsight hello 날짜입니다. 2017년 7월 31일부터 사용 중지 날짜 이후에는 HDInsight 클러스터의 크기를 조정할 수 없습니다. 

> [!NOTE]
> HDInsight Windows 클러스터 (포함 하 여 버전 2.1, 3.0, 3.1, 3.2 및 3.3) 버전 4 hello 64 비트 버전의 Windows Server 2012 r 2를 사용 하 여 Azure 게스트 OS 제품군에서 실행 합니다. Azure 게스트 OS 제품군 버전 4 hello.NET Framework 버전 4.0, 4.5, 4.5.1 및 4.5.2 지원합니다.

## <a name="hortonworks-release-notes-associated-with-hdinsight-versions"></a>HDInsight 버전과 관련된 Hortonworks 릴리스 정보

hello 섹션 링크 toorelease 노트 hello Hortonworks Data Platform 분포 및 HDInsight 함께 사용 되는 Apache 구성 요소에 제공 합니다.
* HDInsight 클러스터 버전 3.6에서는 [Hortonworks Data Platform 2.6](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.0/bk_release-notes/content/ch_relnotes.html)을 기반으로 하는 Hadoop 배포를 사용합니다.
* HDInsight 클러스터 버전 3.5에서는 [Hortonworks Data Platform 2.5](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.5.0/bk_release-notes/content/ch_relnotes_v250.html)를 기반으로 하는 Hadoop 배포를 사용합니다. HDInsight 클러스터 버전이 3.5는 hello _기본_ hello Azure 포털에서에서 만들어진 Hadoop 클러스터.
* HDInsight 클러스터 버전 3.4에서는 [Hortonworks Data Platform 2.4](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html)를 기반으로 하는 Hadoop 배포를 사용합니다.
* HDInsight 클러스터 버전 3.3에서는 [Hortonworks Data Platform 2.3](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html)(영문)를 기반으로 하는 Hadoop 배포를 사용합니다.

  * [Apache Storm 릴리스 정보](https://storm.apache.org/2015/11/05/storm0100-released.html) hello Apache 웹 사이트에서 사용할 수 있습니다.
  * [릴리스 정보 Apache Hive](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12332384&styleName=Text&projectId=12310843) hello Apache 웹 사이트에서 사용할 수 있습니다.
* HDInsight 클러스터 버전 3.2에서는 [Hortonworks Data Platform 2.2][hdp-2-2]를 기반으로 하는 Hadoop 배포를 사용합니다.

  * 특정 Apache 구성 요소에 대한 릴리스 정보는 다음과 같이 사용할 수 있습니다. [Hive 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310843&version=12326450), [Pig 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310730&version=12326954), [HBase 0.98.4](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310753&version=12326810), [Phoenix 4.2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12315120&version=12327581), [M/R 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310941&version=12327180), [HDFS 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310942&version=12327181), [YARN 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12313722&version=12327197), [Common](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310240&version=12327179), [Tez 0.5.2](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314426&version=12328742), [Ambari 2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12312020&version=12327486), [Storm 0.9.3](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314820&version=12327112), [Oozie 4.1.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12324960&projectId=12311620).
* HDInsight 클러스터 버전 3.1에서는 [Hortonworks Data Platform 2.1.7][hdp-2-1-7]를 기반으로 하는 Hadoop 배포를 사용합니다. 2014년 11월 7일 이전에 만들어진 HDInsight 3.1 클러스터는 [Hortonworks Data Platform 2.1.1][hdp-2-1-1]을 기반으로 합니다.
* HDInsight 클러스터 버전 3.0에서는 [Hortonworks Data Platform 2.0][hdp-2-0-8]을 기반으로 하는 Hadoop 배포를 사용합니다.
* HDInsight 클러스터 버전 2.1에서는 [Hortonworks Data Platform 1.3][hdp-1-3-0]을 기반으로 하는 Hadoop 배포를 사용합니다.
* HDInsight 클러스터 버전 1.6에서는 [Hortonworks Data Platform 1.1][hdp-1-1-0]을 기반으로 하는 Hadoop 배포를 사용합니다.

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard 및 HDInsight Premium

두 가지 범주의 hello 빅 데이터 클라우드 서비스를 제공 하는 azure HDInsight: _표준_ 및 _프리미엄_합니다. hello 다음 표에서 사용할 수 있는 기능 _만_ HDInsight 프리미엄에 있습니다. Hello 테이블에 명시적으로 설명 되지 않은 기능은 HDInsight Standard 및 Premium에서 사용할 수 있습니다.

> [!NOTE]
> hello HDInsight Premium 서비스는 현재 미리 보기에서 및 Linux 클러스터에만 사용할 수 있습니다.

| HDInsight Premium 기능 | 설명 |
| --- | --- |
| 도메인에 가입된 HDInsight 클러스터 |엔터프라이즈 수준의 보안에 대 한 HDInsight 클러스터 tooAzure Active Directory (Azure AD) 도메인에 가입 시킵니다. HDInsight 프리미엄 tooan HDInsight 클러스터에서 Azure AD toolog를 통해 인증할 수 있는 기업에서 직원의 목록이 구성할 수 있습니다. enterprise admin 님 안녕하세요 하이브 보안에 대 한 역할 기반 액세스 제어를 사용 하 여 구성할 수 [Apache 레인저](http://hortonworks.com/apache/ranger/) 만큼만 필요한 데이터 액세스 toouse를 제한 합니다. 마지막으로, admin 님 안녕하세요 직원이 액세스 하는 데이터를 감사할 수 및 변경 내용을 tooaccess 제어 정책, 있으므로 높은 수준의 회사 리소스의 거 버 넌 스를 달성 합니다. 자세한 내용은 [도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md)을 참조하세요. |

### <a name="cluster-types-supported-in-hdinsight-premium"></a>HDInsight Premium에서 지원되는 클러스터 형식
hello 다음 표에서 hello 클러스터 형식이 나와 HDInsight Premium에서는 사용할 수 있습니다.

| 클러스터 유형 | Standard | Premium(미리 보기) |
| --- | --- | --- |
| Hadoop은 |예 |예(HDInsight 3.6만 해당) |
| Spark |예 |아니요 |
| HBase |예 |아니요 |
| Storm |예 |아니요 |
| R 서버 |예 |아니요 |
| 대화형 Hive(미리 보기) |예 |아니요 |
| Kafka(미리 보기) |예 |아니요 | 

### <a name="support-for-azure-data-lake-store-in-hdinsight-premium"></a>HDInsight Premium에서 Azure Data Lake Store에 대한 지원

HDInsight Premium 클러스터는 Azure Data Lake Store를 기본 저장소로 사용하도록 지원하지 않습니다. 그러나 HDInsight Premium 클러스터에서 Azure Data Lake Store를 추가 기능 저장소로 사용할 수 있습니다.

### <a name="pricing-and-sla"></a>가격 및 SLA
HDInsight Premium의 가격 및 SLA에 대한 자세한 내용은 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.

## <a name="default-node-configuration-and-virtual-machine-sizes-for-clusters"></a>클러스터에 대한 기본 노드 구성 및 가상 컴퓨터 크기
HDInsight 클러스터에 대 한 테이블 목록을 hello 기본 가상 컴퓨터 (VM) 크기를 다음 번호입니다.

> [!IMPORTANT]
> 클러스터에 필요한 작업자 노드 수가 32개를 초과하는 경우 최소한 코어 8개와 14GB RAM을 가진 헤드 노드 크기를 선택해야 합니다.
> 
> 

* 브라질 남부 및 일본 서부를 제외하고 지원되는 모든 지역:

  | 클러스터 유형 | Hadoop은 | HBase | Storm | Spark | R 서버 |
  | --- | --- | --- | --- | --- | --- |
  | 헤드: 기본 VM 크기 |D3 v2 |D3 v2 |A3 |D12 v2 |D12 v2 |
  | 헤드: 권장되는 VM 크기 |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |A3, A4, A5 |D12 v2, D13 v2, D14 v2 |D12 v2, D13 v2, D14 v2 |
  | 작업자: 기본 VM 크기 |D3 v2 |D3 v2 |D3 v2 |Windows: D12 v2; Linux: D4 v2 |Windows: D12 v2; Linux: D4 v2 |
  | 작업자: 권장되는 VM 크기 |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |
  | Zookeeper: 기본 VM 크기 | |A3 |A2 | | |
  | Zookeeper: 권장되는 VM 크기 | |A3, A4, A5 |A2, A3, A4 | | |
  | Edge: 기본 VM 크기 | | | | |Windows: D12 v2; Linux: D4 v2 |
  | Edge: 권장되는 VM 크기 | | | | |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |
* 브라질 남부 및 일본 서부만 해당(v2 크기 제외):

  | 클러스터 유형 | Hadoop은 | HBase | Storm | Spark | R 서버 |
  | --- | --- | --- | --- | --- | --- |
  | 헤드: 기본 VM 크기 |D3 |D3 |A3 |D12 |D12 |
  | 헤드: 권장되는 VM 크기 |D3, D4, D12 |D3, D4, D12 |A3, A4, A5 |D12, D13, D14 |D12, D13, D14 |
  | 작업자: 기본 VM 크기 |D3 |D3 |D3 |Windows: D12; Linux: D4 |Windows: D12; Linux: D4 |
  | 작업자: 권장되는 VM 크기 |D3, D4, D12 |D3, D4, D12 |D3, D4, D12 |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |
  | Zookeeper: 기본 VM 크기 | |A2 |A2 | | |
  | Zookeeper: 권장되는 VM 크기 | |A2, A3, A4 |A2, A3, A4 | | |
  | Edge: 기본 VM 크기 | | | | |Windows: D12; Linux: D4 |
  | Edge: 권장되는 VM 크기 | | | | |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |

> [!NOTE]
> - H e a d로 알려져 *Nimbus* hello Storm 클러스터 유형입니다.
> - 작업자 라고 *감독자* hello Storm 클러스터 유형입니다.
> - 작업자 라고 *지역* hello HBase 클러스터 유형입니다.

## <a name="next-steps"></a>다음 단계
- [HDInsight의 Hadoop, Spark 등에 대한 클러스터 설정](hdinsight-hadoop-provision-linux-clusters.md)
- [Windows PC에서 HDInsight의 Hadoop 작업](hdinsight-hadoop-windows-tools.md)

[Supported HDInsight versions]:(#supported-hdinsight-versions)

[image-hdi-versioning-versionscreen]: ./media/hdinsight-component-versioning/hdi-versioning-version-screen.png

[wa-forums]: http://azure.microsoft.com/support/forums/

[connect-excel-with-hive-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md

[hdp-2-2]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[ambari-docs]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[zookeeper]: http://zookeeper.apache.org/
