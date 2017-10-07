---
title: "Azure HDInsight 아키텍처 aaaDomain 가입 | Microsoft Docs"
description: "어떻게 tooplan 도메인에 가입 된 HDInsight에 알아봅니다."
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
ms.date: 02/03/2017
ms.author: saurinsh
ms.openlocfilehash: 1c3ecedf3739b4f8fa54160225be9c1d6e2ca6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a>HDInsight에서 Azure 도메인에 가입된 Hadoop 클러스터 계획

hello 기존의 Hadoop 클러스터가 단일 사용자입니다. 대량 데이터 워크로드를 구축하는 작은 응용 프로그램 팀이 있는 대부분의 회사에 적합합니다. Hadoop이 인기를 끌면서 대부분의 기업이 클러스터를 IT 팀에서 관리하고 여러 응용 프로그램 팀이 클러스터를 공유하는 모델로 이동하고 있습니다. 따라서 기능 관련 된 다중 사용자 클러스터 간에 hello Azure HDInsight의 가장 요청 된 기능입니다.

고유한 다중 사용자 인증 및 권한 부여를 작성 하는 대신 HDInsight hello 가장 인기 있는 id 공급자-Active Directory (AD)에 의존 합니다. AD에서 hello 강력한 보안 기능 HDInsight에서 사용 되는 toomanage 다중 사용자 권한 부여 될 수 있습니다. HDInsight AD를 통합 하 여 AD 자격 증명을 사용 하 여 hello 클러스터와 통신할 수 있습니다. 모든 hello에서 HDInsight 서비스를 실행 하므로 HDInsight는 AD 사용자 tooa 로컬 Hadoop 사용자를 매핑합니다 (Ambari, 서버, 레인저 Spark thrift 하이브 서버 및 기타) hello 인증 된 사용자에 대해 원활 하 게 작동 합니다.

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a>AD 및 IaaS VM의 AD와 HDInsight 통합

HDInsight Azure AD 또는 Iaas VM에 AD를 통합 하 여 hello HDInsight 클러스터 노드가 도메인에 가입 된 tooa 도메인 됩니다. HDInsight은 hello에 대 한 서비스 주체를 hello 클러스터에서 실행 되는 Hadoop 서비스 만들어지고 지정 된 조직 구성 단위 (OU) 내에서 Azure AD 또는 IaaS VM에 AD에에서 배치 됩니다. 또한 HDInsight 역방향 DNS 매핑은 조인 된 toohello 도메인 hello 노드의 IP 주소가 hello에 대 한 hello 도메인에 만듭니다.

이러한 설정은 여러 아키텍처를 사용하여 적용할 수 있습니다. Hello 아키텍처를 다음에서 선택할 수 있습니다.

**Azure IaaS에서 실행되는 AD와 통합된 HDInsight**

Hello HDInsight Active Directory와 통합 하기 위한 가장 간단한 아키텍처입니다. hello AD 도메인 컨트롤러 하나 (또는 여러) (Vm) Azure에서 가상 컴퓨터에서 실행 됩니다. 이러한 VM은 일반적으로 가상 네트워크 내에 있습니다. Hello HDInsight 클러스터에 대 한 다른 가상 네트워크를 설정 합니다. HDInsight toohave 시야 tooActive 디렉터리에 대 한 필요한 toopeer 이러한 가상 네트워크를 사용 하 여 [VNet 대 VNet 피어 링](../virtual-network/virtual-network-create-peering.md)합니다. 만들면 hello Active Directory를 만들 수 있습니다 하 고 HDInsight에 동일한 VNet hello ARM에서 Active Directory hello와 toodo 피어 링이 필요 하지 않습니다. 

![도메인에 가입된 HDInsight 클러스터 토폴로지](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> 이 아키텍처에서 hello HDInsight 클러스터와 Azure 데이터 레이크 저장소를 사용할 수 없습니다.


Active Directory에 대한 필수 조건:

* [조직 구성 단위](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) 를 만들고, 배치를 내에서 HDInsight 클러스터 Vm hello 및 hello hello 클러스터에서 사용 하는 서비스 사용자입니다.
* [LDAP(Lightweight Directory Access Protocol)](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md)가 AD와의 통신을 위해 설정되어야 합니다. LDAPS 사용 하는 인증서 tooset hello 실제 인증서 (자체 서명 된 인증서 하지) 이어야 합니다.
* 역방향 DNS 영역은 hello hello HDInsight 서브넷 (예를 들어 hello 이전 그림의 10.2.0.0/24)의 IP 주소 범위에 대 한 hello 도메인에 만들어야 합니다.
* 서비스 계정 또는 사용자 계정이 필요합니다. 이 계정 toocreate hello HDInsight 클러스터를 사용 합니다. 이 계정에는 다음 권한을 hello가 있어야 합니다.

    - 사용 권한 toocreate 서비스 보안 주체 개체 및 hello 조직 구성 단위 내에서 컴퓨터 개체
    - 사용 권한 toocreate 역방향 DNS 프록시 규칙
    - 사용 권한 toojoin 컴퓨터 toohello Active Directory 도메인

**클라우드 전용 Azure AD와 통합된 HDInsight**

클라우드 전용 Azure AD의 경우 HDInsight가 Azure AD와 통합될 수 있도록 도메인 컨트롤러를 구성합니다. 이 작업은 Azure AD DS([Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md))를 사용하여 이루어집니다. Azure AD DS 도메인 컨트롤러 컴퓨터에 hello 클라우드 만들고 IP 주소를 제공 하 합니다. 고가용성을 위해 두 개의 도메인 컨트롤러를 만듭니다.

현재 Azure AD DS는 클래식 가상 네트워크에만 존재합니다. 만 액세스할 수 있는 hello Azure 클래식 포털을 사용 하 여 hello HDInsight 가상 네트워크가 hello toobe는 Azure 포털에서에서 VNet 대 VNet 피어 링을 사용 하 여 hello 클래식 가상 네트워크와 겹치기 합니다.

> [!NOTE]
> 동일한 지역 hello 클래식 가상 네트워크와 가상 네트워크 가상 네트워크 모두에 있어야 하는 Azure 리소스 관리자 간의 피어 링 및 아래에서 동일한 hello Azure 구독.

![도메인에 가입된 HDInsight 클러스터 토폴로지](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

Azure AD에 대한 필수 조건:

* [조직 구성 단위](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) 배치 있는 내 만들어야 hello HDInsight 클러스터 Vm 및 서비스 사용자 hello 클러스터에서 사용 하는 hello 합니다.
* [LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md)는 Azure AD DS를 구성할 때 설정되어야 합니다. LDAPS 사용 하는 인증서 tooset hello 실제 인증서 (자체 서명 된 인증서 하지) 이어야 합니다.
* 역방향 DNS 영역은 hello hello HDInsight 서브넷 (예를 들어 hello 이전 그림의 10.2.0.0/24)의 IP 주소 범위에 대 한 hello 도메인에 만들어야 합니다.
* [암호 해시](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md) Azure AD tooAzure AD DS에서에서 동기화 되어야 합니다.
* 서비스 계정 또는 사용자 계정이 필요합니다. 이 계정 toocreate hello HDInsight 클러스터를 사용 합니다. 이 계정에는 다음 권한을 hello가 있어야 합니다.

    - 사용 권한 toocreate 서비스 보안 주체 개체 및 hello 조직 구성 단위 내에서 컴퓨터 개체
    - 사용 권한 toocreate 역방향 DNS 프록시 규칙
    - 사용 권한 toojoin 컴퓨터 toohello Azure AD 도메인

## <a name="next-steps"></a>다음 단계
* 도메인에 가입 된 HDInsight 클러스터 tooconfigure 참조 [도메인에 가입 된 HDInsight 클러스터를 구성할](hdinsight-domain-joined-configure.md)합니다.
* toomanage 도메인에 가입 된 HDInsight 클러스터 참조 [도메인에 가입 된 HDInsight 클러스터를 관리](hdinsight-domain-joined-manage.md)합니다.
* tooconfigure 하이브 정책 및 실행된 된 Hive 쿼리 참조 [도메인에 가입 하는 HDInsight 클러스터에 대 한 하이브 구성 정책을](hdinsight-domain-joined-run-hive.md)합니다.
* 도메인에 가입 된 HDInsight 클러스터에 SSH를 사용 하 여 toorun 하이브 쿼리에서 참조 [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md)합니다.
