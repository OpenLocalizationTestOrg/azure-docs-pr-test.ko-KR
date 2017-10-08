---
title: "가상 네트워크-Azure HDInsight aaaExtend | Microsoft Docs"
description: "어떻게 toouse Azure 가상 네트워크 tooconnect HDInsight tooother 클라우드 리소스 또는 데이터 센터의 리소스에 알아봅니다"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a>Azure Virtual Network를 사용하여 Azure HDInsight 확장

자세한 내용은 방법 toouse HDInsight와는 [Azure 가상 네트워크](../virtual-network/virtual-networks-overview.md)합니다. Azure 가상 네트워크를 사용 하 여 다음 시나리오는 hello 수 있습니다.

* 온-프레미스 네트워크에서 직접 tooHDInsight를 연결 합니다.

* HDInsight toodata 연결 된 Azure 가상 네트워크에 저장 합니다.

* 직접 넘는 공개적으로 사용할 수 없는 Hadoop 서비스 액세스 방법에 인터넷 hello 합니다. 예를 들어 Kafka Api 또는 hello HBase Java API입니다.

> [!WARNING]
> hello이이 문서의 정보에에서는 TCP/IP 네트워킹 이해를 해야 합니다. TCP/IP 네트워킹 잘 모르는 경우 tooproduction 네트워크 수정 하기 전에 장애가 있는 사용자와 파트너가 해야 합니다.

## <a name="planning"></a>계획

hello 다음은 가상 네트워크의 tooinstall HDInsight를 계획할 때 대답 해야 하는 hello 질문입니다.

* 기존 가상 네트워크에 HDInsight tooinstall 필요 한가요? 아니면 새 네트워크를 만드나요?

    기존 가상 네트워크를 사용 하는 경우 HDInsight를 설치 하기 전에 toomodify hello 네트워크 구성을 할 수 있습니다. 자세한 내용은 참조 hello [HDInsight tooan 기존 가상 네트워크 추가](#existingvnet) 섹션.

* 온-프레미스 네트워크 또는 tooconnect hello 가상 네트워크 HDInsight tooanother 가상 네트워크를 포함 하 시겠습니까?

    tooeasily 작업 네트워크를 통해 리소스를 리소스와 필요한 사용자 지정 DNS toocreate 및 DNS 전달 구성 될 수 있습니다. 자세한 내용은 참조 hello [여러 네트워크 연결](#multinet) 섹션.

* Toorestrict/리디렉션 원하는 인바운드 또는 아웃 바운드 트래픽 tooHDInsight?

    HDInsight은 hello Azure 데이터 센터에서 특정 IP 주소와 통신을 제한 해야 있습니다. 또한 클라이언트 통신에 방화벽을 통해 허용해야 하는 여러 포트가 있습니다. 자세한 내용은 참조 hello [네트워크 트래픽을 제어](#networktraffic) 섹션.

## <a id="existingvnet"></a>HDInsight tooan 기존 가상 네트워크 추가

이 섹션 toodiscover을 어떻게 hello 단계를 사용 하 여 Azure 가상 네트워크를 기존 새 HDInsight tooan tooadd 합니다.

> [!NOTE]
> 기존 HDInsight 클러스터를 가상 네트워크에 추가할 수 없습니다.

1. 사용 하는 기본 리소스 관리자 배포 모델 hello 가상 네트워크에 대 한?

    HDInsight 3.4 이상에는 리소스 관리자 가상 네트워크가 필요합니다. 이전 버전의 HDInsightㅇ는 클래식 가상 네트워크가 필요했습니다.

    기존 네트워크 클래식 가상 네트워크 인 경우 다음 리소스 관리자 가상 네트워크를 만들고 해야 다음 두 hello를 연결 합니다. [클래식 Vnet toonew Vnet 연결](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md)합니다.

    조인, hello 리소스 관리자 네트워크에 설치 하는 HDInsight hello 클래식 네트워크 리소스와 상호 작용할 수 있습니다.

2. 강제 터널링을 사용하나요? 강제 터널링 하는 것은 검사에 대 한 아웃 바운드 인터넷 트래픽을 tooa 장치를 강제로 수행 하는 서브넷 설정 및 로깅입니다. HDInsight는 강제 터널링을 지원하지 않습니다. 서브넷에 HDInsight를 설치하기 전에 강제 터널링을 제거하거나 HDInsight에 대해 새 서브넷을 만듭니다.

3. 사용 합니까 네트워크 보안 그룹, 사용자 정의 경로 또는 가상 네트워크 어플라이언스에 toorestrict 트래픽 내부 또는 외부로 가상 네트워크 hello?

    관리 되는 서비스로 HDInsight hello Azure 데이터 센터에 대 한 무제한 액세스 tooseveral IP 주소가 필요합니다. 이러한 IP 주소와 통신을 tooallow 모든 기존 네트워크 보안 그룹 또는 사용자 정의 경로 업데이트 합니다.

    HDInsight는 다양한 포트를 사용하는 여러 서비스를 호스팅합니다. 트래픽이 toothese 포트를 차단 하지 않습니다. 가상 어플라이언스 방화벽을 통해 포트 tooallow 목록이 참조 hello [보안](#security) 섹션.

    toofind 기존 보안 구성에 따라 Azure PowerShell 또는 Azure CLI 명령을 사용 하 여 hello:

    * 네트워크 보안 그룹

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        자세한 내용은 참조 hello [네트워크 보안 그룹 문제 해결](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) 문서.

        > [!IMPORTANT]
        > 네트워크 보안 그룹 규칙은 규칙 우선 순위에 따라 적용됩니다. hello 트래픽 패턴과 일치 하는 hello 첫 번째 규칙을 적용 하 고 해당 트래픽을 에서만 적용 됩니다. 순서에서 가장 높은 tooleast 허용 되는 규칙입니다. 자세한 내용은 참조 hello [네트워크 보안 그룹과 네트워크 트래픽 필터](../virtual-network/virtual-networks-nsg.md) 문서.

    * 사용자 정의 경로

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        자세한 내용은 참조 hello [경로 문제를 해결](../virtual-network/virtual-network-routes-troubleshoot-portal.md) 문서.

4. HDInsight 클러스터를 만들고 구성 하는 동안 hello Azure 가상 네트워크를 선택 합니다. Hello 문서 toounderstand hello 클러스터 만들기 프로세스의 단계를 사용 하 여 hello:

    * [HDInsight hello Azure 포털을 사용 하 여 만들기](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [Azure PowerShell을 사용하여 HDInsight 만들기](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [Azure CLI 1.0을 사용하여 HDInsight 만들기](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [Azure Resource Manager 템플릿을 사용하여 HDInsight 만들기](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > 옵션 구성 단계를 tooa 가상 네트워크는 HDInsight를 추가 합니다. Hello 클러스터를 구성할 때 있는지 tooselect hello 가상 네트워크를 수 있습니다.

## <a id="multinet"></a>다중 네트워크 연결

hello 다중 네트워크 구성이 포함 된 가장 큰 문제는 hello 네트워크 간에 이름 확인 합니다.

Azure는 가상 네트워크에 설치된 Azure 서비스에 대한 이름 확인을 제공합니다. 기본 제공 이름 확인이 정규화 된 도메인 이름 (FQDN)을 사용 하 여 리소스를 다음 HDInsight tooconnect toohello를 허용 됩니다.

* 사용할 수 있는 모든 리소스에는 인터넷 hello 합니다. 예를 들어, microsoft.com, google.com.

* 에 hello 동일한 Azure 가상 네트워크에서 hello를 사용 하 여 모든 리소스 __내부 DNS 이름을__ hello 리소스의 합니다. 예를 들어 hello 기본 이름 확인을 사용할 경우 hello 다음은 예제 내부 DNS 이름이 할당된 tooHDInsight 작업자 노드.

    * wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net
    * wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net

    이러한 두 노드는 내부 DNS 이름을 사용하여 서로 직접 통신하고 HDInsight의 다른 노드와 통신할 수 있습니다.

기본 이름 확인 기능 hello 않습니다 __하지__ 조인된 toohello 가상 네트워크에 있는 네트워크에 HDInsight tooresolve hello 리소스 이름에 허용 합니다. 예를 들어, 일반적인 toojoin는 온-프레미스 네트워크 toohello 가상 네트워크입니다. 만 hello 기본 이름 확인을 HDInsight 이름별 hello 온-프레미스 네트워크의 리소스를 액세스할 수 없습니다. hello 반대도 온-프레미스 네트워크의 리소스 이름으로 hello 가상 네트워크의 리소스에 액세스할 수 없습니다 마찬가지입니다.

> [!WARNING]
> 사용자 지정 DNS 서버 hello을 만들고 가상 네트워크 toouse hello를 구성 해야 HDInsight 클러스터를 hello를 만들기 전에 것입니다.

tooenable hello 가상 네트워크와 조인 된 네트워크의 리소스 간에 이름 확인을 hello 다음 작업을 수행 해야 합니다.

1. Hello tooinstall HDInsight을 계획 하는 Azure 가상 네트워크에서에서 사용자 지정 DNS 서버를 만듭니다.

2. Hello 가상 네트워크 toouse hello 사용자 지정 DNS 서버를 구성 합니다.

3. Azure 가상 네트워크에 대 한 DNS 접미사를 할당 하는 hello를 찾습니다. 이 값이 너무 유사`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`합니다. Hello DNS 접미사를 찾는 방법에 대 한 정보를 참조 hello [예제: 사용자 지정 DNS](#example-dns) 섹션.

4. Hello DNS 서버 간에 전달을 구성 합니다. hello 구성 hello 유형의 원격 네트워크에 따라 달라 집니다.

    * Hello 원격 네트워크는 온-프레미스 네트워크를 DNS를 다음과 같이 구성 합니다.
        
        * __사용자 지정 DNS__ hello 가상 네트워크) (에:

            * Hello 가상 네트워크 toohello Azure 재귀 확인자 (168.63.129.16)의 hello DNS 접미사에 대 한 요청을 전달 합니다. Azure는 hello 가상 네트워크의 리소스에 대 한 요청 처리

            * 모든 다른 요청 toohello 온-프레미스 DNS 서버를 전달 합니다. hello 온-프레미스 DNS 처리 다른 모든 이름 확인 요청을 Microsoft.com 같은 인터넷 리소스에 대 한 요청을 포함 합니다.

        * __온-프레미스 DNS__: hello 가상 네트워크 DNS 접미사 toohello 사용자 지정 DNS 서버에 대 한 요청을 전달 합니다. 사용자 지정 DNS 서버 hello toohello Azure 재귀 확인자를 전달합니다.

        이 구성 경로 요청에 대 한 정규화 된 도메인 이름 hello 가상 네트워크 toohello 사용자 지정 DNS 서버 hello DNS 접미사를 포함 하는 합니다. (공용 인터넷 주소)에 다른 모든 요청은 hello 온-프레미스 DNS 서버에서 처리 됩니다.

    * Hello 원격 네트워크는 다른 Azure 가상 네트워크를 DNS를 다음과 같이 구성 합니다.

        * __사용자 지정 DNS(각 가상 네트워크에서)__:

            * Hello 가상 네트워크의 DNS 접미사 hello에 대 한 요청 toohello 사용자 지정 DNS 서버에 전달 됩니다. 각 가상 네트워크에 DNS hello는 해당 네트워크 내에서 리소스를 확인 해야 합니다.

            * 다른 모든 요청 toohello Azure 재귀 확인자를 전달 합니다. hello 재귀 확인자는 로컬 해결 하 고 인터넷 리소스 하는 일을 담당 합니다.

        각 네트워크에 대 한 hello DNS 서버, DNS 접미사에 따라 요청 toohello를 전달합니다. 다른 요청 hello Azure 재귀 확인자를 사용 하 여 확인 됩니다.

    예를 보려면 각 구성 참조 hello [예제: 사용자 지정 DNS](#example-dns) 섹션.

자세한 내용은 참조 hello [Vm 및 역할 인스턴스에 대 한 이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) 문서.

## <a name="directly-connect-toohadoop-services"></a>TooHadoop 서비스에 직접 연결

HDInsight에 대 한 대부분 설명서 hello를 통해 액세스 toohello 클러스터 있다고 가정 합니다. 인터넷 합니다. 예를 들어, https://CLUSTERNAME.azurehdinsight.net에 toohello 클러스터를 연결할 수 있습니다. 이 주소에서 UDRs toorestrict 액세스 hello 인터넷 또는 Nsg를 사용 하는 경우에 사용할 수 없는 hello 공용 게이트웨이 사용 합니다.

tooconnect tooAmbari 및 hello 가상 네트워크를 통해 다른 웹 페이지 단계를 수행 하는 hello를 사용 합니다.

1. hello HDInsight 클러스터 노드의 toodiscover hello 내부 정규화 된 도메인 이름 (FQDN) hello 메서드를 다음 중 하나를 사용 합니다.

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    반환 되는 노드 hello 목록의 hello FQDN hello에 대 한 헤드 노드 찾아 hello Fqdn tooconnect tooAmbari 및 기타 웹 서비스를 사용 합니다. 사용 예를 들어 `http://<headnode-fqdn>:8080` tooaccess Ambari 합니다.

    > [!IMPORTANT]
    > 일부 서비스의 hello 헤드 노드에 호스팅되 한 번에 한 노드에서 활성화만 됩니다. 헤드 노드 하나에서 서비스에 액세스 하면 404 오류를 반환 하는 경우 toohello 다른 헤드 노드를 전환 합니다.

2. toodetermine hello 노드 및 서비스를 사용할 수 있는 포트 참조 hello [HDInsight의 Hadoop 서비스에 의해 사용 되는 포트](./hdinsight-hadoop-port-settings-for-services.md) 문서.

## <a id="networktraffic"></a> 네트워크 트래픽 제어

메서드를 다음 hello를 사용 하 여 Azure 가상 네트워크에서 네트워크 트래픽을 제어할 수 있습니다.

* **네트워크 보안 그룹** (NSG) toofilter 인바운드 및 아웃 바운드 트래픽을 toohello 네트워크를 허용 합니다. 자세한 내용은 참조 hello [네트워크 보안 그룹과 네트워크 트래픽 필터](../virtual-network/virtual-networks-nsg.md) 문서.

    > [!WARNING]
    > HDInsight는 아웃바운드 트래픽을 제한하도록 지원하지 않습니다.

* **사용자 정의 경로** (UDR) hello 네트워크의 리소스 간의 트래픽 흐름 방식을 정의 합니다. 자세한 내용은 참조 hello [사용자 정의 경로 및 IP 전달](../virtual-network/virtual-networks-udr-overview.md) 문서.

* **네트워크 가상 어플라이언스** 방화벽, 라우터 등과 같은 장치의 기능을 hello를 복제 합니다. 자세한 내용은 참조 hello [네트워크 어플라이언스에](https://azure.microsoft.com/solutions/network-appliances) 문서.

HDInsight 관리 되는 서비스로 Azure 클라우드 hello에 대 한 무제한 액세스 tooAzure 상태 및 관리 서비스를 필요합니다. NSG 및 UDR을 사용할 때는 이러한 서비스에서 HDInsight와 계속 통신할 수 있는지 확인해야 합니다.

HDInsight는 여러 포트에서 서비스를 공개합니다. 가상 기기 방화벽을 사용 하는 경우에 이러한 서비스에 사용 되는 포트를 hello의 트래픽을 허용 해야 합니다. 자세한 내용은 hello [필요한 포트] 섹션을 참조 합니다.

### <a id="hdinsight-ip"></a> 네트워크 보안 그룹 및 사용자 정의 경로가 있는 HDInsight

사용 하려는 경우 **네트워크 보안 그룹** 또는 **사용자 정의 경로** toocontrol 네트워크 트래픽 hello 동작 HDInsight를 설치 하기 전에 다음을 수행 하십시오.

1. Hello Azure 지역 toouse HDInsight에 대 한 계획을 식별 합니다.

2. HDInsight에서 요구 하는 hello IP 주소를 식별 합니다. 자세한 내용은 참조 hello [HDInsight에 필요한 IP 주소](#hdinsight-ip) 섹션.

3. 만들기 또는 수정 hello 네트워크 보안 그룹 또는 tooinstall HDInsight를 계획 하는 hello 서브넷에 대 한 사용자 정의 경로에 있습니다.

    * __네트워크 보안 그룹__: 허용 __인바운드__ 포트에서 트래픽을 __443__ hello IP 주소의 기능과 동일에서 합니다.
    * __사용자 정의 경로__: 경로 tooeach IP 주소를 만들고 hello 설정 __다음 홉 형식__ too__Internet__ 합니다.

네트워크 보안 그룹 또는 사용자 정의 된 경로에 대 한 자세한 내용은 hello 설명서를 참조 하세요.

* [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md)

* [사용자 정의 경로](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a>강제 터널링

강제 터널링은 하나의 사용자 정의 라우팅 구성 강제 tooa 특정 네트워크 또는 온-프레미스 네트워크와 같은 위치에서 서브넷의에서 모든 트래픽이입니다. HDInsight는 강제 터널링을 지원하지 __않습니다.__

## <a id="hdinsight-ip"></a> 필수 IP 주소

> [!IMPORTANT]
> Azure health hello 및 관리 서비스 수 toocommunicate HDInsight와 이어야 합니다. 네트워크 보안 그룹 또는 사용자 정의 경로 사용 하는 경우 트래픽을 hello에서 이러한 서비스 tooreach HDInsight에 대 한 IP 주소를 허용 합니다.
>
> 네트워크 보안 그룹 또는 사용자 정의 경로 toocontrol 트래픽을 사용 하지 않는 경우에이 섹션을 무시할 수 있습니다.

네트워크 보안 그룹 또는 사용자 정의 경로 사용 하는 경우에 hello Azure 상태 및 관리 서비스 tooreach HDInsight에서 트래픽을 허용 해야 합니다. 사용 하 여 hello 다음 단계 toofind hello IP 주소를 허용 해야 합니다.

1. 항상 트래픽을 hello 다음 IP 주소를 허용 해야 합니다.

    | IP 주소 | 허용되는 포트 | 방향 |
    | ---- | ----- | ----- |
    | 168.61.49.99 | 443 | 인바운드 |
    | 23.99.5.239 | 443 | 인바운드 |
    | 168.61.48.131 | 443 | 인바운드 |
    | 138.91.141.162 | 443 | 인바운드 |

2. HDInsight 클러스터에 hello 영역을 다음 중 하나에 있으면 hello 지역에 대해 나열 된 hello IP 주소에서 트래픽을 허용 해야 합니다.

    > [!IMPORTANT]
    > 사용 하는 Azure 지역 hello 나열 되지 않으면 사용만 hello 1 단계에서 네 개의 IP 주소입니다.

    | 국가 | 지역 | 허용된 IP 주소 | 허용되는 포트 | 방향 |
    | ---- | ---- | ---- | ---- | ----- |
    | 아시아 | 동아시아 | 23.102.235.122</br>52.175.38.134 | 443 | 인바운드 |
    | &nbsp; | 동남아시아 | 13.76.245.160</br>13.76.136.249 | 443 | 인바운드 |
    | 오스트레일리아 | 오스트레일리아 동부 | 104.210.84.115</br>13.75.152.195 | 443 | 인바운드 |
    | &nbsp; | 오스트레일리아 남동부 | 13.77.2.56</br>13.77.2.94 | 443 | 인바운드 |
    | 브라질 | 브라질 남부 | 191.235.84.104</br>191.235.87.113 | 443 | 인바운드 |
    | 캐나다 | 캐나다 동부 | 52.229.127.96</br>52.229.123.172 | 443 | 인바운드 |
    | &nbsp; | 캐나다 중부 | 52.228.37.66</br>52.228.45.222 | 443 | 인바운드 |
    | 중국 | 중국 북부 | 42.159.96.170</br>139.217.2.219 | 443 | 인바운드 |
    | &nbsp; | 중국 동부 | 42.159.198.178</br>42.159.234.157 | 443 | 인바운드 |
    | 유럽 | 북유럽 | 52.164.210.96</br>13.74.153.132 | 443 | 인바운드 |
    | &nbsp; | 서유럽| 52.166.243.90</br>52.174.36.244 | 443 | 인바운드 |
    | 독일 | 독일 중부 | 51.4.146.68</br>51.4.146.80 | 443 | 인바운드 |
    | &nbsp; | 독일 북동부 | 51.5.150.132</br>51.5.144.101 | 443 | 인바운드 |
    | 인도 | 인도 중부 | 52.172.153.209</br>52.172.152.49 | 443 | 인바운드 |
    | 일본 | 일본 동부 | 13.78.125.90</br>13.78.89.60 | 443 | 인바운드 |
    | &nbsp; | 일본 서부 | 40.74.125.69</br>138.91.29.150 | 443 | 인바운드 |
    | 한국 | 한국 중부 | 52.231.39.142</br>52.231.36.209 | 433 | 인바운드 |
    | &nbsp; | 한국 남부 | 52.231.203.16</br>52.231.205.214 | 443 | 인바운드
    | 영국 | 영국 서부 | 51.141.13.110</br>51.141.7.20 | 443 | 인바운드 |
    | &nbsp; | 영국 남부 | 51.140.47.39</br>51.140.52.16 | 443 | 인바운드 |
    | 미국 | 미국 중부 | 13.67.223.215</br>40.86.83.253 | 443 | 인바운드 |
    | &nbsp; | 미국 중북부 | 157.56.8.38</br>157.55.213.99 | 443 | 인바운드 |
    | &nbsp; | 미국 중서부 | 52.161.23.15</br>52.161.10.167 | 443 | 인바운드 |
    | &nbsp; | 미국 서부 2 | 52.175.211.210</br>52.175.222.222 | 443 | 인바운드 |

    Hello IP에 대 한 정보에 대 한 Azure Government toouse 주소에 대 한 참조 hello [Azure Government Intelligence + 분석](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) 문서.

3. 가상 네트워크에서 사용자 지정 DNS 서버를 사용하는 경우 __168.63.129.16__에서의 액세스도 허용해야 합니다. 이 주소는 Azure 재귀 확인자입니다. 자세한 내용은 참조 hello [Vm 및 역할에 대 한 이름 확인 인스턴스](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) 문서.

자세한 내용은 참조 hello [네트워크 트래픽을 제어](#networktraffic) 섹션.

## <a id="hdinsight-ports"></a> 필수 포트

네트워크를 사용 하려는 경우 **가상 어플라이언스 방화벽** toosecure hello 가상 네트워크 포트를 수행 하는 hello에 아웃 바운드 트래픽을 허용 해야 합니다.

* 53
* 443
* 1433
* 11000-11999
* 14000-14999

특정 서비스에 대 한 포트 목록이 참조 hello [HDInsight의 Hadoop 서비스에 의해 사용 되는 포트](hdinsight-hadoop-port-settings-for-services.md) 문서.

가상 어플라이언스에 대 한 방화벽 규칙에 대 한 자세한 내용은 참조 hello [가상 어플라이언스 시나리오](../virtual-network/virtual-network-scenario-udr-gw-nva.md) 문서.

## <a id="hdinsight-nsg"></a>예제: HDInsight에서 네트워크 보안 그룹

이 섹션의 예제 hello hello로 HDInsight toocommunicate를 허용 하는 Azure 관리 서비스 toocreate 네트워크 보안 그룹을 규칙 하는 방법을 보여 줍니다. Hello 예제를 사용 하기 전에 hello 사용 하는 Azure 지역에 대 한 hello IP 주소 toomatch hello 것을 조정 합니다. Hello에서이 정보를 찾을 수 있습니다 [네트워크 보안 그룹 및 사용자 정의 경로 포함 하는 HDInsight](#hdinsight-ip) 섹션.

### <a name="azure-resource-management-template"></a>Azure Resource Management 템플릿

hello 다음 리소스 관리 템플릿을 만듭니다 인바운드 트래픽을 제한 하지만 HDInsight에 필요한 hello IP 주소에서의 트래픽을 허용 하는 가상 네트워크. 또한이 템플릿은 hello 가상 네트워크에는 HDInsight 클러스터를 만듭니다.

* [보안 Azure Virtual Network 및 HDInsight Hadoop 클러스터 배포](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> 이 예제에서는 toomatch hello 사용 하는 Azure 지역에서에서 사용 하는 hello IP 주소를 변경 합니다. Hello에서이 정보를 찾을 수 있습니다 [네트워크 보안 그룹 및 사용자 정의 경로 포함 하는 HDInsight](#hdinsight-ip) 섹션.

### <a name="azure-powershell"></a>Azure PowerShell

다음 PowerShell 스크립트 toocreate 인바운드 트래픽을 제한 하 고 hello 트래픽을 hello 유럽 북부 지역에 대 한 IP 주소를 허용 하는 가상 네트워크는 hello를 사용 합니다.

> [!IMPORTANT]
> 이 예제에서는 toomatch hello 사용 하는 Azure 지역에서에서 사용 하는 hello IP 주소를 변경 합니다. Hello에서이 정보를 찾을 수 있습니다 [네트워크 보안 그룹 및 사용자 정의 경로 포함 하는 HDInsight](#hdinsight-ip) 섹션.

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> 이 예제에서는 tooadd 규칙 tooallow hello 필요한 IP 주소에서 트래픽을 인바운드 하는 방법을 보여 줍니다. 규칙 toorestrict 포함 하지 않으므로 다른 소스에서 인바운드 액세스 합니다.
>
> 다음 예제는 hello tooenable SSH hello 인터넷에서에서 액세스 하는 방법을 보여 줍니다.
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a>Azure CLI

다음 단계 toocreate 인바운드 트래픽을 제한 하지만 HDInsight에 필요한 hello IP 주소에서의 트래픽을 허용 하는 가상 네트워크는 hello를 사용 합니다.

1. 새 네트워크 보안 그룹 이라는 명령 toocreate 다음 사용 하 여 hello `hdisecure`합니다. 대체 **RESOURCEGROUPNAME** hello Azure 가상 네트워크를 포함 하는 hello 리소스 그룹을 사용 합니다. 대체 **위치** hello 위치 (지역)와 해당 hello 그룹에서 만든 합니다.

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    Hello 그룹을 만든 후 hello 새 그룹에 정보가 나타납니다.

2. Hello tooadd 규칙 toohello 새 네트워크 보안 그룹 hello Azure HDInsight 상태 및 관리 서비스에서에서 포트 443에서 인바운드 통신을 허용 하는 다음을 사용 합니다. 대체 **RESOURCEGROUPNAME** hello Azure 가상 네트워크를 포함 하는 hello 리소스 그룹의 hello 이름으로 합니다.

    > [!IMPORTANT]
    > 이 예제에서는 toomatch hello 사용 하는 Azure 지역에서에서 사용 하는 hello IP 주소를 변경 합니다. Hello에서이 정보를 찾을 수 있습니다 [네트워크 보안 그룹 및 사용자 정의 경로 포함 하는 HDInsight](#hdinsight-ip) 섹션.

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. 이 네트워크 보안 그룹을 다음 명령을 사용 하 여 hello에 대 한 tooretrieve hello의 고유 식별자:

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    이 명령은 텍스트 다음 값 비슷한 toohello를 반환 합니다.

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    Hello 예상 결과 얻지 못할 경우 hello 명령에서 id 주위 큰따옴표를 사용 합니다.

4. 다음 명령은 tooapply hello 네트워크 보안 그룹 tooa 서브넷 hello를 사용 합니다. Hello 대체 __GUID__ 및 __RESOURCEGROUPNAME__ hello 이전 단계에서 반환 된 것과 hello 사용 하 여 값입니다. 대체 __VNETNAME__ 및 __SUBNETNAME__ hello 가상 네트워크 이름 및 toocreate 서브넷 이름을 사용 합니다.

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    이 명령은 완료 되 면 hello 가상 네트워크에 HDInsight를 설치할 수 있습니다.

> [!IMPORTANT]
> 이러한 단계는 access toohello HDInsight 상태 및 관리 서비스에 hello Azure 클라우드만 엽니다. 모든 다른 액세스 toohello HDInsight 클러스터에서 가상 네트워크 외부 hello 차단 됩니다. tooenable 액세스 hello 가상 네트워크 외부에서 추가 네트워크 보안 그룹 규칙을 추가 해야 합니다.
>
> 다음 예제는 hello tooenable SSH hello 인터넷에서에서 액세스 하는 방법을 보여 줍니다.
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <a id="example-dns"></a> 예제: DNS 구성

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a>가상 네트워크와 연결된 온-프레미스 네트워크 간에 이름 확인

이 예제에서는 다음 가정을 hello:

* Azure 가상 네트워크 VPN 게이트웨이 사용 하 여 연결 된 tooan 온-프레미스 네트워크를 해야 합니다.

* hello 가상 네트워크의 사용자 지정 DNS 서버 hello hello 운영 체제로 Linux 또는 Unix 실행 합니다.

* [바인딩](https://www.isc.org/downloads/bind/) hello 사용자 지정 DNS 서버에 설치 되어 있습니다.

Hello 사용자 지정 DNS 서버 hello 가상 네트워크에서:

1. Hello 가상 네트워크의 Azure PowerShell 또는 Azure CLI toofind hello DNS 접미사를 사용 합니다.

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Hello 사용자 지정 DNS 서버에서 가상 네트워크 hello에 대 한 hello의 hello 콘텐츠로 텍스트를 다음 hello를 사용 하 여 `/etc/bind/named.conf.local` 파일:

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    Hello 대체 `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` 가상 네트워크의 DNS 접미사 hello 사용 하 여 값입니다.

    이 구성은 Azure 재귀 해결 프로그램을 toohello hello 가상 네트워크의 DNS 접미사 hello에 대 한 모든 DNS 요청을 라우팅합니다.

2. Hello 사용자 지정 DNS 서버에서 가상 네트워크 hello에 대 한 hello의 hello 콘텐츠로 텍스트를 다음 hello를 사용 하 여 `/etc/bind/named.conf.options` 파일:

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Hello 대체 `10.0.0.0/16` 가상 네트워크의 IP 주소 범위 hello 사용 하 여 값입니다. 이 항목으로 이 범위 내의 주소로 이름 확인 요청이 가능합니다.

    * Hello 온-프레미스 네트워크 toohello의 hello IP 주소 범위 추가 `acl goodclients { ... }` 섹션.  항목은 hello 온-프레미스 네트워크에 리소스에서 이름 확인 요청을 허용합니다.
    
    * Hello 값을 대체 `192.168.0.1` 온-프레미스 DNS 서버의 hello IP 주소를 사용 합니다. 이 항목에는 모든 DNS 요청 toohello 온-프레미스 DNS 서버를 라우팅합니다.

3. toouse hello 구성 바인딩을 다시 시작 합니다. 예: `sudo service bind9 restart`.

4. 조건부 전달자 toohello 온-프레미스 DNS 서버를 추가 합니다. 단계 1 toohello 사용자 지정 DNS 서버에서 DNS 접미사 hello에 대 한 hello 조건 전달자 toosend 요청을 구성 합니다.

    > [!NOTE]
    > 방법에 대 한 구체적인 정보에 대 한 DNS 소프트웨어에 대 한 hello 설명서를 참조 하십시오. tooadd 조건 전달자 합니다.

다음이 단계를 완료 한 후 tooresources 정규화 된 도메인 이름 (FQDN)을 사용 하 여 두 네트워크에 연결할 수 있습니다. 이제 hello 가상 네트워크로 HDInsight를 설치할 수 있습니다.

### <a name="name-resolution-between-two-connected-virtual-networks"></a>두 개의 연결된 가상 네트워크 간의 이름 확인

이 예제에서는 다음 가정을 hello:

* VPN 게이트웨이 또는 피어링을 사용하여 연결된 두 Azure Virtual Networks가 있습니다.

* 두 네트워크에에서 사용자 지정 DNS 서버 hello hello 운영 체제로 Linux 또는 Unix 실행 합니다.

* [바인딩](https://www.isc.org/downloads/bind/) hello 사용자 지정 DNS 서버에 설치 됩니다.

1. 두 가상 네트워크의 Azure PowerShell 또는 Azure CLI toofind hello DNS 접미사를 사용 합니다.

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. 콘텐츠로 사용 hello hello 텍스트를 다음으로 사용 하 여 hello `/etc/bind/named.config.local` hello 사용자 지정 DNS 서버에는 파일입니다. 두 가상 네트워크에서 사용자 지정 DNS 서버 hello에 이와 같이 변경 합니다.

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    Hello 대체 `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` hello의 hello DNS 접미사를 사용 하 여 값 __다른__ 가상 네트워크입니다. 이 항목의 hello 원격 네트워크 toohello hello DNS 접미사에 대 한 요청을 라우팅하는 네트워크에 있는 사용자 지정 DNS 합니다.

3. 콘텐츠로 사용 hello hello 텍스트를 다음 hello를 사용 하 여 hello 사용자 지정 DNS 서버에서 두 가상 네트워크에 `/etc/bind/named.conf.options` 파일:

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Hello 대체 `10.0.0.0/16` 및 `10.1.0.0/16` 값 hello ip 주소 범위가 가상 네트워크의 합니다. 이 항목을 사용 하면 각 네트워크의 리소스의 DNS 서버 hello toomake 요청 합니다.

    Hello 가상 네트워크 (예를 들어, microsoft.com) hello DNS 접미사에 대 한 하지 않은 모든 요청은 hello Azure 재귀 확인자에 의해 처리 됩니다.

4. toouse hello 구성 바인딩을 다시 시작 합니다. 예를 들어, 두 DNS 서버에서 `sudo service bind9 restart`입니다.

다음이 단계를 완료 한 후 tooresources 정규화 된 도메인 이름 (FQDN)을 사용 하 여 hello 가상 네트워크에 연결할 수 있습니다. 이제 hello 가상 네트워크로 HDInsight를 설치할 수 있습니다.

## <a name="next-steps"></a>다음 단계

* HDInsight tooconnect tooan 온-프레미스 네트워크 구성의 종단 간 예제를 참조 하십시오. [HDInsight 연결 tooan 온-프레미스 네트워크](./connect-on-premises-network.md)합니다.

* Azure 가상 네트워크에 대 한 자세한 내용은 참조 hello [Azure 가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)합니다.

* 네트워크 보안 그룹에 대한 자세한 내용은 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md)을 참조하세요.

* 사용자 정의 경로에 대한 자세한 내용은 [사용자 정의 경로 및 IP 전달](../virtual-network/virtual-networks-udr-overview.md)을 참조하세요.