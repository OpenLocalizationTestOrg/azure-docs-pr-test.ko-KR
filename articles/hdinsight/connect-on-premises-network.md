---
title: "aaaConnect HDInsight tooyour 온-프레미스 네트워크 Azure HDInsight | Microsoft Docs"
description: "Azure 가상 네트워크에서 toocreate HDInsight 클러스터를 방법을 알아보고 tooyour 온-프레미스 네트워크 연결 합니다. 사용자 지정 DNS 서버를 사용 하 여 tooconfigure HDInsight와 온-프레미스 네트워크 간의 이름을 어떻게에 대해 알아봅니다."
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a>HDInsight tooyour 온-프레미스 네트워크에 연결

어떻게 tooconnect HDInsight tooyour 온-프레미스 네트워크 VPN 게이트웨이 및 Azure 가상 네트워크를 사용 하 여에 대해 알아봅니다. 이 문서는 다음에 대한 계획 정보를 제공합니다.

* HDInsight를 사용 하 여 tooyour 연결 하는 Azure 가상 네트워크에서 온-프레미스 네트워크.

* Hello 가상 네트워크와 온-프레미스 네트워크의 DNS 이름 확인을 구성 합니다.

* 네트워크 보안 그룹 toorestrict 인터넷 액세스 tooHDInsight를 구성 합니다.

* HDInsight hello 가상 네트워크에서 제공 하는 포트입니다.

## <a name="create-hello-virtual-network-configuration"></a>Hello 가상 네트워크 구성 만들기

> [!IMPORTANT]
> HDInsight tooyour 온-프레미스 Azure 가상 네트워크를 사용 하는 네트워크, hello 참조에 대 한 연결에 대 한 단계별 지침을 원하는 경우 [HDInsight 연결 tooyour 온-프레미스 네트워크](connect-on-premises-network.md) 문서.

사용 하 여 hello 다음 문서 toolearn 어떻게 toocreate Azure 가상 네트워크를 연결 된 tooyour 온-프레미스 네트워크:
    
* [Hello Azure 포털을 사용 하 여](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [Azure PowerShell 사용](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [Azure CLI 사용](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a>이름 확인 구성

HDInsight tooallow 및 리소스 이름으로 네트워크 toocommunicate 가입 hello에에서 hello 다음 작업을 수행 해야 합니다.

* Hello Azure 가상 네트워크의에서 사용자 지정 DNS 서버를 만듭니다.

* Hello 가상 네트워크 toouse hello 사용자 지정 DNS 서버 hello 기본 Azure 재귀 확인자 대신를 구성 합니다.

* 사용자 지정 DNS 서버 hello와 온-프레미스 DNS 서버 간의 전달을 구성 합니다.

이러한 구성을 통해 동작을 수행 하는 hello:

* Hello DNS 접미사가 정규화 된 도메인 이름에 대 한 요청 __hello 가상 네트워크에 대 한__ toohello 사용자 지정 DNS 서버에 전달 됩니다. 사용자 지정 DNS 서버 hello 이러한 요청 toohello hello IP 주소를 반환 하는 Azure 재귀 확인자, 전달 합니다.

* 다른 모든 요청 toohello 온-프레미스 DNS 서버에 전달 됩니다. Microsoft.com 등 공용 인터넷 리소스에 대 한 요청을 포함 toohello 온-프레미스 DNS 서버 이름 확인을 위해 전달 됩니다.

다음 다이어그램 hello에서 녹색 선은 hello 가상 네트워크의 DNS 접미사 hello로 끝나는 리소스에 대 한 요청이 포함 됩니다. 파란색 선은 또는 hello 온-프레미스 네트워크 리소스에 대 한 요청에는 공용 인터넷 hello입니다.

![이 문서에 사용 되는 hello 구성에서 DNS 요청 해결 되는 방법의 다이어그램](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a>사용자 지정 DNS 서버 만들기

> [!IMPORTANT]
> 만들기 및 HDInsight hello 가상 네트워크에 설치 하기 전에 hello DNS 서버를 구성 해야 합니다.

toocreate hello를 사용 하 여 Linux VM [바인딩할](https://www.isc.org/downloads/bind/) DNS 소프트웨어를 사용 하 여 hello 단계를 수행 합니다.

> [!NOTE]
> hello 다음 단계 사용 하 여 hello [Azure 포털](https://portal.azure.com) toocreate Azure 가상 컴퓨터. 가상 컴퓨터의 다른 방법으로 toocreate 참조 hello [VM 만들기-Azure CLI](../virtual-machines/linux/quick-create-cli.md) 및 [VM 만들기-Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) 문서.

1. Hello에서 [Azure 포털](https://portal.azure.com)선택,  __+__ , __계산__, 및 __Ubuntu Server 16.04 LTS__합니다.

    ![Ubuntu 가상 컴퓨터 만들기](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. Hello에서 __기본 사항__ 섹션을 hello 다음 정보를 입력 합니다.

    * __이름__: 이 가상 컴퓨터를 식별하는 친숙한 이름입니다. 예: __DNSProxy__
    * __사용자 이름__: hello 이름 hello SSH 계정입니다.
    * __SSH 공개 키__ 또는 __암호__: hello hello SSH 계정에 대 한 인증 방법입니다. 보다 안전한 공개 키를 사용하는 것이 좋습니다. 자세한 내용은 참조 hello [Linux Vm에 대 한 SSH 키를 만들고 사용 하 여](../virtual-machines/linux/mac-create-ssh-keys.md) 문서.
    * __리소스 그룹__: 선택 __기존 항목 사용__, 한 다음 앞에서 만든 hello 가상 네트워크를 포함 하는 hello 리소스 그룹을 선택 합니다.
    * __위치__: 선택 hello hello 가상 네트워크와 동일한 위치입니다.

    ![가상 컴퓨터 기본 구성](./media/connect-on-premises-network/vm-basics.png)

    다른 항목을 hello에 기본값을 유지 한 다음 선택 __확인__합니다.

3. Hello에서 __크기 선택__ 섹션에서 선택 hello VM 크기입니다. 이 자습서에 대 한 가장 작은 hello를 선택 하 고 가장 낮은 비용 옵션. toocontinue를 사용 하 여 hello __선택__ 단추입니다.

4. Hello에서 __설정__ 섹션을 hello 다음 정보를 입력 합니다.

    * __가상 네트워크__: 선택 hello 앞에서 만든 가상 네트워크입니다.

    * __서브넷__: hello 가상 네트워크에 대 한 hello 기본 서브넷을 선택 합니다. 수행 __하지__ 선택 hello hello VPN 게이트웨이에서 사용 되는 서브넷입니다.

    * __진단 저장소 계정__: 기존 저장소 계정을 선택하거나 새 저장소 계정을 만듭니다.

    ![가상 네트워크 설정](./media/connect-on-premises-network/virtual-network-settings.png)

    Hello 기본값 hello 다른 항목을 유지 한 다음 선택 __확인__ toocontinue 합니다.

5. Hello에서 __구매__ 섹션을 선택 하는 hello __구매__ 단추 toocreate hello 가상 컴퓨터.

6. Hello 가상 컴퓨터를 만든 후 해당 __개요__ 섹션이 표시 됩니다. Hello 왼쪽에 hello 목록에서 선택 __속성__합니다. Hello 저장 __공용 IP 주소__ 및 __개인 IP 주소가__ 값입니다. Hello 다음 섹션에 사용 됩니다.

    ![공용 및 개인 IP 주소](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a>Bind(DNS 소프트웨어) 설치 및 구성

1. SSH tooconnect toohello를 사용 하 여 __공용 IP 주소__ hello 가상 컴퓨터의 합니다. 다음 예제는 hello 40.68.254.142에 tooa 가상 컴퓨터를 연결 합니다.

    ```bash
    ssh sshuser@40.68.254.142
    ```

    대체 `sshuser` hello 클러스터를 만들 때 지정한 hello SSH 사용자 계정 사용 합니다.

    > [!NOTE]
    > 다양 한 방법으로 tooobtain hello `ssh` 유틸리티입니다. Linux, Unix 및 macOS에 hello 운영 체제의 일부로 제공 됩니다. Windows를 사용 하는 경우 hello 다음 옵션 중 하나를 고려해 보십시오.
    >
    > * [Azure Cloud Shell](../cloud-shell/quickstart.md)
    > * [Windows 10에서 Ubuntu의 Bash](https://msdn.microsoft.com/commandline/wsl/about)
    > * [Git(https://git-scm.com/)](https://git-scm.com/)
    > * [OpenSSH(https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. 바인딩을 tooinstall hello SSH 세션에서 명령을 수행 하는 hello를 사용 합니다.

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. tooconfigure 바인딩 tooforward 이름 확인 요청 tooyour 온-프레미스 DNS 서버를 사용 하 여 hello의 hello 콘텐츠로 텍스트를 다음 hello `/etc/bind/named.conf.options` 파일:

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > Hello hello 값을 교체 `goodclients` hello 가상 네트워크와 온-프레미스 네트워크의 IP 주소 범위 hello와 섹션. 이 섹션에서는이 DNS 서버에 요청을 수락 하는 hello 주소를 정의 합니다.
    >
    > Hello 대체 `192.168.0.1` hello에 항목 `forwarders` hello IP 주소로 온-프레미스 DNS 서버의 섹션. 이 항목 경로 DNS 요청 tooyour 온-프레미스 DNS 서버를 확인 합니다.

    tooedit이이 파일에 다음 명령을 사용 하 여 hello:

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    toosave hello 파일을 사용 하 여 __Ctrl + X__, __Y__, 차례로 __Enter__합니다.

4. Hello SSH 세션에서 다음 명령을 hello를 사용 합니다.

    ```bash
    hostname -f
    ```

    이 명령은 텍스트 다음 값 비슷한 toohello를 반환 합니다.

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` 텍스트는 hello __DNS 접미사__ 이 가상 네트워크에 대 한 합니다. 나중에 사용하므로 이 값을 저장합니다.

5. tooconfigure hello 가상 네트워크 내에서 리소스에 대 한 바인딩 tooresolve DNS 이름을 사용 하 여 hello hello의 hello 콘텐츠로 텍스트를 다음 `/etc/bind/named.conf.local` 파일:

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > Hello 바꾸어야 `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` 앞서 검색 hello DNS 접미사를 사용 합니다.

    tooedit이이 파일에 다음 명령을 사용 하 여 hello:

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    toosave hello 파일을 사용 하 여 __Ctrl + X__, __Y__, 차례로 __Enter__합니다.

6. 다음 명령을 사용 하 여 hello 바인딩 toostart:

    ```bash
    sudo service bind9 restart
    ```

7. tooverify 바인딩하는 다음 명령을 사용 하 여 hello 온-프레미스 네트워크의 리소스 이름을 hello를 해결할 수 있습니다.

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > 대체 `dns.mynetwork.net` hello 온-프레미스 네트워크에 있는 리소스의 정규화 된 도메인 이름 (FQDN)으로 합니다.
    >
    > 대체 `10.0.0.4` hello로 __내부 IP 주소__ hello 가상 네트워크에 사용자 지정 DNS 서버입니다.

    hello 응답 텍스트 다음 유사한 toohello 나타납니다.

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a>Hello 가상 네트워크 toouse hello 사용자 지정 DNS 서버를 구성 합니다.

tooconfigure hello 가상 네트워크 toouse hello 사용자 지정 DNS 서버 hello Azure 재귀 확인자, 대신 단계를 수행 하는 hello를 사용 합니다.

1. Hello에 [Azure 포털](https://portal.azure.com)hello 가상 네트워크를 선택한 다음 선택 __DNS 서버__합니다.

2. 선택 __사용자 지정__, hello 입력 __내부 IP 주소__ hello 사용자 지정 DNS 서버입니다. 마지막으로 __저장__을 선택합니다.

    ![Hello hello 네트워크에 대 한 사용자 지정 DNS 서버 설정](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a>Hello 온-프레미스 DNS 서버 구성

Hello 이전 단원의 hello 사용자 지정 DNS 서버 tooforward 요청 toohello 온-프레미스 DNS 서버를 구성 합니다. 다음으로 hello 온-프레미스 DNS 서버 tooforward 요청 toohello 사용자 지정 DNS 서버를 구성 해야 합니다.

특정 단계는 방법에 대 한 tooconfigure DNS 서버, DNS 서버 소프트웨어에 대 한 hello 설명서를 참조 하십시오. 확인 방법에 대 hello tooconfigure는 __조건 전달자__합니다.

조건부 전달은 특정 DNS 접미사에 대한 요청만을 전달합니다. 이 경우 hello 가상 네트워크의 DNS 접미사 hello에 대 한 전달자를 구성 해야 합니다. 이 접미사에 대 한 요청 toohello hello 사용자 지정 하는 DNS 서버의 IP 주소를 전달 해야 합니다. 

hello 다음 텍스트는 hello에 대 한 조건 전달자 구성의 예 **바인딩할** DNS 소프트웨어:

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

DNS를 사용 하 여에 대 한 내용은 **Windows Server 2016**, hello 참조 [추가 DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) 설명서...

Hello 온-프레미스 DNS 서버를 구성한 후 사용할 수 있습니다 `nslookup` hello 온-프레미스 네트워크 tooverify에서 hello 가상 네트워크의 이름을 해결할 수 있습니다. 다음 예제는 hello 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

이 예제를 사용 하 여 온-프레미스 DNS 서버에 196.168.0.4 hello tooresolve hello 이름 hello 사용자 지정 DNS 서버입니다. 온-프레미스 DNS 서버 hello에 대 한 hello 하나 있는 hello IP 주소를 대체 합니다. Hello 대체 `dnsproxy` 주소 hello 사용자 지정 DNS 서버 hello 정규화 된 도메인 이름 사용 합니다.

## <a name="optional-control-network-traffic"></a>선택 사항: 네트워크 트래픽 제어

네트워크 보안 그룹 (NSG) 또는 사용자 정의 경로 (UDR) toocontrol 네트워크 트래픽을 사용할 수 있습니다. Nsg 사용 하면 toofilter 인바운드 및 아웃 바운드 트래픽을, 및 트래픽을 허용 하거나 거부 hello 합니다. UDRs는 toocontrol hello 가상 네트워크의 리소스 간의 트래픽 흐름 방식을 사용 하면, 인터넷, hello 및 온-프레미스 네트워크 hello 합니다.

> [!WARNING]
> HDInsight은 hello Azure 클라우드에서에서 특정 IP 주소에서의 인바운드 액세스 및 제한 없이 아웃 바운드 액세스가 필요합니다. Nsg 또는 UDRs toocontrol 트래픽을 사용할 때는 hello 다음 단계를 수행 해야 합니다.
>
> 1. 가상 네트워크를 포함 하는 hello 위치에 대 한 hello IP 주소를 찾습니다. 위치별로 필요한 IP 목록은 [필요한 IP 주소](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip)를 참조하세요.
>
> 2. Hello IP 주소에서 인바운드 트래픽을 허용 합니다.
>
>    * __NSG__: 허용 __인바운드__ 포트에서 트래픽을 __443__ hello에서 __인터넷__합니다.
>    * __UDR__: 집합 hello __다음 홉__ hello 경로 too__Internet__의 형식입니다.

Azure PowerShell 또는 hello Azure CLI toocreate Nsg 사용 하는 예제를 보려면 hello [Azure 가상 네트워크와 확장 HDInsight](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) 문서.

## <a name="create-hello-hdinsight-cluster"></a>Hello HDInsight 클러스터 만들기

> [!WARNING]
> HDInsight hello 가상 네트워크에 설치 하기 전에 hello 사용자 지정 DNS 서버를 구성 해야 합니다.

Hello에서 단계를 사용 하 여 hello [hello Azure 포털을 사용 하 여 HDInsight 클러스터를 만들 수](./hdinsight-hadoop-create-linux-clusters-portal.md) 문서 toocreate HDInsight 클러스터입니다.

> [!WARNING]
> * 클러스터를 만드는 동안 가상 네트워크를 포함 하는 hello 위치를 선택 해야 합니다.
>
> * Hello에 __고급 설정__ 부분 구성의 hello 가상 네트워크를 이전에 만든 서브넷을 선택 해야 합니다.

## <a name="connecting-toohdinsight"></a>TooHDInsight 연결

HDInsight에 대 한 대부분 설명서 hello를 통해 액세스 toohello 클러스터 있다고 가정 합니다. 인터넷 합니다. 예를 들어, https://CLUSTERNAME.azurehdinsight.net에 toohello 클러스터를 연결할 수 있습니다. 이 주소에서 UDRs toorestrict 액세스 hello 인터넷 또는 Nsg를 사용 하는 경우에 사용할 수 없는 hello 공용 게이트웨이 사용 합니다.

toodirectly는 tooHDInsight hello 가상 네트워크를 통해 연결 하려면이 단계를 수행 하는 hello를 사용 합니다.

1. hello HDInsight 클러스터 노드의 toodiscover hello 내부 정규화 된 도메인 이름을 hello 메서드를 다음 중 하나를 사용 합니다.

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

2. 서비스를 사용할 수 있는 toodetermine hello 포트 참조 hello [HDInsight의 Hadoop 서비스에 의해 사용 되는 포트](./hdinsight-hadoop-port-settings-for-services.md) 문서.

    > [!IMPORTANT]
    > 일부 서비스의 hello 헤드 노드에 호스팅되 한 번에 한 노드에서 활성화만 됩니다. 헤드 노드 하나에서 서비스에 액세스를 시도 하는 경우 실패 toohello 다른 헤드 노드를 전환 합니다.
    >
    > 예를 들어 Ambari는 한 번에 하나의 헤드 노드에서만 활성화됩니다. Ambari 헤드 노드 하나에서 액세스를 시도 하 고에서 실행 되 고 다음 404 오류를 반환 하는 경우 다른 헤드 노드를 hello 합니다.

## <a name="next-steps"></a>다음 단계

* 가상 네트워크에서 HDInsight를 사용하는 방법에 대한 자세한 내용은 [Azure Virtual Network를 사용하여 HDInsight 확장](./hdinsight-extend-hadoop-virtual-network.md)을 참조하세요.

* Azure 가상 네트워크에 대 한 자세한 내용은 참조 hello [Azure 가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)합니다.

* 네트워크 보안 그룹에 대한 자세한 내용은 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md)을 참조하세요.

* 사용자 정의 경로에 대한 자세한 내용은 [사용자 정의 경로 및 IP 전달](../virtual-network/virtual-networks-udr-overview.md)을 참조하세요.
