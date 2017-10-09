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
# <a name="connect-hdinsight-tooyour-on-premise-network"></a><span data-ttu-id="78bc3-104">HDInsight tooyour 온-프레미스 네트워크에 연결</span><span class="sxs-lookup"><span data-stu-id="78bc3-104">Connect HDInsight tooyour on-premise network</span></span>

<span data-ttu-id="78bc3-105">어떻게 tooconnect HDInsight tooyour 온-프레미스 네트워크 VPN 게이트웨이 및 Azure 가상 네트워크를 사용 하 여에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-105">Learn how tooconnect HDInsight tooyour on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="78bc3-106">이 문서는 다음에 대한 계획 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-106">This document provides planning information on:</span></span>

* <span data-ttu-id="78bc3-107">HDInsight를 사용 하 여 tooyour 연결 하는 Azure 가상 네트워크에서 온-프레미스 네트워크.</span><span class="sxs-lookup"><span data-stu-id="78bc3-107">Using HDInsight in an Azure Virtual Network that connects tooyour on-premises network.</span></span>

* <span data-ttu-id="78bc3-108">Hello 가상 네트워크와 온-프레미스 네트워크의 DNS 이름 확인을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-108">Configuring DNS name resolution between hello virtual network and your on-premises network.</span></span>

* <span data-ttu-id="78bc3-109">네트워크 보안 그룹 toorestrict 인터넷 액세스 tooHDInsight를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-109">Configuring network security groups toorestrict internet access tooHDInsight.</span></span>

* <span data-ttu-id="78bc3-110">HDInsight hello 가상 네트워크에서 제공 하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-110">Ports provided by HDInsight on hello virtual network.</span></span>

## <a name="create-hello-virtual-network-configuration"></a><span data-ttu-id="78bc3-111">Hello 가상 네트워크 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="78bc3-111">Create hello Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78bc3-112">HDInsight tooyour 온-프레미스 Azure 가상 네트워크를 사용 하는 네트워크, hello 참조에 대 한 연결에 대 한 단계별 지침을 원하는 경우 [HDInsight 연결 tooyour 온-프레미스 네트워크](connect-on-premises-network.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="78bc3-112">If you are looking for step by step guidance on connecting HDInsight tooyour on-premises network using an Azure Virtual Network, see hello [Connect HDInsight tooyour on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="78bc3-113">사용 하 여 hello 다음 문서 toolearn 어떻게 toocreate Azure 가상 네트워크를 연결 된 tooyour 온-프레미스 네트워크:</span><span class="sxs-lookup"><span data-stu-id="78bc3-113">Use hello following documents toolearn how toocreate an Azure Virtual Network that is connected tooyour on-premises network:</span></span>
    
* [<span data-ttu-id="78bc3-114">Hello Azure 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="78bc3-114">Using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="78bc3-115">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="78bc3-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="78bc3-116">Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="78bc3-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="78bc3-117">이름 확인 구성</span><span class="sxs-lookup"><span data-stu-id="78bc3-117">Configure name resolution</span></span>

<span data-ttu-id="78bc3-118">HDInsight tooallow 및 리소스 이름으로 네트워크 toocommunicate 가입 hello에에서 hello 다음 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-118">tooallow HDInsight and resources in hello joined network toocommunicate by name, you must perform hello following actions:</span></span>

* <span data-ttu-id="78bc3-119">Hello Azure 가상 네트워크의에서 사용자 지정 DNS 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-119">Create a custom DNS server in hello Azure Virtual Network.</span></span>

* <span data-ttu-id="78bc3-120">Hello 가상 네트워크 toouse hello 사용자 지정 DNS 서버 hello 기본 Azure 재귀 확인자 대신를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-120">Configure hello virtual network toouse hello custom DNS server instead of hello default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="78bc3-121">사용자 지정 DNS 서버 hello와 온-프레미스 DNS 서버 간의 전달을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-121">Configure forwarding between hello custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="78bc3-122">이러한 구성을 통해 동작을 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="78bc3-122">This configuration enables hello following behavior:</span></span>

* <span data-ttu-id="78bc3-123">Hello DNS 접미사가 정규화 된 도메인 이름에 대 한 요청 __hello 가상 네트워크에 대 한__ toohello 사용자 지정 DNS 서버에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-123">Requests for fully qualified domain names that have hello DNS suffix __for hello virtual network__ are forwarded toohello custom DNS server.</span></span> <span data-ttu-id="78bc3-124">사용자 지정 DNS 서버 hello 이러한 요청 toohello hello IP 주소를 반환 하는 Azure 재귀 확인자, 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-124">hello custom DNS server then forwards these requests toohello Azure Recursive Resolver, which returns hello IP address.</span></span>

* <span data-ttu-id="78bc3-125">다른 모든 요청 toohello 온-프레미스 DNS 서버에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-125">All other requests are forwarded toohello on-premises DNS server.</span></span> <span data-ttu-id="78bc3-126">Microsoft.com 등 공용 인터넷 리소스에 대 한 요청을 포함 toohello 온-프레미스 DNS 서버 이름 확인을 위해 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-126">Even requests for public internet resources such as microsoft.com are forwarded toohello on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="78bc3-127">다음 다이어그램 hello에서 녹색 선은 hello 가상 네트워크의 DNS 접미사 hello로 끝나는 리소스에 대 한 요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-127">In hello following diagram, green lines are requests for resources that end in hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="78bc3-128">파란색 선은 또는 hello 온-프레미스 네트워크 리소스에 대 한 요청에는 공용 인터넷 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-128">Blue lines are requests for resources in hello on-premises network or on hello public internet.</span></span>

![이 문서에 사용 되는 hello 구성에서 DNS 요청 해결 되는 방법의 다이어그램](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="78bc3-130">사용자 지정 DNS 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="78bc3-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78bc3-131">만들기 및 HDInsight hello 가상 네트워크에 설치 하기 전에 hello DNS 서버를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-131">You must create and configure hello DNS server before installing HDInsight into hello virtual network.</span></span>

<span data-ttu-id="78bc3-132">toocreate hello를 사용 하 여 Linux VM [바인딩할](https://www.isc.org/downloads/bind/) DNS 소프트웨어를 사용 하 여 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-132">toocreate a Linux VM that uses hello [Bind](https://www.isc.org/downloads/bind/) DNS software, use hello following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="78bc3-133">hello 다음 단계 사용 하 여 hello [Azure 포털](https://portal.azure.com) toocreate Azure 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="78bc3-133">hello following steps use hello [Azure portal](https://portal.azure.com) toocreate an Azure Virtual Machine.</span></span> <span data-ttu-id="78bc3-134">가상 컴퓨터의 다른 방법으로 toocreate 참조 hello [VM 만들기-Azure CLI](../virtual-machines/linux/quick-create-cli.md) 및 [VM 만들기-Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="78bc3-134">For other ways toocreate a virtual machine, see hello [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="78bc3-135">Hello에서 [Azure 포털](https://portal.azure.com)선택,  __+__ , __계산__, 및 __Ubuntu Server 16.04 LTS__합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-135">From hello [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Ubuntu 가상 컴퓨터 만들기](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="78bc3-137">Hello에서 __기본 사항__ 섹션을 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-137">From hello __Basics__ section, enter hello following information:</span></span>

    * <span data-ttu-id="78bc3-138">__이름__: 이 가상 컴퓨터를 식별하는 친숙한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="78bc3-139">예: __DNSProxy__</span><span class="sxs-lookup"><span data-stu-id="78bc3-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="78bc3-140">__사용자 이름__: hello 이름 hello SSH 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-140">__User name__: hello name of hello SSH account.</span></span>
    * <span data-ttu-id="78bc3-141">__SSH 공개 키__ 또는 __암호__: hello hello SSH 계정에 대 한 인증 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-141">__SSH public key__ or __Password__: hello authentication method for hello SSH account.</span></span> <span data-ttu-id="78bc3-142">보다 안전한 공개 키를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="78bc3-143">자세한 내용은 참조 hello [Linux Vm에 대 한 SSH 키를 만들고 사용 하 여](../virtual-machines/linux/mac-create-ssh-keys.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="78bc3-143">For more information, see hello [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="78bc3-144">__리소스 그룹__: 선택 __기존 항목 사용__, 한 다음 앞에서 만든 hello 가상 네트워크를 포함 하는 hello 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-144">__Resource group__: Select __Use existing__, and then select hello resource group that contains hello virtual network created earlier.</span></span>
    * <span data-ttu-id="78bc3-145">__위치__: 선택 hello hello 가상 네트워크와 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-145">__Location__: Select hello same location as hello virtual network.</span></span>

    ![가상 컴퓨터 기본 구성](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="78bc3-147">다른 항목을 hello에 기본값을 유지 한 다음 선택 __확인__합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-147">Leave other entries at hello default values and then select __OK__.</span></span>

3. <span data-ttu-id="78bc3-148">Hello에서 __크기 선택__ 섹션에서 선택 hello VM 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-148">From hello __Choose a size__ section, select hello VM size.</span></span> <span data-ttu-id="78bc3-149">이 자습서에 대 한 가장 작은 hello를 선택 하 고 가장 낮은 비용 옵션.</span><span class="sxs-lookup"><span data-stu-id="78bc3-149">For this tutorial, select hello smallest and lowest cost option.</span></span> <span data-ttu-id="78bc3-150">toocontinue를 사용 하 여 hello __선택__ 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-150">toocontinue, use hello __Select__ button.</span></span>

4. <span data-ttu-id="78bc3-151">Hello에서 __설정__ 섹션을 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-151">From hello __Settings__ section, enter hello following information:</span></span>

    * <span data-ttu-id="78bc3-152">__가상 네트워크__: 선택 hello 앞에서 만든 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-152">__Virtual network__: Select hello virtual network that you created earlier.</span></span>

    * <span data-ttu-id="78bc3-153">__서브넷__: hello 가상 네트워크에 대 한 hello 기본 서브넷을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-153">__Subnet__: Select hello default subnet for hello virtual network.</span></span> <span data-ttu-id="78bc3-154">수행 __하지__ 선택 hello hello VPN 게이트웨이에서 사용 되는 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-154">Do __not__ select hello subnet used by hello VPN gateway.</span></span>

    * <span data-ttu-id="78bc3-155">__진단 저장소 계정__: 기존 저장소 계정을 선택하거나 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![가상 네트워크 설정](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="78bc3-157">Hello 기본값 hello 다른 항목을 유지 한 다음 선택 __확인__ toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-157">Leave hello other entries at hello default value, then select __OK__ toocontinue.</span></span>

5. <span data-ttu-id="78bc3-158">Hello에서 __구매__ 섹션을 선택 하는 hello __구매__ 단추 toocreate hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="78bc3-158">From hello __Purchase__ section, select hello __Purchase__ button toocreate hello virtual machine.</span></span>

6. <span data-ttu-id="78bc3-159">Hello 가상 컴퓨터를 만든 후 해당 __개요__ 섹션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-159">Once hello virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="78bc3-160">Hello 왼쪽에 hello 목록에서 선택 __속성__합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-160">From hello list on hello left, select __Properties__.</span></span> <span data-ttu-id="78bc3-161">Hello 저장 __공용 IP 주소__ 및 __개인 IP 주소가__ 값입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-161">Save hello __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="78bc3-162">Hello 다음 섹션에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-162">It will be used in hello next section.</span></span>

    ![공용 및 개인 IP 주소](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="78bc3-164">Bind(DNS 소프트웨어) 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="78bc3-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="78bc3-165">SSH tooconnect toohello를 사용 하 여 __공용 IP 주소__ hello 가상 컴퓨터의 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-165">Use SSH tooconnect toohello __public IP address__ of hello virtual machine.</span></span> <span data-ttu-id="78bc3-166">다음 예제는 hello 40.68.254.142에 tooa 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-166">hello following example connects tooa virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="78bc3-167">대체 `sshuser` hello 클러스터를 만들 때 지정한 hello SSH 사용자 계정 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-167">Replace `sshuser` with hello SSH user account you specified when creating hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="78bc3-168">다양 한 방법으로 tooobtain hello `ssh` 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-168">There are a variety of ways tooobtain hello `ssh` utility.</span></span> <span data-ttu-id="78bc3-169">Linux, Unix 및 macOS에 hello 운영 체제의 일부로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-169">On Linux, Unix, and macOS, it is provided as part of hello operating system.</span></span> <span data-ttu-id="78bc3-170">Windows를 사용 하는 경우 hello 다음 옵션 중 하나를 고려해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="78bc3-170">If you are using Windows, consider one of hello following options:</span></span>
    >
    > * [<span data-ttu-id="78bc3-171">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="78bc3-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="78bc3-172">Windows 10에서 Ubuntu의 Bash</span><span class="sxs-lookup"><span data-stu-id="78bc3-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="78bc3-173">Git(https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="78bc3-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="78bc3-174">OpenSSH(https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="78bc3-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="78bc3-175">바인딩을 tooinstall hello SSH 세션에서 명령을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-175">tooinstall Bind, use hello following commands from hello SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="78bc3-176">tooconfigure 바인딩 tooforward 이름 확인 요청 tooyour 온-프레미스 DNS 서버를 사용 하 여 hello의 hello 콘텐츠로 텍스트를 다음 hello `/etc/bind/named.conf.options` 파일:</span><span class="sxs-lookup"><span data-stu-id="78bc3-176">tooconfigure Bind tooforward name resolution requests tooyour on-prem DNS server, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

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
    > <span data-ttu-id="78bc3-177">Hello hello 값을 교체 `goodclients` hello 가상 네트워크와 온-프레미스 네트워크의 IP 주소 범위 hello와 섹션.</span><span class="sxs-lookup"><span data-stu-id="78bc3-177">Replace hello values in hello `goodclients` section with hello IP address range of hello virtual network and on-premises network.</span></span> <span data-ttu-id="78bc3-178">이 섹션에서는이 DNS 서버에 요청을 수락 하는 hello 주소를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-178">This section defines hello addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="78bc3-179">Hello 대체 `192.168.0.1` hello에 항목 `forwarders` hello IP 주소로 온-프레미스 DNS 서버의 섹션.</span><span class="sxs-lookup"><span data-stu-id="78bc3-179">Replace hello `192.168.0.1` entry in hello `forwarders` section with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="78bc3-180">이 항목 경로 DNS 요청 tooyour 온-프레미스 DNS 서버를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-180">This entry routes DNS requests tooyour on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="78bc3-181">tooedit이이 파일에 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="78bc3-181">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="78bc3-182">toosave hello 파일을 사용 하 여 __Ctrl + X__, __Y__, 차례로 __Enter__합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-182">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="78bc3-183">Hello SSH 세션에서 다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-183">From hello SSH session, use hello following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="78bc3-184">이 명령은 텍스트 다음 값 비슷한 toohello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-184">This command returns a value similar toohello following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="78bc3-185">hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` 텍스트는 hello __DNS 접미사__ 이 가상 네트워크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-185">hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is hello __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="78bc3-186">나중에 사용하므로 이 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="78bc3-187">tooconfigure hello 가상 네트워크 내에서 리소스에 대 한 바인딩 tooresolve DNS 이름을 사용 하 여 hello hello의 hello 콘텐츠로 텍스트를 다음 `/etc/bind/named.conf.local` 파일:</span><span class="sxs-lookup"><span data-stu-id="78bc3-187">tooconfigure Bind tooresolve DNS names for resources within hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="78bc3-188">Hello 바꾸어야 `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` 앞서 검색 hello DNS 접미사를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-188">You must replace hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with hello DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="78bc3-189">tooedit이이 파일에 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="78bc3-189">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="78bc3-190">toosave hello 파일을 사용 하 여 __Ctrl + X__, __Y__, 차례로 __Enter__합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-190">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="78bc3-191">다음 명령을 사용 하 여 hello 바인딩 toostart:</span><span class="sxs-lookup"><span data-stu-id="78bc3-191">toostart Bind, use hello following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="78bc3-192">tooverify 바인딩하는 다음 명령을 사용 하 여 hello 온-프레미스 네트워크의 리소스 이름을 hello를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-192">tooverify that bind can resolve hello names of resources in your on-premises network, use hello following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="78bc3-193">대체 `dns.mynetwork.net` hello 온-프레미스 네트워크에 있는 리소스의 정규화 된 도메인 이름 (FQDN)으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-193">Replace `dns.mynetwork.net` with hello fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="78bc3-194">대체 `10.0.0.4` hello로 __내부 IP 주소__ hello 가상 네트워크에 사용자 지정 DNS 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-194">Replace `10.0.0.4` with hello __internal IP address__ of your custom DNS server in hello virtual network.</span></span>

    <span data-ttu-id="78bc3-195">hello 응답 텍스트 다음 유사한 toohello 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-195">hello response appears similar toohello following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a><span data-ttu-id="78bc3-196">Hello 가상 네트워크 toouse hello 사용자 지정 DNS 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-196">Configure hello virtual network toouse hello custom DNS server</span></span>

<span data-ttu-id="78bc3-197">tooconfigure hello 가상 네트워크 toouse hello 사용자 지정 DNS 서버 hello Azure 재귀 확인자, 대신 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-197">tooconfigure hello virtual network toouse hello custom DNS server instead of hello Azure recursive resolver, use hello following steps:</span></span>

1. <span data-ttu-id="78bc3-198">Hello에 [Azure 포털](https://portal.azure.com)hello 가상 네트워크를 선택한 다음 선택 __DNS 서버__합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-198">In hello [Azure portal](https://portal.azure.com), select hello virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="78bc3-199">선택 __사용자 지정__, hello 입력 __내부 IP 주소__ hello 사용자 지정 DNS 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-199">Select __Custom__, and enter hello __internal IP address__ of hello custom DNS server.</span></span> <span data-ttu-id="78bc3-200">마지막으로 __저장__을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-200">Finally, select __Save__.</span></span>

    ![Hello hello 네트워크에 대 한 사용자 지정 DNS 서버 설정](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a><span data-ttu-id="78bc3-202">Hello 온-프레미스 DNS 서버 구성</span><span class="sxs-lookup"><span data-stu-id="78bc3-202">Configure hello on-premises DNS server</span></span>

<span data-ttu-id="78bc3-203">Hello 이전 단원의 hello 사용자 지정 DNS 서버 tooforward 요청 toohello 온-프레미스 DNS 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-203">In hello previous section, you configured hello custom DNS server tooforward requests toohello on-premises DNS server.</span></span> <span data-ttu-id="78bc3-204">다음으로 hello 온-프레미스 DNS 서버 tooforward 요청 toohello 사용자 지정 DNS 서버를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-204">Next, you must configure hello on-premises DNS server tooforward requests toohello custom DNS server.</span></span>

<span data-ttu-id="78bc3-205">특정 단계는 방법에 대 한 tooconfigure DNS 서버, DNS 서버 소프트웨어에 대 한 hello 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="78bc3-205">For specific steps on how tooconfigure your DNS server, consult hello documentation for your DNS server software.</span></span> <span data-ttu-id="78bc3-206">확인 방법에 대 hello tooconfigure는 __조건 전달자__합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-206">Look for hello steps on how tooconfigure a __conditional forwarder__.</span></span>

<span data-ttu-id="78bc3-207">조건부 전달은 특정 DNS 접미사에 대한 요청만을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="78bc3-208">이 경우 hello 가상 네트워크의 DNS 접미사 hello에 대 한 전달자를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-208">In this case, you must configure a forwarder for hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="78bc3-209">이 접미사에 대 한 요청 toohello hello 사용자 지정 하는 DNS 서버의 IP 주소를 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-209">Requests for this suffix should be forwarded toohello IP address of hello custom DNS server.</span></span> 

<span data-ttu-id="78bc3-210">hello 다음 텍스트는 hello에 대 한 조건 전달자 구성의 예 **바인딩할** DNS 소프트웨어:</span><span class="sxs-lookup"><span data-stu-id="78bc3-210">hello following text is an example of a conditional forwarder configuration for hello **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

<span data-ttu-id="78bc3-211">DNS를 사용 하 여에 대 한 내용은 **Windows Server 2016**, hello 참조 [추가 DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) 설명서...</span><span class="sxs-lookup"><span data-stu-id="78bc3-211">For information on using DNS on **Windows Server 2016**, see hello [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="78bc3-212">Hello 온-프레미스 DNS 서버를 구성한 후 사용할 수 있습니다 `nslookup` hello 온-프레미스 네트워크 tooverify에서 hello 가상 네트워크의 이름을 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-212">Once you have configured hello on-premises DNS server, you can use `nslookup` from hello on-premises network tooverify that you can resolve names in hello virtual network.</span></span> <span data-ttu-id="78bc3-213">다음 예제는 hello</span><span class="sxs-lookup"><span data-stu-id="78bc3-213">hello following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="78bc3-214">이 예제를 사용 하 여 온-프레미스 DNS 서버에 196.168.0.4 hello tooresolve hello 이름 hello 사용자 지정 DNS 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-214">This example uses hello on-premises DNS server at 196.168.0.4 tooresolve hello name of hello custom DNS server.</span></span> <span data-ttu-id="78bc3-215">온-프레미스 DNS 서버 hello에 대 한 hello 하나 있는 hello IP 주소를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-215">Replace hello IP address with hello one for hello on-premises DNS server.</span></span> <span data-ttu-id="78bc3-216">Hello 대체 `dnsproxy` 주소 hello 사용자 지정 DNS 서버 hello 정규화 된 도메인 이름 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-216">Replace hello `dnsproxy` address with hello fully qualified domain name of hello custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="78bc3-217">선택 사항: 네트워크 트래픽 제어</span><span class="sxs-lookup"><span data-stu-id="78bc3-217">Optional: Control network traffic</span></span>

<span data-ttu-id="78bc3-218">네트워크 보안 그룹 (NSG) 또는 사용자 정의 경로 (UDR) toocontrol 네트워크 트래픽을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-218">You can use network security groups (NSG) or user-defined routes (UDR) toocontrol network traffic.</span></span> <span data-ttu-id="78bc3-219">Nsg 사용 하면 toofilter 인바운드 및 아웃 바운드 트래픽을, 및 트래픽을 허용 하거나 거부 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-219">NSGs allow you toofilter inbound and outbound traffic, and allow or deny hello traffic.</span></span> <span data-ttu-id="78bc3-220">UDRs는 toocontrol hello 가상 네트워크의 리소스 간의 트래픽 흐름 방식을 사용 하면, 인터넷, hello 및 온-프레미스 네트워크 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-220">UDRs allow you toocontrol how traffic flows between resources in hello virtual network, hello internet, and hello on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="78bc3-221">HDInsight은 hello Azure 클라우드에서에서 특정 IP 주소에서의 인바운드 액세스 및 제한 없이 아웃 바운드 액세스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-221">HDInsight requires inbound access from specific IP addresses in hello Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="78bc3-222">Nsg 또는 UDRs toocontrol 트래픽을 사용할 때는 hello 다음 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-222">When using NSGs or UDRs toocontrol traffic, you must perform hello following steps:</span></span>
>
> 1. <span data-ttu-id="78bc3-223">가상 네트워크를 포함 하는 hello 위치에 대 한 hello IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-223">Find hello IP addresses for hello location that contains your virtual network.</span></span> <span data-ttu-id="78bc3-224">위치별로 필요한 IP 목록은 [필요한 IP 주소](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78bc3-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="78bc3-225">Hello IP 주소에서 인바운드 트래픽을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-225">Allow inbound traffic from hello IP addresses.</span></span>
>
>    * <span data-ttu-id="78bc3-226">__NSG__: 허용 __인바운드__ 포트에서 트래픽을 __443__ hello에서 __인터넷__합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-226">__NSG__: Allow __inbound__ traffic on port __443__ from hello __Internet__.</span></span>
>    * <span data-ttu-id="78bc3-227">__UDR__: 집합 hello __다음 홉__ hello 경로 too__Internet__의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-227">__UDR__: Set hello __Next Hop__ type of hello route too__Internet__.</span></span>

<span data-ttu-id="78bc3-228">Azure PowerShell 또는 hello Azure CLI toocreate Nsg 사용 하는 예제를 보려면 hello [Azure 가상 네트워크와 확장 HDInsight](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) 문서.</span><span class="sxs-lookup"><span data-stu-id="78bc3-228">For an example of using Azure PowerShell or hello Azure CLI toocreate NSGs, see hello [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-hello-hdinsight-cluster"></a><span data-ttu-id="78bc3-229">Hello HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="78bc3-229">Create hello HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="78bc3-230">HDInsight hello 가상 네트워크에 설치 하기 전에 hello 사용자 지정 DNS 서버를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-230">You must configure hello custom DNS server before installing HDInsight in hello virtual network.</span></span>

<span data-ttu-id="78bc3-231">Hello에서 단계를 사용 하 여 hello [hello Azure 포털을 사용 하 여 HDInsight 클러스터를 만들 수](./hdinsight-hadoop-create-linux-clusters-portal.md) 문서 toocreate HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-231">Use hello steps in hello [Create an HDInsight cluster using hello Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document toocreate an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="78bc3-232">클러스터를 만드는 동안 가상 네트워크를 포함 하는 hello 위치를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-232">During cluster creation, you must choose hello location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="78bc3-233">Hello에 __고급 설정__ 부분 구성의 hello 가상 네트워크를 이전에 만든 서브넷을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-233">In hello __Advanced settings__ part of configuration, you must select hello virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-toohdinsight"></a><span data-ttu-id="78bc3-234">TooHDInsight 연결</span><span class="sxs-lookup"><span data-stu-id="78bc3-234">Connecting tooHDInsight</span></span>

<span data-ttu-id="78bc3-235">HDInsight에 대 한 대부분 설명서 hello를 통해 액세스 toohello 클러스터 있다고 가정 합니다. 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-235">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="78bc3-236">예를 들어, https://CLUSTERNAME.azurehdinsight.net에 toohello 클러스터를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-236">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="78bc3-237">이 주소에서 UDRs toorestrict 액세스 hello 인터넷 또는 Nsg를 사용 하는 경우에 사용할 수 없는 hello 공용 게이트웨이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-237">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="78bc3-238">toodirectly는 tooHDInsight hello 가상 네트워크를 통해 연결 하려면이 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-238">toodirectly connect tooHDInsight through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="78bc3-239">hello HDInsight 클러스터 노드의 toodiscover hello 내부 정규화 된 도메인 이름을 hello 메서드를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-239">toodiscover hello internal fully qualified domain names of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

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

2. <span data-ttu-id="78bc3-240">서비스를 사용할 수 있는 toodetermine hello 포트 참조 hello [HDInsight의 Hadoop 서비스에 의해 사용 되는 포트](./hdinsight-hadoop-port-settings-for-services.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="78bc3-240">toodetermine hello port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="78bc3-241">일부 서비스의 hello 헤드 노드에 호스팅되 한 번에 한 노드에서 활성화만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-241">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="78bc3-242">헤드 노드 하나에서 서비스에 액세스를 시도 하는 경우 실패 toohello 다른 헤드 노드를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-242">If you try accessing a service on one head node and it fails, switch toohello other head node.</span></span>
    >
    > <span data-ttu-id="78bc3-243">예를 들어 Ambari는 한 번에 하나의 헤드 노드에서만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="78bc3-244">Ambari 헤드 노드 하나에서 액세스를 시도 하 고에서 실행 되 고 다음 404 오류를 반환 하는 경우 다른 헤드 노드를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on hello other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78bc3-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="78bc3-245">Next steps</span></span>

* <span data-ttu-id="78bc3-246">가상 네트워크에서 HDInsight를 사용하는 방법에 대한 자세한 내용은 [Azure Virtual Network를 사용하여 HDInsight 확장](./hdinsight-extend-hadoop-virtual-network.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78bc3-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="78bc3-247">Azure 가상 네트워크에 대 한 자세한 내용은 참조 hello [Azure 가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="78bc3-247">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="78bc3-248">네트워크 보안 그룹에 대한 자세한 내용은 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78bc3-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="78bc3-249">사용자 정의 경로에 대한 자세한 내용은 [사용자 정의 경로 및 IP 전달](../virtual-network/virtual-networks-udr-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78bc3-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
