---
title: "aaaUsing 동적 DNS tooregister 호스트 이름"
description: "이 페이지 방법에 대해 자세하게 tooset 사용자 고유의 DNS 서버에 동적 DNS tooregister 호스트 이름 구성 합니다."
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
ms.openlocfilehash: 8d4b44265714e6976f26bfb3446e8101aa70996a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a>자체 DNS 서버에서 동적 DNS tooregister 호스트 이름을 사용 하 여
[Azure가 이름 확인을 제공](virtual-networks-name-resolution-for-vms-and-role-instances.md) 합니다. 그러나 이름 확인을 위해 Azure가 제공하는 기능 이상이 필요한 경우 자체 DNS 서버를 제공할 수 있습니다. 전원 tootailor DNS 솔루션 toosuit hello이에서는 특정 요구 사항입니다. 예를 들어 Active Directory 도메인 컨트롤러를 통해 tooaccess 온-프레미스 리소스를 할 수 있습니다.

사용자 지정 DNS 서버에서 전달할 수는 Azure Vm으로 호스팅되는 경우 호스트 이름 쿼리 hello에 대 한 동일한 vnet tooAzure tooresolve 호스트 이름입니다. 싶지 않은 toouse이이 경로 동적 DNS를 사용 하 여 DNS 서버에서 VM 호스트를 등록할 수 있습니다.  Azure는 hello 기능 (예: 자격 증명) toodirectly 대체 정렬 필요 하므로 DNS 서버에 레코드를 만들 필요는 없습니다. 대체 항목으로 몇 가지 일반적인 시나리오는 다음과 같습니다.

## <a name="windows-clients"></a>Windows 클라이언트
비 도메인에 연결된 Windows 클라이언트는 부팅하거나 해당 IP 주소가 변경될 때 보안되지 않은 DDNS(동적 DNS) 업데이트를 시도합니다. hello DNS 이름은 hello 주 DNS 접미사 함께 hello 호스트 이름입니다. Azure hello 주 DNS 접미사를 빈 상태로 두고 hello 통해 VM hello에 설정할 수 있습니다 [UI](https://technet.microsoft.com/library/cc794784.aspx) 또는 [자동화를 사용 하 여](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix)합니다.

보안 동적 DNS를 사용 하 여 hello 도메인 컨트롤러와 해당 IP 주소를 등록 하는 도메인에 가입 된 Windows 클라이언트. hello 도메인 가입 프로세스 hello 클라이언트 hello 주 DNS 접미사를 설정 하 고 만들고 hello 트러스트 관계를 유지 관리 합니다.

## <a name="linux-clients"></a>Linux 클라이언트
Linux 클라이언트 일반적으로 등록 하지 않는 자체를 시작할 때 hello DNS 서버, DHCP 서버 hello는 가정 합니다. Azure의 DHCP 서버 hello 기능 또는 자격 증명 tooregister 레코드에에서 없는 DNS 서버입니다.  라는 도구를 사용할 수 있습니다 *nsupdate*, hello 바인딩 패키지에 포함 되어 있는, toosend 동적 DNS 업데이트 합니다. 동적 DNS 프로토콜 hello는 표준화 되었으므로 사용할 수 있습니다 *nsupdate* 도 경우 사용 하지 않는 바인딩 hello DNS 서버에 있습니다.

Hello DHCP 클라이언트 toocreate에서 제공 하는 hello 후크를 사용할 수 있으며 hello hostname 항목 hello DNS 서버에서 유지 관리할 수 있습니다. Hello 클라이언트 hello DHCP 주기 중에 hello 스크립트를 실행 */etc/dhcp/dhclient-exit-hooks.d/*합니다. 이 수를 사용 하 여 tooregister hello 새 IP 주소를 사용할 *nsupdate*합니다. 예:

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on hello primary nic
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

        
        

Hello를 사용할 수도 있습니다 *nsupdate* 명령 tooperform 보안 동적 DNS 업데이트 합니다. 예를 들어 Bind DNS 서버를 사용하는 경우 공개-개인 키 쌍이 [생성](http://linux.yyz.us/nsupdate/)됩니다.  hello DNS 서버는 [구성](http://linux.yyz.us/dns/ddns-server.html) hello 한다는 hello 요청에서 hello 서명을 확인할 수 있도록 hello 키의 공개 부분을 사용 합니다. Hello를 사용 해야 *-k* 옵션 tooprovide 키 쌍을 너무 hello*nsupdate* 순서로 hello에 대 한 동적 DNS 업데이트 요청 toobe 서명 합니다.

Windows DNS 서버를 사용 하는 경우 hello로 Kerberos 인증을 사용할 수 있습니다 *-g* 매개 변수에서 *nsupdate* (의 hello Windows 버전에서 사용할 수 없는 *nsupdate* ). toodo이를 사용 하이 여 *kinit* tooload hello 자격 증명 (예: 한 [keytab 파일](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)). 그런 다음 *nsupdate g* hello 캐시에서 hello 자격 증명을 선택 합니다.

필요한 경우 DNS 검색 접미사 tooyour Vm을 추가할 수 있습니다. hello DNS 접미사 hello에 지정 된 */etc/resolv.conf* 파일입니다. Hello 콘텐츠를 자동으로 관리 하는 대부분의 Linux 배포판이이 파일의 하므로 일반적으로 편집할 수 없습니다. 그러나 hello DHCP 클라이언트를 사용 하 여 hello 접미사를 재정의할 수 있습니다 *교체* 명령입니다. toodo이, */etc/dhcp/dhclient.conf*, 추가:

        supersede domain-name <required-dns-suffix>;

