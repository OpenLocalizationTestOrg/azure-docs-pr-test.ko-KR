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
# <a name="configuring-dhcpv6-for-linux-vms"></a>Linux VM에 대한 DHCPv6 구성

Hello Azure Marketplace의에서 hello Linux 가상 컴퓨터 이미지 중 일부는 기본적으로 구성 하는 DHCPv6 갖지 않습니다. IPv6, DHCPv6 toosupport 사용 중인 hello Linux 운영 체제 배포 내에서 구성 되어야 합니다. 다른 Linux 배포는 다른 패키지를 사용하기 때문에 DHCPv6는 다른 방법으로 구성됩니다.

> [!NOTE]
> Hello Azure Marketplace에서에서 최근 SUSE Linux 및 CoreOS 이미지 DHCPv6와 미리 구성 되어 있습니다. 이러한 이미지를 사용할 경우 추가 변경이 필요하지 않습니다.

이 문서에서는 설명 방법을 tooenable DHCPv6 Linux 가상 컴퓨터는 IPv6 주소를 가져오도록 합니다.

> [!WARNING]
> 부적절 하 게 네트워크 구성 파일을 편집 하면 toolose 네트워크 액세스 tooyour VM 발생할 수 있습니다. 구성 변경 테스트는 비프로덕션 시스템에서 하는 것이 좋습니다. 이 문서의 지침 hello hello 최신 버전의 hello Azure Marketplace에서에서 hello Linux 이미지에서 테스트 되었습니다. 자세한 지침은 Linux의 특정 버전에 대 한 hello 설명서를 참조 하십시오.

## <a name="ubuntu"></a>Ubuntu

1. Hello 파일을 편집 `/etc/dhcp/dhclient6.conf` hello 다음 줄 추가:

        timeout 10;

2. 같은 구성이 hello로 hello eth0 인터페이스에 대 한 hello 네트워크 구성을 편집 합니다.

   * **Ubuntu 12.04 및 14.04**, hello 파일 편집`/etc/network/interfaces.d/eth0.cfg`
   * **Ubuntu 16.04**, hello 파일 편집`/etc/network/interfaces.d/50-cloud-init.cfg`

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. IPv6 주소를 갱신합니다.

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a>Debian

1. Hello 파일을 편집 `/etc/dhcp/dhclient6.conf` hello 다음 줄 추가:

        timeout 10;

2. Hello 파일을 편집 `/etc/network/interfaces` hello 같은 구성이 추가:

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. IPv6 주소를 갱신합니다.

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a>RHEL / CentOS / Oracle Linux

1. Hello 파일을 편집 `/etc/sysconfig/network` hello 매개 변수 뒤에 추가 합니다.

        NETWORKING_IPV6=yes

2. Hello 파일을 편집 `/etc/sysconfig/network-scripts/ifcfg-eth0` hello 다음 두 개의 매개 변수를 추가 합니다.

        IPV6INIT=yes
        DHCPV6C=yes

3. IPv6 주소를 갱신합니다.

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a>SLES 11 및 openSUSE 13

Azure의 최근 SLES 및 openSUSE 이미지는 DHCPv6를 사용해 미리 구성되었습니다. 이러한 이미지를 사용할 경우 추가 변경이 필요하지 않습니다. 이전 버전 또는 사용자 지정 SUSE 이미지에 따라 VM이 있는 경우 단계를 수행 하는 hello를 사용 합니다.

1. Hello 설치 `dhcp-client` 패키지 하 고, 필요한 경우:

    ```bash
    sudo zypper install dhcp-client
    ```

2. Hello 파일을 편집 `/etc/sysconfig/network/ifcfg-eth0` hello 매개 변수 뒤에 추가 합니다.

        DHCLIENT6_MODE='managed'

3. Hello IPv6 주소를 갱신 합니다.

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a>SLES 12 및 openSUSE Leap

Azure의 최근 SLES 및 openSUSE 이미지는 DHCPv6를 사용해 미리 구성되었습니다. 이러한 이미지를 사용할 경우 추가 변경이 필요하지 않습니다. 이전 버전 또는 사용자 지정 SUSE 이미지에 따라 VM이 있는 경우 단계를 수행 하는 hello를 사용 합니다.

1. Hello 파일을 편집 `/etc/sysconfig/network/ifcfg-eth0` 및이 매개 변수 바꾸기

        #BOOTPROTO='dhcp4'

    다음 값 hello로:

        BOOTPROTO='dhcp'

2. 추가 매개 변수를 너무 다음 hello`/etc/sysconfig/network/ifcfg-eth0`:

        DHCLIENT6_MODE='managed'

3. Hello IPv6 주소를 갱신 합니다.

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a>CoreOS

Azure의 최근 CoreOS 이미지는 DHCPv6를 사용해 미리 구성되었습니다. 이러한 이미지를 사용할 경우 추가 변경이 필요하지 않습니다. 이전 버전 또는 사용자 지정 CoreOS 이미지에 따라 VM이 있는 경우 단계를 수행 하는 hello를 사용 합니다.

1. Hello 파일 편집`/etc/systemd/network/10_dhcp.network`

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. Hello IPv6 주소를 갱신 합니다.

    ```bash
    sudo systemctl restart systemd-networkd
    ```
