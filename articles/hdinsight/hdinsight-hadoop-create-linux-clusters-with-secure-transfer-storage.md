---
title: "Azure HDInsight의 보안 전송 저장소 계정을 가진 aaaCreate Hadoop 클러스터 | Microsoft Docs"
description: "안전 하 게 전송 된 toocreate HDInsight 클러스터를 Azure 저장소 계정을 사용 하는 방법을 알아봅니다."
keywords: "hadoop 시작,hadoop linux,hadoop 빠른 시작,보안 전송,azure 저장소 계정"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a>Azure HDInsight에서 보안 전송 저장소 계정으로 Hadoop 클러스터 만들기

hello [보안 전송 필요](../storage/common/storage-require-secure-transfer.md) 기능은 보안 연결을 통해 모든 요청 tooyour 계정을 적용 하 여 Azure 저장소 계정의 hello 보안을 향상 시킵니다. 이 기능 및 hello wasbs 체계 HDInsight 클러스터 버전이 3.6 이상 버전 에서만 지원 됩니다. 

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작하기 전에 다음이 있어야 합니다.

* **Azure 구독**: toocreate 무료 1 개월 평가판 계정을 너무 찾아보기[azure.microsoft.com/free](https://azure.microsoft.com/free)합니다.
* **보안 전송이 활성화된 Azure Storage 계정**. Hello 지침은 [저장소 계정을 만드는](../storage/common/storage-create-storage-account.md#create-a-storage-account) 및 [보안 전송 필요](../storage/common/storage-require-secure-transfer.md)합니다.
* **Hello 저장소 계정에서 Blob 컨테이너**합니다. 
## <a name="create-cluster"></a>클러스터 만들기

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


이 섹션에서는 [Azure Resource Manager 템플릿](../azure-resource-manager/resource-group-template-deploy.md)을 사용하여 HDInsight에서 Hadoop 클러스터를 만듭니다. hello 서식 파일에 있는 [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/)합니다. 이 자습서를 따라 하는 데 Resource Manager 템플릿 환경이 필요하지는 않습니다. 다른 클러스터 생성 방법 및이 자습서에 사용 되는 hello 속성을 이해, 참조 [만들 HDInsight 클러스터](hdinsight-hadoop-provision-linux-clusters.md)합니다.

1. Hello tooAzure에 이미지 toosign와 hello Azure 포털에서에서 열기 hello 리소스 관리자 템플릿을 다음를 클릭 합니다. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. 사양을 따르는 hello로 hello 지침 toocreate hello 클러스터를 수행 합니다. 

    - HDInsight 버전 3.6을 지정합니다.  hello 기본 버전은 3.5입니다. 3.6 이상 버전이 필요합니다.
    - 보안 전송이 활성화된 저장소 계정을 지정합니다.
    - Hello 저장소 계정에 대 한 짧은 이름을 사용 합니다.
    - Hello 저장소 계정과 blob 컨테이너 hello 모두 미리 생성 되어야 합니다. 

    Hello 지침은 [클러스터 만들기](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)합니다. 

스크립트 동작 tooprovide 사용자 고유의 구성 파일을 사용 하는 경우 hello 설정을 다음에 wasbs를 사용 해야 합니다.

- fs.defaultFS(코어 사이트)
- spark.eventLog.dir 
- spark.history.fs.logDirectory

## <a name="add-additional-storage-accounts"></a>추가 저장소 계정 추가

몇 가지 옵션 tooadd 사용 하도록 설정 하는 추가 보안 전송 저장소 계정이 있습니다.

- Hello 마지막 섹션에서 hello Azure 리소스 관리자 템플릿을 수정 합니다.
- Hello를 사용 하 여 클러스터 만들기 [Azure 포털](https://portal.azure.com) 연결 된 저장소 계정을 지정 합니다.
- 사용 하 여 스크립트 작업 tooadd 추가 보안 전송 저장소 계정을 tooan 기존 HDInsight 클러스터를 사용할 수 있습니다.  자세한 내용은 참조 [추가 저장소 계정을 tooHDInsight 추가](hdinsight-hadoop-add-storage.md)합니다.

## <a name="next-steps"></a>다음 단계
이 자습서에서는 toocreate는 HDInsight 클러스터를 사용 하도록 설정한 보안 전송 toohello 저장소 계정에 방법을 배웠습니다.

HDInsight 사용 하 여 데이터 분석에 대 한 더 toolearn hello 다음 문서를 참조 하십시오.

* Visual Studio에서 tooperform 하이브 쿼리 하는 방법을 포함 하 여 HDInsight Hive 사용에 대 한 더 toolearn 참조 [HDInsight를 사용 하 여 하이브][hdinsight-use-hive]합니다.
* Pig에 대 한 toolearn, 언어를 사용 하는 tootransform 데이터, 참조 [HDInsight와 Pig][hdinsight-use-pig]합니다.
* toolearn MapReduce, Hadoop에서 데이터를 처리 하는 방식으로 toowrite 프로그램에 대 한 참조 [HDInsight 사용 하 여 MapReduce][hdinsight-use-mapreduce]합니다.
* Visual Studio tooanalyze 데이터 HDInsight에 대 한 hello HDInsight 도구를 사용 하는 방법에 대 한 toolearn 참조 [HDInsight에 대 한 Visual Studio Hadoop 도구 사용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.

HDInsight에서 데이터를 저장 하는 방법에 대 한 자세한 toolearn tooget 데이터 HDInsight hello 다음 문서를 참조 하는 방법 또는:

* HDInsight에서 Azure Storage를 사용하는 방법에 대한 자세한 내용은 [HDInsight에서 Azure Storage 사용](hdinsight-hadoop-use-blob-storage.md)을 참조하세요.
* 방법에 대 한 내용은 tooupload 데이터 tooHDInsight 참조 [데이터 tooHDInsight 업로드][hdinsight-upload-data]합니다.

toolearn 만들거나는 HDInsight 클러스터 관리에 대 한 참조 문서 다음 hello:

* Linux 기반 HDInsight 클러스터를 관리 하는 방법에 대 한 toolearn 참조 [Ambari를 사용 하 여 관리 하는 HDInsight 클러스터](hdinsight-hadoop-manage-ambari.md)합니다.
* HDInsight 클러스터를 만들 때 선택할 수는 hello 옵션에 대해 자세히 toolearn 참조 [사용자 지정 옵션을 사용 하 여 Linux에서 HDInsight를 만드는](hdinsight-hadoop-provision-linux-clusters.md)합니다.
* Linux, Hadoop와 잘 알고 있는 해도 hello HDInsight에서 Hadoop에 대 한 tooknow 고유 정보를 사용할 경우 참조 [Linux에서 HDInsight 작업](hdinsight-hadoop-linux-information.md)합니다. 이 문서에서 제공하는 정보는 다음과 같습니다.
  
  * Ambari 등 WebHCat hello 클러스터에서 호스팅되는 서비스에 대 한 Url
  * Hadoop 파일 및 hello 로컬 파일 시스템에 예제의 hello 위치
  * hello 기본 데이터 저장소로의 Azure 저장소 (WASB) HDFS 대신 hello 사용

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


