---
title: "동적 DNS를 사용하여 호스트 이름 등록"
description: "이 페이지에서는 고유의 DNS 서버에서 호스트 이름을 등록하기 위해 동적 DNS를 설치하는 방법에 대한 세부 정보를 제공합니다."
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: 
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 440a062e5fff73526b2d77d7d0a7c52ca72a66f1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-dynamic-dns-to-register-hostnames-in-your-own-dns-server"></a>동적 DNS를 사용하여 자체 DNS 서버에 호스트 이름 등록
[Azure가 이름 확인을 제공](virtual-networks-name-resolution-for-vms-and-role-instances.md) 합니다. 그러나 이름 확인을 위해 Azure가 제공하는 기능 이상이 필요한 경우 자체 DNS 서버를 제공할 수 있습니다. 그러면 특정한 자체 요구에 맞게 DNS 솔루션을 맞춤식 구성을 할 수 있게 됩니다. 예를 들어 Active Directory 도메인 컨트롤러를 통해 온-프레미스 리소스에 액세스해야 할 수 있습니다.

사용자 지정 DNS 서버가 Azure VM으로 호스트되는 경우 호스트 이름 쿼리(동일한 VNet에 대해)를 Azure로 전달하여 호스트 이름을 확인할 수 있습니다. 이 경로를 사용하지 않으려는 경우 동적 DNS를 사용하여 DNS 서버에 VM 호스트 이름을 등록할 수 있습니다.  Azure에는 DNS 서버에 레코드를 직접 등록하는 기능(예: 자격 증명)이 없으므로 종종 대체 정렬이 필요합니다. 대체 항목으로 몇 가지 일반적인 시나리오는 다음과 같습니다.

## <a name="windows-clients"></a>Windows 클라이언트
비 도메인에 연결된 Windows 클라이언트는 부팅하거나 해당 IP 주소가 변경될 때 보안되지 않은 DDNS(동적 DNS) 업데이트를 시도합니다. DNS 이름은 호스트 이름과 주 DNS 접미사입니다. Azure는 주 DNS 접미사를 비워 두지만 [UI](https://technet.microsoft.com/library/cc794784.aspx)를 통하거나 [자동화를 사용하여](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix) VM에서 설정할 수 있습니다.

도메인에 연결된 Windows 클라이언트는 보안 동적 DNS를 사용하여 해당 IP를 도메인 컨트롤러에 등록합니다. 도메인 연결 프로세스는 클라이언트에 대한 주 DNS 접미사를 설정하고 트러스트 관계를 만들고 유지 관리합니다.

## <a name="linux-clients"></a>Linux 클라이언트
Linux 클라이언트는 시작할 때 DNS 서버를 사용하여 일반적으로 등록하지 않고 DHCP 서버가 수행한다고 가정합니다. Azure의 DHCP 서버에는 DNS 서버에 레코드를 등록할 수 있는 기능 또는 자격 증명이 없습니다.  동적 DNS 업데이트에 전송하는 데 Bind 패키지에 포함되어 있는 *nsupdate*라는 도구를 사용할 수 있습니다. 동적 DNS 프로토콜은 표준화되어 있으므로 DNS 서버에서 Bind를 사용하지 않는 경우에도 *nsupdate* 를 사용할 수 있습니다.

DNS 서버에서 호스트 이름을 만들고 유지 관리하기 위해 DHCP 클라이언트에서 제공하는 후크를 사용할 수 있습니다. DHCP 주기 동안 클라이언트는 */etc/dhcp/dhclient-exit-hooks.d/*에서 스크립트를 실행합니다. *nsupdate*를 사용하여 새 IP 주소를 등록하는 데 사용할 수 있습니다. 예:

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on the primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
        if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
           [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
        then
            host=`hostname`
            nsupdatecmds=/var/tmp/nsupdatecmds
              echo "update delete $host.$requireddomain a" > $nsupdatecmds
              echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
              echo "send" >> $nsupdatecmds

              nsupdate $nsupdatecmds
        fi

        
        

보안 동적 DNS 업데이트를 수행하는 데 *nsupdate* 명령도 사용할 수 있습니다. 예를 들어 Bind DNS 서버를 사용하는 경우 공개-개인 키 쌍이 [생성](http://linux.yyz.us/nsupdate/)됩니다.  요청된 서명을 확인할 수 있도록 DNS 서버는 키의 공개 부분으로 [구성](http://linux.yyz.us/dns/ddns-server.html) 됩니다. 동적 DNS 업데이트 요청이 서명되도록 하기 위해 *nsupdate*에 키-쌍을 제공하는 데 *-k* 옵션을 사용해야 합니다.

Windows DNS 서버를 사용하는 경우 Kerberos 인증은 *nsupdate*의 *-g* 매개 변수와 함께 사용할 수 있습니다(Windows 버전의 *nsupdate*에서 사용할 수 없음). 이렇게 하려면 *kinit* 를 사용하여 자격 증명을 로드합니다(예: [keytab 파일](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)에서). 그런 다음 *nsupdate -g* 를 통해 캐시에서 자격 증명을 선택합니다.

필요한 경우 DNS 검색 접미사를 VM에 추가할 수 있습니다. DNS 접미사는 */etc/resolv.conf* 파일에 지정됩니다. 대부분의 Linux 배포판은 자동으로 이 파일의 콘텐츠를 관리하므로 일반적으로 편집할 수 없습니다. 그러나 DHCP 클라이언트의 *supersede* 명령을 사용하여 접미사를 재정의할 수 있습니다. 이렇게 하려면 */etc/dhcp/dhclient.conf*에서 추가합니다.

        supersede domain-name <required-dns-suffix>;

