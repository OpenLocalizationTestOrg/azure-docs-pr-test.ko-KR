---
title: "Linux VM에 대한 DHCPv6 구성 | Microsoft Docs"
description: "Linux VM에 대한 DHCPv6를 구성하는 방법"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "ipv6, Azure Load Balancer, 이중 스택, 공용 IP, 기본 ipv6, 모바일, iot"
ms.assetid: b32719b6-00e8-4cd0-ba7f-e60e8146084b
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 5c591e7f1838c86ca74caea9dd3a5e8f874fd8a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="d3b94-104">Linux VM에 대한 DHCPv6 구성</span><span class="sxs-lookup"><span data-stu-id="d3b94-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="d3b94-105">Azure Marketplace의 Linux 가상 컴퓨터 이미지 중 일부에는 기본적으로 구성된 DHCPv6가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-105">Some of the Linux virtual machine images in the Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="d3b94-106">IPv6를 지원하려면 DHCPv6가 사용 중인 Linux OS 배포 내에 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-106">To support IPv6, DHCPv6 must be configured in within the Linux OS distribution that you are using.</span></span> <span data-ttu-id="d3b94-107">다른 Linux 배포는 다른 패키지를 사용하기 때문에 DHCPv6는 다른 방법으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="d3b94-108">Azure Marketplace의 최근 SUSE Linux 및 CoreOS 이미지는 DHCPv6를 사용해 미리 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-108">Recent SUSE Linux and CoreOS images in the Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="d3b94-109">이러한 이미지를 사용할 경우 추가 변경이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="d3b94-110">이 문서에서는 Linux 가상 컴퓨터가 IPv6 주소를 확보할 수 있게 DHCPv6를 사용하도록 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-110">This document describes how to enable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="d3b94-111">네트워크 구성 파일을 부적절하게 편집한다면 VM에 대한 네트워크 액세스를 하지 못하게 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-111">Improperly editing network configuration files can cause you to lose network access to your VM.</span></span> <span data-ttu-id="d3b94-112">구성 변경 테스트는 비프로덕션 시스템에서 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="d3b94-113">이 문서의 지침에서는 Linux 이미지는 Azure Marketplace의 최신 버전에서 테스트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-113">The instructions in this article have been tested on the latest versions of the Linux images in the Azure Marketplace.</span></span> <span data-ttu-id="d3b94-114">더 자세한 지침은 특정 버전의 Linux 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3b94-114">Consult the documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="d3b94-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d3b94-115">Ubuntu</span></span>

1. <span data-ttu-id="d3b94-116">파일 `/etc/dhcp/dhclient6.conf` 을 편집하고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-116">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="d3b94-117">다음 구성을 사용하여 eth0 인터페이스에 대한 네트워크 구성을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-117">Edit the network configuration for the eth0 interface with the following configuration:</span></span>

   * <span data-ttu-id="d3b94-118">**Ubuntu 12.04 and 14.04**에서 `/etc/network/interfaces.d/eth0.cfg` 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-118">On **Ubuntu 12.04 and 14.04**, edit the file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="d3b94-119">**Ubuntu 16.04**에서 `/etc/network/interfaces.d/50-cloud-init.cfg` 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-119">On **Ubuntu 16.04**, edit the file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="d3b94-120">IPv6 주소를 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="d3b94-121">Debian</span><span class="sxs-lookup"><span data-stu-id="d3b94-121">Debian</span></span>

1. <span data-ttu-id="d3b94-122">파일 `/etc/dhcp/dhclient6.conf` 을 편집하고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-122">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="d3b94-123">파일 `/etc/network/interfaces` 을 편집하고 다음 구성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-123">Edit the file `/etc/network/interfaces` and add the following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="d3b94-124">IPv6 주소를 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="d3b94-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="d3b94-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="d3b94-126">파일 `/etc/sysconfig/network` 을 편집하고 다음 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-126">Edit the file `/etc/sysconfig/network` and add the following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="d3b94-127">파일 `/etc/sysconfig/network-scripts/ifcfg-eth0` 을 편집하고 다음 두 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-127">Edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="d3b94-128">IPv6 주소를 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="d3b94-129">SLES 11 및 openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="d3b94-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="d3b94-130">Azure의 최근 SLES 및 openSUSE 이미지는 DHCPv6를 사용해 미리 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="d3b94-131">이러한 이미지를 사용할 경우 추가 변경이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="d3b94-132">이전 또는 사용자 지정 SUSE 이미지를 기반으로 하는 VM인 경우 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-132">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="d3b94-133">필요하다면 `dhcp-client` 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-133">Install the `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="d3b94-134">파일 `/etc/sysconfig/network/ifcfg-eth0` 을 편집하고 다음 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-134">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and add the following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="d3b94-135">IPv6 주소를 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-135">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="d3b94-136">SLES 12 및 openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="d3b94-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="d3b94-137">Azure의 최근 SLES 및 openSUSE 이미지는 DHCPv6를 사용해 미리 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="d3b94-138">이러한 이미지를 사용할 경우 추가 변경이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="d3b94-139">이전 또는 사용자 지정 SUSE 이미지를 기반으로 하는 VM인 경우 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-139">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="d3b94-140">파일 `/etc/sysconfig/network/ifcfg-eth0` 을 편집하고 이 매개 변수를 교체합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-140">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="d3b94-141">다음 값으로.</span><span class="sxs-lookup"><span data-stu-id="d3b94-141">with the following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="d3b94-142">다음 매개 변수를 `/etc/sysconfig/network/ifcfg-eth0`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-142">Add the following parameter to `/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="d3b94-143">IPv6 주소를 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-143">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="d3b94-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="d3b94-144">CoreOS</span></span>

<span data-ttu-id="d3b94-145">Azure의 최근 CoreOS 이미지는 DHCPv6를 사용해 미리 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="d3b94-146">이러한 이미지를 사용할 경우 추가 변경이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="d3b94-147">이전 또는 사용자 지정 CoreOS 이미지를 기반으로 하는 VM인 경우 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-147">If you have a VM based on an older or custom CoreOS image, use the following steps:</span></span>

1. <span data-ttu-id="d3b94-148">파일 `/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="d3b94-148">Edit the file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="d3b94-149">IPv6 주소를 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="d3b94-149">Renew the IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
