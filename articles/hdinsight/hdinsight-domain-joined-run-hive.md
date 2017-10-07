---
title: "도메인에 가입 된 HDInsight-Azure에서에서 aaaConfigure 하이브 정책 | Microsoft Docs"
description: "유용한 정보"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a>도메인에 가입된 HDInsight에서 Hive 정책 구성(미리 보기)
자세한 방법을 하이브에 대 한 tooconfigure Apache 레인저 정책입니다. 이 문서에서는 두 개의 레인저 정책 toorestrict 액세스 toohello hivesampletable를 만듭니다. hello hivesampletable HDInsight 클러스터에 포함 되어 있습니다. Hello 정책을 구성한 경우 HDInsight에서 Excel 및 ODBC 드라이버 tooconnect tooHive 테이블을 사용 합니다.

## <a name="prerequisites"></a>필수 조건
* 도메인에 가입된 HDInsight 클러스터 [도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md)을 참조하세요.
* Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone 또는 Office 2010 Professional Plus를 포함한 워크스테이션

## <a name="connect-tooapache-ranger-admin-ui"></a>TooApache 레인저 관리 UI를 연결 합니다.
**tooconnect tooRanger 관리 UI**

1. 브라우저에서 tooRanger 관리 UI를 연결 합니다. hello URL은 https://&lt;ClusterName >.azurehdinsight.net/Ranger/ 합니다.

   > [!NOTE]
   > Ranger는 다른 Hadoop 클러스터가 아닌 자격 증명을 사용합니다. tooprevent 브라우저 캐시의 Hadoop 자격 증명을 사용 하 여 새 inprivate 브라우저 창 tooconnect toohello 레인저 관리 UI를 사용 합니다.
   >
   >
2. Hello 클러스터 관리자가 도메인 사용자 이름 및 암호를 사용 하 여 로그인:

    ![HDInsight 도메인에 가입된 Ranger 홈페이지](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    Ranger는 현재 Yarn 및 Hive에서만 작동합니다.

## <a name="create-domain-users"></a>도메인 사용자 만들기
[도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad)에서 hiveruser1 및 hiveuser2를 만들었습니다. 이 자습서에서는 두 개의 사용자 계정을 hello를 사용 합니다.

## <a name="create-ranger-policies"></a>Ranger 정책 만들기
이 섹션에서는 hivesampletable에 액세스하기 위한 두 개의 Ranger 정책을 만듭니다. 다른 열 집합에 대한 선택 사용 권한을 제공합니다. 두 사용자는 모두 [도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad)에서 만들어집니다.  Hello 다음 섹션에서는 Excel에서 hello 두 정책을 테스트 합니다.

**toocreate 레인저 정책**

1. Ranger 관리 UI를 엽니다. 참조 [tooApache 레인저 관리 UI를 연결](#connect-to-apache-ranager-admin-ui)합니다.
2. **Hive**에서 **&lt;ClusterName>_hive**를 클릭합니다. 두 개의 미리 구성 정책이 표시되어야 합니다.
3. 클릭 **새 정책 추가**, hello 다음 값을 입력 합니다.

   * 정책 이름: read-hivesampletable-all
   * Hive 데이터베이스: 기본값
   * 테이블: hivesampletable
   * Hive 열: *
   * 사용자 선택: hiveuser1
   * 사용 권한: 선택

     ![HDInsight 도메인에 가입된 Ranger Hive 정책 구성](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)에서도 확인할 수 있습니다.

     > [!NOTE]
     > 도메인 사용자가 사용자 선택에 채워지지 않았습니다를 AAD에 레인저 toosync 잠시 기다립니다.
     >
     >
4. 클릭 **추가** toosave hello 정책입니다.
5. 다음과 같은 속성 hello로 hello 마지막 두 단계 toocreate 다른 정책을 반복 합니다.

   * 정책 이름: read-hivesampletable-devicemake
   * Hive 데이터베이스: 기본값
   * 테이블: hivesampletable
   * Hive 열: clientid, devicemake
   * 사용자 선택: hiveuser2
   * 사용 권한: 선택

## <a name="create-hive-odbc-data-source"></a>Hive ODBC 데이터 원본 만들기
hello 지침은에서 [만들기 하이브 ODBC 데이터 원본](hdinsight-connect-excel-hive-odbc-driver.md)합니다.  

    속성|설명
    ---|---
    데이터 원본 이름|이름 tooyour 데이터 소스를 제공 합니다.
    호스트|&lt;HDInsightClusterName>.azurehdinsight.net을 입력합니다. 예를 들면 myHDICluster.azurehdinsight.net과 같습니다.
    포트|<strong>443</strong>을 사용합니다. (이 포트를 변경 하지 563 too443에서.)
    데이터베이스|<strong>기본값</strong>을 사용합니다.
    Hive 서버 유형|<strong>Hive 서버 2</strong> 선택
    메커니즘|<strong>Azure HDInsight Service</strong> 선택
    HTTP 경로|비워 둠
    사용자 이름|hiveuser1@contoso158.onmicrosoft.com을 입력합니다. 다른 경우 hello 도메인 이름을 업데이트 합니다.
    암호|Hiveuser1 hello 암호를 입력 합니다.
    </table>

있는지 tooclick 확인 **테스트** hello 데이터 소스를 저장 하기 전에.

## <a name="import-data-into-excel-from-hdinsight"></a>HDInsight에서 Excel로 데이터 가져오기
Hello 마지막 섹션에서 두 개의 정책을 구성 해야 합니다.  hiveuser1 모든 hello 열에 대 한 select 권한 hello 많고 hiveuser2 hello 두 개의 열에 대 한 select 권한입니다. 이 섹션에서는 Excel로 hello 두 명의 사용자가 tooimport 데이터를 가장 합니다.

1. Excel에서 새 통합 문서나 기존 통합 문서를 엽니다.
2. Hello에서 **데이터** 탭을 클릭 **기타 데이터 원본**, 클릭 하 고 **데이터 연결 마법사** toolaunch hello **데이터연결마법사**.

    ![데이터 연결 마법사 열기][img-hdi-simbahiveodbc.excel.dataconnection]
3. 선택 **ODBC DSN** hello 데이터 원본과 클릭으로 **다음**합니다.
4. ODBC 데이터 원본의 선택 hello 데이터 원본 이름 hello 이전 단계에서 만든 및 클릭 **다음**합니다.
5. Hello 마법사에서 hello 클러스터에 대 한 hello 암호를 다시 입력 하 고 클릭 **확인**합니다. Hello에 대 한 대기 **데이터베이스 및 테이블 선택** 대화 tooopen 합니다. 몇 초 정도 걸릴 수 있습니다.
6. **hivesampletable**을 선택하고 **다음**을 클릭합니다.
7. **마침**을 클릭합니다.
8. Hello에 **데이터 가져오기** 대화 상자에서 변경 하거나 hello 쿼리를 지정할 수 있습니다. toodo 이므로, 클릭 **속성**합니다. 몇 초 정도 걸릴 수 있습니다.
9. Hello 클릭 **정의** hello 명령 텍스트가 탭:

       SELECT * FROM "HIVE"."default"."hivesampletable"

   Hiveuser1는 hello 레인저 정책 정의 의해 모든 hello 열에 대해 select 권한을 가집니다.  따라서 이 쿼리를 hiveuser1의 자격 증명에서 사용할 수 있지만 hiveuser2의 자격 증명과 함께 사용할 수 없습니다.

   ![연결 속성][img-hdi-simbahiveodbc-excel-connectionproperties]
10. 클릭 **확인** tooclose hello에 대 한 연결 속성 대화 상자.
11. 클릭 **확인** tooclose hello **데이터 가져오기** 대화 상자.  
12. Hiveuser1에 대 한 hello 암호를 다시 입력 하 고 클릭 **확인**합니다. 걸리는 시간은 몇 초 전에 데이터를 가져온된 tooExcel 가져옵니다. 작업이 완료되면 11개 열의 데이터가 표시됩니다.

hello 마지막 섹션에서 만든 tootest hello 두 번째 정책이 (읽기 hivesampletable devicemake)

1. Excel에서 새 시트를 추가합니다.
2. Hello 마지막 절차 tooimport hello 데이터를 따릅니다.  hello만 변경 사항이 됩니다 hiveuser1의 대신 toouse hiveuser2 자격 증명입니다. Hiveuser2 permission toosee 두 열에만 실패 합니다. 다음 오류가 hello를 발생할 점에 있습니다.

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. 다음과 같은 hello 프로시저 tooimport 데이터입니다. 이 시간 hiveuser2의 자격 증명을 사용 하 고 또한에서 select 문을 hello를 수정 합니다.

        SELECT * FROM "HIVE"."default"."hivesampletable"

    to:

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    작업이 완료되면 가져온 두 개 열의 데이터가 표시됩니다.

## <a name="next-steps"></a>다음 단계
* 도메인에 가입된 HDInsight 클러스터 구성에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md)을 참조하세요.
* 도메인에 가입된 HDInsight 클러스터 관리에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터 관리](hdinsight-domain-joined-manage.md)를 참조하세요.
* 도메인에 가입된 HDInsight 클러스터에서 SSH를 사용하여 Hive 쿼리를 실행하려면 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)을 참조하세요.
* 하이브 JDBC를 사용 하 여 하이브 연결에 대 한 참조 [tooHive hello 하이브 JDBC 드라이버를 사용 하 여 Azure HDInsight에 연결](hdinsight-connect-hive-jdbc-driver.md)
* 하이브 ODBC를 사용 하 여 연결 Excel tooHadoop 참조 [Microsoft 하이브 ODBC 드라이브 hello로 Excel 연결 tooHadoop](hdinsight-connect-excel-hive-odbc-driver.md)
* 파워 쿼리를 사용 하 여 연결 Excel tooHadoop 참조 [파워 쿼리를 사용 하 여 Excel 연결 tooHadoop](hdinsight-connect-excel-power-query.md)
