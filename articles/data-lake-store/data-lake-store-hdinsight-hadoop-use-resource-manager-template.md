---
title: "Azure 템플릿 toocreate aaaUse HDInsight 및 데이터 레이크 저장소 | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿 toocreate를 사용 하 고 HDInsight 클러스터를 사용 하 여 Azure 데이터 레이크 저장소"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a>Azure Resource Manager 템플릿을 사용하여 Data Lake Store로 HDInsight 클러스터 만들기
> [!div class="op_single_selector"]
> * [포털 사용](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [PowerShell 사용(기본 저장소의 경우)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [PowerShell 사용(추가 저장소의 경우)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Resource Manager 사용](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Azure 데이터 레이크 저장소와 toouse Azure PowerShell tooconfigure HDInsight 클러스터 되는 방법에 대해 알아봅니다 **추가 저장소로**합니다.

지원되는 클러스터 유형의 경우 Data Lake Store는 기본 저장소 또는 추가 저장소 계정으로 사용됩니다. 데이터 레이크 저장소는 추가 저장소로 사용 되는, hello 클러스터에 대 한 기본 저장소 계정 hello 계속 Azure 저장소 Blob (WASB) 이며 hello 클러스터 관련 파일 (예: 로그 등) 동안 hello 데이터 toohello 기본 저장소 계속 기록 했는지 원하는 tooprocess 데이터 레이크 저장소 계정에 저장할 수 있습니다. 데이터 레이크 저장소를 사용 하 여 추가 저장소 계정으로 영향을 주지 않습니다 성능이 나 hello 기능 tooread/쓰기 toohello hello 클러스터에서 저장소입니다.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>HDInsight 클러스터 저장소에서 Data Lake Store 사용

Data Lake Store에서 HDInsight를 사용하는 몇 가지 중요한 고려 사항은 다음과 같습니다.

* 옵션 toocreate HDInsight 클러스터에 액세스할 수 있는 기본 저장소로 tooData Lake 저장소는 HDInsight 버전 3.5 및 3.6 수 있습니다.

* 옵션 toocreate HDInsight 클러스터에 액세스할 수 있는 추가 저장소로 tooData Lake 저장소는 HDInsight 버전 3.2, 3.4, 3.5, 및 3.6 수 있습니다.

이 문서에서 데이터 레이크 저장소를 추가 저장소로 사용하여 Hadoop 클러스터를 프로비저닝합니다. 기본 저장소로 데이터 레이크 저장소와 toocreate Hadoop 클러스터 되는 방법에 지침은 [Azure 포털을 사용 하 여 데이터 레이크 저장소는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)합니다.

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure PowerShell 1.0 이상**. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
* **Azure Active Directory 서비스 사용자**. 이 자습서의 단계는 방법에 지침을 제공 toocreate Azure AD에서 서비스 사용자입니다. 그러나는 Azure AD 관리자 toobe 수 toocreate 서비스 사용자 여야 합니다. Azure AD 관리자 인 경우이 필수 구성이 요소를 건너뛰고 hello 자습서를 진행할 수 있습니다.

    **Azure AD 관리자가 아닌 경우**, 수 tooperform hello 단계 필요한 toocreate 서비스 사용자 됩니다. 이 경우 먼저 Azure AD 관리자가 서비스 사용자를 만들어야 Data Lake Store와 HDInsight 클러스터를 만들 수 있습니다. 또한 hello 서비스 사용자 사용 하 여 만들어야는 인증서에 설명 된 대로 [인증서로 서비스 사용자를 만들](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)합니다.

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a>Azure Data Lake Store로 HDInsight 클러스터 만들기
hello 리소스 관리자 템플릿 및 hello hello 템플릿을 사용 하 여 필수 구성 요소에는 GitHub에서 사용할 수 있는 [새 데이터 레이크 저장소를 사용 하 여 HDInsight Linux 클러스터 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage)합니다. 에 제공 된 링크 toocreate이 HDInsight 클러스터와 Azure 데이터 레이크 저장소로 저장소를 추가 하는 hello hello 지침을 따릅니다.

위에서 언급 한 hello 링크에서 지침 hello PowerShell이 필요 합니다. 이러한 지침을 시작 하기 전에 tooyour Azure 계정에에서 로그인 해야 합니다. 바탕 화면에서 새 Azure PowerShell 창을 열고 hello 조각 다음을 입력 합니다. , 입력 정보 요청된 toolog 있는지 확인 하는 경우 로그인 할 hello 구독 admininistrators/소유자 중 하나로:

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a>샘플 데이터 toohello Azure Data Lake 저장소에 업로드
hello 리소스 관리자 템플릿을 새 데이터 레이크 저장소 계정을 만들고 hello HDInsight 클러스터에 연결 합니다. 지금 일부 샘플 데이터 toohello Data Lake 저장소를 업로드 해야 합니다. Hello 데이터 레이크 저장소의에서 데이터를 액세스 하는 HDInsight 클러스터에서 hello 자습서 toorun 작업에서 나중에이 데이터를 필요 합니다. 방법에 대 한 지침은 tooupload 데이터 참조 [파일 tooyour 데이터 레이크 저장소 업로드](data-lake-store-get-started-portal.md#uploaddata)합니다. 몇 가지 샘플 데이터 tooupload를 찾고 hello를 얻을 수 있습니다 **Ambulance 데이터** hello 폴더 [Azure 데이터 레이크 Git 리포지토리](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData)합니다.

## <a name="set-relevant-acls-on-hello-sample-data"></a>Hello 예제 데이터에서 관련 Acl 설정
toomake hello 샘플 데이터 업로드 hello HDInsight 클러스터에서 액세스할 수 있는지를 확인 해야 hello HDInsight 클러스터와 데이터 레이크 저장소 간에 사용 되는 tooestablish id가 있는 hello Azure AD 응용 프로그램에는 액세스 toohello 파일/폴더는 tooaccess를 하려고합니다. toodo이 hello 다음 단계를 수행 합니다.

1. Hello HDInsight 클러스터와 연결 된 Azure AD 응용 프로그램 및 hello 데이터 레이크 저장소의 hello 이름을 찾습니다. Hello 이름에 대 한 한 가지 방법은 toolook tooopen hello HDInsight 클러스터 블레이드 hello 리소스 관리자 템플릿을 사용 하 여 만든 이면 hello 클릭 **클러스터 AAD Id** 탭을 hello 값 찾기 위해 **서비스 사용자 표시 이름**합니다.
2. 이제 hello 파일/폴더 tooaccess hello HDInsight 클러스터에서 원하는 액세스 toothis Azure AD 응용 프로그램을 제공 합니다. 데이터 레이크 저장소의 파일/폴더 hello tooset hello 오른쪽 Acl 참조 [데이터 레이크 저장소의 데이터를 보호 하려면](data-lake-store-secure-data.md#filepermissions)합니다.

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Hello HDInsight 클러스터 toouse hello 데이터 레이크 저장소에서 테스트 작업 실행
HDInsight 클러스터를 구성 하 고 나면에서 실행할 수 있습니다 테스트 작업이 hello 클러스터 tootest 해당 hello HDInsight 클러스터 Data Lake 저장소에 액세스할 수 있습니다. toodo, 이전 tooyour 데이터 레이크 저장소를 업로드 하는 hello 샘플 데이터를 사용 하 여 테이블을 만드는 예제 Hive 작업을 수행 됩니다.

이 섹션에서는 SSH HDInsight Linux 클러스터와 실행된 hello에 샘플 Hive 쿼리 합니다. Windows 클라이언트를 사용 중인 경우 **PuTTY**를 사용하는 것이 좋습니다([http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)에서 다운로드할 수 있음).

PuTTY 사용에 대한 자세한 내용은 [Windows에서 HDInsight의 Linux 기반 Hadoop과 SSH 사용 ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)을 참조하세요.

1. 연결 되 면 다음 명령을 hello를 사용 하 여 hello 하이브 CLI를 시작 합니다.

   ```
   hive
   ```
2. Hello CLI를 사용 하 여 hello 문을 toocreate 라는 새 테이블을 다음 입력 **차량** hello 데이터 레이크 저장소의에서 hello 예제 데이터를 사용 하 여:

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   출력 유사한 toohello 다음을 나타나야 합니다.

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a>HDFS 명령을 사용한 액세스 데이터 레이크 저장소
Hello HDInsight 클러스터 toouse Data Lake 저장소를 구성한 후에 hello HDFS 셸 명령을 tooaccess hello 저장소를 사용할 수 있습니다.

이 섹션에서는 SSH HDInsight Linux 클러스터 및 실행된 hello HDFS 명령입니다. Windows 클라이언트를 사용 중인 경우 **PuTTY**를 사용하는 것이 좋습니다([http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)에서 다운로드할 수 있음).

PuTTY 사용에 대한 자세한 내용은 [Windows에서 HDInsight의 Linux 기반 Hadoop과 SSH 사용 ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)을 참조하세요.

연결 되 면 hello Data Lake 저장소에 있는 HDFS 파일 시스템 명령 toolist hello 파일을 다음 hello를 사용 합니다.

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

이전 toohello 데이터 레이크 저장소를 업로드 하는 hello 파일을 나열 됩니다.

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

Hello를 사용할 수도 있습니다 `hdfs dfs -put` 일부 파일 toohello 데이터 레이크 저장소 tooupload 명령을 클릭 한 다음 사용 하 여 `hdfs dfs -ls` tooverify hello 파일이 성공적으로 업로드 된 여부.


## <a name="next-steps"></a>다음 단계
* [Azure 저장소 Blob tooData Lake 저장소에서 데이터 복사](data-lake-store-copy-data-wasb-distcp.md)
