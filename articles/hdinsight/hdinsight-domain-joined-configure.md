---
title: "aaaConfigure 도메인에 가입 된 HDInsight 클러스터-Azure | Microsoft Docs"
description: "자세한 내용은 방법 tooset 및 도메인에 가입 된 HDInsight 클러스터를 구성 합니다."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 0cbb49cc-0de1-4a1a-b658-99897caf827c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 8c4b3d269a7662d27a49b839e5cd05a3e24f7023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview"></a>도메인에 가입된 HDInsight 클러스터 구성(미리 보기)

Azure Active Directory (Azure AD)와 tooset Azure HDInsight를 클러스터링 하는 방법에 대해 알아봅니다 및 [Apache 레인저](http://hortonworks.com/apache/ranger/) tootake 강력한 인증 및 다양 한 역할 기반 액세스 제어 (RBAC) 정책을 사용 합니다.  도메인에 가입된 HDInsight는 Linux 기반 클러스터에만 구성할 수 있습니다. 자세한 내용은 [도메인에 가입된 HDInsight 클러스터 소개](hdinsight-domain-joined-introduction.md)를 참조하세요.

> [!IMPORTANT]
> 도메인에 가입된 HDInsight에서는 Oozie를 사용할 수 없습니다.

이 문서는 일련의 첫 번째 자습서 hello:

* 사용 하도록 설정 하는 Apache 레인저 사용 (Azure Directory 도메인 서비스 기능 hello)를 통해 HDInsight 연결 된 클러스터 tooAzure AD를 만듭니다.
* 만들기 및 Apache 레인저 통해 하이브 정책을 적용 하며 (예를 들어, 데이터 과학자) 사용자가 ODBC 기반 도구, 예를 들어 Excel, Tableau 등을 사용 하 여 tooconnect tooHive. Microsoft는 협력 하 여 HBase, Spark, and 스톰, HDInsight tooDomain 조인 같은 다른 워크 로드를 곧 추가 합니다.

Hello 최종 토폴로지에 대 한 예는 다음과 같습니다.

![도메인에 가입된 HDInsight 토폴로지](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

현재 Azure AD는 클래식 가상 네트워크(VNet)만 지원하고 Linux 기반 HDInsight 클러스터는 Azure Resource Manager 기반 VNet만 지원하므로 HDInsight Azure AD를 통합하려면 두 VNet이 있어야 하고 또 두 VNet을 피어링해야 합니다. Hello 두 배포 모델 간의 hello 비교 내용은 [Azure 리소스 관리자 및 클래식 배포: 배포 모델을 이해 하 고 리소스 상태를 hello](../azure-resource-manager/resource-manager-deployment-model.md)합니다. 두 개의 Vnet hello에 있어야 하는 hello hello Azure AD DS와 동일한 영역입니다.

Azure 서비스 이름은 전역적으로 고유해야 합니다. hello 이름 다음이 자습서에 사용 됩니다. Contoso는 가상의 이름입니다. 바꾸어야 *contoso* hello 자습서를 진행 하는 경우 다른 이름을 사용 합니다. 

**이름:**

| 속성 | 값 |
| --- | --- |
| Azure AD VNet |contosoaadvnet |
| Azure AD VNet 리소스 그룹 |contosoaadrg |
| Azure AD Directory |contosoaaddirectory |
| Azure AD 도메인 이름 |contoso(contoso.onmicrosoft.com) |
| HDInsight VNet |contosohdivnet |
| HDInsight VNet 리소스 그룹 |contosohdirg |
| HDInsight 클러스터 |contosohdicluster |

이 자습서는 도메인에 가입 된 HDInsight 클러스터를 구성 하는 hello 단계를 제공 합니다. 각 섹션에는 자세한 배경 정보로 링크 tooother 문서가 있습니다.

## <a name="prerequisite"></a>필수 조건:
* [Azure AD Domain Services](https://azure.microsoft.com/services/active-directory-ds/) 및 [가격 책정](https://azure.microsoft.com/pricing/details/active-directory-ds/) 구조를 숙지합니다.
* 구독이 이 공개 미리 보기에 대한 허용 목록에 추가되었는지 확인합니다. 전자 메일을 전송 하 여 그렇게 할 수 toohdipreview@microsoft.com 구독 ID로
* 도메인의 서명 기관에서 서명한 SSL 인증서가 필요합니다. 보안 LDAP를 구성 하 여 hello 인증서가 필요 합니다. 자체 서명된 인증서는 사용할 수 없습니다.

## <a name="procedures"></a>프로시저
1. Azure AD에 대한 Azure 클래식 VNet을 만듭니다.  
2. Azure AD 및 Azure AD DS를 만들고 구성합니다.
3. Hello Azure 리소스 관리 모드에서 HDInsight VNet을 만듭니다.
4. 피어에는 두 개의 Vnet hello 합니다.
5. HDInsight 클러스터 만들기

> [!NOTE]
> 이 자습서에서는 사용자에게 Azure AD가 없다고 가정합니다. 하나를 설정한 경우 2 단계에서 hello 부분을 건너뛸 수 있습니다.
> 
> 

3단계에서 7단계까지 자동화하는 PowerShell 스크립트가 있습니다.  자세한 내용은 [Azure PowerShell을 사용하여 도메인 가입 HDInsight 클러스터 구성](hdinsight-domain-joined-configure-use-powershell.md)을 참조하세요.

## <a name="create-an-azure-virtual-network-classic"></a>Azure 가상 네트워크(클래식) 만들기
이 섹션에서는 hello Azure 포털을 사용 하 여 가상 네트워크 (클래식)를 만듭니다. Hello 다음 섹션에서 hello 가상 네트워크에 Azure AD에 Azure AD DS hello를 사용합니다. 절차를 수행 하 고 다른 가상 네트워크 만들기 방법을 사용 하 여 hello에 대 한 자세한 내용은 참조 [hello Azure 포털을 사용 하 여 가상 네트워크 (클래식) 만들기](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)합니다.

**클래식 VNet toocreate**

1. Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다. 
2. **새로 만들기** > **네트워킹** > **가상 네트워크**를 클릭합니다.
3. **배포 모델 선택**에서 **클래식**을 선택한 다음 **만들기**를 클릭합니다.
4. 입력 하거나 다음 값에는 hello를 선택 합니다.
   
   * **이름**: contosoaadvnet
   * **주소 공간**: 10.1.0.0/16
   * **서브넷 이름**: Subnet1
   * **서브넷 주소 범위**: 10.1.0.0/24
   * **구독** - (이 VNet을 만드는 데 사용할 구독을 선택합니다.)
   * **ResourceGroup**: contosoaadrg
   * **위치**: (HDInsight 클러스터의 지역을 선택합니다.)
     
     > [!IMPORTANT]
     > Azure AD DS를 지원하는 위치를 선택해야 합니다. 자세한 내용은 [지역별 사용 가능한 제품](https://azure.microsoft.com/en-us/regions/services/)을 참조하세요. 
     > 
     > 클래식 VNet hello 둘 다 고 hello 리소스 그룹 VNet 내에 있어야 hello hello Azure AD DS와 동일한 영역입니다.
     > 
     > 
5. 클릭 **만들기** toocreate hello VNet입니다.

## <a name="create-and-configure-azure-ad-ds-for-your-azure-ad"></a>Azure AD에 대한 Azure AD DS를 만들고 구성합니다.
이 섹션에서는 다음을 수행합니다.

1. Azure AD를 만듭니다.
2. Azure AD 사용자를 만듭니다. 이러한 사용자는 도메인 사용자입니다. Hello Azure AD로 hello HDInsight 클러스터를 구성 하기 위한 첫 번째 사용자는 hello를 사용 합니다.  hello 다른 두 사용자는 선택적이 자습서에 대 한입니다. 두 사용자는 Apache Ranger 정책을 구성할 때 [도메인에 가입된 HDInsight 클러스터에 대한 Hive 정책 구성](hdinsight-domain-joined-run-hive.md)에 사용됩니다.
3. Hello AAD DC 관리자 그룹을 만들고 hello Azure AD 사용자 toohello 그룹을 추가 합니다. 이 사용자 toocreate hello 조직 구성 단위를 사용 합니다.
4. Hello Azure AD에 대해 Azure AD 도메인 서비스 (Azure AD DS)를 사용 합니다.
5. Hello Azure AD에 대 한 LDAPS를 구성 합니다. hello LDAP Lightweight Directory Access Protocol ()에서 사용 되는 tooread 이며 tooAzure AD 작성 합니다.

기존 Azure AD는 toouse를 선호 하는 경우 1 및 2 단계를 건너뛸 수 있습니다.

**Azure AD는 toocreate**

1. Hello에서 [Azure 클래식 포털](https://manage.windowsazure.com), 클릭 **새로** > **응용 프로그램 서비스** > **Active Directory**  >  **디렉터리** > **사용자 지정 만들기**합니다. 
2. 입력 하거나 다음 값에는 hello를 선택 합니다.
   
   * **이름**: contosoaaddirectory
   * **도메인 이름**: contoso.  이 이름은 전역적으로 고유해야 합니다.
   * **국가 또는 지역**: 국가 또는 지역을 선택합니다.
3. **완료**를 클릭합니다.

**Azure AD 사용자 만들기**

1. Hello에서 [Azure 클래식 포털](https://manage.windowsazure.com), 클릭 **Active Directory** -> **contosoaaddirectory**합니다. 
2. 클릭 **사용자** hello 상단 메뉴에서 합니다.
3. **사용자 추가**를 클릭합니다.
4. **사용자 이름**을 입력하고 **다음**을 클릭합니다. 
5. 사용자 프로필을 구성합니다. **역할**에서 **전역 관리자**를 클릭하고 **다음**을 클릭합니다.  hello 전역 관리자 역할은 필요한 toocreate 조직 구성 단위입니다.
6. 클릭 **만들기** tooget 임시 암호입니다.
7. Hello 암호의 복사본을 확인 한 다음 클릭 **완료**합니다. 이 자습서의 뒷부분에 나오는이 전역 관리자 사용자 toocreate hello HDInsight 클러스터를 사용 합니다.

다음 hello 동일한 프로시저 toocreate 두 개 더 많은 사용자가 hello로 **사용자** 역할과 hiveuser1 hiveuser2 합니다. hello 다음 사용자에 사용할 [도메인에 가입 된 HDInsight 클러스터에 대 한 하이브 구성 정책을](hdinsight-domain-joined-run-hive.md)합니다.

**toocreate hello AAD DC 관리자 그룹 및 Azure AD 사용자 추가**

1. Hello에서 [Azure 클래식 포털](https://manage.windowsazure.com), 클릭 **Active Directory** > **contosoaaddirectory**합니다. 
2. 클릭 **그룹** hello 상단 메뉴에서 합니다.
3. **그룹 추가** 또는 **그룹 추가**를 클릭합니다.
4. 입력 하거나 다음 값에는 hello를 선택 합니다.
   
   * **이름**: AAD DC 관리자.  Hello 그룹 이름을 변경 하지 마십시오.
   * **그룹 종류**: 보안 그룹.
5. 페이지 맨 아래에 있는 **완료**을 참조하세요.
6. 클릭 **AAD DC 관리자** tooopen hello 그룹입니다.
7. **멤버 추가**를 클릭합니다.
8. Hello 이전 단계에서 만든 첫 번째 사용자는 hello를 선택한 다음 클릭 **완료**합니다.
9. 반복 hello 동일한 단계 toocreate 다른 그룹 이라는 **HiveUsers**, 두 hello 하이브 사용자 toohello 그룹을 추가 합니다.

자세한 내용은 참조 [Azure AD 도메인 서비스 (미리 보기)-만들 hello ' AAD DC Administrators' 그룹](../active-directory-domain-services/active-directory-ds-getting-started.md)합니다.

**Azure AD에 대 한 Azure AD DS tooenable**

1. Hello에서 [Azure 클래식 포털](https://manage.windowsazure.com), 클릭 **Active Directory** > **contosoaaddirectory**합니다. 
2. 클릭 **구성** hello 상단 메뉴에서 합니다.
3. 너무 아래로 스크롤하여**도메인 서비스**, 다음 값에 집합 hello 및:
   
   * **이 디렉터리에 대해 도메인 서비스 사용**: 예.
   * **도메인 서비스의 DNS 도메인 이름을**: hello Azure 디렉터리의 hello 기본 DNS 이름을 표시 합니다. 예: contoso.onmicrosoft.com.
   * **도메인 서비스 toothis 가상 네트워크에 연결**: 선택 hello, 이전에 만든 클래식 가상 네트워크, 즉 **contosoaadvnet**합니다.
4. 클릭 **저장** hello hello 페이지 아래에서 합니다. 나타납니다 **보류 중...**  다음 너무**이 디렉터리에 대 한 도메인 서비스 사용**합니다.  
5. **보류 중...**이 사라질 때까지 기다리면 **IP 주소**가 채워집니다. 두 개의 IP 주소가 채워집니다. 이들은 도메인 서비스에서 프로 비전 하는 hello 도메인 컨트롤러의 hello IP 주소입니다. Hello 해당 하는 도메인 컨트롤러가 프로 비전 되 고 준비 된 후 각 IP 주소를 볼 수 있습니다. Hello 두 개의 IP 주소를 적어 둡니다. 나중에 필요합니다.

자세한 내용은 [Azure AD Domain Services(미리 보기) - Azure AD Domain Services 활성화](../active-directory-domain-services/active-directory-ds-getting-started-enableaadds.md)를 참조하세요.

**toosynchronize 암호**

사용자의 도메인을 사용 하는 경우 toosynchronize hello 암호가 필요 합니다. 참조 [클라우드 전용 Azure에 대 한 암호 동기화 tooAzure AD 도메인 서비스 사용 AD 디렉터리](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md)합니다.

**hello Azure AD에 대 한 LDAPS tooconfigure**

1. 도메인의 서명 기관에서 서명한 SSL 인증서를 가져옵니다. Toouse 자체 서명 된 인증서를 사용 하도록 하려는 경우에 게 연락 하세요 toohdipreview@microsoft.com 예외에 대 한 합니다.
2. Hello에서 [Azure 클래식 포털](https://manage.windowsazure.com), 클릭 **Active Directory** > **contosoaaddirectory**합니다. 
3. 클릭 **구성** hello 상단 메뉴에서 합니다.
4. 너무 스크롤하여**도메인 서비스**합니다.
5. **인증서 구성**을 클릭합니다.
6. Hello 지침 toospecify hello 인증서 파일 및 hello 암호를 따릅니다. 나타납니다 **보류 중...**  다음 너무**이 디렉터리에 대 한 도메인 서비스 사용**합니다.  
7. **보류 중...**이 사라질 때까지 기다리면 **보안 LDAP 인증서**가 채워집니다.  이 작업은 10분 이상 걸릴 수 있습니다.

> [!NOTE]
> 일부 백그라운드 작업 hello Azure AD DS에서 실행 될 경우-인증서를 업로드 하는 동안 오류가 표시 될 수 있습니다 <i>이 테 넌이 트에 대해 수행 중인 작업이입니다. 나중에 다시 시도하십시오</i>.  이 오류가 발생하면 잠시 후 다시 시도하세요. hello 두 번째 도메인 컨트롤러 IP를 프로 비전 too3 시간 toobe 걸릴 수 있습니다.
> 
> 

자세한 내용은 [Azure AD Domain Services 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md)을 참조하세요.

## <a name="create-a-resource-manager-vnet-for-hdinsight-cluster"></a>HDInsight 클러스터에 대한 Resource Manager VNet 만들기
이 섹션에서는 hello HDInsight 클러스터에 사용할 Azure 리소스 관리자 VNet을 만듭니다. Azure VNET을 만드는 다른 방법에 대한 자세한 내용은 [가상 네트워크 만들기](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)를 참조하세요.

Hello VNet을 만든 후 hello 리소스 관리자 VNet toouse hello hello Azure AD VNet에 대 한 동일한 DNS 서버를 구성 합니다. 이 자습서 toocreate의 hello 단계를 따른 경우 클래식 VNet과 Azure AD hello hello 10.1.0.4 및 10.1.0.5 hello DNS 서버가 있습니다.

**리소스 관리자 VNet toocreate**

1. Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.
2. **새로 만들기**, **네트워킹**, **가상 네트워크**를 차례로 클릭합니다. 
3. **배포 모델 선택**에서 **Resource Manager**를 선택하고 **만들기**를 클릭합니다.
4. 입력 하거나 다음 값에는 hello 선택:
   
   * **이름**: contosohdivnet
   * **주소 공간**: 10.2.0.0/16. Hello 주소 범위는 hello의 hello IP 주소 범위와 겹칠 수 없습니다 있는지 확인 클래식 VNet입니다.
   * **서브넷 이름**: Subnet1
   * **서브넷 주소 범위**: 10.2.0.0/24
   * **구독**: (Azure 구독을 선택합니다.)
   * **리소스 그룹**: contosohdirg
   * **위치**: (선택 hello 동일한 위치 contosoaadvnet 즉, Azure AD VNet hello 대로.)
5. **만들기**를 클릭합니다.

**리소스 관리자 VNet hello에 대 한 DNS tooconfigure**

1. Hello에서 [Azure 포털](https://portal.azure.com), 클릭 **더 많은 서비스** -> **가상 네트워크**합니다. 확인 되지 tooclick **가상 네트워크 (클래식)**합니다.
2. **contosohdivnet**을 클릭합니다.
3. 클릭 **DNS 서버** hello hello 새 블레이드의 왼쪽에서 합니다.
4. 클릭 **사용자 지정**, hello 다음 값을 입력 합니다.
   
   * 10.1.0.4
   * 10.1.0.5
     
     이러한 DNS 서버 IP 주소는 hello Azure AD (클래식 VNet) VNet에에서 DNS 서버 toohello 일치 해야 합니다.
5. **Save**를 클릭합니다.

## <a name="peer-hello-azure-ad-vnet-and-hello-hdinsight-vnet"></a>Azure AD VNet hello 피어 투 피어 및 HDInsight VNet hello
**toopeer hello 두 VNet**

1. Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.
2. 클릭 **더 많은 서비스** hello 왼쪽된 메뉴에서 합니다.
3. **가상 네트워크**를 클릭합니다. **가상 네트워크(클래식)**을 클릭하지 마세요.
4. **contosohdivnet**을 클릭합니다.  이 hello HDInsight VNet입니다.
5. 클릭 **피어 링** hello 블레이드의 hello 왼쪽된 메뉴에 있습니다.
6. 클릭 **추가** hello 상단 메뉴에서 합니다. Hello 열었을 **피어 링 추가** 블레이드입니다.
7. Hello에 **추가 피어 링** 블레이드, 다음 값으로 설정 하거나 선택 hello:
   
   * **이름**: ContosoAADHDIVNetPeering
   * **가상 네트워크 배포 모델**: 클래식
   * **구독**: hello 클래식 (Azure AD) vnet에 사용 되는 구독 이름을 선택 합니다.
   * **가상 네트워크**: contosoaadvnet.
   * **가상 네트워크 액세스 허용**: (확인)
   * **전달된 트래픽 허용**: (확인). 선택 hello 다른 두 확인란을 선택 합니다.
8. **확인**을 클릭합니다.

## <a name="create-hdinsight-cluster"></a>HDInsight 클러스터 만들기
이 섹션에서는 두 hello Azure 포털을 사용 하 여 HDInsight의 Linux 기반 Hadoop 클러스터를 만들 또는 [Azure 리소스 관리자 템플릿](../azure-resource-manager/resource-group-template-deploy.md)합니다. 다른 클러스터 생성 방법 및 참조 hello 설정을 이해, [만들 HDInsight 클러스터](hdinsight-hadoop-provision-linux-clusters.md)합니다. 리소스 관리자 템플릿 toocreate Hadoop을 사용 하는 방법에 대 한 자세한 내용은 HDInsight 클러스터를, 참조 [리소스 관리자 템플릿을 사용 하 여 HDInsight 클러스터를 만들기 Hadoop](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

**사용 하 여 도메인에 가입 된 HDInsight 클러스터 toocreate hello Azure 포털**

1. Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.
2. **새로 만들기**, **인텔리전스 + 분석**, **HDInsight**를 차례로 클릭합니다.
3. Hello에서 **새 HDInsight 클러스터** 블레이드를 입력 하거나 다음 값에는 hello를 선택 합니다.
   
   * **클러스터 이름**: hello 도메인에 가입 된 HDInsight 클러스터에 대 한 새 클러스터 이름을 입력 합니다.
   * **구독**: 이 클러스터를 만드는 데 사용할 Azure 구독을 선택합니다.
   * **클러스터 구성**:
     
     * **클러스터 유형**: Hadoop. 도메인에 가입된 HDInsight는 현재 Hadoop 클러스터에서만 지원됩니다.
     * **운영 체제**: Linux.  도메인에 가입된 HDInsight는 Linux 기반 HDInsight 클러스터에서만 지원됩니다.
     * **버전**: HDI 3.6. 도메인에 가입된 HDInsight는 HDInsight 클러스터 버전 3.6에서만 지원됩니다.
     * **클러스터 유형**: PREMIUM
       
       클릭 **선택** toosave hello 변경 합니다.
   * **자격 증명**: hello hello 클러스터 사용자와 hello SSH 사용자 자격 증명을 구성 합니다.
   * **데이터 원본**: 새 저장소 계정을 만들거나 hello hello HDInsight 클러스터에 대 한 기본 저장소 계정으로 기존 저장소 계정을 사용 합니다. hello 위치는 두 개의 Vnet hello와 같을 hello 해야 합니다.  hello 위치 hello HDInsight 클러스터의 hello 위치 이기도합니다.
   * **가격 책정**: hello 클러스터의 작업자 노드 수를 선택 합니다.
   * **고급 구성**: 
     
     * **도메인 가입 및 Vnet/Subnet**: 
       
       * **도메인 설정**: 
         
         * **도메인 이름**: contoso.onmicrosoft.com
         * **도메인 사용자 이름**: 도메인 사용자 이름을 입력합니다. 이 도메인 hello 다음 권한이 있어야 합니다.: toohello 도메인에 컴퓨터 가입 및; 클러스터를 만드는 동안 지정 hello 조직 구성 단위에 배치 클러스터 생성 중에 지정 하는 hello 조직 구성 단위 내에서 서비스 사용자 만들기 역방향 DNS 항목을 만듭니다. 이 도메인 사용자는이 도메인에 가입 된 HDInsight 클러스터의 관리자에 게 될 것입니다.
         * **도메인 암호**: hello 도메인 사용자 암호를 입력 합니다.
         * **조직 구성 단위**: hello hello HDInsight 클러스터와 toouse OU의 고유 이름을 입력 합니다. 예: OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com. HDInsight 클러스터는이 OU가 없으면이 OU toocreate를 시도 합니다. Hello OU가 이미 표시 되거나 hello 도메인 계정에 사용 권한을 toocreate 새 있는지 확인 합니다. AADDC 관리자의 일부인 hello 도메인 계정을 사용 하는 경우가 필요한 권한을 toocreate hello OU입니다.
         * **LDAPS URL**: ldaps://contoso.onmicrosoft.com:636
         * **사용자 액세스 그룹**: hello 보안 그룹을 사용자가 속한 지정 toosync toohello 클러스터를 구축할 합니다. 예: HiveUsers.
           
           클릭 **선택** toosave hello 변경 합니다.
           
           ![도메인에 가입된 HDInsight 도메인 설정 구성](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-portal-domain-setting.png)
       * **가상 네트워크**: contosohdivnet
       * **서브넷**: Subnet1
         
         클릭 **선택** toosave hello 변경 합니다.        
         클릭 **선택** toosave hello 변경 합니다.
   * **리소스 그룹**: hello HDInsight VNet (contosohdirg)에 사용 되는 선택 hello 리소스 그룹입니다.
4. **만들기**를 클릭합니다.  

도메인에 가입 된 HDInsight 클러스터를 만드는 또 다른 옵션은 toouse Azure 리소스 관리 템플릿입니다. 절차를 수행 하는 hello 방법을 보여 줍니다.

**toocreate 리소스 관리 템플릿을 사용 하 여 도메인에 가입 된 HDInsight 클러스터**

1. 다음 이미지 tooopen hello Azure 포털에서에서 리소스 관리자 템플릿으로 hello를 클릭 합니다. hello 리소스 관리자 템플릿은 공용 blob 컨테이너에 있습니다. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Hello에서 **매개 변수** 블레이드에서 hello 다음 값을 입력 합니다.
   
   * **구독**: (Azure 구독을 선택합니다.)
   * **리소스 그룹**: 클릭 **기존 항목 사용**, hello를 지정 하 고 동일한 리소스 그룹 사용 되 고 있습니다.  예: contosohdirg. 
   * **위치**: 리소스 그룹 위치를 지정합니다.
   * **클러스터 이름**: 만들 hello Hadoop 클러스터에 대 한 이름을 입력 합니다. 예: contosohdicluster.
   * **클러스터 유형**: 클러스터 유형을 선택합니다.  hello 기본값은 **hadoop**합니다.
   * **위치**: hello 클러스터에 대 한 위치를 선택 합니다.  사용 하 여 동일한 위치 hello hello 기본 저장소 계정입니다.
   * **작업자 노드 수를 클러스터**: hello 작업자 노드 수를 선택 합니다.
   * **로그인 이름 및 암호를 클러스터**: hello 기본 로그인 이름은 **admin**합니다.
   * **SSH 사용자 이름 및 암호**: hello 기본 사용자 이름은 **sshuser**합니다.  이름은 변경할 수 있습니다. 
   * **가상 네트워크 Id**: /subscriptions/&lt;SubscriptionID>/resourceGroups/&lt;ResourceGroupName>/providers/Microsoft.Network/virtualNetworks/&lt;VNetName>
   * **가상 네트워크 서브넷**: /subscriptions/&lt;SubscriptionID>/resourceGroups/&lt;ResourceGroupName>/providers/Microsoft.Network/virtualNetworks/&lt;VNetName>/subnets/Subnet1
   * **도메인 이름**: contoso.onmicrosoft.com
   * **조직 구성 단위 DN**: OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com
   * **클러스터 사용자 그룹 DN**: [\"HiveUsers\"]
   * **LDAPUrl**: ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (Enter hello 도메인 관리자 사용자 이름)
   * **DomainAdminPassword**: (hello 도메인 관리자 사용자 암호 입력)
   * **Toohello 약관 위에서 설명한 동의**: (확인)
   * **Pin toodashboard**: (확인)
3. **구매**를 클릭합니다. **템플릿 배포 배포 중**이라는 제목의 새 타일이 표시됩니다. 클러스터에 대 한 약 20 분 toocreate 걸립니다. Hello 클러스터를 만든 후 클릭할 수 있는 hello 포털 tooopen hello 클러스터 블레이드 것입니다.

Hello 자습서를 완료 한 후 toodelete hello 클러스터를 할 수 있습니다. HDInsight를 사용하면 데이터가 Azure 저장소에 저장되기 때문에 클러스터를 사용하지 않을 때 안전하게 삭제할 수 있습니다. HDInsight 클러스터를 사용하지 않는 기간에도 요금이 청구됩니다. Hello 클러스터에 대 한 hello 요금이 저장소에 대 한 hello 요금 보다 많은 배 더 많은 경우 이렇게 하면 경제 toodelete 클러스터 사용에서 되지 않은 있습니다. 클러스터를 삭제할 경우의 hello 지침은 참조 [를 사용 하 여 HDInsight의 Hadoop 관리 클러스터에 Azure 포털 hello](hdinsight-administer-use-management-portal.md#delete-clusters)합니다.

## <a name="next-steps"></a>다음 단계
* Hive 정책 및 Hive 쿼리 실행에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터에 대한 Hive 정책 구성](hdinsight-domain-joined-run-hive.md)을 참조하세요.
* SSH tooconnect tooDomain에 가입 된 HDInsight 클러스터를 사용 하 여 참조 [SSH Linux, Unix, 또는 OS X에서 HDInsight의 Hadoop Linux 기반를 사용](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)합니다.

