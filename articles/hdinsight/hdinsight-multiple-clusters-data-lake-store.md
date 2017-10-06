---
title: "Azure 데이터 레이크 저장소 계정-Azure로 여러 HDInsight 클러스터 aaaUse | Microsoft Docs"
description: "단일 데이터 레이크 저장소 계정을 사용 하 여 클러스터 toouse 두 개 이상의 하나의 HDInsight에 알아봅니다"
keywords: "hdinsight 저장소, hdfs, 구조화된 데이터, 구조화되지 않은 데이터, Data Lake Store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: nitinme
ms.openlocfilehash: 3a125b91fcc1e436270a1bd349f7a2d8f27e06fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-multiple-hdinsight-clusters-with-an-azure-data-lake-store-account"></a>Azure Data Lake Store 계정으로 여러 HDInsight 클러스터 사용

HDInsight 버전 3.5 이상에서는 HDInsight 클러스터에 Azure 데이터 레이크 저장소 계정으로 hello 기본 파일 시스템으로 만들 수 있습니다.
Data Lake Store는 많은 양의 데이터 호스팅 뿐만 아니라 단일 Data Lake Store 계정을 공유하는 여러 HDInsight 클러스터 호스팅에 적합하도록 만드는 제한되지 않은 저장소를 지원합니다. Hello 저장소로 데이터 레이크 저장소 인 toocreate HDInsight 클러스터를 어떻게 instructionson, 참조 [데이터 레이크 저장소와 만들 HDInsight 클러스터](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)합니다.

이 문서는 단일 및 공유 데이터 레이크 저장소 계정 여러 사용할 수 있는 설정에 대 한 권장 사항을 toohello 데이터 레이크 저장소 관리자에서는 **활성** HDInsight 클러스터에 있습니다. 이러한 권장 사항은 toohosting 여러 보안 뿐만 아니라 안전 하지 않은 Hadoop 클러스터는 공유 데이터 레이크 저장소 계정에 적용 합니다.


## <a name="data-lake-store-file-and-folder-level-acls"></a>Data Lake Store 파일 및 폴더 수준 ACL

hello이 문서의 나머지 부분 가정에서 자세히 설명 되어 있는 Azure 데이터 레이크 저장소의 파일 및 폴더 수준 Acl에 대해 잘 알고 있다고 [Azure 데이터 레이크 저장소의 액세스 제어](../data-lake-store/data-lake-store-access-control.md)합니다.

## <a name="data-lake-store-setup-for-multiple-hdinsight-clusters"></a>여러 HDInsight 클러스터에 대한 Data Lake Store 설정
주세요 두 수준의 폴더 계층 구조를 HDInsight 클러스터에 여러 데이터 레이크 저장소 계정으로 사용 하기 위한 tooexplain hello 권장 사항을 수행 합니다. Hello 폴더 구조와 데이터 레이크 저장소 계정이 있어야 하는 것이 좋습니다. **/클러스터/finance**합니다. 이 구조와 hello 재무 부서에 필요한 모든 hello 클러스터 hello 저장소 위치로 /clusters/finance를 사용할 수 있습니다. Hello, 다른 조직의 마케팅 예를 들어, toocreate HDInsight 클러스터를 사용 하 여 hello 동일한 데이터 레이크 저장소 계정, /clusters/marketing을 일으킬가 경우에 향후에 있습니다. 이제 **/클러스터/재무**를 사용해보겠습니다.

tooenable이 폴더 구조 toobe HDInsight 클러스터에서 효과적으로 사용, 데이터 레이크 저장소 관리자에 게 적절 한 권한을 할당 하 해야 hello 표에 설명 된 대로 합니다. hello 표에 표시 된 hello 사용 권한이 tooAccess Acl 및 하지 기본 Acl에 해당 합니다. 


|폴더  |권한  |소유 사용자  |소유 그룹  | 명명된 사용자 | 명명된 사용자 권한 | 명명된 그룹 | 명명된 그룹 권한 |
|---------|---------|---------|---------|---------|---------|---------|---------|
|/ | rwxr-x--x  |관리자 |관리자  |서비스 주체 |--x  |FINGRP   |r-x         |
|/클러스터 | rwxr-x--x |관리자 |관리자 |서비스 주체 |--x  |FINGRP |r-x         |
|/클러스터/재무 | rwxr-x--t |관리자 |FINGRP  |서비스 주체 |rwx  |-  |-     |

Hello 표에

- **관리자** hello 만든이 및 관리자의 hello Data Lake 저장소 계정이 됩니다.
- **서비스 사용자** hello Azure Active Directory (AAD) 서비스 사용자 hello 계정과 연결 된 됩니다.
- **FINGRP** hello 금융 기관에서에서 사용자가 포함 된 AAD에서 만든 사용자 그룹입니다.

Toocreate (서비스 사용자.dgml 파일) 하는 AAD 응용 프로그램을 확인 하는 방법에 대 한 지침은 [AAD 응용 프로그램을 만들려면](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application)합니다. Toocreate AAD의 사용자 그룹 확인 하려면 어떻게 해야에 대 한 지침은 [Azure Active Directory에서 그룹 관리](../active-directory/active-directory-accessmanagement-manage-groups.md)합니다.

몇 가지 주요 사항 tooconsider 합니다.

- hello 두 수준 폴더 구조 (**클러스터/finance / /**) 만들고 hello 데이터 레이크 저장소 관리자가 적절 한 권한이 있는 사용자를 프로 비전 해야 합니다 **전에** hello 저장소 계정을 사용 하 여 클러스터에 대 한 합니다. 이 구조는 클러스터를 만드는 동안 자동으로 생성되지 않습니다.
- 위의 hello 예제에서 권장 하는 그룹을 소유 하는 hello **/클러스터/finance** 으로 **FINGRP** 허용 **r-x** tooFINGRP toohello 하 던 전체 폴더 계층 구조에 액세스 hello 루트에서 시작 합니다. 이렇게 하면 FINGRP의 hello 멤버가 루트에서 시작 하는 hello 폴더 구조를 탐색할 수 있습니다.
- 다른 AAD 서비스 주체에서 클러스터를 만든 경우 hello **/클러스터/finance**, hello 스티커 비트 (hello에 설정 된 경우 **재무** 폴더) 하나의 서비스 폴더가 만들어졌는지 확인 보안 주체는 다른 hello 하 여 삭제할 수 없습니다.
- HDInsight 클러스터 만들기 프로세스에서 클러스터 전용 저장소 loaction 만듭니다 hello 폴더 구조와 사용 권한을 적용 되 면 **클러스터/finance / /**합니다. 예를 들어 이름 fincluster01 hello 사용 하 여 클러스터에 대 한 hello 저장 될 수 **/clusters/finance/fincluster01**합니다. hello 소유권 및 HDInsight 클러스터에서 만들어진 hello 폴더에 대 한 사용 권한 표에 나와 hello 여기 합니다.

    |폴더  |권한  |소유 사용자  |소유 그룹  | 명명된 사용자 | 명명된 사용자 권한 | 명명된 그룹 | 명명된 그룹 권한 |
    |---------|---------|---------|---------|---------|---------|---------|---------|
    |/클러스터/재무/fincluster01 | rwxr-x---  |서비스 주체 |FINGRP  |- |-  |-   |-  | 
   


## <a name="recommendations-for-job-input-and-output-data"></a>작업 입력 및 출력 데이터에 대한 권장 사항

에서는 데이터 tooa 작업 입력 및 출력 작업에서 hello 하는 권장 되는 외부 폴더에 저장 **클러스터/**합니다. 그러면는 hello 클러스터 특정 폴더는 삭제 된 tooreclaim 하는 경우에 일부 저장소 공간에서 hello 작업 입력 및 출력 나중에 계속 사용할 수 있습니다. 이러한 경우 hello 작업 입력 및 출력을 저장 하기 위한 hello 폴더 계층을 허용 하는지 hello에 대 한 액세스를 적절 한 수준의 서비스 사용자를 확인 합니다.

## <a name="limit-on-clusters-sharing-a-single-storage-account"></a>단일 저장소 계정을 공유하는 클러스터에 대한 제한

데이터 레이크 저장소 계정 하나를 공유할 수 있는 클러스터의 hello 수 제한을 15 hello 해당 클러스터에서 실행 되 고 hello 작업 부하에 따라 달라 집니다. 너무 많은 클러스터 또는 매우 많은 작업에 대 한 저장소 계정을 공유 하는 hello 클러스터 보유 hello 저장소 계정 송/수신 tooget 제한 될 수 있습니다.

## <a name="support-for-default-acls"></a>기본 ACL에 대한 지원

권장 (표와 같이 hello 위의) 명명 된 사용자 액세스 권한이 있는 서비스 사용자를 만들 때 **하지** 기본-ACL로 hello 명명 된 사용자를 추가 합니다. 사용자 소유, 소유 그룹 및 다른 사용자에 대 한 hello 770 사용 권한 할당의 기본 Acl 결과 사용 하 여 명명 된 사용자 액세스를 프로 비전 합니다. 770의 기본값은 소유 사용자(7) 또는 소유 그룹(7)에서 권한을 가져가지 않는 반면 다른 사용자(0)에 대한 모든 권한을 가져갑니다. 이 인해 한 특정 사용 사례 hello에 자세히 설명 하는 알려진된 문제로 [알려진 문제 및 대안](#known-issues-and-workarounds) 섹션.

## <a name="known-issues-and-workarounds"></a>알려진 문제 및 해결 방법

이 섹션에서는 hello 알려진 데이터 레이크 저장소 및 해결 방법을 HDInsight 사용을 위한 문제를 나열 합니다.

### <a name="publicly-visible-localized-yarn-resources"></a>공개적으로 표시되는 지역화된 YARN 리소스

새 Azure 데이터 레이크 저장소 계정이 만들어질 때 hello 루트 디렉터리 ACL 액세스 권한 비트 집합 too770와 자동으로 프로 비전 됩니다. hello 루트 폴더는 사용자가 만든 hello 계정 (데이터 레이크 저장소 admin 님 안녕하세요) toohello 사용자 설정 및 hello 소유 그룹 toohello hello 계정을 만든 hello 사용자의 주 그룹 설정 소유 합니다. "다른 사용자"에 대한 액세스는 제공되지 않습니다.

이러한 설정은 tooaffect 하나의 특정 HDInsight 사용 사례에서 캡처된 알려진 [YARN 247](https://hwxmonarch.atlassian.net/browse/YARN-247)합니다. 작업 제출을 오류 메시지와 비슷한 toothis와 함께 실패할 수 없습니다.

    Resource XXXX is not publicly accessible and as such cannot be part of hello public cache.

로컬라이저의 hello 모두 유효성을 검사 YARN JIRA 지역화 하는 동안 공용 리소스 hello 이전에 연결 하는 hello에 명시 된 대로 hello 원격 파일 시스템에 해당 사용 권한을 확인 하 여 요청 된 리소스는 실제로 공용입니다. 지역화를 위해 해당 조건에 맞지 않는 모든 LocalResource는 거부됩니다. 사용 권한에 대 한 검사 hello, "기타"에 대 한 읽기 액세스 toohello 파일을 포함 합니다. Azure 데이터 레이크 너무 모든 액세스를 거부 때문에 Azure 데이터 레이크 HDInsight 클러스터를 호스트 하는 경우이 시나리오의 기본 작동 하지 않습니다 "기타" 루트 폴더 수준입니다.

#### <a name="workaround"></a>해결 방법
에 대 한 권한을 설정 읽기-실행 **다른** hello 계층 구조를 통해에서 예를 들어  **/** , **클러스터/** 및   **/클러스터/재무**  위의 hello 표에 나와 있는 것 처럼 합니다.

## <a name="see-also"></a>참고 항목

* [Data Lake 저장소를 저장소로 사용하여 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)


