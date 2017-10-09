---
title: "도메인에 가입 된 HDInsight PowerShell-Azure를 사용 하는 클러스터 aaaConfigure | Microsoft Docs"
description: "자세한 내용은 방법 tooset 및 Azure PowerShell을 사용 하 여 도메인에 가입 된 HDInsight 클러스터를 구성 합니다."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a13b2f7a-612d-4800-bc92-7fc0524f3e89
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 49da3439513d1e51171f0f7f7f9c3d967d55cb7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview-using-azure-powershell"></a>Azure PowerShell을 사용하여 도메인 가입 HDInsight 클러스터 구성(미리 보기)
Azure Active Directory (Azure AD)와 tooset Azure HDInsight를 클러스터링 하는 방법에 대해 알아봅니다 및 [Apache 레인저](http://hortonworks.com/apache/ranger/) Azure PowerShell을 사용 하 여 합니다. Azure PowerShell 스크립트는 더 빠른 toomake hello 구성 및 오류 발생 가능성에 제공 됩니다. 도메인에 가입된 HDInsight는 Linux 기반 클러스터에만 구성할 수 있습니다. 자세한 내용은 [도메인에 가입된 HDInsight 클러스터 소개](hdinsight-domain-joined-introduction.md)를 참조하세요.

> [!IMPORTANT]
> 도메인에 가입된 HDInsight에서는 Oozie를 사용할 수 없습니다.

일반적인 도메인에 가입 된 HDInsight 클러스터 구성 단계를 수행 하는 hello 포함 됩니다.

1. Azure AD에 대한 Azure 클래식 VNet을 만듭니다.  
2. Azure AD 및 Azure AD DS를 만들고 구성합니다.
3. 추가 VM toohello 조직 구성 단위를 만들기 위한 클래식 VNet입니다. 
4. Azure AD DS에 대한 조직 구성 단위를 만듭니다.
5. Hello Azure 리소스 관리 모드에서 HDInsight VNet을 만듭니다.
6. Azure AD DS hello에 대 한 역방향 DNS 영역을 설정 합니다.
7. 피어에는 두 개의 Vnet hello 합니다.
8. HDInsight 클러스터 만들기

제공 된 PowerShell 스크립트 hello 3-7 단계를 수행 합니다. 1단계와 2단계는 수동으로 수행해야 합니다.  Toouse Azure PowerShell 되지 원하면 참조 [구성 도메인에 가입 된 HDInsight 클러스터](hdinsight-domain-joined-configure.md)합니다. 

Hello 최종 토폴로지에 대 한 예는 다음과 같습니다.

![도메인에 가입된 HDInsight 토폴로지](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

현재 Azure AD는 클래식 가상 네트워크(VNet)만 지원하고 Linux 기반 HDInsight 클러스터는 Azure Resource Manager 기반 VNet만 지원하므로 HDInsight Azure AD를 통합하려면 두 VNet이 있어야 하고 또 두 VNet을 피어링해야 합니다. Hello 두 배포 모델 간의 hello 비교 내용은 [Azure 리소스 관리자 및 클래식 배포: 배포 모델을 이해 하 고 리소스 상태를 hello](../azure-resource-manager/resource-manager-deployment-model.md)합니다. 두 개의 Vnet hello에 있어야 하는 hello hello Azure AD DS와 동일한 영역입니다.

> [!NOTE]
> 이 자습서에서는 사용자에게 Azure AD가 없다고 가정합니다. 하나를 설정한 경우 2 단계에서 hello 부분을 건너뛸 수 있습니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
Hello 항목 toogo이이 자습서를 통해 다음이 필요 합니다.

* [Azure AD Domain Services](https://azure.microsoft.com/services/active-directory-ds/) 및 [가격 책정](https://azure.microsoft.com/pricing/details/active-directory-ds/) 구조를 숙지합니다.
* 구독이 이 공개 미리 보기에 대한 허용 목록에 추가되었는지 확인합니다. 전자 메일을 전송 하 여 그렇게 할 수 toohdipreview@microsoft.com 구독 ID로
* 도메인의 서명 기관에서 서명한 SSL 인증서가 필요합니다. 보안 LDAP를 구성 하 여 hello 인증서가 필요 합니다. 자체 서명된 인증서는 사용할 수 없습니다.
* Azure PowerShell.  [Azure PowerShell 설치 및 구성](/powershell/azure/overview)을 참조하세요.

## <a name="create-an-azure-classic-vnet-for-your-azure-ad"></a>Azure AD에 대한 Azure 클래식 VNet을 만듭니다.
Hello 지침은 [여기](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic)합니다.

## <a name="create-and-configure-azure-ad-and-azure-ad-ds"></a>Azure AD 및 Azure AD DS를 만들고 구성합니다.
Hello 지침은 [여기](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad)합니다.

## <a name="run-hello-powershell-script"></a>Hello PowerShell 스크립트 실행
hello PowerShell 스크립트에서 다운로드할 수 있습니다 [GitHub](https://github.com/hdinsight/DomainJoinedHDInsight)합니다. Hello zip 파일 압축을 풀고 hello 파일을 로컬로 저장 합니다.

**tooedit hello PowerShell 스크립트**

1. Windows PowerShell ISE 또는 다른 텍스트 편집기를 사용하여 run.ps1을 엽니다.
2. 변수를 다음 hello에 대 한 hello 값을 채웁니다.
   
   * **$SubscriptionName** – hello hello Azure 구독을 저장할 toocreate HDInsight 클러스터의 이름입니다. 이 구독에서 클래식 가상 네트워크를 이미 만든 및 구독에서 hello HDInsight 클러스터에는 Azure 리소스 관리자 가상 네트워크를 만들어야 합니다.
   * **$ClassicVNetName** -hello 클래식 가상 네트워크에 있는 hello Azure AD DS가 포함 되어 있습니다. 이 가상 네트워크는 hello에 있어야 합니다. 위의 제공 되는 동일한 구독 합니다. Hello Azure 포털을 사용 하 고 클래식 포털을 사용 하지이 가상 네트워크를 만들어야 합니다. Hello 명령에서 수행 하는 경우 [구성 도메인에 가입 된 HDInsight 클러스터 (미리 보기)](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic), hello 기본 이름은 contosoaadvnet입니다.
   * **$ClassicResourceGroupName** – hello 클래식 가상 네트워크에 대해 위에서 언급 된 hello 리소스 관리자 그룹 이름입니다. 예를 들어 contosoaadrg과 같습니다. 
   * **$ArmResourceGroupName** –는, 리소스 그룹 이름은 hello toocreate hello HDInsight 클러스터를 구축할 합니다. Hello를 사용할 수 있습니다 $ArmResourceGroupName와 동일한 리소스 그룹입니다.  Hello 리소스 그룹이 없으면 hello 스크립트 hello 리소스 그룹을 만듭니다.
   * **$ArmVNetName** -toocreate hello HDInsight 클러스터 원하는 hello 리소스 관리자 가상 네트워크 이름입니다. 이 가상 네트워크는 $ArmResourceGroupName에 배치됩니다.  Hello VNet가 없는 경우 hello PowerShell 스크립트를 만듭니다. 파일이 존재 하는 경우 위에 제공 하는 hello 리소스 그룹의 일부 여야 합니다.
   * **$AddressVnetAddressSpace** – hello 네트워크 주소 공간 hello 리소스 관리자 가상 네트워크에 대 한 합니다. 이 주소 공간을 사용할 수 있는지 확인합니다. 이 주소 공간 hello 클래식 가상 네트워크의 주소 공간에 겹칠 수 없습니다. 예를 들어 "10.1.0.0/16"과 같습니다.
   * **$ArmVnetSubnetName** -tooplace hello HDInsight 클러스터 Vm 원하는 hello 리소스 관리자 가상 네트워크 서브넷 이름입니다. Hello 서브넷이 없는 경우 hello PowerShell 스크립트를 만듭니다. 파일이 존재 하는 경우 위에 제공 하는 hello 가상 네트워크의 일부 여야 합니다.
   * **$AddressSubnetAddressSpace** – hello 네트워크 hello 리소스 관리자 가상 네트워크 서브넷에 대 한 주소 범위입니다. 이 서브넷 주소 범위에서 VM IP 주소는 hello HDInsight 클러스터가 됩니다. 예를 들어 "10.1.0.0/24"와 같습니다.
   * **$ActiveDirectoryDomainName** – hello Azure AD 도메인 이름을 원하는 toojoin hello HDInsight 클러스터에 Vm입니다. 예를 들어 "contoso.onmicrosoft.com"과 같습니다.
   * **$ClusterUsersGroups** – hello toosync toohello HDInsight 클러스터를 원하는 AD의 hello 보안 그룹의 일반 이름입니다. 이 보안 그룹 내의 hello 사용자가 active directory 도메인 자격 증명을 사용 하 여 toohello 클러스터 대시보드에서 수 toolog 됩니다. 이러한 보안 그룹 hello active directory에 존재 해야 합니다. 예를 들어 "hiveusers" 또는 "clusteroperatorusers"과 같습니다.
   * **$OrganizationalUnitName** -hello hello 도메인에 있는 tooplace hello HDInsight 클러스터 Vm을 hello hello 클러스터에서 사용 하는 서비스 사용자의 조직 구성 단위입니다. hello PowerShell 스크립트는 존재 하지 않는 경우이 OU 만들어집니다. 예를 들어 "HDInsightOU"와 같습니다.
3. Hello 변경 내용을 저장 합니다.

**toorun hello 스크립트**

1. 관리자 권한으로 **Windows PowerShell**을 실행합니다.
2. Run.ps1의 toohello 폴더를 찾습니다. 
3. Hello 파일 이름을 입력 하 여 hello 스크립트를 실행 하 고 키를 눌러 **ENTER**합니다.  다음과 같은 3개의 로그인 대화 상자가 나타납니다.
   
   1. **TooAzure 클래식 포털에 로그인** -사용할 수 있는 자격 증명을 입력 toosign tooAzure 클래식 포털의. Azure AD와 Azure AD DS 이러한 자격 증명을 사용 하 여 hello를 만들었어야 합니다.
   2. **TooAzure 리소스 관리자 포털에 로그인** -사용할 수 있는 자격 증명을 입력 tooAzure 리소스 관리자 포털에서 toosign 합니다.
   3. **도메인 사용자 이름** – toobe hello HDInsight 클러스터의 관리자를 지정 하는 hello 도메인 사용자 이름의 hello 자격 증명을 입력 합니다. 처음부터 Azure AD를 만든 경우 이 설명서를 사용하여 해당 사용자를 만들어야 합니다. 
      
      > [!IMPORTANT]
      > 이 형식으로 hello 사용자 이름 입력: 
      > 
      > Domainname\username(예: contoso.onmicrosoft.com\clusteradmin)
      > 
      > 
      
      이 사용자 3 권한이 있어야: toojoin 컴퓨터 toohello 제공 Active Directory 도메인. 제공 된 조직 구성 단위; toocreate 서비스 보안 주체 및 hello 내에서 컴퓨터 개체 및 tooadd 역방향 DNS 프록시 규칙입니다.

만드는 역방향 DNS 영역, hello 스크립트 물어봅니다 동안 tooenter 네트워크 id. 이 네트워크 ID hello 리소스 관리자 가상 네트워크의 주소 접두사 여야 합니다. 예를 들어 10.2.0.0/24 리소스 관리자 가상 네트워크 서브넷 주소 공간을 사용 하는 경우 입력 10.2.0.0/24 hello 도구 입력 하 라는 메시지가 hello 네트워크 id입니다. 

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
     * **버전**: Hadoop 2.7.3(HDI 3.5). 도메인에 가입된 HDInsight는 HDInsight 클러스터 버전 3.5에서만 지원됩니다.
     * **클러스터 유형**: PREMIUM
       
       클릭 **선택** toosave hello 변경 합니다.
   * **자격 증명**: hello hello 클러스터 사용자와 hello SSH 사용자 자격 증명을 구성 합니다.
   * **데이터 원본**: 새 저장소 계정을 만들거나 hello hello HDInsight 클러스터에 대 한 기본 저장소 계정으로 기존 저장소 계정을 사용 합니다. hello 위치는 두 개의 Vnet hello와 같을 hello 해야 합니다.  hello 위치 hello HDInsight 클러스터의 hello 위치 이기도합니다.
   * **가격 책정**: hello 클러스터의 작업자 노드 수를 선택 합니다.
   * **고급 구성**: 
     
     * **도메인 가입 및 Vnet/Subnet**: 
       
       * **도메인 설정**: 
         
         * **도메인 이름**: contoso.onmicrosoft.com
         * **도메인 사용자 이름**: 도메인 사용자 이름을 입력합니다. 이 도메인 hello 다음 권한이 있어야 합니다.: toohello 도메인에 컴퓨터 가입 및; 이전에 구성한 hello 조직 구성 단위에 배치 앞서; 구성한 hello 조직 구성 단위 내에서 서비스 사용자 만들기 역방향 DNS 항목을 만듭니다. 이 도메인 사용자는이 도메인에 가입 된 HDInsight 클러스터의 관리자에 게 될 것입니다.
         * **도메인 암호**: hello 도메인 사용자 암호를 입력 합니다.
         * **조직 구성 단위**: hello hello 이전에 구성 하는 OU의 고유 이름을 입력 합니다. 예: OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com
         * **LDAPS URL**: ldaps://contoso.onmicrosoft.com:636
         * **사용자 액세스 그룹**: hello 보안 임의의 사용자가 속한 그룹을 지정 toosync toohello 클러스터입니다. 예: HiveUsers.
           
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
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure-use-powershell/deploy-to-azure.png" alt="Deploy tooAzure"></a>
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
   * **클러스터 사용자 그룹 DN**: "\"CN=HiveUsers,OU=AADDC Users,DC=<DomainName>,DC=onmicrosoft,DC=com\""
   * **LDAPUrl**: ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (Enter hello 도메인 관리자 사용자 이름)
   * **DomainAdminPassword**: (hello 도메인 관리자 사용자 암호 입력)
   * **Toohello 약관 위에서 설명한 동의**: (확인)
   * **Pin toodashboard**: (확인)
3. **구매**를 클릭합니다. **템플릿 배포 배포 중**이라는 제목의 새 타일이 표시됩니다. 클러스터에 대 한 약 20 분 toocreate 걸립니다. Hello 클러스터를 만든 후 클릭할 수 있는 hello 포털 tooopen hello 클러스터 블레이드 것입니다.

Hello 자습서를 완료 한 후 toodelete hello 클러스터를 할 수 있습니다. HDInsight를 사용하면 데이터가 Azure 저장소에 저장되기 때문에 클러스터를 사용하지 않을 때 안전하게 삭제할 수 있습니다. HDInsight 클러스터를 사용하지 않는 기간에도 요금이 청구됩니다. Hello 클러스터에 대 한 hello 요금이 저장소에 대 한 hello 요금 보다 많은 배 더 많은 경우 이렇게 하면 경제 toodelete 클러스터 사용에서 되지 않은 있습니다. 클러스터를 삭제할 경우의 hello 지침은 참조 [를 사용 하 여 HDInsight의 Hadoop 관리 클러스터에 Azure 포털 hello](hdinsight-administer-use-management-portal.md#delete-clusters)합니다.

## <a name="next-steps"></a>다음 단계

* Hive 정책 및 Hive 쿼리 실행에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터에 대한 Hive 정책 구성](hdinsight-domain-joined-run-hive.md)을 참조하세요.
* SSH tooconnect tooDomain에 가입 된 HDInsight 클러스터를 사용 하 여 참조 [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)합니다.

