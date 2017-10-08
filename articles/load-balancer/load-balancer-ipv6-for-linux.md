---
title: "Linux vm의 DHCPv6 aaaConfiguring | Microsoft Docs"
description: "어떻게 tooconfigure DHCPv6 Linux Vm에 대 한 합니다."
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
ms.openlocfilehash: abd5a98c3496b189946f59bab1d9c20dcd0aa2c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="2900e-104">Linux VM에 대한 DHCPv6 구성</span><span class="sxs-lookup"><span data-stu-id="2900e-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="2900e-105">Hello Azure Marketplace의에서 hello Linux 가상 컴퓨터 이미지 중 일부는 기본적으로 구성 하는 DHCPv6 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-105">Some of hello Linux virtual machine images in hello Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="2900e-106">IPv6, DHCPv6 toosupport 사용 중인 hello Linux 운영 체제 배포 내에서 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-106">toosupport IPv6, DHCPv6 must be configured in within hello Linux OS distribution that you are using.</span></span> <span data-ttu-id="2900e-107">다른 Linux 배포는 다른 패키지를 사용하기 때문에 DHCPv6는 다른 방법으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="2900e-108">Hello Azure Marketplace에서에서 최근 SUSE Linux 및 CoreOS 이미지 DHCPv6와 미리 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-108">Recent SUSE Linux and CoreOS images in hello Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="2900e-109">이러한 이미지를 사용할 경우 추가 변경이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="2900e-110">이 문서에서는 설명 방법을 tooenable DHCPv6 Linux 가상 컴퓨터는 IPv6 주소를 가져오도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-110">This document describes how tooenable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="2900e-111">부적절 하 게 네트워크 구성 파일을 편집 하면 toolose 네트워크 액세스 tooyour VM 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-111">Improperly editing network configuration files can cause you toolose network access tooyour VM.</span></span> <span data-ttu-id="2900e-112">구성 변경 테스트는 비프로덕션 시스템에서 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="2900e-113">이 문서의 지침 hello hello 최신 버전의 hello Azure Marketplace에서에서 hello Linux 이미지에서 테스트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-113">hello instructions in this article have been tested on hello latest versions of hello Linux images in hello Azure Marketplace.</span></span> <span data-ttu-id="2900e-114">자세한 지침은 Linux의 특정 버전에 대 한 hello 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2900e-114">Consult hello documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="2900e-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="2900e-115">Ubuntu</span></span>

1. <span data-ttu-id="2900e-116">Hello 파일을 편집 `/etc/dhcp/dhclient6.conf` hello 다음 줄 추가:</span><span class="sxs-lookup"><span data-stu-id="2900e-116">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="2900e-117">같은 구성이 hello로 hello eth0 인터페이스에 대 한 hello 네트워크 구성을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-117">Edit hello network configuration for hello eth0 interface with hello following configuration:</span></span>

   * <span data-ttu-id="2900e-118">**Ubuntu 12.04 및 14.04**, hello 파일 편집`/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="2900e-118">On **Ubuntu 12.04 and 14.04**, edit hello file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="2900e-119">**Ubuntu 16.04**, hello 파일 편집`/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="2900e-119">On **Ubuntu 16.04**, edit hello file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="2900e-120">IPv6 주소를 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="2900e-121">Debian</span><span class="sxs-lookup"><span data-stu-id="2900e-121">Debian</span></span>

1. <span data-ttu-id="2900e-122">Hello 파일을 편집 `/etc/dhcp/dhclient6.conf` hello 다음 줄 추가:</span><span class="sxs-lookup"><span data-stu-id="2900e-122">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="2900e-123">Hello 파일을 편집 `/etc/network/interfaces` hello 같은 구성이 추가:</span><span class="sxs-lookup"><span data-stu-id="2900e-123">Edit hello file `/etc/network/interfaces` and add hello following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="2900e-124">IPv6 주소를 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="2900e-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="2900e-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="2900e-126">Hello 파일을 편집 `/etc/sysconfig/network` hello 매개 변수 뒤에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-126">Edit hello file `/etc/sysconfig/network` and add hello following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="2900e-127">Hello 파일을 편집 `/etc/sysconfig/network-scripts/ifcfg-eth0` hello 다음 두 개의 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-127">Edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="2900e-128">IPv6 주소를 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="2900e-129">SLES 11 및 openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="2900e-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="2900e-130">Azure의 최근 SLES 및 openSUSE 이미지는 DHCPv6를 사용해 미리 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="2900e-131">이러한 이미지를 사용할 경우 추가 변경이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="2900e-132">이전 버전 또는 사용자 지정 SUSE 이미지에 따라 VM이 있는 경우 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-132">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="2900e-133">Hello 설치 `dhcp-client` 패키지 하 고, 필요한 경우:</span><span class="sxs-lookup"><span data-stu-id="2900e-133">Install hello `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="2900e-134">Hello 파일을 편집 `/etc/sysconfig/network/ifcfg-eth0` hello 매개 변수 뒤에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-134">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and add hello following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="2900e-135">Hello IPv6 주소를 갱신 합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-135">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="2900e-136">SLES 12 및 openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="2900e-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="2900e-137">Azure의 최근 SLES 및 openSUSE 이미지는 DHCPv6를 사용해 미리 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="2900e-138">이러한 이미지를 사용할 경우 추가 변경이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="2900e-139">이전 버전 또는 사용자 지정 SUSE 이미지에 따라 VM이 있는 경우 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-139">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="2900e-140">Hello 파일을 편집 `/etc/sysconfig/network/ifcfg-eth0` 및이 매개 변수 바꾸기</span><span class="sxs-lookup"><span data-stu-id="2900e-140">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="2900e-141">다음 값 hello로:</span><span class="sxs-lookup"><span data-stu-id="2900e-141">with hello following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="2900e-142">추가 매개 변수를 너무 다음 hello`/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="2900e-142">Add hello following parameter too`/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="2900e-143">Hello IPv6 주소를 갱신 합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-143">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="2900e-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2900e-144">CoreOS</span></span>

<span data-ttu-id="2900e-145">Azure의 최근 CoreOS 이미지는 DHCPv6를 사용해 미리 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="2900e-146">이러한 이미지를 사용할 경우 추가 변경이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="2900e-147">이전 버전 또는 사용자 지정 CoreOS 이미지에 따라 VM이 있는 경우 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-147">If you have a VM based on an older or custom CoreOS image, use hello following steps:</span></span>

1. <span data-ttu-id="2900e-148">Hello 파일 편집`/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="2900e-148">Edit hello file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="2900e-149">Hello IPv6 주소를 갱신 합니다.</span><span class="sxs-lookup"><span data-stu-id="2900e-149">Renew hello IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
