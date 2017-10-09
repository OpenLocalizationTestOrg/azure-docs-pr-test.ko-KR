---
title: "SQL Server 가상 컴퓨터 (리소스 관리자) aaaConnect tooa | Microsoft Docs"
description: "자세한 내용은 방법 tooconnect tooSQL 서버 Azure에서 가상 컴퓨터에서 실행 합니다. 이 항목에서는 hello 클래식 배포 모델을 사용 합니다. hello 시나리오 hello 네트워킹 구성 및 hello 클라이언트의 hello 위치에 따라 다릅니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="bc69c-105">Tooa (리소스 관리자) Azure에서 SQL Server 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-105">Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc69c-106">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="bc69c-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="bc69c-107">클래식</span><span class="sxs-lookup"><span data-stu-id="bc69c-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="bc69c-108">개요</span><span class="sxs-lookup"><span data-stu-id="bc69c-108">Overview</span></span>

<span data-ttu-id="bc69c-109">이 항목에서는 tooconnect tooyour SQL Server 인스턴스는 Azure 가상 컴퓨터에서 실행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-109">This topic describes how tooconnect tooyour SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="bc69c-110">여기서는 몇 가지 [일반 연결 시나리오](#connection-scenarios)를 다룬 다음 [Azure VM에서 SQL Server 연결을 구성하기 위한 상세 단계](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="bc69c-111">프로비저닝 및 연결의 전체 연습 과정을 확인하려면 [Azure에서 SQL Server 가상 컴퓨터 프로비전](virtual-machines-windows-portal-sql-server-provision.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc69c-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="bc69c-112">연결 시나리오</span><span class="sxs-lookup"><span data-stu-id="bc69c-112">Connection scenarios</span></span>

<span data-ttu-id="bc69c-113">hello 방식으로 클라이언트 tooSQL hello 클라이언트와 hello 네트워킹 구성의 hello 위치에 따라 달라 집니다 가상 컴퓨터에서 실행 중인 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-113">hello way a client connects tooSQL Server running on a Virtual Machine differs depending on hello location of hello client and hello networking configuration.</span></span>

<span data-ttu-id="bc69c-114">hello 형식 지정의 hello 옵션이 hello Azure 포털에서에서 SQL Server VM을 프로 비전 하는 경우 **SQL 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-114">If you provision a SQL Server VM in hello Azure portal, you have hello option of specifying hello type of **SQL connectivity**.</span></span>

![프로비전 중 공용 SQL 연결 옵션](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="bc69c-116">연결에 대한 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="bc69c-117">옵션</span><span class="sxs-lookup"><span data-stu-id="bc69c-117">Option</span></span> | <span data-ttu-id="bc69c-118">설명</span><span class="sxs-lookup"><span data-stu-id="bc69c-118">Description</span></span> |
|---|---|
| <span data-ttu-id="bc69c-119">**공용**</span><span class="sxs-lookup"><span data-stu-id="bc69c-119">**Public**</span></span> | <span data-ttu-id="bc69c-120">TooSQL 서버 hello 통해 연결 인터넷</span><span class="sxs-lookup"><span data-stu-id="bc69c-120">Connect tooSQL Server over hello internet</span></span> |
| <span data-ttu-id="bc69c-121">**개인**</span><span class="sxs-lookup"><span data-stu-id="bc69c-121">**Private**</span></span> | <span data-ttu-id="bc69c-122">연결 tooSQL 서버 hello에 동일한 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="bc69c-122">Connect tooSQL Server in hello same virtual network</span></span> |
| <span data-ttu-id="bc69c-123">**로컬**</span><span class="sxs-lookup"><span data-stu-id="bc69c-123">**Local**</span></span> | <span data-ttu-id="bc69c-124">TooSQL 서버 hello에 로컬로 연결 동일한 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="bc69c-124">Connect tooSQL Server locally on hello same virtual machine</span></span> | 

<span data-ttu-id="bc69c-125">hello 다음 섹션에 설명 hello **공용** 및 **개인** 자세히 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-125">hello following sections explain hello **Public** and **Private** options in more detail.</span></span>

## <a name="connect-toosql-server-over-hello-internet"></a><span data-ttu-id="bc69c-126">TooSQL 서버 hello 인터넷을 통해 연결</span><span class="sxs-lookup"><span data-stu-id="bc69c-126">Connect tooSQL Server over hello Internet</span></span>

<span data-ttu-id="bc69c-127">Tooconnect hello 인터넷에서에서 SQL Server 데이터베이스 엔진 tooyour 선택 **공용** hello에 대 한 **SQL 연결** 프로 비전 시 hello 포털의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-127">If you want tooconnect tooyour SQL Server database engine from hello Internet, select **Public** for hello **SQL connectivity** type in hello portal during provisioning.</span></span> <span data-ttu-id="bc69c-128">다음 단계는 자동으로 hello 포털 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-128">hello portal automatically does hello following steps:</span></span>

* <span data-ttu-id="bc69c-129">SQL Server에 대 한 hello TCP/IP 프로토콜을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-129">Enables hello TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="bc69c-130">방화벽 규칙 tooopen hello SQL Server TCP 포트 (기본값 1433)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-130">Configures a firewall rule tooopen hello SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="bc69c-131">공용 액세스에 필요한 SQL Server 인증을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="bc69c-132">SQL Server 포트 hello VM tooall TCP 트래픽 hello에 hello 네트워크 보안 그룹을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-132">Configures hello network security group on hello VM tooall TCP traffic on hello SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc69c-133">SQL Server Developer hello에 대 한 가상 컴퓨터 이미지 hello 및 Express edition 사용 하지 마십시오 자동으로 hello TCP/IP 프로토콜.</span><span class="sxs-lookup"><span data-stu-id="bc69c-133">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="bc69c-134">개발자 및 Express 버전만 사용 해야 SQL Server 구성 관리자 너무[수동으로 hello TCP/IP 프로토콜을 사용 하도록 설정](#manualtcp) hello VM을 만든 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-134">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="bc69c-135">인터넷에 연결 된 모든 클라이언트 hello hello 가상 컴퓨터의 공용 IP 주소 또는 toothat IP 주소를 할당 한 모든 DNS 레이블을 지정 하 여 toohello SQL Server 인스턴스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-135">Any client with internet access can connect toohello SQL Server instance by specifying either hello public IP address of hello virtual machine or any DNS label assigned toothat IP address.</span></span> <span data-ttu-id="bc69c-136">Toospecify 불필요 hello SQL Server 포트 1433 이면 hello 연결 문자열에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-136">If hello SQL Server port is 1433, you do not need toospecify it in hello connection string.</span></span> <span data-ttu-id="bc69c-137">다음 연결 문자열 hello DNS 레이블이 tooa SQL VM 연결의 `sqlvmlabel.eastus.cloudapp.azure.com` (사용할 수도 있습니다 hello 공용 IP 주소)는 SQL 인증을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-137">hello following connection string connects tooa SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use hello public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="bc69c-138">통해 클라이언트에 대 한 연결을 통해이 있지만 인터넷 hello, 것은 아닙니다 모든 사용자가 SQL Server tooyour 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-138">Although this enables connectivity for clients over hello internet, this does not imply that anyone can connect tooyour SQL Server.</span></span> <span data-ttu-id="bc69c-139">클라이언트 외부 toohello 올바른 사용자 이름 및 암호가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-139">Outside clients have toohello correct username and password.</span></span> <span data-ttu-id="bc69c-140">그러나 추가 보안을 위해 hello 잘 알려진 포트 1433을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-140">However, for additional security, you can avoid hello well-known port 1433.</span></span> <span data-ttu-id="bc69c-141">예를 들어 포트 1500에서 SQL Server toolisten 및 설정 된 적절 한 방화벽과 네트워크 보안 그룹 규칙을 구성한 경우 hello 포트 번호 toohello 서버 이름을 추가 하 여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-141">For example, if you configured SQL Server toolisten on port 1500 and established proper firewall and network security group rules, you could connect by appending hello port number toohello Server name.</span></span> <span data-ttu-id="bc69c-142">hello 다음 예제에서는 변경 hello 이전 쿼리와 사용자 지정 포트 번호를 추가 하 여 **1500**, toohello 서버 이름:</span><span class="sxs-lookup"><span data-stu-id="bc69c-142">hello following example alters hello previous one by adding a custom port number, **1500**, toohello server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="bc69c-143">VM의 SQL Server를 통해 쿼리할 때 hello 인터넷, 보내는 데이터를 모두 hello Azure에서에서의 데이터 센터는 주체 toonormal [아웃 바운드 데이터 전송에 대 한 가격](https://azure.microsoft.com/pricing/details/data-transfers/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-143">When you query SQL Server in a VM over hello internet, all outgoing data from hello Azure datacenter is subject toonormal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-toosql-server-within-a-virtual-network"></a><span data-ttu-id="bc69c-144">가상 네트워크 내에서 tooSQL 서버 연결</span><span class="sxs-lookup"><span data-stu-id="bc69c-144">Connect tooSQL Server within a virtual network</span></span>

<span data-ttu-id="bc69c-145">선택 하는 경우 **개인** hello에 대 한 **SQL 연결** 형식 hello 포털, Azure에서에서 구성 대부분의 동일한 hello 설정이 너무**공용**합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-145">When you choose **Private** for hello **SQL connectivity** type in hello portal, Azure configures most of hello settings identical too**Public**.</span></span> <span data-ttu-id="bc69c-146">한 가지 차이점 hello hello SQL Server 포트 (기본값 1433)에서 트래픽 밖에 없는 네트워크 보안 그룹 규칙 tooallow 된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-146">hello one difference is that there is no network security group rule tooallow outside traffic on hello SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc69c-147">SQL Server Developer hello에 대 한 가상 컴퓨터 이미지 hello 및 Express edition 사용 하지 마십시오 자동으로 hello TCP/IP 프로토콜.</span><span class="sxs-lookup"><span data-stu-id="bc69c-147">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="bc69c-148">개발자 및 Express 버전만 사용 해야 SQL Server 구성 관리자 너무[수동으로 hello TCP/IP 프로토콜을 사용 하도록 설정](#manualtcp) hello VM을 만든 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-148">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="bc69c-149">개인 연결은 종종 여러 가지 시나리오를 활성화하는 [Virtual Network](../../../virtual-network/virtual-networks-overview.md)와 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="bc69c-150">Hello 다른 리소스 그룹에 있는 동일한 가상 네트워크에서 이러한 경우에 Vm의에서 Vm에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-150">You can connect VMs in hello same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="bc69c-151">또한 [사이트 간 VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)을 통해 온-프레미스 네트워크와 컴퓨터에 VM을 연결하는 하이브리드 아키텍처를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="bc69c-152">가상 네트워크는 또한 toojoin 하면 Azure Vm tooa 도메인을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-152">Virtual networks also enable     you toojoin your Azure VMs tooa domain.</span></span> <span data-ttu-id="bc69c-153">이 hello 유일한 방법은 toouse Windows 인증 tooSQL 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-153">This is hello only way toouse Windows Authentication tooSQL Server.</span></span> <span data-ttu-id="bc69c-154">hello 다른 연결 시나리오의 SQL 인증을 요구할 사용자 이름 및 암호.</span><span class="sxs-lookup"><span data-stu-id="bc69c-154">hello other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="bc69c-155">가상 네트워크의 DNS 구성한 것 이라고 가정할 hello SQL Server VM 컴퓨터 이름 hello 연결 문자열에 지정 하 여 tooyour SQL Server 인스턴스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-155">Assuming that you have configured DNS in your virtual network, you can connect tooyour SQL Server instance by specifying hello SQL Server VM computer name in hello connection string.</span></span> <span data-ttu-id="bc69c-156">다음 예에서는 또한 hello Windows 인증도 구성 되어 있고 해당 hello 사용자 액세스 toohello SQL Server 인스턴스에 부여 받았는지 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-156">hello following example also assumes that Windows Authentication has also been configured and that hello user has been granted access toohello SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="bc69c-157"><a id="change"></a> SQL 연결 설정 변경</span><span class="sxs-lookup"><span data-stu-id="bc69c-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="bc69c-158">Hello Azure 포털의에서 SQL Server 가상 컴퓨터에 대 한 hello 연결 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-158">You can change hello connectivity settings for your SQL Server virtual machine in hello Azure portal.</span></span>

1. <span data-ttu-id="bc69c-159">Hello Azure 포털에서에서 선택 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-159">In hello Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="bc69c-160">SQL Server VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="bc69c-161">**설정** 아래에서 **SQL Server 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="bc69c-162">변경 hello **SQL 연결 수준을** tooyour 필요한 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-162">Change hello **SQL connectivity level** tooyour required setting.</span></span> <span data-ttu-id="bc69c-163">필요에 따라이 SQL Server 포트 영역 toochange hello 또는 hello SQL 인증 설정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-163">You can optionally use this area toochange hello SQL Server port or hello SQL Authentication settings.</span></span>

   ![SQL 연결 변경](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="bc69c-165">Hello 업데이트 toocomplete 몇 분 동안 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-165">Wait several minutes for hello update toocomplete.</span></span>

   ![SQL VM 업데이트 알림](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="bc69c-167"><a id="manualtcp"></a> Developer 및 Express 버전에 대해 TCP/IP 사용</span><span class="sxs-lookup"><span data-stu-id="bc69c-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="bc69c-168">SQL Server 연결 설정을 변경 하는 경우 Azure는 자동으로 사용 되지 hello TCP/IP 프로토콜 SQL Server Developer 및 Express 버전에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-168">When changing SQL Server connectivity settings, Azure does not automatically enable hello TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="bc69c-169">다음 hello 단계 IP 주소를 통해 원격으로 연결할 수 있도록 toomanually TCP/IP를 설정 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-169">hello steps below explain how toomanually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="bc69c-170">먼저, toohello SQL Server 컴퓨터와 원격 데스크톱 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-170">First, connect toohello SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="bc69c-171">다음으로 hello TCP/IP 프로토콜을 사용 하도록 설정 **SQL Server 구성 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-171">Next, enable hello TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="bc69c-172">SSMS로 연결</span><span class="sxs-lookup"><span data-stu-id="bc69c-172">Connect with SSMS</span></span>

<span data-ttu-id="bc69c-173">hello 다음 단계 어떻게 toocreate 선택적 DNS는 Azure vm을 레이블을 표시 하 고 SQL Server Management Studio (SSMS)와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-173">hello following steps show how toocreate an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="bc69c-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bc69c-174">Next Steps</span></span>

<span data-ttu-id="bc69c-175">이러한 연결 단계와 함께 프로 비전 방법은 toosee 확인 [Azure에서 SQL Server 가상 컴퓨터를 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-175">toosee provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="bc69c-176">다른 항목은 서로 관련 toorunning Azure Vm에서 SQL Server에 대 한 참조 [Azure 가상 컴퓨터에 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc69c-176">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
