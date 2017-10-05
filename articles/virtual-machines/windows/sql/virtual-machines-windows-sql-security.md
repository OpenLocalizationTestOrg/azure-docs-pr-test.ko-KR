---
title: "Azure의 SQL Server에 대한 보안 고려 사항 | Microsoft Docs"
description: "이 항목에서는 Azure Virtual Machine에서 실행되는 SQL Server 보안에 대한 일반적인 지침을 제공합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/02/2017
ms.author: jroth
ms.openlocfilehash: 4ad9156e481eac0bae32bca35a2b126363e5d8b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a><span data-ttu-id="ba040-103">Azure 가상 컴퓨터의 SQL Server에 대한 보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="ba040-103">Security Considerations for SQL Server in Azure Virtual Machines</span></span>

<span data-ttu-id="ba040-104">이 항목에는 Azure VM(Virtual Machine)에서 SQL Server 인스턴스로의 보안 액세스를 설정하는 데 도움이 되는 전반적인 보안 지침이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-104">This topic includes overall security guidelines that help establish secure access to SQL Server instances in an Azure virtual machine (VM).</span></span>

<span data-ttu-id="ba040-105">Azure는 가상 컴퓨터에서 실행되는 SQL Server로 호환되는 솔루션을 제작할 수 있도록 하는 몇 가지 산업 규정 및 표준을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-105">Azure complies with several industry regulations and standards that can enable you to build a compliant solution with SQL Server running in a virtual machine.</span></span> <span data-ttu-id="ba040-106">Azure 규정 준수에 대한 자세한 내용은 [Azure 보안 센터](https://azure.microsoft.com/support/trust-center/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba040-106">For information about regulatory compliance with Azure, see [Azure Trust Center](https://azure.microsoft.com/support/trust-center/).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-to-the-sql-vm"></a><span data-ttu-id="ba040-107">SQL VM에 대한 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="ba040-107">Control access to the SQL VM</span></span>

<span data-ttu-id="ba040-108">SQL Server 가상 컴퓨터를 만들 때는 컴퓨터 및 SQL Server에 대한 액세스 권한을 갖는 사용자를 신중하게 제어하는 방법을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-108">When you create your SQL Server virtual machine, consider how to carefully control who has access to the machine and to SQL Server.</span></span> <span data-ttu-id="ba040-109">일반적으로 다음과 같이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-109">In general, you should do the following:</span></span>

- <span data-ttu-id="ba040-110">SQL Server에 대한 액세스 권한을 이러한 권한이 필요한 응용 프로그램 및 클라이언트로만 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-110">Restrict access to SQL Server to only the applications and clients that need it.</span></span>
- <span data-ttu-id="ba040-111">사용자 계정 및 암호를 관리하는 모범 사례를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-111">Follow best practices for managing user accounts and passwords.</span></span>

<span data-ttu-id="ba040-112">다음 섹션에서는 이러한 내용을 충분히 생각해 보도록 제안 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-112">The following sections provide suggestions on thinking through these points.</span></span>

## <a name="secure-connections"></a><span data-ttu-id="ba040-113">보안 연결</span><span class="sxs-lookup"><span data-stu-id="ba040-113">Secure connections</span></span>

<span data-ttu-id="ba040-114">갤러리 이미지를 사용하여 SQL Server 가상 컴퓨터를 만들 때 **SQL Server 연결** 옵션은 **로컬(VM 내부)**, **개인(가상 네트워크 내)** 또는 **공용(인터넷)** 중에서 선택할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-114">When you create a SQL Server virtual machine with a gallery image, the **SQL Server Connectivity** option gives you the choice of **Local (inside VM)**, **Private (within Virtual Network)**, or **Public (Internet)**.</span></span>

![SQL Server 연결](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

<span data-ttu-id="ba040-116">최상의 보안을 위해 해당 시나리오에 대해 가장 제한적인 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-116">For the best security, choose the most restrictive option for your scenario.</span></span> <span data-ttu-id="ba040-117">예를 들어 같은 VM에 있는 SQL Server에 액세스하는 응용 프로그램을 실행 중인 경우 **로컬**이 가장 안전한 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-117">For example, if you are running an application that accesses SQL Server on the same VM, then **Local** is the most secure choice.</span></span> <span data-ttu-id="ba040-118">SQL Server에 액세스해야 하는 Azure 응용 프로그램을 실행 중인 경우 **개인**은 지정된 [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md) 내에 있는 SQL Server로의 통신만 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-118">If you are running an Azure application that requires access to the SQL Server, then **Private** secures communication to SQL Server only within the specified [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="ba040-119">SQL Server VM에 대한 **공용**(인터넷) 액세스가 필요한 경우 이 항목의 모범 사례를 따라 공격 노출 영역을 줄이도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-119">If you require **Public** (internest) access to the SQL Server VM, then make sure to follow other best practices in this topic to reduce your attack surface area.</span></span>

<span data-ttu-id="ba040-120">포털에서 선택한 옵션은 VM NSG([네트워크 보안 그룹 ](../../../virtual-network/virtual-networks-nsg.md))에 대해 인바운드 보안 규칙을 사용하여 가상 컴퓨터에 대한 네트워크 트래픽을 허용하거나 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-120">The selected options in the portal use inbound security rules on the VMs [Network Security Group](../../../virtual-network/virtual-networks-nsg.md) (NSG) to allow or deny network traffic to your virtual machine.</span></span> <span data-ttu-id="ba040-121">SQL Server 포트(기본값 1433)에 대한 트래픽을 허용하도록 인바운드 NSG 규칙을 수정하거나 새 인바운드 NSG 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-121">You can modify or create new inbound NSG rules to allow traffic to the SQL Server port (default 1433).</span></span> <span data-ttu-id="ba040-122">이 포트를 통해 통신할 수 있는 특정 IP 주소를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-122">You can also specify specific IP addresses that are allowed to communicate over this port.</span></span>

![네트워크 보안 그룹 규칙](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

<span data-ttu-id="ba040-124">네트워크 트래픽을 제한하기 위한 NSG 규칙 외에 가상 컴퓨터에서 Windows 방화벽을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-124">In addition to NSG rules to restrict network traffic, you can also use the Windows Firewall on the virtual machine.</span></span>

<span data-ttu-id="ba040-125">클래식 배포 모델이 적용된 끝점을 사용하는 경우 사용하지 않는 모든 끝점을 가상 컴퓨터에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-125">If you are using endpoints with the classic deployment model, remove any endpoints on the virtual machine if you do not use them.</span></span> <span data-ttu-id="ba040-126">끝점에서 ACL을 사용하는 방법에 대한 지침은 [끝점에 대한 ACL 관리](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba040-126">For instructions on using ACLs with endpoints, see [Manage the ACL on an endpoint](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span> <span data-ttu-id="ba040-127">Resource Manager를 사용하는 VM에는 이렇게 할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-127">This is not necessary for VMs that use the Resource Manager.</span></span>

<span data-ttu-id="ba040-128">마지막으로, Azure Virtual Machine에서 SQL Server 데이터베이스 엔진의 인스턴스에 대해 암호화된 연결 사용을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-128">Finally, consider enabling encrypted connections for the instance of the SQL Server Database Engine in your Azure virtual machine.</span></span> <span data-ttu-id="ba040-129">서명된 인증서로 SQL server 인스턴스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-129">Configure SQL server instance with a signed certificate.</span></span> <span data-ttu-id="ba040-130">자세한 내용은 [데이터베이스 엔진에 암호화된 연결 사용](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) 및 [연결 문자열 구문](https://msdn.microsoft.com/library/ms254500.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba040-130">For more information, see [Enable Encrypted Connections to the Database Engine](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) and [Connection String Syntax](https://msdn.microsoft.com/library/ms254500.aspx).</span></span>

## <a name="use-a-non-default-port"></a><span data-ttu-id="ba040-131">기본 포트가 아닌 포트 사용</span><span class="sxs-lookup"><span data-stu-id="ba040-131">Use a non-default port</span></span>

<span data-ttu-id="ba040-132">기본적으로 SQL Server는 잘 알려진 포트 1433에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-132">By default, SQL Server listens on a well-known port, 1433.</span></span> <span data-ttu-id="ba040-133">보안 강화를 위해 기본 포트가 아닌 포트(예: 1401)에서 수신 대기하도록 SQL Server를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-133">For increased security, configure SQL Server to listen on a non-default port, such as 1401.</span></span> <span data-ttu-id="ba040-134">Azure Portal에서 SQL Server 갤러리 이미지를 프로비전하는 경우 **SQL Server 설정** 블레이드에서 이 포트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-134">If you provision a SQL Server gallery image in the Azure portal, you can specify this port in the **SQL Server settings** blade.</span></span>

<span data-ttu-id="ba040-135">프로비전한 후 이를 구성할 때 다음과 같은 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-135">To configure this after provisioning, you have two options:</span></span>

- <span data-ttu-id="ba040-136">Resource Manager VM의 경우 VM 개요 블레이드에서 **SQL Server 구성**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-136">For Resource Manager VMs, you can select **SQL Server configuration** from the VM overview blade.</span></span> <span data-ttu-id="ba040-137">그러면 포트를 변경하는 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-137">This provides an option to change the port.</span></span>

  ![포털에서 TCP 포트 변경](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- <span data-ttu-id="ba040-139">포털에서 프로비전되지 않은 클래식 VM 또는 SQL Server VM의 경우 원격으로 VM에 연결하여 포트를 수동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-139">For Classic VMs or for SQL Server VMs that were not provisioned with the portal, you can manually configure the port by connecting remotely to the VM.</span></span> <span data-ttu-id="ba040-140">구성 단계는 [Configure a Server to Listen on a Specific TCP Port](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)(특정 TCP 포트에서 수신 대기하도록 서버 구성)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba040-140">For the configuration steps, see [Configure a Server to Listen on a Specific TCP Port](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).</span></span> <span data-ttu-id="ba040-141">이 수동 기법을 사용하는 경우 해당 TCP 포트에서 들어오는 트래픽을 허용하도록 Windows 방화벽 규칙도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-141">If you use this manual technique, you also need to add a Windows Firewall rule to allow incoming traffic on that TCP port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba040-142">SQL Server 포트가 공용 인터넷 연결에 대해 열려 있는 경우 기본 포트가 아닌 포트를 지정하는 것은 좋은 생각입니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-142">Specifying a non-default port is a good idea if your SQL Server port is open to public internet connections.</span></span>

<span data-ttu-id="ba040-143">SQL Server가 기본 포트가 아닌 포트에서 수신 대기하는 경우 연결할 때 포트를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-143">When SQL Server is listening on a non-default port, you must specify the port when you connect.</span></span> <span data-ttu-id="ba040-144">예를 들어 서버 IP 주소가 13.55.255.255이고 SQL Server가 포트 1401에서 수신 대기하고 있는 시나리오를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-144">For example, consider a scenario where the server IP address is 13.55.255.255 and SQL Server is listening on port 1401.</span></span> <span data-ttu-id="ba040-145">SQL Server에 연결하려면 연결 문자열에 `13.55.255.255,1401`을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-145">To connect to SQL Server, you would specify `13.55.255.255,1401` in the connection string.</span></span>

## <a name="manage-accounts"></a><span data-ttu-id="ba040-146">계정 관리</span><span class="sxs-lookup"><span data-stu-id="ba040-146">Manage accounts</span></span>

<span data-ttu-id="ba040-147">공격자가 쉽게 계정 이름이나 암호를 추측하기를 원하지는 않을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-147">You don't want attackers to easily guess account names or passwords.</span></span> <span data-ttu-id="ba040-148">도움이 되도록 다음 팁을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="ba040-148">Use the following tips to help:</span></span>

- <span data-ttu-id="ba040-149">로컬 관리자 계정의 이름을 **Administrator**가 아닌 다른 이름으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-149">Create a unique local administrator account that is not named **Administrator**.</span></span>

- <span data-ttu-id="ba040-150">모든 계정에 복잡하고 강력한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-150">Use complex strong passwords for all your accounts.</span></span> <span data-ttu-id="ba040-151">강력한 암호를 만드는 방법에 대한 자세한 내용은 [강력한 암호 만들기](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba040-151">For more information about how to create a strong password, see [Create a strong password](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) article.</span></span>

- <span data-ttu-id="ba040-152">기본적으로 Azure는 SQL Server 가상 컴퓨터를 설치하는 동안 Windows 인증을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-152">By default, Azure selects Windows Authentication during SQL Server Virtual Machine setup.</span></span> <span data-ttu-id="ba040-153">따라서 **SA** 로그인이 사용하지 않도록 설정되고 설치 프로그램에서 암호를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-153">Therefore, the **SA** login is disabled and a password is assigned by setup.</span></span> <span data-ttu-id="ba040-154">**SA** 로그인을 사용하거나 사용하도록 설정하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-154">We recommend that the **SA** login should not be used or enabled.</span></span> <span data-ttu-id="ba040-155">SQL 로그인이 있어야 하는 경우 다음 전략 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-155">If you must have a SQL login, use one of the following strategies:</span></span>

  - <span data-ttu-id="ba040-156">**sysadmin** 멤버 자격이 있는 고유한 이름을 가진 SQL 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-156">Create a SQL account with a unique name that has **sysadmin** membership.</span></span> <span data-ttu-id="ba040-157">포털에서 프로비전하는 동안 **SQL 인증**을 사용하도록 설정하여 이렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-157">You can do this from the portal by enabling **SQL Authentication** during provisioning.</span></span>

    > [!TIP] 
    > <span data-ttu-id="ba040-158">프로비전하는 동안 SQL 인증을 사용하도록 설정하지 않으면 인증 모드를 수동으로 **SQL Server 및 Windows 인증 모드**로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-158">If you do not enable SQL Authentication during provisioning, you must manually change the authentication mode to **SQL Server and Windows Authentication Mode**.</span></span> <span data-ttu-id="ba040-159">자세한 내용은 [서버 인증 모드 변경](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba040-159">For more information, see [Change Server Authentication Mode](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode).</span></span>

  - <span data-ttu-id="ba040-160">**SA** 로그인을 사용해야 하는 경우 프로비전한 후 로그인을 사용하도록 설정하고 새로운 강력한 암호를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-160">If you must use the **SA** login, enable the login after provisioning and assign a new strong password.</span></span>

## <a name="follow-on-premises-best-practices"></a><span data-ttu-id="ba040-161">온-프레미스 모범 사례 따르기</span><span class="sxs-lookup"><span data-stu-id="ba040-161">Follow on-premises best practices</span></span>

<span data-ttu-id="ba040-162">이 항목에서 설명하는 모범 사례 외에 해당하는 경우 기존의 온-프레미스 보안 방법을 검토하고 구현하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ba040-162">In addition to the practices described in this topic, we recommend that you review and implement the traditional on-premises security practices where applicable.</span></span> <span data-ttu-id="ba040-163">자세한 내용은 [SQL Server 설치에 대한 보안 고려 사항](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba040-163">For more information, see [Security Considerations for a SQL Server Installation](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba040-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ba040-164">Next Steps</span></span>

<span data-ttu-id="ba040-165">성능에 대한 모범 사례에도 관심이 있으면 [Azure Virtual Machines의 SQL Server에 대한 성능 모범 사례](virtual-machines-windows-sql-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba040-165">If you are also interested in best practices around performance, see [Performance Best Practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

<span data-ttu-id="ba040-166">Azure VM에서 SQL Server 실행과 관련된 다른 항목은 [Azure Virtual Machines의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba040-166">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

