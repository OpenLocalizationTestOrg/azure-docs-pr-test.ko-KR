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
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="0cc42-104">Azure 가상 네트워크를 통해 tooKafka HDInsight (미리 보기)에 연결</span><span class="sxs-lookup"><span data-stu-id="0cc42-104">Connect tooKafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="0cc42-105">Toodirectly tooKafka Azure 가상 네트워크를 사용 하 여 HDInsight에 연결 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-105">Learn how toodirectly connect tooKafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="0cc42-106">이 문서에서는 설명 하는 구성을 따르고 hello를 사용 하 여 tooKafka 연결에:</span><span class="sxs-lookup"><span data-stu-id="0cc42-106">This document provides information on connecting tooKafka using hello following configurations:</span></span>

* <span data-ttu-id="0cc42-107">온-프레미스 네트워크 리소스에서.</span><span class="sxs-lookup"><span data-stu-id="0cc42-107">From resources in an on-premises network.</span></span> <span data-ttu-id="0cc42-108">이 연결은 로컬 네트워크에서 VPN 장치(소프트웨어 또는 하드웨어)를 사용하여 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="0cc42-109">VPN 소프트웨어 클라이언트를 사용한 개발 환경에서.</span><span class="sxs-lookup"><span data-stu-id="0cc42-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="0cc42-110">아키텍처 및 계획</span><span class="sxs-lookup"><span data-stu-id="0cc42-110">Architecture and planning</span></span>

<span data-ttu-id="0cc42-111">HDInsight hello를 통해 직접 연결 tooKafka를 허용 하지 않습니다 공용 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-111">HDInsight does not allow direct connection tooKafka over hello public internet.</span></span> <span data-ttu-id="0cc42-112">대신, Kafka 클라이언트 (생산자와 소비자) hello 연결 방법을 다음 중 하나를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-112">Instead, Kafka clients (producers and consumers) must use one of hello following connection methods:</span></span>

* <span data-ttu-id="0cc42-113">Hello 클라이언트 hello에 실행 Kafka HDInsight에서와 동일한 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-113">Run hello client in hello same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="0cc42-114">Hello에이 구성은 사용 [HDInsight의 Apache Kafka (미리 보기)로 시작](hdinsight-apache-kafka-get-started.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="0cc42-114">This configuration is used in hello [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="0cc42-115">hello 클라이언트 실행 직접 hello HDInsight 클러스터 노드 또는 다른 가상 컴퓨터에서 동일한 hello 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-115">hello client runs directly on hello HDInsight cluster nodes or on another virtual machine in hello same network.</span></span>

* <span data-ttu-id="0cc42-116">예: toohello 가상 네트워크는 온-프레미스 네트워크의 개인 네트워크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-116">Connect a private network, such as your on-premises network, toohello virtual network.</span></span> <span data-ttu-id="0cc42-117">이 구성은 Kafka와 온-프레미스 네트워크 toodirectly 작업에서 클라이언트를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-117">This configuration allows clients in your on-premises network toodirectly work with Kafka.</span></span> <span data-ttu-id="0cc42-118">tooenable이이 구성에서는 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-118">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="0cc42-119">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="0cc42-120">사이트 간 구성을 사용하는 VPN 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="0cc42-121">이 문서에 사용 되는 hello 구성 tooa VPN 게이트웨이 장치 온-프레미스 네트워크에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-121">hello configuration used in this document connects tooa VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="0cc42-122">Hello 가상 네트워크에 DNS 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-122">Create a DNS server in hello virtual network.</span></span>
    4. <span data-ttu-id="0cc42-123">각 네트워크의 DNS 서버 hello 사이 전달을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-123">Configure forwarding between hello DNS server in each network.</span></span>
    5. <span data-ttu-id="0cc42-124">HDInsight에 hello 가상 네트워크로 Kafka를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-124">Install Kafka on HDInsight into hello virtual network.</span></span>

    <span data-ttu-id="0cc42-125">자세한 내용은 참조 hello [tooKafka 온-프레미스 네트워크에서 연결](#on-premises) 섹션.</span><span class="sxs-lookup"><span data-stu-id="0cc42-125">For more information, see hello [Connect tooKafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="0cc42-126">VPN 게이트웨이 및 VPN 클라이언트를 사용 하 여 개별 컴퓨터 toohello 가상 네트워크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-126">Connect individual machines toohello virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="0cc42-127">tooenable이이 구성에서는 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-127">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="0cc42-128">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="0cc42-129">지점-사이트 간 구성을 사용하는 VPN 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="0cc42-130">이 구성은 Windows 클라이언트에 설치할 수 있는 VPN 클라이언트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="0cc42-131">HDInsight에 hello 가상 네트워크로 Kafka를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-131">Install Kafka on HDInsight into hello virtual network.</span></span>
    4. <span data-ttu-id="0cc42-132">IP 보급을 위한 Kafka 구성.</span><span class="sxs-lookup"><span data-stu-id="0cc42-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="0cc42-133">이 구성은 도메인 이름 대신 주소를 지정 하는 IP를 사용 하 여 hello 클라이언트 tooconnect을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-133">This configuration allows hello client tooconnect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="0cc42-134">다운로드 하 여 hello 개발 시스템에서 VPN 클라이언트 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-134">Download and use hello VPN client on hello development system.</span></span>

    <span data-ttu-id="0cc42-135">자세한 내용은 참조 hello [tooKafka VPN 클라이언트를 사용 하 여 연결](#vpnclient) 섹션.</span><span class="sxs-lookup"><span data-stu-id="0cc42-135">For more information, see hello [Connect tooKafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="0cc42-136">이 구성은 다음과 같은 제한을 hello 인해 개발 용도로 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-136">This configuration is only recommended for development purposes because of hello following limitations:</span></span>
    >
    > * <span data-ttu-id="0cc42-137">각 클라이언트는 VPN 소프트웨어 클라이언트를 사용하여 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="0cc42-138">Azure는 Windows 기반 클라이언트만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="0cc42-139">클라이언트 hello 사용한 IP 주소 지정 toocommunicate Kafka 사용 해야 하므로 이름 확인 요청 toohello 가상 네트워크를 전달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-139">hello client does not pass name resolution requests toohello virtual network, so you must use IP addressing toocommunicate with Kafka.</span></span> <span data-ttu-id="0cc42-140">IP 통신에는 hello Kafka 클러스터에 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-140">IP communication requires additional configuration on hello Kafka cluster.</span></span>

<span data-ttu-id="0cc42-141">가상 네트워크에서 HDInsight를 사용하는 방법에 대한 자세한 내용은 [Azure Virtual Network를 사용하여 HDInsight 확장](./hdinsight-extend-hadoop-virtual-network.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cc42-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="0cc42-142"><a id="on-premises"></a>TooKafka 온-프레미스 네트워크에서 연결</span><span class="sxs-lookup"><span data-stu-id="0cc42-142"><a id="on-premises"></a> Connect tooKafka from an on-premises network</span></span>

<span data-ttu-id="0cc42-143">toocreate 온-프레미스 네트워크와 통신 하는 Kafka 클러스터에서에서 다음과 같이 hello hello [HDInsight 연결 tooyour 온-프레미스 네트워크](./connect-on-premises-network.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="0cc42-143">toocreate a Kafka cluster that communicates with your on-premises network, follow hello steps in hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0cc42-144">Hello HDInsight 클러스터를 만들 때 선택 hello __Kafka__ 클러스터 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-144">When creating hello HDInsight cluster, select hello __Kafka__ cluster type.</span></span>

<span data-ttu-id="0cc42-145">이러한 단계는 같은 구성이 hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-145">These steps create hello following configuration:</span></span>

* <span data-ttu-id="0cc42-146">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="0cc42-146">Azure Virtual Network</span></span>
* <span data-ttu-id="0cc42-147">사이트 간 VPN 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="0cc42-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="0cc42-148">Azure Storage 계정(HDInsight에서 사용)</span><span class="sxs-lookup"><span data-stu-id="0cc42-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="0cc42-149">HDInsight의 Kafka</span><span class="sxs-lookup"><span data-stu-id="0cc42-149">Kafka on HDInsight</span></span>

<span data-ttu-id="0cc42-150">Kafka 클라이언트를 온-프레미스를 사용 하 여 hello 단계 hello toohello 클러스터를 연결할 수 있는지 tooverify [예제: Python 클라이언트](#python-client) 섹션.</span><span class="sxs-lookup"><span data-stu-id="0cc42-150">tooverify that a Kafka client can connect toohello cluster from on-premises, use hello steps in hello [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="0cc42-151"><a id="vpnclient"></a>TooKafka VPN 클라이언트를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="0cc42-151"><a id="vpnclient"></a> Connect tooKafka with a VPN client</span></span>

<span data-ttu-id="0cc42-152">이 섹션 toocreate hello 같은 구성이의 단계를 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="0cc42-152">Use hello steps in this section toocreate hello following configuration:</span></span>

* <span data-ttu-id="0cc42-153">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="0cc42-153">Azure Virtual Network</span></span>
* <span data-ttu-id="0cc42-154">지점-사이트 간 VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="0cc42-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="0cc42-155">Azure Storage 계정(HDInsight에서 사용)</span><span class="sxs-lookup"><span data-stu-id="0cc42-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="0cc42-156">HDInsight의 Kafka</span><span class="sxs-lookup"><span data-stu-id="0cc42-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="0cc42-157">Hello에 hello 단계를 따라 [지점 및 사이트 간 연결에 대 한 자체 서명 된 인증서 작업](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="0cc42-157">Follow hello steps in hello [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="0cc42-158">이 문서는 hello 게이트웨이에 대 한 필요한 hello 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-158">This document creates hello certificates needed for hello gateway.</span></span>

2. <span data-ttu-id="0cc42-159">PowerShell 프롬프트를 열고 코드 toolog tooyour Azure 구독에에서 따라 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-159">Open a PowerShell prompt and use hello following code toolog in tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="0cc42-160">다음 구성 정보를 포함 하는 코드 toocreate 변수 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-160">Use hello following code toocreate variables that contain configuration information:</span></span>

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

4. <span data-ttu-id="0cc42-161">사용 하 여 hello 다음 코드 toocreate hello Azure 리소스 그룹 및 가상 네트워크:</span><span class="sxs-lookup"><span data-stu-id="0cc42-161">Use hello following code toocreate hello Azure resource group and virtual network:</span></span>

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
    > <span data-ttu-id="0cc42-162">이 프로세스 toocomplete에 대 일 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-162">It can take several minutes for this process toocomplete.</span></span>

5. <span data-ttu-id="0cc42-163">다음 코드는 hello Azure 저장소 계정과 blob 컨테이너를 toocreate hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-163">Use hello following code toocreate hello Azure Storage Account and blob container:</span></span>

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

6. <span data-ttu-id="0cc42-164">다음 코드 toocreate hello HDInsight 클러스터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-164">Use hello following code toocreate hello HDInsight cluster:</span></span>

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
  > <span data-ttu-id="0cc42-165">이 프로세스는 약 20 분 toocomplete를 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-165">This process takes around 20 minutes toocomplete.</span></span>

8. <span data-ttu-id="0cc42-166">Hello 가상 네트워크에 대 한 Windows VPN 클라이언트 hello에 대 한 cmdlet tooretrieve hello url hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-166">Use hello following cmdlet tooretrieve hello URL for hello Windows VPN client for hello virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="0cc42-167">toodownload hello Windows VPN 클라이언트를 사용 하 여 hello 웹 브라우저에서 URI를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-167">toodownload hello Windows VPN client, use hello returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="0cc42-168">IP 보급을 위해 Kafka 구성</span><span class="sxs-lookup"><span data-stu-id="0cc42-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="0cc42-169">기본적으로 사육 hello Kafka 브로커 tooclients의 hello 도메인 이름을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-169">By default, Zookeeper returns hello domain name of hello Kafka brokers tooclients.</span></span> <span data-ttu-id="0cc42-170">이 구성은 대로 되지 않을 hello로 VPN 소프트웨어 클라이언트 hello 가상 네트워크의 엔터티에 대 한 이름 확인을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-170">This configuration does not work with hello VPN software client, as it cannot use name resolution for entities in hello virtual network.</span></span> <span data-ttu-id="0cc42-171">이 구성에 대 한 hello 다음 이름을 사용해 서 도메인 이름 대신 단계 tooconfigure Kafka tooadvertise IP 주소:</span><span class="sxs-lookup"><span data-stu-id="0cc42-171">For this configuration, use hello following steps tooconfigure Kafka tooadvertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="0cc42-172">웹 브라우저를 사용 하 여, toohttps://CLUSTERNAME.azurehdinsight.net 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-172">Using a web browser, go toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="0cc42-173">대체 __CLUSTERNAME__ hello Kafka HDInsight 클러스터에서의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-173">Replace __CLUSTERNAME__ with hello name of hello Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="0cc42-174">메시지가 표시 되 면 hello 클러스터에 대 한 hello HTTPS 사용자 이름 및 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-174">When prompted, use hello HTTPS user name and password for hello cluster.</span></span> <span data-ttu-id="0cc42-175">hello 클러스터에 대 한 hello Ambari 웹 UI에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-175">hello Ambari Web UI for hello cluster is displayed.</span></span>

2. <span data-ttu-id="0cc42-176">tooview 알아보려면 Kafka, 선택 __Kafka__ hello hello 왼쪽 목록에서.</span><span class="sxs-lookup"><span data-stu-id="0cc42-176">tooview information on Kafka, select __Kafka__ from hello list on hello left.</span></span>

    ![Kafka가 강조 표시된 서비스 목록](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="0cc42-178">tooview Kafka 구성 선택 __Configs__ hello 위쪽 가운데에서.</span><span class="sxs-lookup"><span data-stu-id="0cc42-178">tooview Kafka configuration, select __Configs__ from hello top middle.</span></span>

    ![Kafka에 대한 링크 구성](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="0cc42-180">toofind hello __kafka env__ 구성을 입력 `kafka-env` hello에 __필터__ 필드 hello 오른쪽 상단에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-180">toofind hello __kafka-env__ configuration, enter `kafka-env` in hello __Filter__ field on hello upper right.</span></span>

    ![kafka-env의 Kafka 구성](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="0cc42-182">tooconfigure Kafka tooadvertise IP 주소, hello 텍스트 toohello 아래쪽을 따라 hello 추가 __kafka env 템플릿__ 필드:</span><span class="sxs-lookup"><span data-stu-id="0cc42-182">tooconfigure Kafka tooadvertise IP addresses, add hello following text toohello bottom of hello __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="0cc42-183">Kafka 수신 tooconfigure hello 인터페이스 입력 `listeners` hello에 __필터__ 필드 hello 오른쪽 상단에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-183">tooconfigure hello interface that Kafka listens on, enter `listeners` in hello __Filter__ field on hello upper right.</span></span>

7. <span data-ttu-id="0cc42-184">tooconfigure 변경 hello 값 hello에서 모든 네트워크 인터페이스에서 Kafka toolisten __수신기__ 너무 필드`PLAINTEXT://0.0.0.0:9092`합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-184">tooconfigure Kafka toolisten on all network interfaces, change hello value in hello __listeners__ field too`PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="0cc42-185">toosave hello 구성 변경 내용을 사용 하 여 hello __저장__ 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-185">toosave hello configuration changes, use hello __Save__ button.</span></span> <span data-ttu-id="0cc42-186">Hello 변경 내용을 설명 하는 문자 메시지를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-186">Enter a text message describing hello changes.</span></span> <span data-ttu-id="0cc42-187">선택 __확인__ 면 hello 변경 내용이 저장 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-187">Select __OK__ once hello changes have been saved.</span></span>

    ![구성 저장 단추](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="0cc42-189">tooprevent 오류 Kafka를 다시 시작할 때 hello를 사용 하 여 __서비스 작업__ 선택한 단추 __유지 관리 모드에서 설정__합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-189">tooprevent errors when restarting Kafka, use hello __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="0cc42-190">확인 toocomplete이이 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-190">Select OK toocomplete this operation.</span></span>

    ![유지 관리 모드 켜기가 강조 표시된 서비스 작업](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="0cc42-192">toorestart Kafka를 사용 하 여 hello __다시 시작__ 선택한 단추 __모든 영향을 다시 시작__합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-192">toorestart Kafka, use hello __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="0cc42-193">Hello 다시 시작을 확인 하 고 다음 hello를 사용 하 여 __확인__ hello 작업이 완료 된 후 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-193">Confirm hello restart, and then use hello __OK__ button after hello operation has completed.</span></span>

    ![영향 받은 모든 항목 다시 시작이 강조 표시된 다시 시작 단추](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="0cc42-195">toodisable 유지 관리 모드를 사용 하 여 hello __서비스 작업__ 선택한 단추 __유지 관리 모드 해제 기능__합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-195">toodisable maintenance mode, use hello __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="0cc42-196">선택 **확인** toocomplete이이 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-196">Select **OK** toocomplete this operation.</span></span>

### <a name="connect-toohello-vpn-gateway"></a><span data-ttu-id="0cc42-197">Toohello VPN 게이트웨이 연결</span><span class="sxs-lookup"><span data-stu-id="0cc42-197">Connect toohello VPN gateway</span></span>

<span data-ttu-id="0cc42-198">tooconnect toohello VPN 게이트웨이 __Windows 클라이언트__, hello를 사용 하 여 __tooAzure 연결__ hello 섹션 [지점 및 사이트 간 연결 구성](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) 문서.</span><span class="sxs-lookup"><span data-stu-id="0cc42-198">tooconnect toohello VPN gateway from a __Windows client__, use hello __Connect tooAzure__ section of hello [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="0cc42-199"><a id="python-client"></a>예: Python 클라이언트</span><span class="sxs-lookup"><span data-stu-id="0cc42-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="0cc42-200">다음 단계 toocreate hello를 사용 하 고 Python 생산자와 소비자를 실행 하는 toovalidate 연결 tooKafka:</span><span class="sxs-lookup"><span data-stu-id="0cc42-200">toovalidate connectivity tooKafka, use hello following steps toocreate and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="0cc42-201">정규화 된 도메인 이름 (FQDN) 및 IP 주소 hello Kafka 클러스터에 있는 hello 노드의 경우 hello 메서드 tooretrieve hello를 완벽 하 게 다음 중 하나를 사용:</span><span class="sxs-lookup"><span data-stu-id="0cc42-201">Use one of hello following methods tooretrieve hello fully qualified domain name (FQDN) and IP addresses of hello nodes in hello Kafka cluster:</span></span>

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

    <span data-ttu-id="0cc42-202">이 스크립트는 있다고 가정 `$resourceGroupName` hello hello 가상 네트워크를 포함 하는 hello Azure 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-202">This script assumes that `$resourceGroupName` is hello name of hello Azure resource group that contains hello virtual network.</span></span>

    <span data-ttu-id="0cc42-203">Hello 다음 단계에 사용 하기 위해 정보를 반환 하는 hello를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-203">Save hello returned information for use in hello next steps.</span></span>

2. <span data-ttu-id="0cc42-204">사용 하 여 hello tooinstall hello 다음 [kafka python](http://kafka-python.readthedocs.io/) 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="0cc42-204">Use hello following tooinstall hello [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="0cc42-205">Python 코드 다음 사용 하 여 hello toosend 데이터 tooKafka:</span><span class="sxs-lookup"><span data-stu-id="0cc42-205">toosend data tooKafka, use hello following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="0cc42-206">Hello 대체 `'kafka_broker'` hello 주소를 가진 항목이이 섹션의 1 단계에서 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-206">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="0cc42-207">사용 하는 경우는 __소프트웨어 VPN 클라이언트__, 대체 hello `kafka_broker` 작업자 노드 hello IP 주소를 가진 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-207">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="0cc42-208">있는 경우 __사용자 지정 DNS 서버를 통해 이름 확인을 사용__, 대체 hello `kafka_broker` hello hello 작업자 노드 FQDN 가진 항목이 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-208">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0cc42-209">이 코드는 hello 문자열 보냅니다 `test message` toohello 항목 `testtopic`합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-209">This code sends hello string `test message` toohello topic `testtopic`.</span></span> <span data-ttu-id="0cc42-210">HDInsight의 Kafka의 hello 기본 구성은 존재 하지 않는 경우 toocreate hello 항목을입니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-210">hello default configuration of Kafka on HDInsight is toocreate hello topic if it does not exist.</span></span>

4. <span data-ttu-id="0cc42-211">Kafka 사용 하 여 hello Python 코드 다음 tooretrieve hello 메시지:</span><span class="sxs-lookup"><span data-stu-id="0cc42-211">tooretrieve hello messages from Kafka, use hello following Python code:</span></span>

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

    <span data-ttu-id="0cc42-212">Hello 대체 `'kafka_broker'` hello 주소를 가진 항목이이 섹션의 1 단계에서 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-212">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="0cc42-213">사용 하는 경우는 __소프트웨어 VPN 클라이언트__, 대체 hello `kafka_broker` 작업자 노드 hello IP 주소를 가진 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-213">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="0cc42-214">있는 경우 __사용자 지정 DNS 서버를 통해 이름 확인을 사용__, 대체 hello `kafka_broker` hello hello 작업자 노드 FQDN 가진 항목이 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc42-214">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cc42-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0cc42-215">Next steps</span></span>

<span data-ttu-id="0cc42-216">HDInsight를 사용 하 여 가상 네트워크에 대 한 자세한 내용은 참조 hello [Azure 가상 네트워크를 사용 하 여 Azure HDInsight 확장](hdinsight-extend-hadoop-virtual-network.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="0cc42-216">For more information on using HDInsight with a virtual network, see hello [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="0cc42-217">지점-사이트 VPN 게이트웨이와 Azure 가상 네트워크를 만드는 방법에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0cc42-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see hello following documents:</span></span>

* [<span data-ttu-id="0cc42-218">Hello Azure 포털을 사용 하는 지점 및 사이트 간 연결 구성</span><span class="sxs-lookup"><span data-stu-id="0cc42-218">Configure a Point-to-Site connection using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="0cc42-219">Azure PowerShell을 사용하여 지점 및 사이트 간 연결 구성</span><span class="sxs-lookup"><span data-stu-id="0cc42-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="0cc42-220">HDInsight의 Kafka와 작업에 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="0cc42-220">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="0cc42-221">HDInsight에서 Apache Kafka 시작</span><span class="sxs-lookup"><span data-stu-id="0cc42-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="0cc42-222">HDInsight에서 Kafka에 미러링 사용</span><span class="sxs-lookup"><span data-stu-id="0cc42-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
