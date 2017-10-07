---
title: "가상 네트워크-Azure HDInsight를 사용 하 여 aaaConnect tooKafka | Microsoft Docs"
description: "Azure 가상 네트워크를 통해 toodirectly tooKafka HDInsight에 연결 하는 방법에 대해 알아봅니다. Tooconnect tooKafka 또는 온-프레미스에서 클라이언트는 VPN 게이트웨이 사용 하 여 개발 클라이언트에서 VPN 게이트웨이 장치를 사용 하 여 네트워크 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.custom: hdinsightactive
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/01/2017
ms.author: larryfr
ms.openlocfilehash: 03542fe14b9a1d010dffa22a8f8d96b098a1576e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a>Azure 가상 네트워크를 통해 tooKafka HDInsight (미리 보기)에 연결

Toodirectly tooKafka Azure 가상 네트워크를 사용 하 여 HDInsight에 연결 하는 방법에 대해 알아봅니다. 이 문서에서는 설명 하는 구성을 따르고 hello를 사용 하 여 tooKafka 연결에:

* 온-프레미스 네트워크 리소스에서. 이 연결은 로컬 네트워크에서 VPN 장치(소프트웨어 또는 하드웨어)를 사용하여 설정됩니다.
* VPN 소프트웨어 클라이언트를 사용한 개발 환경에서.

## <a name="architecture-and-planning"></a>아키텍처 및 계획

HDInsight hello를 통해 직접 연결 tooKafka를 허용 하지 않습니다 공용 인터넷 합니다. 대신, Kafka 클라이언트 (생산자와 소비자) hello 연결 방법을 다음 중 하나를 사용 해야 합니다.

* Hello 클라이언트 hello에 실행 Kafka HDInsight에서와 동일한 가상 네트워크입니다. Hello에이 구성은 사용 [HDInsight의 Apache Kafka (미리 보기)로 시작](hdinsight-apache-kafka-get-started.md) 문서. hello 클라이언트 실행 직접 hello HDInsight 클러스터 노드 또는 다른 가상 컴퓨터에서 동일한 hello 네트워크입니다.

* 예: toohello 가상 네트워크는 온-프레미스 네트워크의 개인 네트워크를 연결 합니다. 이 구성은 Kafka와 온-프레미스 네트워크 toodirectly 작업에서 클라이언트를 허용합니다. tooenable이이 구성에서는 hello 다음 작업을 수행 합니다.

    1. 가상 네트워크를 만듭니다.
    2. 사이트 간 구성을 사용하는 VPN 게이트웨이를 만듭니다. 이 문서에 사용 되는 hello 구성 tooa VPN 게이트웨이 장치 온-프레미스 네트워크에 연결 합니다.
    3. Hello 가상 네트워크에 DNS 서버를 만듭니다.
    4. 각 네트워크의 DNS 서버 hello 사이 전달을 구성 합니다.
    5. HDInsight에 hello 가상 네트워크로 Kafka를 설치 합니다.

    자세한 내용은 참조 hello [tooKafka 온-프레미스 네트워크에서 연결](#on-premises) 섹션. 

* VPN 게이트웨이 및 VPN 클라이언트를 사용 하 여 개별 컴퓨터 toohello 가상 네트워크를 연결 합니다. tooenable이이 구성에서는 hello 다음 작업을 수행 합니다.

    1. 가상 네트워크를 만듭니다.
    2. 지점-사이트 간 구성을 사용하는 VPN 게이트웨이를 만듭니다. 이 구성은 Windows 클라이언트에 설치할 수 있는 VPN 클라이언트를 제공합니다.
    3. HDInsight에 hello 가상 네트워크로 Kafka를 설치 합니다.
    4. IP 보급을 위한 Kafka 구성. 이 구성은 도메인 이름 대신 주소를 지정 하는 IP를 사용 하 여 hello 클라이언트 tooconnect을 허용 합니다.
    5. 다운로드 하 여 hello 개발 시스템에서 VPN 클라이언트 hello를 사용 합니다.

    자세한 내용은 참조 hello [tooKafka VPN 클라이언트를 사용 하 여 연결](#vpnclient) 섹션.

    > [!WARNING]
    > 이 구성은 다음과 같은 제한을 hello 인해 개발 용도로 권장 됩니다.
    >
    > * 각 클라이언트는 VPN 소프트웨어 클라이언트를 사용하여 연결해야 합니다. Azure는 Windows 기반 클라이언트만 제공합니다.
    > * 클라이언트 hello 사용한 IP 주소 지정 toocommunicate Kafka 사용 해야 하므로 이름 확인 요청 toohello 가상 네트워크를 전달 하지 않습니다. IP 통신에는 hello Kafka 클러스터에 추가 구성이 필요합니다.

가상 네트워크에서 HDInsight를 사용하는 방법에 대한 자세한 내용은 [Azure Virtual Network를 사용하여 HDInsight 확장](./hdinsight-extend-hadoop-virtual-network.md)을 참조하세요.

## <a id="on-premises"></a>TooKafka 온-프레미스 네트워크에서 연결

toocreate 온-프레미스 네트워크와 통신 하는 Kafka 클러스터에서에서 다음과 같이 hello hello [HDInsight 연결 tooyour 온-프레미스 네트워크](./connect-on-premises-network.md) 문서.

> [!IMPORTANT]
> Hello HDInsight 클러스터를 만들 때 선택 hello __Kafka__ 클러스터 유형입니다.

이러한 단계는 같은 구성이 hello를 만듭니다.

* Azure Virtual Network
* 사이트 간 VPN 게이트웨이
* Azure Storage 계정(HDInsight에서 사용)
* HDInsight의 Kafka

Kafka 클라이언트를 온-프레미스를 사용 하 여 hello 단계 hello toohello 클러스터를 연결할 수 있는지 tooverify [예제: Python 클라이언트](#python-client) 섹션.

## <a id="vpnclient"></a>TooKafka VPN 클라이언트를 사용 하 여 연결

이 섹션 toocreate hello 같은 구성이의 단계를 사용 하 여 hello:

* Azure Virtual Network
* 지점-사이트 간 VPN Gateway
* Azure Storage 계정(HDInsight에서 사용)
* HDInsight의 Kafka

1. Hello에 hello 단계를 따라 [지점 및 사이트 간 연결에 대 한 자체 서명 된 인증서 작업](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) 문서. 이 문서는 hello 게이트웨이에 대 한 필요한 hello 인증서를 만듭니다.

2. PowerShell 프롬프트를 열고 코드 toolog tooyour Azure 구독에에서 따라 hello를 사용 합니다.

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. 다음 구성 정보를 포함 하는 코드 toocreate 변수 hello를 사용 합니다.

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is hello resource group name?"
    $baseName = Read-Host "What is hello base name? It is used toocreate names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want toocreate hello resources in?"
    $rootCert = Read-Host "What is hello file path toohello root certificate? It is used toosecure hello VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter hello HTTPS user name and password for hello HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter hello SSH user name and password for hello HDInsight cluster" -UserName "sshuser"

    # Names for Azure resources
    $networkName = "net-$baseName"
    $clusterName = "kafka-$baseName"
    $storageName = "store$baseName" # Can't use dashes in storage names
    $defaultContainerName = $clusterName
    $defaultSubnetName = "default"
    $gatewaySubnetName = "GatewaySubnet"
    $gatewayPublicIpName = "GatewayIp"
    $gatewayIpConfigName = "GatewayConfig"
    $vpnRootCertName = "rootcert"
    $vpnName = "VPNGateway"

    # Network settings
    $networkAddressPrefix = "10.0.0.0/16"
    $defaultSubnetPrefix = "10.0.0.0/24"
    $gatewaySubnetPrefix = "10.0.1.0/24"
    $vpnClientAddressPool = "172.16.201.0/24"

    # HDInsight settings
    $HdiWorkerNodes = 4
    $hdiVersion = "3.5"
    $hdiType = "Kafka"
    ```

4. 사용 하 여 hello 다음 코드 toocreate hello Azure 리소스 그룹 및 가상 네트워크:

    ```powershell
    # Create hello resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create hello subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get hello network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for hello gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get hello certificate info
    # Get hello full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create hello VPN gateway
    New-AzureRmVirtualNetworkGateway -Name $vpnName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -IpConfigurations $gatewayIpConfig `
        -GatewayType Vpn `
        -VpnType RouteBased `
        -EnableBgp $false `
        -GatewaySku Standard `
        -VpnClientAddressPool $vpnClientAddressPool `
        -VpnClientRootCertificates $p2sRootCert
    ```

    > [!WARNING]
    > 이 프로세스 toocomplete에 대 일 분 정도 걸릴 수 있습니다.

5. 다음 코드는 hello Azure 저장소 계정과 blob 컨테이너를 toocreate hello를 사용 합니다.

    ```powershell
    # Create hello storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get hello storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create hello default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. 다음 코드 toocreate hello HDInsight 클러스터 hello를 사용 합니다.

    ```powershell
    # Create hello HDInsight cluster
    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $hdiWorkerNodes `
        -ClusterType $hdiType `
        -OSType Linux `
        -Version $hdiVersion `
        -HttpCredential $adminCreds `
        -SshCredential $sshCreds `
        -DefaultStorageAccountName "$storageName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageKey `
        -DefaultStorageContainer $defaultContainerName `
        -VirtualNetworkId $network.Id `
        -SubnetName $defaultSubnet.Id
    ```

  > [!WARNING]
  > 이 프로세스는 약 20 분 toocomplete를 걸립니다.

8. Hello 가상 네트워크에 대 한 Windows VPN 클라이언트 hello에 대 한 cmdlet tooretrieve hello url hello를 사용 합니다.

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    toodownload hello Windows VPN 클라이언트를 사용 하 여 hello 웹 브라우저에서 URI를 반환 합니다.

### <a name="configure-kafka-for-ip-advertising"></a>IP 보급을 위해 Kafka 구성

기본적으로 사육 hello Kafka 브로커 tooclients의 hello 도메인 이름을 반환합니다. 이 구성은 대로 되지 않을 hello로 VPN 소프트웨어 클라이언트 hello 가상 네트워크의 엔터티에 대 한 이름 확인을 사용할 수 없습니다. 이 구성에 대 한 hello 다음 이름을 사용해 서 도메인 이름 대신 단계 tooconfigure Kafka tooadvertise IP 주소:

1. 웹 브라우저를 사용 하 여, toohttps://CLUSTERNAME.azurehdinsight.net 이동 합니다. 대체 __CLUSTERNAME__ hello Kafka HDInsight 클러스터에서의 hello 이름으로 합니다.

    메시지가 표시 되 면 hello 클러스터에 대 한 hello HTTPS 사용자 이름 및 암호를 사용 합니다. hello 클러스터에 대 한 hello Ambari 웹 UI에 표시 됩니다.

2. tooview 알아보려면 Kafka, 선택 __Kafka__ hello hello 왼쪽 목록에서.

    ![Kafka가 강조 표시된 서비스 목록](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. tooview Kafka 구성 선택 __Configs__ hello 위쪽 가운데에서.

    ![Kafka에 대한 링크 구성](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. toofind hello __kafka env__ 구성을 입력 `kafka-env` hello에 __필터__ 필드 hello 오른쪽 상단에 있습니다.

    ![kafka-env의 Kafka 구성](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. tooconfigure Kafka tooadvertise IP 주소, hello 텍스트 toohello 아래쪽을 따라 hello 추가 __kafka env 템플릿__ 필드:

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. Kafka 수신 tooconfigure hello 인터페이스 입력 `listeners` hello에 __필터__ 필드 hello 오른쪽 상단에 있습니다.

7. tooconfigure 변경 hello 값 hello에서 모든 네트워크 인터페이스에서 Kafka toolisten __수신기__ 너무 필드`PLAINTEXT://0.0.0.0:9092`합니다.

8. toosave hello 구성 변경 내용을 사용 하 여 hello __저장__ 단추입니다. Hello 변경 내용을 설명 하는 문자 메시지를 입력 합니다. 선택 __확인__ 면 hello 변경 내용이 저장 되었습니다.

    ![구성 저장 단추](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. tooprevent 오류 Kafka를 다시 시작할 때 hello를 사용 하 여 __서비스 작업__ 선택한 단추 __유지 관리 모드에서 설정__합니다. 확인 toocomplete이이 작업을 선택 합니다.

    ![유지 관리 모드 켜기가 강조 표시된 서비스 작업](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. toorestart Kafka를 사용 하 여 hello __다시 시작__ 선택한 단추 __모든 영향을 다시 시작__합니다. Hello 다시 시작을 확인 하 고 다음 hello를 사용 하 여 __확인__ hello 작업이 완료 된 후 단추입니다.

    ![영향 받은 모든 항목 다시 시작이 강조 표시된 다시 시작 단추](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. toodisable 유지 관리 모드를 사용 하 여 hello __서비스 작업__ 선택한 단추 __유지 관리 모드 해제 기능__합니다. 선택 **확인** toocomplete이이 작업 합니다.

### <a name="connect-toohello-vpn-gateway"></a>Toohello VPN 게이트웨이 연결

tooconnect toohello VPN 게이트웨이 __Windows 클라이언트__, hello를 사용 하 여 __tooAzure 연결__ hello 섹션 [지점 및 사이트 간 연결 구성](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) 문서.

## <a id="python-client"></a>예: Python 클라이언트

다음 단계 toocreate hello를 사용 하 고 Python 생산자와 소비자를 실행 하는 toovalidate 연결 tooKafka:

1. 정규화 된 도메인 이름 (FQDN) 및 IP 주소 hello Kafka 클러스터에 있는 hello 노드의 경우 hello 메서드 tooretrieve hello를 완벽 하 게 다음 중 하나를 사용:

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

    이 스크립트는 있다고 가정 `$resourceGroupName` hello hello 가상 네트워크를 포함 하는 hello Azure 리소스 그룹 이름입니다.

    Hello 다음 단계에 사용 하기 위해 정보를 반환 하는 hello를 저장 합니다.

2. 사용 하 여 hello tooinstall hello 다음 [kafka python](http://kafka-python.readthedocs.io/) 클라이언트:

        pip install kafka-python

3. Python 코드 다음 사용 하 여 hello toosend 데이터 tooKafka:

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    Hello 대체 `'kafka_broker'` hello 주소를 가진 항목이이 섹션의 1 단계에서 반환 합니다.

    * 사용 하는 경우는 __소프트웨어 VPN 클라이언트__, 대체 hello `kafka_broker` 작업자 노드 hello IP 주소를 가진 항목입니다.

    * 있는 경우 __사용자 지정 DNS 서버를 통해 이름 확인을 사용__, 대체 hello `kafka_broker` hello hello 작업자 노드 FQDN 가진 항목이 합니다.

    > [!NOTE]
    > 이 코드는 hello 문자열 보냅니다 `test message` toohello 항목 `testtopic`합니다. HDInsight의 Kafka의 hello 기본 구성은 존재 하지 않는 경우 toocreate hello 항목을입니다.

4. Kafka 사용 하 여 hello Python 코드 다음 tooretrieve hello 메시지:

   ```python
   from kafka import KafkaConsumer
   # Replace hello `ip_address` entries with hello IP address of your worker nodes
   # Again, you only need one or two, not hello full list.
   # Note: auto_offset_reset='earliest' resets hello starting offset toohello beginning
   #       of hello topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    Hello 대체 `'kafka_broker'` hello 주소를 가진 항목이이 섹션의 1 단계에서 반환 합니다.

    * 사용 하는 경우는 __소프트웨어 VPN 클라이언트__, 대체 hello `kafka_broker` 작업자 노드 hello IP 주소를 가진 항목입니다.

    * 있는 경우 __사용자 지정 DNS 서버를 통해 이름 확인을 사용__, 대체 hello `kafka_broker` hello hello 작업자 노드 FQDN 가진 항목이 합니다.

## <a name="next-steps"></a>다음 단계

HDInsight를 사용 하 여 가상 네트워크에 대 한 자세한 내용은 참조 hello [Azure 가상 네트워크를 사용 하 여 Azure HDInsight 확장](hdinsight-extend-hadoop-virtual-network.md) 문서.

지점-사이트 VPN 게이트웨이와 Azure 가상 네트워크를 만드는 방법에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.

* [Hello Azure 포털을 사용 하는 지점 및 사이트 간 연결 구성](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [Azure PowerShell을 사용하여 지점 및 사이트 간 연결 구성](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

HDInsight의 Kafka와 작업에 자세한 내용은 다음 문서는 hello 참조:

* [HDInsight에서 Apache Kafka 시작](hdinsight-apache-kafka-get-started.md)
* [HDInsight에서 Kafka에 미러링 사용](hdinsight-apache-kafka-mirroring.md)
