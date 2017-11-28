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
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a><span data-ttu-id="c8f90-103">자체 DNS 서버에서 동적 DNS tooregister 호스트 이름을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c8f90-103">Using Dynamic DNS tooregister hostnames in your own DNS server</span></span>
<span data-ttu-id="c8f90-104">[Azure가 이름 확인을 제공](virtual-networks-name-resolution-for-vms-and-role-instances.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="c8f90-105">그러나 이름 확인을 위해 Azure가 제공하는 기능 이상이 필요한 경우 자체 DNS 서버를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="c8f90-106">전원 tootailor DNS 솔루션 toosuit hello이에서는 특정 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-106">This gives you hello power tootailor your DNS solution toosuit your own specific needs.</span></span> <span data-ttu-id="c8f90-107">예를 들어 Active Directory 도메인 컨트롤러를 통해 tooaccess 온-프레미스 리소스를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-107">For example, you may need tooaccess on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="c8f90-108">사용자 지정 DNS 서버에서 전달할 수는 Azure Vm으로 호스팅되는 경우 호스트 이름 쿼리 hello에 대 한 동일한 vnet tooAzure tooresolve 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for hello same vnet tooAzure tooresolve hostnames.</span></span> <span data-ttu-id="c8f90-109">싶지 않은 toouse이이 경로 동적 DNS를 사용 하 여 DNS 서버에서 VM 호스트를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-109">If you do not wish toouse this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="c8f90-110">Azure는 hello 기능 (예: 자격 증명) toodirectly 대체 정렬 필요 하므로 DNS 서버에 레코드를 만들 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-110">Azure doesn't have hello ability (e.g. credentials) toodirectly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="c8f90-111">대체 항목으로 몇 가지 일반적인 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="c8f90-112">Windows 클라이언트</span><span class="sxs-lookup"><span data-stu-id="c8f90-112">Windows clients</span></span>
<span data-ttu-id="c8f90-113">비 도메인에 연결된 Windows 클라이언트는 부팅하거나 해당 IP 주소가 변경될 때 보안되지 않은 DDNS(동적 DNS) 업데이트를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="c8f90-114">hello DNS 이름은 hello 주 DNS 접미사 함께 hello 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-114">hello DNS name is hello hostname plus hello primary DNS suffix.</span></span> <span data-ttu-id="c8f90-115">Azure hello 주 DNS 접미사를 빈 상태로 두고 hello 통해 VM hello에 설정할 수 있습니다 [UI](https://technet.microsoft.com/library/cc794784.aspx) 또는 [자동화를 사용 하 여](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-115">Azure leaves hello primary DNS suffix blank, but you can set this in hello VM, via hello [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="c8f90-116">보안 동적 DNS를 사용 하 여 hello 도메인 컨트롤러와 해당 IP 주소를 등록 하는 도메인에 가입 된 Windows 클라이언트.</span><span class="sxs-lookup"><span data-stu-id="c8f90-116">Domain-joined Windows clients register their IP addresses with hello domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="c8f90-117">hello 도메인 가입 프로세스 hello 클라이언트 hello 주 DNS 접미사를 설정 하 고 만들고 hello 트러스트 관계를 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-117">hello domain-join process sets hello primary DNS suffix on hello client and creates and maintains hello trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="c8f90-118">Linux 클라이언트</span><span class="sxs-lookup"><span data-stu-id="c8f90-118">Linux clients</span></span>
<span data-ttu-id="c8f90-119">Linux 클라이언트 일반적으로 등록 하지 않는 자체를 시작할 때 hello DNS 서버, DHCP 서버 hello는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-119">Linux clients generally don't register themselves with hello DNS server on startup, they assume hello DHCP server does it.</span></span> <span data-ttu-id="c8f90-120">Azure의 DHCP 서버 hello 기능 또는 자격 증명 tooregister 레코드에에서 없는 DNS 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-120">Azure's DHCP servers do not have hello ability or credentials tooregister records in your DNS server.</span></span>  <span data-ttu-id="c8f90-121">라는 도구를 사용할 수 있습니다 *nsupdate*, hello 바인딩 패키지에 포함 되어 있는, toosend 동적 DNS 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-121">You can use a tool called *nsupdate*, which is included in hello Bind package, toosend Dynamic DNS updates.</span></span> <span data-ttu-id="c8f90-122">동적 DNS 프로토콜 hello는 표준화 되었으므로 사용할 수 있습니다 *nsupdate* 도 경우 사용 하지 않는 바인딩 hello DNS 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-122">Because hello Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on hello DNS server.</span></span>

<span data-ttu-id="c8f90-123">Hello DHCP 클라이언트 toocreate에서 제공 하는 hello 후크를 사용할 수 있으며 hello hostname 항목 hello DNS 서버에서 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-123">You can use hello hooks that are provided by hello DHCP client toocreate and maintain hello hostname entry in hello DNS server.</span></span> <span data-ttu-id="c8f90-124">Hello 클라이언트 hello DHCP 주기 중에 hello 스크립트를 실행 */etc/dhcp/dhclient-exit-hooks.d/*합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-124">During hello DHCP cycle, hello client executes hello scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="c8f90-125">이 수를 사용 하 여 tooregister hello 새 IP 주소를 사용할 *nsupdate*합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-125">This can be used tooregister hello new IP address by using *nsupdate*.</span></span> <span data-ttu-id="c8f90-126">예:</span><span class="sxs-lookup"><span data-stu-id="c8f90-126">For example:</span></span>

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

        
        

<span data-ttu-id="c8f90-127">Hello를 사용할 수도 있습니다 *nsupdate* 명령 tooperform 보안 동적 DNS 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-127">You can also use hello *nsupdate* command tooperform secure Dynamic DNS updates.</span></span> <span data-ttu-id="c8f90-128">예를 들어 Bind DNS 서버를 사용하는 경우 공개-개인 키 쌍이 [생성](http://linux.yyz.us/nsupdate/)됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="c8f90-129">hello DNS 서버는 [구성](http://linux.yyz.us/dns/ddns-server.html) hello 한다는 hello 요청에서 hello 서명을 확인할 수 있도록 hello 키의 공개 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-129">hello DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with hello public part of hello key so that it can verify hello signature on hello request.</span></span> <span data-ttu-id="c8f90-130">Hello를 사용 해야 *-k* 옵션 tooprovide 키 쌍을 너무 hello*nsupdate* 순서로 hello에 대 한 동적 DNS 업데이트 요청 toobe 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-130">You must use hello *-k* option tooprovide hello key-pair too*nsupdate* in order for hello Dynamic DNS update request toobe signed.</span></span>

<span data-ttu-id="c8f90-131">Windows DNS 서버를 사용 하는 경우 hello로 Kerberos 인증을 사용할 수 있습니다 *-g* 매개 변수에서 *nsupdate* (의 hello Windows 버전에서 사용할 수 없는 *nsupdate* ).</span><span class="sxs-lookup"><span data-stu-id="c8f90-131">When you're using a Windows DNS server, you can use Kerberos authentication with hello *-g* parameter in *nsupdate* (not available in hello Windows version of *nsupdate*).</span></span> <span data-ttu-id="c8f90-132">toodo이를 사용 하이 여 *kinit* tooload hello 자격 증명 (예: 한 [keytab 파일](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="c8f90-132">toodo this, use *kinit* tooload hello credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="c8f90-133">그런 다음 *nsupdate g* hello 캐시에서 hello 자격 증명을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-133">Then *nsupdate -g* will pick up hello credentials from hello cache.</span></span>

<span data-ttu-id="c8f90-134">필요한 경우 DNS 검색 접미사 tooyour Vm을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-134">If needed, you can add a DNS search suffix tooyour VMs.</span></span> <span data-ttu-id="c8f90-135">hello DNS 접미사 hello에 지정 된 */etc/resolv.conf* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-135">hello DNS suffix is specified in hello */etc/resolv.conf* file.</span></span> <span data-ttu-id="c8f90-136">Hello 콘텐츠를 자동으로 관리 하는 대부분의 Linux 배포판이이 파일의 하므로 일반적으로 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-136">Most Linux distros automatically manage hello content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="c8f90-137">그러나 hello DHCP 클라이언트를 사용 하 여 hello 접미사를 재정의할 수 있습니다 *교체* 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f90-137">However, you can override hello suffix by using hello DHCP client's *supersede* command.</span></span> <span data-ttu-id="c8f90-138">toodo이, */etc/dhcp/dhclient.conf*, 추가:</span><span class="sxs-lookup"><span data-stu-id="c8f90-138">toodo this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

