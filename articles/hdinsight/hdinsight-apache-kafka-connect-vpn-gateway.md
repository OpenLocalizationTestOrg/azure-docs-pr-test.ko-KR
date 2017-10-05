---
title: "가상 네트워크를 사용하여 Kafka에 연결 - Azure HDInsight | Microsoft Docs"
description: "Azure Virtual Network를 통해 HDInsight에서 Kafka에 직접 연결하는 방법을 알아봅니다. VPN Gateway를 사용하여 개발 클라이언트에서 또는 VPN 게이트웨이 장치를 사용하여 온-프레미스 네트워크의 클라이언트에서 Kafka에 연결하는 방법을 알아봅니다."
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
ms.openlocfilehash: 245bee7c1dbb0236afdc2506e7ab84b5573cbc85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-kafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="169a0-104">Azure Virtual Network를 통해 HDInsight(미리 보기)의 Kafka에 연결</span><span class="sxs-lookup"><span data-stu-id="169a0-104">Connect to Kafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="169a0-105">Azure Virtual Network를 사용하여 HDInsight의 Kafka에 직접 연결하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-105">Learn how to directly connect to Kafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="169a0-106">이 문서는 다음 구성을 사용하여 Kafka에 연결하는 것에 관한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-106">This document provides information on connecting to Kafka using the following configurations:</span></span>

* <span data-ttu-id="169a0-107">온-프레미스 네트워크 리소스에서.</span><span class="sxs-lookup"><span data-stu-id="169a0-107">From resources in an on-premises network.</span></span> <span data-ttu-id="169a0-108">이 연결은 로컬 네트워크에서 VPN 장치(소프트웨어 또는 하드웨어)를 사용하여 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="169a0-109">VPN 소프트웨어 클라이언트를 사용한 개발 환경에서.</span><span class="sxs-lookup"><span data-stu-id="169a0-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="169a0-110">아키텍처 및 계획</span><span class="sxs-lookup"><span data-stu-id="169a0-110">Architecture and planning</span></span>

<span data-ttu-id="169a0-111">HDInsight는 공용 인터넷을 통해 Kafka에 직접 연결하는 것을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-111">HDInsight does not allow direct connection to Kafka over the public internet.</span></span> <span data-ttu-id="169a0-112">대신, Kafka 클라이언트(생산자와 소비자)는 다음 연결 방법 중 하나를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-112">Instead, Kafka clients (producers and consumers) must use one of the following connection methods:</span></span>

* <span data-ttu-id="169a0-113">클라이언트를 동일한 가상 네트워크에서 Kafka로 HDInsight 상에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-113">Run the client in the same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="169a0-114">이 구성은 [HDInsight의 Apache Kafka(미리 보기)에서 시작](hdinsight-apache-kafka-get-started.md) 문서에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-114">This configuration is used in the [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="169a0-115">클라이언트는 동일한 네트워크 내의 HDInsight 클러스터 노드나 또 다른 가상 컴퓨터에서 직접 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-115">The client runs directly on the HDInsight cluster nodes or on another virtual machine in the same network.</span></span>

* <span data-ttu-id="169a0-116">온-프레미스 네트워크와 같은 개인 네트워크를 가상 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-116">Connect a private network, such as your on-premises network, to the virtual network.</span></span> <span data-ttu-id="169a0-117">이 구성을 통해 온-프레미스 네트워크의 클라이언트들은 직접 Kafka를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-117">This configuration allows clients in your on-premises network to directly work with Kafka.</span></span> <span data-ttu-id="169a0-118">이 구성을 사용하도록 설정하려면 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-118">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="169a0-119">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="169a0-120">사이트 간 구성을 사용하는 VPN 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="169a0-121">이 문서에 사용된 구성을 통해 온-프레미스 네트워크의 VPN 게이트웨이 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-121">The configuration used in this document connects to a VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="169a0-122">가상 네트워크에 DNS 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-122">Create a DNS server in the virtual network.</span></span>
    4. <span data-ttu-id="169a0-123">각 네트워크의 DNS 서버 간에 전달을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-123">Configure forwarding between the DNS server in each network.</span></span>
    5. <span data-ttu-id="169a0-124">HDInsight의 Kafka를 가상 네트워크에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-124">Install Kafka on HDInsight into the virtual network.</span></span>

    <span data-ttu-id="169a0-125">자세한 내용은 [온-프레미스 네트워크에서 Kafka에 연결](#on-premises) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="169a0-125">For more information, see the [Connect to Kafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="169a0-126">VPN 게이트웨이와 VPN 클라이언트를 사용하여 개별 컴퓨터를 가상 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-126">Connect individual machines to the virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="169a0-127">이 구성을 사용하도록 설정하려면 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-127">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="169a0-128">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="169a0-129">지점-사이트 간 구성을 사용하는 VPN 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="169a0-130">이 구성은 Windows 클라이언트에 설치할 수 있는 VPN 클라이언트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="169a0-131">HDInsight의 Kafka를 가상 네트워크에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-131">Install Kafka on HDInsight into the virtual network.</span></span>
    4. <span data-ttu-id="169a0-132">IP 보급을 위한 Kafka 구성.</span><span class="sxs-lookup"><span data-stu-id="169a0-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="169a0-133">이 구성은 클라이언트가 도메인 이름 대신 IP 주소 지정을 사용하여 연결하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-133">This configuration allows the client to connect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="169a0-134">VPN 클라이언트를 개발 시스템에 다운로드하여 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-134">Download and use the VPN client on the development system.</span></span>

    <span data-ttu-id="169a0-135">자세한 내용은 [VPN 클라이언트와 함께 Kafka 연결](#vpnclient) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="169a0-135">For more information, see the [Connect to Kafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="169a0-136">이 구성은 다음과 같은 제한 사항 때문에 개발 용도로만 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-136">This configuration is only recommended for development purposes because of the following limitations:</span></span>
    >
    > * <span data-ttu-id="169a0-137">각 클라이언트는 VPN 소프트웨어 클라이언트를 사용하여 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="169a0-138">Azure는 Windows 기반 클라이언트만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="169a0-139">클라이언트는 가상 네트워크에 이름 확인 요청을 전달 하지 않으므로, Kafka와 통신하기 위해 IP 주소 지정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-139">The client does not pass name resolution requests to the virtual network, so you must use IP addressing to communicate with Kafka.</span></span> <span data-ttu-id="169a0-140">IP 통신을 하려면 Kafka 클러스터에 추가 구성을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-140">IP communication requires additional configuration on the Kafka cluster.</span></span>

<span data-ttu-id="169a0-141">가상 네트워크에서 HDInsight를 사용하는 방법에 대한 자세한 내용은 [Azure Virtual Network를 사용하여 HDInsight 확장](./hdinsight-extend-hadoop-virtual-network.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="169a0-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="169a0-142"><a id="on-premises"></a>온-프레미스 네트워크에서 Kafka에 연결</span><span class="sxs-lookup"><span data-stu-id="169a0-142"><a id="on-premises"></a> Connect to Kafka from an on-premises network</span></span>

<span data-ttu-id="169a0-143">온-프레미스 네트워크와 통신하는 Kafka 클러스터를 만들려면 [온-프레미스 네트워크에 HDInsight 연결](./connect-on-premises-network.md) 문서에 나오는 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-143">To create a Kafka cluster that communicates with your on-premises network, follow the steps in the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="169a0-144">HDInsight 클러스터를 만들 때 __Kafka__ 클러스터 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-144">When creating the HDInsight cluster, select the __Kafka__ cluster type.</span></span>

<span data-ttu-id="169a0-145">이러한 단계를 거쳐 다음 구성이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-145">These steps create the following configuration:</span></span>

* <span data-ttu-id="169a0-146">Azure 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="169a0-146">Azure Virtual Network</span></span>
* <span data-ttu-id="169a0-147">사이트 간 VPN 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="169a0-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="169a0-148">Azure Storage 계정(HDInsight에서 사용)</span><span class="sxs-lookup"><span data-stu-id="169a0-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="169a0-149">HDInsight의 Kafka</span><span class="sxs-lookup"><span data-stu-id="169a0-149">Kafka on HDInsight</span></span>

<span data-ttu-id="169a0-150">Kafka 클라이언트가 온-프레미스에서 클러스터로 연결할 수 있는지 확인하려면 [예: Python 클라이언트](#python-client) 섹션에 나오는 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-150">To verify that a Kafka client can connect to the cluster from on-premises, use the steps in the [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="169a0-151"><a id="vpnclient"></a>VPN 클라이언트와 함께 Kafka에 연결</span><span class="sxs-lookup"><span data-stu-id="169a0-151"><a id="vpnclient"></a> Connect to Kafka with a VPN client</span></span>

<span data-ttu-id="169a0-152">다음 구성을 만들려면 이 섹션에 나오는 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-152">Use the steps in this section to create the following configuration:</span></span>

* <span data-ttu-id="169a0-153">Azure 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="169a0-153">Azure Virtual Network</span></span>
* <span data-ttu-id="169a0-154">지점-사이트 간 VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="169a0-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="169a0-155">Azure Storage 계정(HDInsight에서 사용)</span><span class="sxs-lookup"><span data-stu-id="169a0-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="169a0-156">HDInsight의 Kafka</span><span class="sxs-lookup"><span data-stu-id="169a0-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="169a0-157">[지점 및 사이트 간 연결에 대한 자체 서명된 인증서로 작업](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) 문서에 나오는 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-157">Follow the steps in the [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="169a0-158">이 문서는 게이트웨이에 필요한 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-158">This document creates the certificates needed for the gateway.</span></span>

2. <span data-ttu-id="169a0-159">PowerShell 프롬프트를 열고 다음 코드를 사용하여 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-159">Open a PowerShell prompt and use the following code to log in to your Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment to set the subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="169a0-160">다음 코드를 사용하여 구성 정보를 포함하는 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-160">Use the following code to create variables that contain configuration information:</span></span>

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is the resource group name?"
    $baseName = Read-Host "What is the base name? It is used to create names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want to create the resources in?"
    $rootCert = Read-Host "What is the file path to the root certificate? It is used to secure the VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter the HTTPS user name and password for the HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter the SSH user name and password for the HDInsight cluster" -UserName "sshuser"

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

4. <span data-ttu-id="169a0-161">다음 코드를 사용하여 Azure 리소스 그룹 및 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-161">Use the following code to create the Azure resource group and virtual network:</span></span>

    ```powershell
    # Create the resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create the subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create the subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get the network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for the gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get the certificate info
    # Get the full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create the VPN gateway
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
    > <span data-ttu-id="169a0-162">이 프로세스는 완료하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-162">It can take several minutes for this process to complete.</span></span>

5. <span data-ttu-id="169a0-163">다음 코드를 사용하여 Azure Storage 계정 및 Blob 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-163">Use the following code to create the Azure Storage Account and blob container:</span></span>

    ```powershell
    # Create the storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get the storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create the default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. <span data-ttu-id="169a0-164">다음 코드를 사용하여 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-164">Use the following code to create the HDInsight cluster:</span></span>

    ```powershell
    # Create the HDInsight cluster
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
  > <span data-ttu-id="169a0-165">이 프로세스를 완료하는 데 약 20분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-165">This process takes around 20 minutes to complete.</span></span>

8. <span data-ttu-id="169a0-166">다음 cmdlet을 사용하여 가상 네트워크에서 Windows VPN 클라이언트의 URL을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-166">Use the following cmdlet to retrieve the URL for the Windows VPN client for the virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="169a0-167">Windows VPN 클라이언트를 다운로드하려면 웹 브라우저에서 반환된 URI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-167">To download the Windows VPN client, use the returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="169a0-168">IP 보급을 위해 Kafka 구성</span><span class="sxs-lookup"><span data-stu-id="169a0-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="169a0-169">기본적으로 Zookeeper는 Kafka 브로커의 도메인 이름을 클라이언트에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-169">By default, Zookeeper returns the domain name of the Kafka brokers to clients.</span></span> <span data-ttu-id="169a0-170">이 구성은 가상 네트워크의 엔터티에 대해 이름 확인을 사용할 수 없으므로 VPN 소프트웨어 클라이언트에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-170">This configuration does not work with the VPN software client, as it cannot use name resolution for entities in the virtual network.</span></span> <span data-ttu-id="169a0-171">이 구성의 경우, 다음 단계에 따라 도메인 이름 대신 IP 주소를 보급하도록 Kafka를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-171">For this configuration, use the following steps to configure Kafka to advertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="169a0-172">웹 브라우저를 사용하여 https://CLUSTERNAME.azurehdinsight.net으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-172">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="169a0-173">__CLUSTERNAME__을 HDInsight 클러스터의 Kafka 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-173">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="169a0-174">메시지가 표시되면, 클러스터의 HTTPS 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-174">When prompted, use the HTTPS user name and password for the cluster.</span></span> <span data-ttu-id="169a0-175">클러스터에 대한 Ambari Web UI가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-175">The Ambari Web UI for the cluster is displayed.</span></span>

2. <span data-ttu-id="169a0-176">Kafka에 대한 정보를 보려면 왼쪽 목록에서 __Kafka__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-176">To view information on Kafka, select __Kafka__ from the list on the left.</span></span>

    ![Kafka가 강조 표시된 서비스 목록](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="169a0-178">Kafka 구성을 보려면 위쪽 가운데에서 __Configs__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-178">To view Kafka configuration, select __Configs__ from the top middle.</span></span>

    ![Kafka에 대한 링크 구성](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="169a0-180">__kafka-env__ 구성을 찾으려면 오른쪽 위에 있는 __필터__ 필드에 `kafka-env`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-180">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span></span>

    ![kafka-env의 Kafka 구성](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="169a0-182">IP 주소를 보급하도록 Kafka를 구성하려면 __kafka-env-template__ 맨 아래에 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-182">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka to advertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="169a0-183">Kafka에서 수신 대기하는 인터페이스를 구성하려면 오른쪽 위의 __필터__ 필드에 `listeners`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-183">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span></span>

7. <span data-ttu-id="169a0-184">모든 네트워크 인터페이스에서 수신 대기하도록 Kafka를 구성하려면 __수신기__ 필드의 값을 `PLAINTEXT://0.0.0.0:9092`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-184">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="169a0-185">구성 변경 내용을 저장하려면 __저장__ 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-185">To save the configuration changes, use the __Save__ button.</span></span> <span data-ttu-id="169a0-186">변경 내용을 설명하는 텍스트 메시지를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-186">Enter a text message describing the changes.</span></span> <span data-ttu-id="169a0-187">변경 내용이 저장되면 __확인__을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-187">Select __OK__ once the changes have been saved.</span></span>

    ![구성 저장 단추](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="169a0-189">Kafka를 다시 시작할 때 오류를 방지하려면 __서비스 작업__ 단추를 사용하여 __유지 관리 모드 켜기__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-189">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="169a0-190">확인을 선택하여 이 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-190">Select OK to complete this operation.</span></span>

    ![유지 관리 모드 켜기가 강조 표시된 서비스 작업](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="169a0-192">Kafka를 다시 시작하려면 __다시 시작__ 단추를 사용하고 __영향 받은 모든 항목 다시 시작__을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-192">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="169a0-193">다시 시작을 확인하고 작업이 완료되면 __확인__ 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-193">Confirm the restart, and then use the __OK__ button after the operation has completed.</span></span>

    ![영향 받은 모든 항목 다시 시작이 강조 표시된 다시 시작 단추](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="169a0-195">유지 관리 모드를 사용하지 않도록 설정하려면 __서비스 작업__ 단추를 사용하고 __유지 관리 모드 끄기__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-195">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="169a0-196">**확인**을 선택하여 이 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-196">Select **OK** to complete this operation.</span></span>

### <a name="connect-to-the-vpn-gateway"></a><span data-ttu-id="169a0-197">VPN Gateway에 연결</span><span class="sxs-lookup"><span data-stu-id="169a0-197">Connect to the VPN gateway</span></span>

<span data-ttu-id="169a0-198">__Windows 클라이언트__에서 VPN Gateway에 연결하려면 [지점- 사이트 간 연결 구성](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) 문서의 __Azure에 연결__ 섹션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-198">To connect to the VPN gateway from a __Windows client__, use the __Connect to Azure__ section of the [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="169a0-199"><a id="python-client"></a>예: Python 클라이언트</span><span class="sxs-lookup"><span data-stu-id="169a0-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="169a0-200">Kafka에 대한 연결 유효성 검사를 하려면, 다음 단계를 사용하여 Python 생산자와 소비자를 만들고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-200">To validate connectivity to Kafka, use the following steps to create and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="169a0-201">다음 방법 중 하나를 사용하여 Kafka 클러스터에서 정규화된 도메인 이름(FQDN) 및 노드 IP 주소를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-201">Use one of the following methods to retrieve the fully qualified domain name (FQDN) and IP addresses of the nodes in the Kafka cluster:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

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

    <span data-ttu-id="169a0-202">이 스크립트에서는 `$resourceGroupName`을 가상 네트워크가 포함된 Azure 리소스 그룹의 이름으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-202">This script assumes that `$resourceGroupName` is the name of the Azure resource group that contains the virtual network.</span></span>

    <span data-ttu-id="169a0-203">다음 단계에서의 사용을 위해 반환된 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-203">Save the returned information for use in the next steps.</span></span>

2. <span data-ttu-id="169a0-204">다음을 사용하여 [kafka-python](http://kafka-python.readthedocs.io/) 클라이언트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-204">Use the following to install the [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="169a0-205">Kafka로 데이터를 전송하려면 다음 Python 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-205">To send data to Kafka, use the following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace the `ip_address` entries with the IP address of your worker nodes
  # NOTE: you don't need the full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="169a0-206">`'kafka_broker'` 항목을 이 섹션의 1단계에서 반환된 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-206">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="169a0-207">__소프트웨어 VPN 클라이언트__를 사용하는 경우, `kafka_broker` 항목을 작업자 노드의 IP 주소와 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-207">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="169a0-208">__사용자 지정 DNS 서버를 통해 이름 확인을 할 수 있게__ 한 경우, `kafka_broker` 항목을 작업자 노드의 FQDN과 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-208">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="169a0-209">이 코드는 문자열 `test message`를 토픽 `testtopic`으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-209">This code sends the string `test message` to the topic `testtopic`.</span></span> <span data-ttu-id="169a0-210">HDInsight에서 Kafka의 기본 구성은 토픽이 없을 때 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-210">The default configuration of Kafka on HDInsight is to create the topic if it does not exist.</span></span>

4. <span data-ttu-id="169a0-211">Kafka에서 메시지를 검색하려면 다음 Python 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-211">To retrieve the messages from Kafka, use the following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace the `ip_address` entries with the IP address of your worker nodes
   # Again, you only need one or two, not the full list.
   # Note: auto_offset_reset='earliest' resets the starting offset to the beginning
   #       of the topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="169a0-212">`'kafka_broker'` 항목을 이 섹션의 1단계에서 반환된 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-212">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="169a0-213">__소프트웨어 VPN 클라이언트__를 사용하는 경우, `kafka_broker` 항목을 작업자 노드의 IP 주소와 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-213">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="169a0-214">__사용자 지정 DNS 서버를 통해 이름 확인을 할 수 있게__ 한 경우, `kafka_broker` 항목을 작업자 노드의 FQDN과 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="169a0-214">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="169a0-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="169a0-215">Next steps</span></span>

<span data-ttu-id="169a0-216">HDInsight와 함께 가상 네트워크를 사용하는 방법에 대한 자세한 내용은 [Azure Virtual Network를 사용하여 Azure HDInsight 확장](hdinsight-extend-hadoop-virtual-network.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="169a0-216">For more information on using HDInsight with a virtual network, see the [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="169a0-217">지점-사이트 간 VPN Gateway를 사용하여 Azure Virtual Network를 만드는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="169a0-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see the following documents:</span></span>

* [<span data-ttu-id="169a0-218">Azure Portal을 사용하여 지점 및 사이트 간 연결 구성</span><span class="sxs-lookup"><span data-stu-id="169a0-218">Configure a Point-to-Site connection using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="169a0-219">Azure PowerShell을 사용하여 지점 및 사이트 간 연결 구성</span><span class="sxs-lookup"><span data-stu-id="169a0-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="169a0-220">HDInsight에서 Kafka를 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="169a0-220">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="169a0-221">HDInsight에서 Apache Kafka 시작</span><span class="sxs-lookup"><span data-stu-id="169a0-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="169a0-222">HDInsight에서 Kafka에 미러링 사용</span><span class="sxs-lookup"><span data-stu-id="169a0-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
