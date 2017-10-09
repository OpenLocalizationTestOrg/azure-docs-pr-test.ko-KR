---
title: "Azure 데이터 레이크 저장소의 aaaOverview | Microsoft Docs"
description: "다른 데이터 저장소를 통해 제공 되는 Azure 데이터 레이크 저장소 및 hello 값 이해"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: b3475057-9427-4492-a3af-25a802a23a79
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 5a60a6b86a51c44647cf4ee168fb333d1c37b1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-data-lake-store"></a>Azure 데이터 레이크 저장소 개요
Azure 데이터 레이크 저장소는 빅 데이터 분석 작업을 위한 엔터프라이즈 수준 하이퍼 스케일 리포지토리입니다. Azure 데이터 레이크 운영 및 예비 분석을 위해 단일 위치에서 원하는 크기, 유형 및 수집 속도의 toocapture 데이터가 있습니다.

> [!TIP]
> 사용 하 여 hello [데이터 레이크 저장소 학습 경로](https://azure.microsoft.com/documentation/learning-paths/data-lake-store-self-guided-training/) toostart hello Azure 데이터 레이크 저장소 서비스를 탐색 합니다.
> 
> 

Azure 데이터 레이크 저장소 Hadoop에서 액세스할 수 있습니다 (HDInsight 클러스터에서 사용 가능)를 사용 하 여 WebHDFS 호환 REST Api를 hello 합니다. Hello 저장 된 데이터에 대해 특별히 디자인 된 tooenable 분석 하 고 데이터 분석 시나리오에 대 한 성능을 위해 조정 됩니다. 모든 hello 기업 수준의 기능이 포함 됩니다 hello 초기-보안, 관리 효율성, 확장성, 안정성 및 가용성-실제 엔터프라이즈 사용 사례에 중요 합니다.

![Azure 데이터 레이크](./media/data-lake-store-overview/data-lake-store-concept.png)

Hello hello Azure 데이터 레이크의 주요 기능 중 일부 hello 다음과를 같습니다.

### <a name="built-for-hadoop"></a>Hadoop용으로 작성
hello Azure 데이터 레이크 저장소와 Hadoop 분산 파일 시스템 (HDFS) 호환 되는 Apache Hadoop 파일 시스템 이며 hello Hadoop 에코 시스템을 사용 합니다.  기존 HDInsight 응용 프로그램이 나 hello WebHDFS API를 사용 하는 서비스에 데이터 레이크 저장소와 쉽게 통합할 수 있습니다. 데이터 레이크 저장소는 또한 응용 프로그램에 대한 WebHDFS 호환 REST 인터페이스를 노출합니다.

데이터 레이크 저장소에 저장된 데이터는 MapReduce 또는 Hive와 같은 Hadoop 분석 프레임워크를 사용하여 쉽게 분석될 수 있습니다. Microsoft Azure HDInsight 클러스터 프로 비전 할 수 하 고 toodirectly 데이터 레이크 저장소에 저장 된 데이터에 액세스를 구성 합니다.

### <a name="unlimited-storage-petabyte-files"></a>무제한 저장소, 페타바이트 파일
Azure 데이터 레이크 저장소는 무제한 저장소를 제공하며 분석에 대한 다양한 데이터를 저장하는데 적합합니다. 계정 크기, 파일 크기 또는 데이터 레이크에 저장할 수 있는 데이터 양을 hello에서 모든 제한이 적용 되지 않습니다. 개별 파일 크기가 최선의 선택 toostore 있어서 킬로바이트 toopetabytes에서 모든 종류의 데이터 범위 수 있습니다. 여러 복사 하 여 데이터를 지속적으로 저장 하 고 있는 hello에 대 한 데이터에에서 저장할 수 hello 데이터 레이크 시간의 hello 기간에 대 한 제한은 없습니다.

### <a name="performance-tuned-for-big-data-analytics"></a>빅 데이터 분석에 대한 성능 조정
Azure 데이터 레이크 저장소는 대규모 massive 처리량 tooquery 필요 하 고 많은 양의 데이터를 분석 하는 분석 시스템을 실행 하기 위한 빌드됩니다. 파일의 일부는 여러 개별 저장소 서버를 통해 확산 하는 hello 데이터 레이크 됩니다. Hello 데이터 분석을 수행 하기 위한 병렬로 hello 파일을 읽을 때 읽기 처리량 향상 됩니다.

### <a name="enterprise-ready-highly-available-and-secure"></a>엔터프라이즈 지원: 고가용성 및 보안
Azure 데이터 레이크 저장소는 업계 표준 가용성과 안정성을 제공합니다. 데이터 자산 모든 예기치 않은 오류에 대비한 중복 복사본 tooguard 하 여 지속적으로 저장 합니다. 기업에서는 기존 데이터 플랫폼의 중요한 부분으로 솔루션에서 Azure 데이터 레이크를 사용할 수 있습니다.

데이터 레이크 저장소는 또한 hello 저장 된 데이터에 대 한 엔터프라이즈 수준의 보안을 제공합니다. 자세한 내용은 [Azure 데이터 레이크 저장소의 데이터 보안](#DataLakeStoreSecurity)을 참조하세요.

### <a name="all-data"></a>모든 데이터
Azure 데이터 레이크 저장소는 사전 변환 없이 모든 데이터를 고유 형식으로 그대로 저장할 수 있습니다. 데이터 레이크 저장소 toohello 개별 분석 프레임 워크 toointerpret hello 데이터를 그대로 두고 hello 데이터를 로드 하기 전에 정의 된 스키마 toobe 필요 하지 않으며 hello hello 분석 시간에 스키마를 정의 합니다. 임의 크기와 형식 수 toostore 파일 되 고 구성 하 고, 데이터 레이크 저장소 toohandle 반 구조화 된 및 구조화 되지 않은 데이터에 대 한 수 있습니다.

데이터에 대한 Azure 데이터 레이크 저장소 컨테이너는 기본적으로 폴더 및 파일입니다. Sdk, Azure 포털 및 Azure Powershell을 사용 하 여 hello 저장 된 데이터에 대해 작동 합니다. 이러한 인터페이스를 사용 하 고 hello 적절 한 컨테이너를 사용 하 여 hello 저장소로 데이터를 설정으로 모든 종류의 데이터를 저장할 수 있습니다. 데이터 레이크 저장소 hello 형식의 저장 된 데이터에 따라 데이터의 특수 한 처리를 수행 하지 않습니다.

## <a name="DataLakeStoreSecurity"></a>Azure 데이터 레이크 저장소의 데이터 보호
인증을 위해 Azure Active Directory를 사용 하는 azure 데이터 레이크 저장소 및 액세스 제어 목록 (Acl) toomanage tooyour 데이터 액세스 합니다.

| 기능 | 설명 |
| --- | --- |
| 인증 |Azure 데이터 레이크 저장소는 Azure 데이터 레이크 저장소에 저장 된 모든 hello 데이터에 대 한 id 및 액세스 관리에 대 한와 Azure Active Directory (AAD)를 통합 합니다. Hello 통합, 다단계 인증, 조건부 액세스, 역할 기반 액세스 제어, 응용 프로그램 사용 모니터링, 보안 모니터링 및 경고를 포함 한 모든 AAD 기능에서 Azure 데이터 레이크 혜택 증분됩니다. Azure 데이터 레이크 저장소 hello REST 인터페이스의 인증을 위한 hello OAuth 2.0 프로토콜을 지원합니다. |
| Access Control |Azure 데이터 레이크 저장소 hello WebHDFS 프로토콜에 의해 노출 되는 POSIX 스타일 권한을 지원 하 여 액세스 제어를 제공 합니다. 데이터 레이크 저장소 공개 미리 보기 (현재 릴리스 hello) hello, Acl hello 루트 폴더, 하위 폴더 및 개별 파일에 대해 사용할 수 있습니다. Data Lake Store의 컨텍스트에서 ACL 작동 방법에 대한 자세한 내용은 [Data Lake Store의 액세스 제어](data-lake-store-access-control.md)를 참조하세요. |
| 암호화 |데이터 레이크 저장소는 또한 hello 계정에 저장 된 데이터에 대 한 암호화를 제공 합니다. 데이터 레이크 저장소 계정을 만드는 동안 hello 암호화 설정을 지정 합니다. 암호화 안 함 선택 하거나 선택한 toohave 암호화 된 데이터를 수 있습니다. 방법에 대 한 자세한 내용은 tooprovide 암호화 관련 구성 참조 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다. |

데이터 레이크 저장소에서 데이터를 보안에 대 한 자세한 toolearn을 합니다. 아래 hello 링크를 수행 합니다.

* 방법에 대 한 데이터 레이크 저장소의 데이터를 toosecure 참조 [Azure 데이터 레이크 저장소의 데이터를 보호 하려면](data-lake-store-secure-data.md)합니다.
* 비디오를 선호하십니까? [이 비디오를 시청](https://mix.office.com/watch/1q2mgzh9nn5lx) toosecure 데이터 데이터 레이크 저장소에 저장 하는 방식에 있습니다.

## <a name="applications-compatible-with-azure-data-lake-store"></a>Azure 데이터 레이크 저장소와 호환되는 응용 프로그램
Azure 데이터 레이크 저장소 hello Hadoop 생태계의 가장 열려 원본 구성 요소와 호환 됩니다. 또한 다른 Azure 서비스와 원활하게 통합됩니다. 따라서 Data Lake 저장소는 데이터 저장소 요구 사항에 맞는 완벽한 옵션입니다. 데이터 레이크 저장소 사용할 수 있는 방법을 모두 오픈 소스 구성 요소 뿐만 아니라 다른 Azure 서비스에 대 한 자세한 toolearn 아래 hello 링크 하십시오.

* Data Lake 저장소와 상호 운용 가능한 오픈 소스 응용 프로그램 목록은 [Azure Data Lake 저장소와 호환되는 응용 프로그램 및 서비스](data-lake-store-compatible-oss-other-applications.md) 를 참조하세요.
* 참조 [다른 Azure 서비스와 통합](data-lake-store-integrate-with-other-services.md) 다른 azure 데이터 레이크 저장소를 사용할 수 있는 방법을 toounderstand tooenable 광범위 한 시나리오를 서비스 합니다.
* 참조 [데이터 레이크 저장소를 사용 하는 시나리오](data-lake-store-data-scenarios.md) toolearn toouse 데이터 레이크 데이터를 수집 하는 방법 등의 시나리오에서 저장 하는 방법, 데이터 처리 하 고, 데이터를 다운로드 하 고, 데이터 시각화.

## <a name="what-is-azure-data-lake-store-file-system-adl"></a>Azure Data Lake Store 파일 시스템(adl://)이란 무엇입니까?
데이터 레이크 저장소 hello 새 파일 시스템을 통해 액세스할 수 있습니다, AzureDataLakeFilesystem hello (adl: / /), Hadoop 환경 (HDInsight 클러스터에서 사용 가능). 응용 프로그램 및 adl를 사용 하는 서비스: / / WebHDFS에서 현재 사용할 수 있는 성능 최적화 추가로 수 tootake 활용 됩니다. 결과적으로, 데이터 레이크 저장소 제공 유연성 tooeither hello 사용할 수 있는 메모리 hello 최상의 성능을 adl를 사용 하 여 권장 hello로: / / 또는 지속적인 toouse hello WebHDFS API에서 직접 기존 코드를 유지 합니다. Azure HDInsight hello AzureDataLakeFilesystem tooprovide hello에서 최적의 성능을 데이터 레이크 저장소를 완벽 하 게 활용합니다.

사용 하 여 hello 데이터 레이크 저장소의 데이터에 액세스할 수 있습니다 `adl://<data_lake_store_name>.azuredatalakestore.net`합니다. Tooaccess hello 데이터 레이크 저장소의에서 데이터를 hello 하는 방법에 대 한 자세한 내용은 참조 하십시오. [저장 된 데이터의 hello 속성 보기](data-lake-store-get-started-portal.md#properties)

## <a name="how-do-i-start-using-azure-data-lake-store"></a>Azure 데이터 레이크 저장소를 사용하여 어떻게 시작합니까?
참조 [Azure 포털 hello 데이터 레이크 저장소를 사용 하 여 시작](data-lake-store-get-started-portal.md), 어떻게 사용 하 여 데이터 레이크 저장소 tooprovision hello Azure 포털에 있습니다. Azure 데이터 레이크를 프로 비전 되 면 학습할 수 있는 방법을 Azure Data Lake 분석 또는 Azure HDInsight 데이터 레이크 저장소와 같은 toouse 빅 데이터 제공 합니다. .NET 응용 프로그램 toocreate Azure 데이터 레이크 저장소 계정을 만들 수 있고 데이터 업로드, 다운로드 데이터 등의 작업을 수행할 수도 있습니다.

* [Azure 데이터 레이크 분석 시작](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [데이터 레이크 저장소와 함께 Azure HDInsight 사용](data-lake-store-hdinsight-hadoop-use-portal.md)
* [.NET SDK를 사용하여 Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-net-sdk.md)

## <a name="data-lake-store-videos"></a>Data Lake 저장소 비디오
Toolearn 비디오를 시청 원하는 경우 데이터 레이크 저장소 다양 한 기능에 비디오를 제공 합니다.

* [Azure Data Lake 저장소 계정 만들기](https://mix.office.com/watch/1k1cycy4l4gen)
* [Hello 데이터 탐색기 tooManage 데이터를 사용 하 여 Azure 데이터 레이크 저장소](https://mix.office.com/watch/icletrxrh6pc)
* [Azure 데이터 레이크 분석 tooAzure 데이터 레이크 저장소 연결](https://mix.office.com/watch/qwji0dc9rx9k)
* [Data Lake 분석을 통해 Azure Data Lake 저장소에 액세스](https://mix.office.com/watch/1n0s45up381a8)
* [Azure HDInsight tooAzure 데이터 레이크 저장소 연결](https://mix.office.com/watch/l93xri2yhtp2)
* [Hive 및 Pig를 통해 Azure Data Lake 저장소에 액세스](https://mix.office.com/watch/1n9g5w0fiqv1q)
* [Azure 데이터 레이크 저장소에서 toocopy 데이터 tooand DistCp (Hadoop Distributed 복사)를 사용 하 여](https://mix.office.com/watch/1liuojvdx6sie)
* [관계형 원본과 Azure 데이터 레이크 저장소 간에 Apache Sqoop toomove 데이터를 사용 하 여](https://mix.office.com/watch/1butcdjxmu114)
* [Azure 데이터 팩터리를 사용하여 Azure Data Lake 저장소에 대한 데이터 오케스트레이션](https://mix.office.com/watch/1oa7le7t2u4ka)
* [Hello Azure 데이터 레이크 저장소의에서 데이터를 보호.](https://mix.office.com/watch/1q2mgzh9nn5lx)

