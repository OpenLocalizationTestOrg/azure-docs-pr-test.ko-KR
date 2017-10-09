---
title: "aaaCreate HBase 클러스터를 Azure 가상 네트워크-| Microsoft Docs"
description: "Azure HDInsight에서 HBase 사용 시작 Azure 가상 네트워크에서 toocreate HDInsight HBase 클러스터 하는 방법에 대해 알아봅니다."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a>Azure Virtual Network의 HDInsight에서 HBase 클러스터 만들기
toocreate Azure HDInsight HBase 클러스터 하는 방법에 대해 알아봅니다는 [Azure 가상 네트워크][1]합니다.

가상 네트워크 통합 HBase 클러스터 동일한 가상 네트워크로 응용 프로그램 이므로 배포 된 toohello 수 있는 응용 프로그램 HBase와 직접 통신할 수 있습니다. hello 이점은 다음과 같습니다.

* Hello 웹 응용 프로그램 toohello 노드 HBase Java 원격 프로시저를 통해 통신할 수 있도록 하는 hello HBase 클러스터의 직접 연결 (RPC) Api를 호출 합니다.
* 트래픽이 여러 게이트웨이 및 부하 분산 장치를 통과하지 않도록 하여 성능을 향상시킵니다.
* hello 기능 tooprocess의에서 중요 한 정보는 공용 끝점을 노출 하지 않고 더 안전 하 게 합니다.

### <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* **Azure PowerShell이 포함된 워크스테이션**. [Azure PowerShell 설치 및 사용](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/)을 참조하세요.

## <a name="create-hbase-cluster-into-virtual-network"></a>가상 네트워크에 HBase 클러스터 만들기
이 섹션에서는 hello 종속 Azure 저장소 계정을 사용 하 여 Azure 가상 네트워크에서 사용 하 여 Linux 기반 HBase 클러스터를 만들는 [Azure 리소스 관리자 템플릿](../azure-resource-manager/resource-group-template-deploy.md)합니다. 다른 클러스터 생성 방법 및 참조 hello 설정을 이해, [만들 HDInsight 클러스터](hdinsight-hadoop-provision-linux-clusters.md)합니다. HDInsight 클러스터를 템플릿 toocreate Hadoop을 사용 하는 방법에 대 한 자세한 내용은 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 HDInsight 클러스터를 만들기 Hadoop](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

> [!NOTE]
> 일부 속성 hello 서식 파일에 하드 코드 되어 있습니다. 예:
>
> * **위치**: 미국 동부 2
> * **클러스터 버전**: 3.5
> * **클러스터 작업자 노드 수**: 2
> * **기본 저장소 계정**: 고유한 문자열
> * **가상 네트워크 이름**: &lt;클러스터 이름>-vnet
> * **가상 네트워크 주소 공간**: 10.0.0.0/16
> * **서브넷 이름**: subnet1
> * **서브넷 주소 범위**: 10.0.0.0/24
>
> &lt;클러스터 이름 > hello 서식 파일을 사용 하는 경우 제공 하는 hello 클러스터 이름 아래 템플릿으로 바뀝니다.
>
>

1. Hello 이미지 tooopen hello 템플릿을 hello Azure 포털에서에서 다음을 클릭 합니다. hello 서식 파일에 있는 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/)합니다.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Hello에서 **사용자 지정 배포** 블레이드에서 hello 다음과 같은 속성을 입력 합니다.

   * **구독**: 사용 된 Azure 구독 toocreate hello HDInsight 클러스터를 선택 하 고, hello 종속 저장소 계정, Azure 가상 네트워크를 hello 합니다.
   * **리소스 그룹**: **새로 만들기**를 선택하고 새 리소스 그룹 이름을 지정합니다.
   * **위치**: hello 리소스 그룹에 대 한 위치를 선택 합니다.
   * **ClusterName**: hello Hadoop 클러스터 toobe 생성에 대 한 이름을 입력 합니다.
   * **로그인 이름 및 암호를 클러스터**: hello 기본 로그인 이름은 **admin**합니다.
   * **SSH 사용자 이름 및 암호**: hello 기본 사용자 이름은 **sshuser**합니다.  이름은 변경할 수 있습니다.
   * **Toohello 약관 hello 위에서 설명한 동의**: (선택)
3. **구매**를 클릭합니다. 클러스터에 대 한 약 20 분 toocreate 걸립니다. Hello 클러스터를 만든 후 클릭할 수 있는 hello 포털 tooopen hello 클러스터 블레이드 것입니다.

Hello 자습서를 완료 한 후 toodelete hello 클러스터를 할 수 있습니다. HDInsight를 사용하면 데이터가 Azure 저장소에 저장되기 때문에 클러스터를 사용하지 않을 때 안전하게 삭제할 수 있습니다. HDInsight 클러스터를 사용하지 않는 기간에도 요금이 청구됩니다. Hello 클러스터에 대 한 hello 요금이 저장소에 대 한 hello 요금 보다 많은 배 더 많은 경우 이렇게 하면 경제 toodelete 클러스터 사용에서 되지 않은 있습니다. 클러스터를 삭제할 경우의 hello 지침은 참조 [를 사용 하 여 HDInsight의 Hadoop 관리 클러스터에 Azure 포털 hello](hdinsight-administer-use-management-portal.md#delete-clusters)합니다.

새 HBase 클러스터를 사용 하는 toobegin hello 프로시저에 사용할 수 있습니다 [HDInsight에서 Hadoop으로 HBase를 사용 하 여 시작](hdinsight-hbase-tutorial-get-started.md)합니다.

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a>HBase Java RPC Api를 사용 하 여 toohello HBase 클러스터를 연결 합니다.
1. 인프라에는 서비스 (IaaS) 가상 컴퓨터로 만드는 hello 동일한 Azure 가상 네트워크와 동일한 서브넷 hello 합니다. 새 IaaS 가상 컴퓨터를 만드는 지침은 [Windows Server를 실행하는 가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md)를 참조하세요. 이 문서의 hello 단계를 수행 하는 경우 다음 hello 네트워크 구성에 대 한 값에는 hello를 사용 해야 합니다.

   * **가상 네트워크**: &lt;클러스터 이름>-vnet
   * **서브넷**: subnet1

   > [!IMPORTANT]
   > 대체 &lt;클러스터 이름 > 이전 단계에서 hello HDInsight 클러스터를 만들 때 사용한 hello 이름의 합니다.
   >
   >

   이러한 값을 사용 하 여 hello 가상 컴퓨터가 배치 된 hello에 동일한 가상 네트워크 및 서브넷 hello HDInsight 클러스터와 합니다. 이 구성은 수 있도록 toodirectly 서로 통신 합니다. 빈 가장자리 노드에 HDInsight 클러스터는 방식으로 toocreate 합니다. hello 가장자리 노드 사용된 toomanage hello 클러스터가 될 수 있습니다.  자세한 내용은 [HDInsight에서 빈 에지 노드 사용](hdinsight-apps-use-edge-node.md)을 참조하세요.

2. Java 응용 프로그램 tooconnect tooHBase를 원격으로 사용 하는 경우에 hello 정규화 된 도메인 이름 (FQDN)를 사용 해야 합니다. toodetermine이 hello HBase 클러스터의 hello 연결별 DNS 접미사를 가져와야 합니다. toodo, hello 메서드를 다음 중 하나를 사용할 수 있습니다.

   * 웹 브라우저 toomake Ambari 호출을 사용 합니다.

     Toohttps 찾아보기: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > 호스트 /? minimal_response = true입니다. Hello DNS 접미사와 JSON 파일을 설정합니다.
   * Hello Ambari 웹 사이트를 사용 합니다.

     1. 너무 찾아보기 https://&lt;ClusterName >. azurehdinsight.net 합니다.
     2. 클릭 **호스트** hello 상단 메뉴에서 합니다.
   * Curl toomake REST 호출을 사용 합니다.

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     반환 된 hello 개체 JSON (JavaScript Notation) 데이터에서 hello "host_name" 항목을 찾습니다. Hello 클러스터의 노드 hello에 대 한 FQDN hello를 포함합니다. 예:

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     hello 클러스터 이름으로 시작 하는 hello 도메인 이름 부분은 hello hello DNS 접미사입니다. 예를 들면 mycluster.b1.cloudapp.net과 같습니다.
   * Azure PowerShell 사용

     다음 Azure PowerShell 스크립트 tooregister hello 사용 하 여 hello **Get ClusterDetail** 함수를 사용 하는 tooreturn hello DNS 접미사를 일 수 있습니다.

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     Hello를 사용 하 여 사용 하 여 hello 다음 명령은 tooreturn hello DNS 접미사 hello Azure PowerShell 스크립트 실행 후 **Get ClusterDetail** 함수입니다. 이 명령을 사용할 때는 HDInsight HBase 클러스터 이름, 관리자 이름 및 관리자 암호를 지정합니다.

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     이 명령은 hello DNS 접미사를 반환합니다. 예를 들면 **yourclustername.b4.internal.cloudapp.net**과 같습니다.


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

가상 컴퓨터를 hello tooverify HBase 클러스터 hello와 통신할 수, hello 명령을 사용 하 여 `ping headnode0.<dns suffix>` hello 가상 컴퓨터에서 합니다. 예를 들면 ping headnode0.mycluster.b1.cloudapp.net을 사용합니다.

toouse Java 응용 프로그램에서이 정보를 참고할 수의 hello 단계 [(Hadoop) HDInsight HBase를 사용 하는 사용 하 여 Maven toobuild Java 응용 프로그램](hdinsight-hbase-build-java-maven.md) toocreate 응용 프로그램입니다. toohave hello 응용 프로그램 tooa 원격 HBase 서버에 연결, hello 수정 **hbase-site.xml** 사육에 대 한 FQDN이 예제에서는 toouse hello에 대 한 파일입니다. 예:

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> Azure 가상 네트워크에서 이름 확인에 대 한 자세한 내용은 방법을 비롯 하 여 toouse 자체 DNS 서버 참조 [이름 확인 (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)합니다.
>
>

## <a name="next-steps"></a>다음 단계
이 자습서에서는 방법에 대해 배웠습니다 toocreate HBase 클러스터입니다. toolearn 더 참조 하십시오.

* [HDInsight 시작](hdinsight-hadoop-linux-tutorial-get-started.md)
* [HDInsight에서 빈 에지 노드 사용](hdinsight-apps-use-edge-node.md)
* [HDInsight에서 HBase 복제 구성](hdinsight-hbase-replication.md)
* [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)
* [HDInsight의 Hadoop에서 HBase 사용 시작](hdinsight-hbase-tutorial-get-started.md)
* [HDInsight에서 HBase를 사용하여 Twitter 데이터 분석](hdinsight-hbase-analyze-twitter-sentiment.md)
* [Virtual Network 개요][vnet-overview]

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "HBase 클러스터를 새 hello에 대 한 프로 비전 정보"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "스크립트 동작 toocustomize HBase 클러스터를 사용 하 여"

[azure-preview-portal]: https://portal.azure.com
