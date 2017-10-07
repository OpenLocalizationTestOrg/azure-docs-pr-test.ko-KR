---
title: "데이터 레이크 저장소와 aaaUse hello Azure 포털 toocreate Azure HDInsight 클러스터 | Microsoft Docs"
description: "Azure 포털 toocreate hello를 사용 하 고 HDInsight 클러스터를 사용 하 여 Azure 데이터 레이크 저장소"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: a8c45a83-a8e3-4227-8b02-1bc1e1de6767
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: nitinme
ms.openlocfilehash: f23113d444a3c5a01894dba29f75f3621b2d16bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-hello-azure-portal"></a>데이터 레이크 저장소와 hello Azure 포털을 사용 하 여 HDInsight 클러스터를 만들려면
> [!div class="op_single_selector"]
> * [Hello Azure 포털을 사용 하 여](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [PowerShell 사용(기본 저장소의 경우)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [PowerShell 사용(추가 저장소의 경우)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Resource Manager 사용](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

어떻게 toouse hello Azure 포털 toocreate Azure 데이터 레이크 저장소 계정 사용 하 여 HDInsight 클러스터로 추가 저장소 또는 hello 기본 저장소에 알아봅니다. 추가 저장소는 HDInsight 클러스터에 대 한 선택적으로 있지만 toostore hello 추가 저장소 계정에서 비즈니스 데이터를 권장 합니다.

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 hello 요구 사항을 준수를 충족 확인 합니다.

* **Azure 구독**. 너무 이동[가져오기 Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다.
* **Azure 데이터 레이크 저장소 계정**. Hello 지침을 따릅니다 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다. Hello 계정에도 루트 폴더를 만들어야 합니다.  이 자습서에서는 __/clusters__라는 루트 폴더가 사용됩니다.
* **Azure Active Directory 서비스 주체** 이 자습서는 방법에 대해 설명 toocreate Azure Active Directory (Azure AD)에 서비스 사용자입니다. 그러나 toocreate 서비스 사용자 여야 Azure AD 관리자입니다. 관리자 인 경우이 필수 구성이 요소를 건너뛰고 hello 자습서를 진행할 수 있습니다.

    >[!NOTE]
    >Azure AD 관리자인 경우에만 서비스 주체를 만들 수 있습니다. Azure AD 관리자가 서비스 주체를 만들어야 Data Lake Store와 HDInsight 클러스터를 만들 수 있습니다. 또한 hello 서비스 사용자에서 만들어야 합니다는 인증서에 설명 된 대로 [인증서로 서비스 사용자를 만들](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate)합니다.
    >

## <a name="create-an-hdinsight-cluster"></a>HDInsight 클러스터 만들기

이 섹션에서는 hello 기본 문화권 이나 hello 추가 저장으로 데이터 레이크 저장소 계정에 HDInsight 클러스터를 만듭니다. 이 문서는 데이터 레이크 저장소 계정을 구성 하는 hello 과정만 집중 합니다.  Hello 일반 클러스터 생성 정보 및 절차에 대 한 참조 [HDInsight 클러스터를 만드는 Hadoop](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)합니다.

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a>Data Lake Store를 기본 저장소로 사용하여 클러스터 만들기

**hello 기본 저장소 계정으로 데이터 레이크 저장소와 toocreate는 HDInsight 클러스터**

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 에 따라 [클러스터를 만들어](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) hello 일반 정보는 HDInsight 클러스터를 만드는 방법에 대 한 합니다.
3. Hello에 **저장소** 블레이드 아래에서 **기본 저장소 형식**을 선택 **데이터 레이크 저장소**, hello 다음 정보를 입력 합니다.

    ![추가 서비스 보안 주체 tooHDInsight 클러스터](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "추가 서비스 보안 주체 tooHDInsight 클러스터")

    - **Data Lake Store 계정 선택**: 기존 Data Lake Store 계정을 선택합니다. 기존 Data Lake Store 계정은 필수입니다.  [필수 조건](#prereuisites)을 참조하세요.
    - **루트 경로**: toobe 저장는 hello 클러스터 전용 파일의 위치 경로 입력 합니다. hello 스크린 샷 __클러스터/myhdiadlcluster / /__, 어떤 hello에 __클러스터/__ 폴더 존재 해야 하며 hello 포털에서는 *myhdicluster* 폴더입니다.  hello *myhdicluster* hello 클러스터 이름입니다.
    - **데이터 레이크 저장소 액세스**: hello Data Lake 저장소 계정 및 HDInsight 클러스터 간의 액세스를 구성 합니다. 지침은 [Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.
    - **추가 저장소 계정을**: hello 클러스터에 대 한 계정 추가 저장소로 Azure 저장소 계정을 추가 합니다. 데이터 레이크 저장소를 추가 하는 tooadd hello 기본 저장소 형식으로 데이터 레이크 저장소 계정을 구성 하는 동안 더 많은 데이터 레이크 저장소 계정에 데이터에 hello 클러스터 사용 권한을 제공 하 여 수행 됩니다. [Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.

4. Hello에 **데이터 레이크 저장소 액세스**, 클릭 **선택**, 다음에 설명 된 대로 클러스터 만들기를 계속 [HDInsight 클러스터를 만드는 Hadoop](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md)합니다.


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a>Data Lake Store를 추가 저장소로 사용하여 클러스터 만들기

hello 다음 지침 HDInsight 클러스터 만들기 hello 기본 저장소로 Azure 저장소 계정과 추가 저장소로 데이터 레이크 저장소 계정을 사용 하 여
**hello 기본 저장소 계정으로 데이터 레이크 저장소와 toocreate는 HDInsight 클러스터**

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 에 따라 [클러스터를 만들어](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) hello 일반 정보는 HDInsight 클러스터를 만드는 방법에 대 한 합니다.
3. Hello에 **저장소** 블레이드 아래에서 **기본 저장소 형식**을 선택 **Azure 저장소**, hello 다음 정보를 입력 합니다.

    ![추가 서비스 보안 주체 tooHDInsight 클러스터](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "추가 서비스 보안 주체 tooHDInsight 클러스터")

    - **선택 방법을**: hello 다음 옵션 중 하나를 사용 합니다.

        * toospecify Azure 구독에 포함 된 저장소 계정을 선택 **내 구독**를 선택한 다음 hello 저장소 계정을 선택 합니다.
        * toospecify Azure 구독 외부에 있는 저장소 계정 **선택 키**, 외부 저장소 계정 hello에 대 한 hello 정보를 제공 합니다.

    - **기본 컨테이너**: hello 기본값 중 하나를 사용 하거나 고유한 이름을 지정 합니다.

    - 추가 저장소 계정: hello 추가 저장소로 Azure 저장소 계정을 더 추가 합니다.
    - 데이터 레이크 저장소 액세스: hello Data Lake 저장소 계정 및 HDInsight 클러스터 간의 액세스를 구성 합니다. 지침은 [Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.

## <a name="configure-data-lake-store-access"></a>Data Lake Store 액세스 구성 

이 섹션에서는 Azure Active Directory 서비스 주체를 사용하여 HDInsight 클러스터에서 Data Lake Store 액세스를 구성합니다. 

### <a name="specify-a-service-principal"></a>서비스 주체 지정

Hello Azure 포털에서에서 기존 서비스 보안 주체를 사용 하거나 새로 만들 수 있습니다.

**toocreate hello Azure 포털에서에서 서비스 사용자**

1. 클릭 **데이터 레이크 저장소 액세스** hello 저장소 블레이드에서 합니다.
2. Hello에 **데이터 레이크 저장소 액세스** 블레이드에서 클릭 **새로 만들기**합니다.
3. 클릭 **서비스 사용자**를 선택한 다음 hello 지침 toocreate 서비스 사용자를 따릅니다.
4. Toouse 결정 한 경우 hello 인증서를 다운로드 hello 나중에 다시 합니다. 다운로드 hello 인증서 추가 하는 HDInsight 클러스터를 만들 때 보안 주체를 서비스 동일 toouse hello 하려는 경우 유용 합니다.

    ![추가 서비스 보안 주체 tooHDInsight 클러스터](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "추가 서비스 보안 주체 tooHDInsight 클러스터")

4. 클릭 **액세스** tooconfigure hello 폴더에 액세스 합니다.  [파일 권한 구성](#configure-file-permissions)을 참조하세요.


**기존 서비스 hello Azure 포털에서에서 사용자 toouse**

1. **Data Lake Store 액세스**를 클릭합니다.
1. Hello에 **데이터 레이크 저장소 액세스** 블레이드에서 클릭 **기존 항목 사용**합니다.
2. **서비스 주체**를 클릭한 다음 서비스 주체를 선택합니다. 
3. 사용자 선택 된 서비스 사용자와 연결 된 hello 인증서 (.pfx 파일)를 업로드 하 고 hello 인증서 암호를 입력 합니다.

    ![추가 서비스 보안 주체 tooHDInsight 클러스터](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "추가 서비스 보안 주체 tooHDInsight 클러스터")

4. 클릭 **액세스** tooconfigure hello 폴더에 액세스 합니다.  [파일 권한 구성](#configure-file-permissions)을 참조하세요.


### <a name="configure-file-permissions"></a>파일 권한 구성

hello 구성 hello 기본 저장소 또는 추가 저장소 계정으로 hello 계정 사용 여부에 따라 달라 집니다.

- 기본 저장소로 사용됨

    - 데이터 레이크 저장소 계정 hello의 hello 루트 수준에서 사용 권한
    - hello HDInsight 클러스터 저장소의 hello 루트 수준에서 권한입니다. 예를 들어 hello __클러스터/__ hello 자습서의 앞부분에서 사용 되는 폴더입니다.
- 추가 저장소로 사용

    - 액세스를 제출 해야 하는 hello 폴더에 대 한 권한입니다.

**hello Data Lake 저장소 계정 루트 수준에서 tooassign 권한**

1. Hello에 **데이터 레이크 저장소 액세스** 블레이드에서 클릭 **액세스**합니다. hello **파일 사용 권한을 선택** 블레이드가 열립니다. 구독에서 모든 hello 데이터 레이크 저장소 계정을 나열합니다.
2. 마우스를 가져가고 (클릭 하지 마십시오) hello hello Data Lake 저장소 계정 선택 확인란 hello 다음 toomake hello 표시 확인란의 hello 이름 위로 마우스를 가져갑니다.

    ![추가 서비스 보안 주체 tooHDInsight 클러스터](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "추가 서비스 보안 주체 tooHDInsight 클러스터")

  기본적으로 __읽기__, __쓰기__ 및 __실행__이 모두 선택되어 있습니다.

3. 클릭 **선택** hello hello 페이지 아래쪽에 있습니다.
4. 클릭 **실행** tooassign 권한.
5. **Done**을 클릭합니다.

**hello HDInsight 클러스터 루트 수준에서 tooassign 권한**

1. Hello에 **데이터 레이크 저장소 액세스** 블레이드에서 클릭 **액세스**합니다. hello **파일 사용 권한을 선택** 블레이드가 열립니다. 구독에서 모든 hello 데이터 레이크 저장소 계정을 나열합니다.
1. Hello에서 **파일 사용 권한을 선택** 블레이드에서 hello 데이터 레이크 저장소 이름 tooshow 해당 콘텐츠를 클릭 합니다.
2. Hello hello 왼쪽 hello 폴더의 확인란을 선택 하 여 hello HDInsight 클러스터 저장소 루트를 선택 합니다. Hello 클러스터 저장소 루트는 toohello 스크린 샷을 이전 버전에 따라, __클러스터/__ 기본 저장소로 hello 데이터 레이크 저장소를 선택 하는 동안 지정한 폴더입니다.
3. Hello 폴더에 hello 사용 권한을 설정 합니다.  기본적으로 읽기, 쓰기 및 실행이 모두 선택되어 있습니다.
4. 클릭 **선택** hello hello 페이지 아래쪽에 있습니다.
5. **실행**을 클릭합니다.
6. **Done**을 클릭합니다.

데이터 레이크 저장소로 추가 저장소를 사용 하는 경우 할당 해야 hello 폴더에 대 한 권한을 hello HDInsight 클러스터에서 tooaccess 되도록 합니다. 예를 들어 아래 hello 스크린샷에서에서 제공한 액세스 너무만**hdiaddonstorage** 데이터 레이크 저장소 계정에는 폴더입니다.

![서비스 보안 주체 권한 toohello HDInsight 클러스터 할당](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "할당 서비스 보안 주체 권한 toohello HDInsight 클러스터")


## <a name="verify-cluster-set-up"></a>클러스터 설정 확인

Hello 클러스터 설치가 완료 되 면 hello 클러스터 블레이드에서 결과 확인 단계를 수행 하는 hello 중 하나 또는 모두를 수행 하 여:

* hello 클러스터는 지정한 hello 데이터 레이크 저장소 계정에 대 한 연결 된 저장소를 hello를 클릭 tooverify **저장소 계정은** hello 왼쪽된 창에서.

    ![추가 서비스 보안 주체 tooHDInsight 클러스터](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "추가 서비스 보안 주체 tooHDInsight 클러스터")

* 서비스 사용자 hello tooverify 올바르게 hello HDInsight 클러스터와 연결 된, 클릭 **데이터 레이크 저장소 액세스** hello 왼쪽된 창에서.

    ![추가 서비스 보안 주체 tooHDInsight 클러스터](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "추가 서비스 보안 주체 tooHDInsight 클러스터")


## <a name="examples"></a>예

데이터 레이크 저장소를 사용 하는 hello 클러스터에서 저장소로 설정한 후에 어떻게 toouse HDInsight 클러스터 데이터 레이크 저장소에 저장 된 tooanalyze hello 데이터의 toothese 예 참조 하십시오.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a>기본 저장소인 Data Lake Store에서 데이터에 대한 Hive 쿼리 실행

toorun 하이브 쿼리 hello Ambari 포털에서 hello 하이브 뷰 인터페이스를 사용 합니다. Ambari 하이브 toouse 보는 방법에 지침은 [사용 하 여 hello HDInsight에서 Hadoop으로 하이브 보기](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md)합니다.

데이터 레이크 저장소의 데이터로 작업할 때 문자열 toochange 몇 가지가 있습니다.

Hello 경로 toohello 데이터를 사용 하는 경우, 예를 들어 주 저장소로 데이터 레이크 저장소를 사용 하 여 만든 hello 클러스터: *adl: / / < data_lake_store_account_name > /azuredatalakestore.net/path/to/file*합니다. 하이브 쿼리 toocreate hello Data Lake 저장소 계정에에서 저장 되어 있는 샘플 데이터에서 테이블 문 다음 hello 같습니다.

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

설명:
* `adl://hdiadlstorage.azuredatalakestore.net/`데이터 레이크 저장소 계정 hello hello 루트가입니다.
* `/clusters/myhdiadlcluster`hello 클러스터를 만드는 동안 지정한 hello 클러스터 데이터의 hello 루트가입니다.
* `/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/`hello hello 쿼리에서 사용 하는 hello 샘플 파일 위치가입니다.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a>추가 저장소인 Data Lake Store에 저장된 데이터에 대한 Hive 쿼리 실행

Blob 저장소를 사용 하 여 기본 저장소로 만든 hello 클러스터, 샘플 데이터 hello hello 추가 저장소로 사용 되는 Azure 데이터 레이크 저장소 계정에에서 포함 되지 않습니다. 이 경우 먼저 Blob 저장소 toohello 데이터 레이크 저장소에서에서 hello 데이터를 전송 하 고 hello 이전 예제와 같이 hello 쿼리를 실행 하십시오.

어떻게 toocopy 데이터 Blob 저장소에서 tooa 데이터 레이크 저장소에 대 한 내용은 다음 문서는 hello 참조:

* [Azure 저장소 blob와 데이터 레이크 저장소 간에 Distcp toocopy 데이터 사용](data-lake-store-copy-data-wasb-distcp.md)
* [Azure 저장소에서 사용 하 여 AdlCopy toocopy 데이터 레이크 저장소 tooData blob](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a>Spark 클러스터에서 Data Lake Store 사용
데이터 레이크 저장소에 저장 된 데이터에서 Spark 클러스터 toorun Spark 작업을 사용할 수 있습니다. 자세한 내용은 참조 [데이터 레이크 저장소에서 사용 하 여 HDInsight Spark 클러스터 tooanalyze 데이터](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md)합니다.


### <a name="use-data-lake-store-in-a-storm-topology"></a>Storm 토폴로지에서 Data Lake 저장소 사용
Storm 토폴로지에서 hello 데이터 레이크 저장소 toowrite 데이터를 사용할 수 있습니다. 방법에 대 한 지침은 tooachieve이이 시나리오에서는 참조 [HDInsight와 Apache Storm를 사용 하 여 Azure 데이터 레이크 저장소](../hdinsight/hdinsight-storm-write-data-lake-store.md)합니다.

## <a name="see-also"></a>참고 항목
* [PowerShell: 만들 HDInsight 클러스터 toouse 데이터 레이크 저장소](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
