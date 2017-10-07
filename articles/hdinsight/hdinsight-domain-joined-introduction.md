---
title: "aaaHadoop 보안-도메인에 가입 된 HDInsight 클러스터-Azure | Microsoft Docs"
description: "유용한 정보"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/31/2016
ms.author: saurinsh
ms.openlocfilehash: 5a9469402a61bcba4017e1ff4bd06dfba23ac963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toohadoop-security-with-domain-joined-hdinsight-clusters-preview"></a>도메인에 가입 된 HDInsight 클러스터 (미리 보기)를 사용 하는 소개 tooHadoop 보안

오늘날까지 Azure HDInsight는 단일 사용자 로컬 관리자만을 지원했습니다. 따라서 소규모 응용 프로그램 팀이나 부서의 경우에 유용하게 작동했습니다. 등급 기능 active directory 기반 인증, 다중 사용자 지원 및 역할 기반 액세스 제어와 같은 Hadoop 엔터프라이즈에 대 한 필요 얻은 hello 엔터프라이즈 섹터에 더 많은 사례가 증가 하 고 hello 기반된 작업으로 점점 더 중요 해 업체가 되었습니다. 도메인에 가입 된 HDInsight 클러스터를 사용 하는 HDInsight 클러스터 가입 tooan Active Directory 도메인을 만들을 tooHDInsight 클러스터에서 Azure Active Directory toolog를 통해 인증할 수 hello 기업에서 직원의 목록을 구성할 수 있습니다. Hello 엔터프라이즈 외부 사용자는 로그온 하거나 hello HDInsight 클러스터에 액세스 수 없습니다. hello 엔터프라이즈 관리자 구성할 수 사용 하 여 하이브 보안에 대 한 역할 기반 액세스 제어 [Apache 레인저](http://hortonworks.com/apache/ranger/), 따라서 필요한 toodata tooonly 액세스를 제한 합니다. 마지막으로, admin 님 안녕하세요 hello 데이터가 직원으로 액세스를 감사할 수 하 고 모든 변경 내용은 tooaccess 제어 정책, 따라서 높은 수준의 회사 리소스의 거 버 넌 스를 달성 합니다.

> [!NOTE]
> hello 새이 미리 보기에 설명 된 기능은 하이브 작업에 대 한 Linux 기반 HDInsight 클러스터에만 사용할 수 있습니다. 다른 워크 로드를 hello, HBase, Spark, 스톰 및 Kafka, 사용할지 나중에 같은 해제 합니다.

> [!IMPORTANT]
> 도메인에 가입된 HDInsight에서는 Oozie를 사용할 수 없습니다.

## <a name="benefits"></a>이점
기업 보안에는 네 가지 기본 요소인 경계 보안, 인증, 권한 부여 및 암호화가 포함됩니다.

![도메인에 가입된 HDInsight 클러스터는 기본 요소를 제공합니다.](./media/hdinsight-domain-joined-introduction/hdinsight-domain-joined-four-pillars.png)을 참조하세요.

### <a name="perimeter-security"></a>경계 보안
HDInsight에서 경계 보안은 가상 네트워크 및 게이트웨이 서비스를 사용하여 이루어집니다. 오늘날에 엔터프라이즈 관리자 가상 네트워크 내는 HDInsight 클러스터를 만들 수 있으며 네트워크 보안 그룹 (인바운드 또는 아웃 바운드 방화벽 규칙) toorestrict 액세스 toohello 가상 네트워크를 사용 하 여 됩니다. 만 hello hello에 정의 된 IP 주소 인바운드 방화벽 규칙 hello HDInsight 클러스터를 경계 보안을 갖출 수 toocommunicate 됩니다. 다른 경계 보안 계층은 게이트웨이 서비스를 사용하여 이루어집니다. hello 게이트웨이 역할을 위한 모든 들어오는 요청 toohello HDInsight 클러스터에 대 한 첫 번째 하는 hello 서비스입니다. Hello 요청을 수락, 유효성 검사를 수행 하 고 그래야만 hello 클러스터의 이름 및 데이터 노드 tooother 경계 보안을 갖출 클러스터 hello 요청 toopass toohello 다른 노드를 허용 합니다.

### <a name="authentication"></a>인증
기업 관리자는 이 공개 미리 보기를 사용하여 [가상 네트워크](https://azure.microsoft.com/services/virtual-network/)에서 도메인에 가입된 HDInsight 클러스터를 프로비전할 수 있습니다. hello HDInsight 클러스터의 노드를 hello 조인된 toohello 도메인 hello 엔터프라이즈에서 관리 됩니다. 이 작업은 [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md)를 사용하여 이루어집니다. Hello 클러스터 모든 hello 노드는 hello 엔터프라이즈를 관리 하는 조인 된 tooa 도메인입니다. 이 설치 프로그램 hello 엔터프라이즈 직원 toohello 클러스터 노드를 해당 도메인 자격 증명을 사용 하 여 로그온 할 수 있습니다. 또한 색상, Ambari 뷰, ODBC, JDBC, PowerShell 및 REST Api toointeract hello 클러스터와 같은 다른 승인 된 끝점과 해당 도메인 자격 증명 tooauthenticate를 사용할 수 있습니다. admin 님 안녕하세요 hello 이러한 끝점을 통해 hello 클러스터와의 상호 작용 하는 사용자 수 제한에 대 한 모든 권한을 있습니다.

### <a name="authorization"></a>권한 부여
대부분의 기업은 뒤 가장 좋은 방법은 모든 직원 tooall 엔터프라이즈 리소스에 액세스 한다는 것입니다. 마찬가지로,이 릴리스에서 admin 님 안녕하세요 hello 클러스터 리소스에 대 한 역할 기반 액세스 제어 정책을 정의할 수 있습니다. Admin 님 안녕하세요 구성할 수는 예를 들어 [Apache 레인저](http://hortonworks.com/apache/ranger/) tooset 액세스 하이브에 대 한 정책을 제어 합니다. 이 기능은 하면 한 직원 수 tooaccess만 필요한 toobe 업무를 성공적으로 많은 데이터입니다. SSH 액세스 toohello 클러스터만 toohello 제한 된 관리자 이기도합니다.

### <a name="auditing"></a>감사
HDInsight 클러스터 리소스 권한 없는 사용자 로부터 및 감사 hello 데이터를 보호 하는 모든 toohello 클러스터 리소스에 액세스 하 고 hello hello 보호와 함께 데이터를 필요한 tootrack hello 리소스의 무단 또는 실수로 실행 액세스 합니다. 이 미리 보기에서는 admin 님 안녕하세요 확인 하 고 모든 toohello HDInsight 클러스터 리소스에 액세스 및 데이터를 보고할 수 있습니다. 모든 변경 내용 toohello 액세스 제어 정책 Apache 레인저에서 수행 하는 보고서에는 끝점 지원 및 admin 님 안녕하세요도 볼 수 있습니다. 도메인에 가입 된 HDInsight 클러스터는 hello 친숙 한 Apache 레인저 UI toosearch 감사 로그를 사용합니다. Hello 백 엔드 시스템에서 레인저 사용 [Apache Solr](http://hortonworks.com/apache/solr/) 저장 하 고 hello 로그를 검색 합니다.

### <a name="encryption"></a>암호화
데이터를 보호 하는 회의 조직의 보안 및 규정 준수 요구 사항에 대 한 중요 한 데이터를 무단으로 직원 들의 toodata 액세스를 제한 하는 함께 것 해야도 보호 암호화 하 여 합니다. HDInsight 클러스터를 Azure 저장소 Blob에 대 한 데이터 저장소 둘 다 hello 및 Azure 데이터 레이크 저장소 지원 투명 한 서버 쪽 [데이터의 암호화](../storage/common/storage-service-encryption.md) 미사용 합니다. HDInsight 클러스터의 보안 유지는 미사용 데이터 용량의 서버 쪽 암호화에서 원활하게 작동합니다.

## <a name="next-steps"></a>다음 단계
* 도메인에 가입된 HDInsight 클러스터 구성에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md)을 참조하세요.
* 도메인에 가입된 HDInsight 클러스터 관리에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터 관리](hdinsight-domain-joined-manage.md)를 참조하세요.
* Hive 정책 및 Hive 쿼리 실행에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터에 대한 Hive 정책 구성](hdinsight-domain-joined-run-hive.md)을 참조하세요.
* 도메인에 가입된 HDInsight 클러스터에서 SSH를 사용하여 Hive 쿼리를 실행하려면 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)을 참조하세요.
