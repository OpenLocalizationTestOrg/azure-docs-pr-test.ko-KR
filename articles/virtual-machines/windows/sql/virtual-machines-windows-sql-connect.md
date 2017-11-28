---
title: "SQL Server 가상 컴퓨터에 연결(리소스 관리자) | Microsoft Docs"
description: "Azure의 가상 컴퓨터에서 실행되는 SQL Server에 연결하는 방법을 알아봅니다. 이 항목에서는 클래식 배포 모드를 사용합니다. 시나리오는 네트워킹 구성 및 클라이언트의 위치에 따라 다릅니다."
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
ms.openlocfilehash: 67ba43f9456bbeffbf602067586143c4c68af672
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-a-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="7f37b-105">Azure에서 SQL Server 가상 컴퓨터 연결(리소스 관리자)</span><span class="sxs-lookup"><span data-stu-id="7f37b-105">Connect to a SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f37b-106">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="7f37b-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="7f37b-107">클래식</span><span class="sxs-lookup"><span data-stu-id="7f37b-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="7f37b-108">개요</span><span class="sxs-lookup"><span data-stu-id="7f37b-108">Overview</span></span>

<span data-ttu-id="7f37b-109">이 항목에서는 Azure 가상 컴퓨터에서 실행되는 SQL Server 인스턴스에 연결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-109">This topic describes how to connect to your SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="7f37b-110">여기서는 몇 가지 [일반 연결 시나리오](#connection-scenarios)를 다룬 다음 [Azure VM에서 SQL Server 연결을 구성하기 위한 상세 단계](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="7f37b-111">프로비저닝 및 연결의 전체 연습 과정을 확인하려면 [Azure에서 SQL Server 가상 컴퓨터 프로비전](virtual-machines-windows-portal-sql-server-provision.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f37b-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="7f37b-112">연결 시나리오</span><span class="sxs-lookup"><span data-stu-id="7f37b-112">Connection scenarios</span></span>

<span data-ttu-id="7f37b-113">클라이언트가 가상 컴퓨터를 실행 중인 SQL Server에 연결하는 방법은 클라이언트의 위치 및 네트워킹 구성에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-113">The way a client connects to SQL Server running on a Virtual Machine differs depending on the location of the client and the networking configuration.</span></span>

<span data-ttu-id="7f37b-114">Azure Portal에서 SQL Server VM을 프로비전하는 경우 **SQL 연결**의 형식을 지정하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-114">If you provision a SQL Server VM in the Azure portal, you have the option of specifying the type of **SQL connectivity**.</span></span>

![프로비전 중 공용 SQL 연결 옵션](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="7f37b-116">연결에 대한 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="7f37b-117">옵션</span><span class="sxs-lookup"><span data-stu-id="7f37b-117">Option</span></span> | <span data-ttu-id="7f37b-118">설명</span><span class="sxs-lookup"><span data-stu-id="7f37b-118">Description</span></span> |
|---|---|
| <span data-ttu-id="7f37b-119">**공용**</span><span class="sxs-lookup"><span data-stu-id="7f37b-119">**Public**</span></span> | <span data-ttu-id="7f37b-120">인터넷을 통해 SQL Server에 연결</span><span class="sxs-lookup"><span data-stu-id="7f37b-120">Connect to SQL Server over the internet</span></span> |
| <span data-ttu-id="7f37b-121">**개인**</span><span class="sxs-lookup"><span data-stu-id="7f37b-121">**Private**</span></span> | <span data-ttu-id="7f37b-122">동일한 가상 네트워크의 SQL Server에 연결</span><span class="sxs-lookup"><span data-stu-id="7f37b-122">Connect to SQL Server in the same virtual network</span></span> |
| <span data-ttu-id="7f37b-123">**로컬**</span><span class="sxs-lookup"><span data-stu-id="7f37b-123">**Local**</span></span> | <span data-ttu-id="7f37b-124">동일한 가상 컴퓨터의 SQL Server에 로컬로 연결</span><span class="sxs-lookup"><span data-stu-id="7f37b-124">Connect to SQL Server locally on the same virtual machine</span></span> | 

<span data-ttu-id="7f37b-125">다음 섹션은 **공용** 및 **개인** 옵션을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-125">The following sections explain the **Public** and **Private** options in more detail.</span></span>

## <a name="connect-to-sql-server-over-the-internet"></a><span data-ttu-id="7f37b-126">인터넷을 통해 SQL Server에 연결 </span><span class="sxs-lookup"><span data-stu-id="7f37b-126">Connect to SQL Server over the Internet</span></span>

<span data-ttu-id="7f37b-127">인터넷에서 SQL Server 데이터베이스 엔진에 연결하려는 경우 프로비전하는 동안 포털에서 **SQL 연결** 형식에 대해 **공용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-127">If you want to connect to your SQL Server database engine from the Internet, select **Public** for the **SQL connectivity** type in the portal during provisioning.</span></span> <span data-ttu-id="7f37b-128">포털에서 다음 단계를 자동으로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-128">The portal automatically does the following steps:</span></span>

* <span data-ttu-id="7f37b-129">SQL Server에 대해 TCP/IP 프로토콜을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-129">Enables the TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="7f37b-130">SQL Server TCP 포트(기본값 1433)를 열도록 방화벽 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-130">Configures a firewall rule to open the SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="7f37b-131">공용 액세스에 필요한 SQL Server 인증을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="7f37b-132">SQL Server 포트의 모든 TCP 트래픽에 대해 VM에서 네트워크 보안 그룹을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-132">Configures the network security group on the VM to all TCP traffic on the SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f37b-133">SQL Server Developer 및 Express 버전용 가상 컴퓨터 이미지는 자동으로 TCP/IP 프로토콜을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-133">The virtual machine images for the SQL Server Developer and Express editions do not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="7f37b-134">Developer 및 Express 버전의 경우 VM을 만든 후에 SQL Server 구성 관리자를 사용하여 [수동으로 TCP/IP 프로토콜을 사용](#manualtcp)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-134">For Developer and Express editions, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#manualtcp) after creating the VM.</span></span>

<span data-ttu-id="7f37b-135">인터넷에 연결된 모든 클라이언트는 가상 컴퓨터의 공용 IP 주소 또는 IP 주소에 할당된 DNS 이름을 지정하여 SQL Server 인스턴스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-135">Any client with internet access can connect to the SQL Server instance by specifying either the public IP address of the virtual machine or any DNS label assigned to that IP address.</span></span> <span data-ttu-id="7f37b-136">SQL Server 포트가 1433인 경우 연결 문자열에 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-136">If the SQL Server port is 1433, you do not need to specify it in the connection string.</span></span> <span data-ttu-id="7f37b-137">다음 연결 문자열은 SQL 인증을 사용하여 `sqlvmlabel.eastus.cloudapp.azure.com`의 DNS 레이블로 SQL VM에 연결합니다(공용 IP 주소를 사용할 수도 있음).</span><span class="sxs-lookup"><span data-stu-id="7f37b-137">The following connection string connects to a SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use the public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="7f37b-138">이를 통해 인터넷을 통한 클라이언트의 연결이 활성화되지만 누구나 SQL Server에 연결할 수 있다는 뜻은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-138">Although this enables connectivity for clients over the internet, this does not imply that anyone can connect to your SQL Server.</span></span> <span data-ttu-id="7f37b-139">외부 클라이언트는 정확한 사용자 이름과 암호가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-139">Outside clients have to the correct username and password.</span></span> <span data-ttu-id="7f37b-140">그러나 추가 보안을 위해 잘 알려진 포트 1433을 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-140">However, for additional security, you can avoid the well-known port 1433.</span></span> <span data-ttu-id="7f37b-141">예를 들어 1500 포트에서 수신하도록 SQL Server를 구성하고 적절한 방화벽 및 네트워크 보안 그룹 규칙을 설정하는 경우 서버 이름에 포트 번호를 추가하여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-141">For example, if you configured SQL Server to listen on port 1500 and established proper firewall and network security group rules, you could connect by appending the port number to the Server name.</span></span> <span data-ttu-id="7f37b-142">다음 예제에서는 서버 이름에 사용자 지정 포트 번호, **1500**을 추가하여 이전 항목을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-142">The following example alters the previous one by adding a custom port number, **1500**, to the server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="7f37b-143">인터넷을 통해 VM에서 SQL Server를 쿼리하는 경우 Azure 데이터 센터에서 보내는 모든 데이터에는 일반적으로 [아웃바운드 데이터 전송 가격](https://azure.microsoft.com/pricing/details/data-transfers/)이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-143">When you query SQL Server in a VM over the internet, all outgoing data from the Azure datacenter is subject to normal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-to-sql-server-within-a-virtual-network"></a><span data-ttu-id="7f37b-144">가상 네트워크 내에서 SQL Server에 연결</span><span class="sxs-lookup"><span data-stu-id="7f37b-144">Connect to SQL Server within a virtual network</span></span>

<span data-ttu-id="7f37b-145">포털에서 **SQL 연결** 형식에 대해 **개인**을 선택하는 경우 Azure는 대부분의 설정을 **공용**과 동일하게 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-145">When you choose **Private** for the **SQL connectivity** type in the portal, Azure configures most of the settings identical to **Public**.</span></span> <span data-ttu-id="7f37b-146">한 가지 차이점은 SQL Server 포트(기본값 1433)에서 외부 트래픽을 허용하는 네트워크 보안 그룹 규칙이 없다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-146">The one difference is that there is no network security group rule to allow outside traffic on the SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f37b-147">SQL Server Developer 및 Express 버전용 가상 컴퓨터 이미지는 자동으로 TCP/IP 프로토콜을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-147">The virtual machine images for the SQL Server Developer and Express editions do not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="7f37b-148">Developer 및 Express 버전의 경우 VM을 만든 후에 SQL Server 구성 관리자를 사용하여 [수동으로 TCP/IP 프로토콜을 사용](#manualtcp)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-148">For Developer and Express editions, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#manualtcp) after creating the VM.</span></span>

<span data-ttu-id="7f37b-149">개인 연결은 종종 여러 가지 시나리오를 활성화하는 [Virtual Network](../../../virtual-network/virtual-networks-overview.md)와 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="7f37b-150">VM이 다른 리소스 그룹에 있더라도 동일한 가상 네트워크의 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-150">You can connect VMs in the same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="7f37b-151">또한 [사이트 간 VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)을 통해 온-프레미스 네트워크와 컴퓨터에 VM을 연결하는 하이브리드 아키텍처를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="7f37b-152">가상 네트워크를 사용하면 Azure VM을 도메인에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-152">Virtual networks also enable     you to join your Azure VMs to a domain.</span></span> <span data-ttu-id="7f37b-153">이것이 SQL Server에 Windows 인증을 사용하는 유일한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-153">This is the only way to use Windows Authentication to SQL Server.</span></span> <span data-ttu-id="7f37b-154">다른 연결 시나리오의 경우 사용자 이름과 암호가 있는 SQL 인증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-154">The other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="7f37b-155">가상 네트워크에 DNS를 구성했다고 가정하면 연결 문자열에 SQL Server VM 컴퓨터 이름을 지정하여 SQL Server에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-155">Assuming that you have configured DNS in your virtual network, you can connect to your SQL Server instance by specifying the SQL Server VM computer name in the connection string.</span></span> <span data-ttu-id="7f37b-156">또한 다음 예에서는 Windows 인증도 구성되었고 사용자에게 SQL Server 인스턴스에 대한 액세스 권한이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-156">The following example also assumes that Windows Authentication has also been configured and that the user has been granted access to the SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="7f37b-157"><a id="change"></a> SQL 연결 설정 변경</span><span class="sxs-lookup"><span data-stu-id="7f37b-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="7f37b-158">Azure Portal에서 SQL Server 가상 컴퓨터에 대한 연결 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-158">You can change the connectivity settings for your SQL Server virtual machine in the Azure portal.</span></span>

1. <span data-ttu-id="7f37b-159">Azure Portal에서 **Virtual Machines**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-159">In the Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="7f37b-160">SQL Server VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="7f37b-161">**설정** 아래에서 **SQL Server 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="7f37b-162">**SQL 연결 수준**을 필요한 설정으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-162">Change the **SQL connectivity level** to your required setting.</span></span> <span data-ttu-id="7f37b-163">필요에 따라 이 영역을 사용하여 SQL Server 포트 또는 SQL 인증 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-163">You can optionally use this area to change the SQL Server port or the SQL Authentication settings.</span></span>

   ![SQL 연결 변경](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="7f37b-165">업데이트를 완료할 때까지 몇 분 동안 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-165">Wait several minutes for the update to complete.</span></span>

   ![SQL VM 업데이트 알림](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="7f37b-167"><a id="manualtcp"></a> Developer 및 Express 버전에 대해 TCP/IP 사용</span><span class="sxs-lookup"><span data-stu-id="7f37b-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="7f37b-168">SQL Server 연결 설정을 변경할 때 Azure는 SQL Server Developer 및 Express 버전에 대해 TCP/IP 프로토콜을 자동으로 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-168">When changing SQL Server connectivity settings, Azure does not automatically enable the TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="7f37b-169">아래 단계에서는 IP 주소를 통해 원격으로 연결할 수 있도록 TCP/IP를 수동으로 사용하도록 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-169">The steps below explain how to manually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="7f37b-170">먼저 원격 데스크톱을 사용하여 SQL Server 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-170">First, connect to the SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="7f37b-171">다음으로 **SQL Server 구성 관리자**를 사용하여 TCP/IP 프로토콜을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-171">Next, enable the TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="7f37b-172">SSMS로 연결</span><span class="sxs-lookup"><span data-stu-id="7f37b-172">Connect with SSMS</span></span>

<span data-ttu-id="7f37b-173">다음 단계에서는 Azure VM에 대한 선택적 DNS 레이블을 만든 다음 SSMS(SQL Server Management Studio)와 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f37b-173">The following steps show how to create an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect to SQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="7f37b-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7f37b-174">Next Steps</span></span>

<span data-ttu-id="7f37b-175">이러한 연결 단계와 함께 프로비저닝 지침을 확인하려면 [Azure에서 SQL Server 가상 컴퓨터 프로비전](virtual-machines-windows-portal-sql-server-provision.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f37b-175">To see provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="7f37b-176">Azure VM에서의 SQL Server 실행에 관한 다른 항목은 [Azure 가상 컴퓨터의 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f37b-176">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>