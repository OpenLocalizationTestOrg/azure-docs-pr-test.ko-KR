---
title: "aaaManage 도메인에 가입 된 HDInsight 클러스터-Azure | Microsoft Docs"
description: "어떻게 toomanage 도메인에 가입 된 HDInsight 클러스터에 대해 알아봅니다"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a>도메인에 가입된 HDInsight 클러스터 관리(미리 보기)
Hello 사용자 및 도메인에 가입 된 HDInsight 클러스터와 어떻게 toomanage 도메인에 가입 된 HDInsight 클러스터에 hello 역할에 알아봅니다.

## <a name="users-of-domain-joined-hdinsight-clusters"></a>도메인에 가입된 HDInsight 클러스터의 사용자
도메인에 가입 되지 않은 하는 HDInsight 클러스터에 hello 클러스터 생성 중에 생성 되는 두 개의 사용자 계정이 있습니다.

* **Ambari 관리자**: 이 계정을 *Hadoop 사용자* 또는 *HTTP 사용자*라고도 합니다. 이 계정에서 https:// tooAmbari에 사용 되는 toolog 수&lt;clustername >. azurehdinsight.net 합니다. 또한 Ambari 뷰에 대 한 사용된 toorun 쿼리 수, 외부 도구 (즉, PowerShell, Templeton, Visual Studio)를 통해 작업을 실행 및 hello 하이브 ODBC 드라이버 및 (즉, Excel, PowerBI, 또는 Tableau)의 BI 도구를 사용 하 여 인증 합니다.
* **SSH 사용자**: 이 계정은 SSH와 함께 사용할 수 있으며, sudo 명령을 실행합니다. 루트 권한이 toohello Linux Vm에 있습니다.

또한 tooAmbari Admin 및 SSH 사용자 3 개의 새 사용자가 포함 하는 도메인에 가입 된 HDInsight 클러스터입니다.

* **레인저 admin**:이 계정은 로컬 hello Apache 레인저 관리자 계정입니다. 이 계정은 Active Directory 도메인 사용자가 아닙니다. 이 계정을 사용 하는 toosetup 정책을 수 있으며 (해당 사용자가 관리할 수 있도록 정책) 다른 사용자가 관리자 또는 위임 된 관리자를 확인 됩니다. 기본적으로 hello username는 *관리자* hello 암호 hello Ambari 관리자 암호와 동일 hello는 및입니다. hello 암호 레인저의 hello 설정 페이지에서 업데이트할 수 있습니다.
* **클러스터 관리: 도메인 사용자**:이 계정은 Ambari 및 레인저 포함 하 여 Hadoop 클러스터 관리자 hello으로 지정 된 active directory 도메인 사용자입니다. 클러스터를 만드는 동안 이 사용자의 자격 증명을 입력해야 합니다. 이 사용자에 게 다음 권한을 hello:

  * 컴퓨터 toohello 도메인에 가입 하 고 클러스터를 만드는 동안 지정 된 OU hello 내에 배치 합니다.
  * Hello 클러스터 생성 중에 지정 된 OU 내에서 서비스 사용자를 만듭니다.
  * 역방향 DNS 항목을 만듭니다.

    참고 hello 다른 AD 사용자는 또한 이러한 권한이 있어야 합니다.

    일부 끝점 (예를 들어, Templeton) hello 클러스터 내에서 레인저를 통해 관리 되지 않는 이며 안전 하지 않은 있습니다. 이러한 끝점 hello 클러스터 관리: 도메인 사용자를 제외한 모든 사용자에 대해 잠겨 있습니다.
* **일반**: 클러스터를 만들 때 여러 Active Directory 그룹을 제공할 수 있습니다. 이러한 그룹의 hello 사용자 Ambari 동기화 된 tooRanger 됩니다. 이러한 사용자는 도메인 사용자를 액세스 tooonly 레인저 관리 끝점 (예를 들어 Hiveserver2)을 갖습니다. RBAC 정책을 모든 hello 및 적용 가능한 toothese 사용자 감사 됩니다.

## <a name="roles-of-domain-joined-hdinsight-clusters"></a>도메인에 가입된 HDInsight 클러스터의 역할
도메인에 가입 된 HDInsight 사용할 역할을 수행 하는 hello 있습니다.

* 클러스터 관리자
* 클러스터 운영자
* 서비스 관리자
* 서비스 운영자
* 클러스터 사용자

**이러한 역할의 toosee hello 사용 권한**

1. Hello Ambari 관리 UI를 엽니다.  참조 [열려 hello Ambari 관리 UI](#open-the-ambari-management-ui)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **역할**합니다.
3. Hello 파란색 물음표 toosee hello 사용 권한을 클릭 합니다.

    ![도메인에 가입된 HDInsight 클러스터의 역할 사용 권한](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a>Hello Ambari 관리 UI를 열으십시오
1. Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.
2. 블레이드에서 HDInsight 클러스터를 엽니다. [클러스터 나열 및 표시](hdinsight-administer-use-management-portal.md#list-and-show-clusters)를 참조하세요.
3. 클릭 **대시보드** hello 상단 메뉴 tooopen Ambari에서에서 합니다.
4. TooAmbari hello 클러스터 관리자가 도메인 사용자 이름 및 암호를 사용 하 여 로그온 합니다.
5. Hello 클릭 **Admin** hello 오른쪽 상단에서 드롭다운 메뉴 **관리 Ambari**합니다.

    ![도메인에 가입된 HDInsight 관리 Ambari](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    hello UI는 다음과 같습니다.

    ![도메인에 가입된 HDInsight Ambari 관리 UI](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a>Active Directory에서 동기화 hello 도메인 사용자를 나열 합니다.
1. Hello Ambari 관리 UI를 엽니다.  참조 [열려 hello Ambari 관리 UI](#open-the-ambari-management-ui)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **사용자**합니다. Active Directory toohello HDInsight 클러스터에서 동기화 하는 모든 hello 사용자를 확인할 않아야 합니다.

    ![도메인에 가입된 HDInsight Ambari 관리 UI 사용자 나열](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a>Hello 도메인 그룹 목록을 Active Directory에서 동기화
1. Hello Ambari 관리 UI를 엽니다.  참조 [열려 hello Ambari 관리 UI](#open-the-ambari-management-ui)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **그룹**합니다. Active Directory toohello HDInsight 클러스터에서 동기화 하는 모든 hello 그룹을 확인 해야 합니다.

    ![도메인에 가입된 HDInsight Ambari 관리 UI 그룹 나열](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a>Hive 뷰 사용 권한 구성
1. Hello Ambari 관리 UI를 엽니다.  참조 [열려 hello Ambari 관리 UI](#open-the-ambari-management-ui)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **뷰**합니다.
3. 클릭 **하이브** tooshow hello 세부 정보입니다.

    ![도메인에 가입된 HDInsight Ambari 관리 UI Hive 뷰](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. Hello 클릭 **하이브 보기** tooconfigure 하이브 뷰를 연결 합니다.
5. Toohello 아래로 스크롤하여 **권한을** 섹션.

    ![도메인에 가입된 HDInsight Ambari 관리 UI Hive 뷰 사용 권한 구성](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. 클릭 **사용자 추가** 또는 **그룹 추가**, 하이브 보기를 사용할 수 있는 hello 사용자 또는 그룹을 지정 합니다.

## <a name="configure-users-for-hello-roles"></a>Hello 역할에 대 한 사용자 구성
 toosee 역할과 해당 사용 권한을 목록이 참조 [역할의 도메인에 가입 된 HDInsight 클러스터](#roles-of-domain---joined-hdinsight-clusters)합니다.

1. Hello Ambari 관리 UI를 엽니다.  참조 [열려 hello Ambari 관리 UI](#open-the-ambari-management-ui)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **역할**합니다.
3. 클릭 **사용자 추가** 또는 **그룹 추가** tooassign 사용자 및 그룹 toodifferent 역할입니다.

## <a name="next-steps"></a>다음 단계
* 도메인에 가입된 HDInsight 클러스터 구성에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md)을 참조하세요.
* Hive 정책 및 Hive 쿼리 실행에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터에 대한 Hive 정책 구성](hdinsight-domain-joined-run-hive.md)을 참조하세요.
* 도메인에 가입된 HDInsight 클러스터에서 SSH를 사용하여 Hive 쿼리를 실행하려면 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)을 참조하세요.
