---
title: "MySQL을 실행하는 클래식 Azure VM 만들기 | Microsoft Docs"
description: "클래식 배포 모델을 사용하여 Windows Server 2012 R2와 MySQL 데이터베이스를 실행하는 Azure 가상 컴퓨터를 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 98fa06d2-9b92-4d05-ac16-3f8e9fd4feaa
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: cynthn
ms.openlocfilehash: 11850e5ce20efae88a7af9c1d2e4761ed2b70cd7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="install-mysql-on-a-virtual-machine-created-with-the-classic-deployment-model-running-windows-server-2016"></a><span data-ttu-id="6c2cd-103">클래식 배포 모델을 사용하여 만든, Windows Server 2016을 실행하는 가상 컴퓨터에 MySQL 설치</span><span class="sxs-lookup"><span data-stu-id="6c2cd-103">Install MySQL on a virtual machine created with the classic deployment model running Windows Server 2016</span></span>
<span data-ttu-id="6c2cd-104">[MySQL](https://www.mysql.com) 은 인기 있는 오픈 소스 SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-104">[MySQL](https://www.mysql.com) is a popular open source, SQL database.</span></span> <span data-ttu-id="6c2cd-105">이 자습서에서는 **Windows Server 2016**을 실행하는 가상 컴퓨터에 MySQL Server로 **커뮤니티 버전의 MySQL 5.7.18**을 설치하고 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-105">This tutorial shows you how to install and run the **community version of MySQL 5.7.18** as a MySQL Server on a virtual machine running **Windows Server 2016**.</span></span> <span data-ttu-id="6c2cd-106">다른 버전의 MySQL 또는 Windows Server에서는 작업 단계가 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-106">Your experience might be slightly different for other versions of MySQL or Windows Server.</span></span>

<span data-ttu-id="6c2cd-107">Linux에서 MySQL을 설치하는 방법에 대한 지침은 [Azure에 MySQL을 설치하는 방법](../../linux/mysql-install.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-107">For instructions on installing MySQL on Linux, refer to: [How to install MySQL on Azure](../../linux/mysql-install.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c2cd-108">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6c2cd-109">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-109">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="6c2cd-110">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

## <a name="create-a-virtual-machine-running-windows-server-2016"></a><span data-ttu-id="6c2cd-111">Windows Server 2016을 실행하는 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="6c2cd-111">Create a virtual machine running Windows Server 2016</span></span>
<span data-ttu-id="6c2cd-112">Windows Server 2016을 실행하는 VM이 아직 없는 경우 이 [자습서](./tutorial.md)를 사용하여 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-112">If you don't already have a VM running Windows Server 2016, you can use this [tutorial](./tutorial.md) to create the virtual machine.</span></span>

## <a name="attach-a-data-disk"></a><span data-ttu-id="6c2cd-113">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="6c2cd-113">Attach a data disk</span></span>
<span data-ttu-id="6c2cd-114">가상 컴퓨터가 만들어진 후에 선택적으로 데이터 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-114">After the virtual machine is created, you can optionally attach a data disk.</span></span> <span data-ttu-id="6c2cd-115">데이터 디스크 추가는 프로덕션 작업에 권장되며, 운영 체제를 포함하는 OS 드라이브(C:)의 공간 부족을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-115">Adding a data disk is recommended for production workloads and to avoid running out of space on the OS drive (C:), which includes the operating system.</span></span>

<span data-ttu-id="6c2cd-116">[Windows 가상 컴퓨터에 데이터 디스크를 연결하는 방법](../attach-managed-disk-portal.md)을 참조하고 빈 디스크를 연결하는 방법에 대한 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-116">See [How to attach a data disk to a Windows virtual machine](../attach-managed-disk-portal.md) and follow the instructions for attaching an empty disk.</span></span> <span data-ttu-id="6c2cd-117">호스트 캐시 설정을 **없음** 또는 **읽기 전용**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-117">Set the host cache setting to **None** or **Read-only**.</span></span>

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="6c2cd-118">가상 컴퓨터에 로그온</span><span class="sxs-lookup"><span data-stu-id="6c2cd-118">Log on to the virtual machine</span></span>
<span data-ttu-id="6c2cd-119">다음으로, MySQL을 설치할 수 있도록 [가상 컴퓨터에 로그온](./connect-logon.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-119">Next, you'll [log on to the virtual machine](./connect-logon.md) so you can install MySQL.</span></span>

## <a name="install-and-run-mysql-community-server-on-the-virtual-machine"></a><span data-ttu-id="6c2cd-120">가상 컴퓨터에서 MySQL Community Server 설치 및 실행</span><span class="sxs-lookup"><span data-stu-id="6c2cd-120">Install and run MySQL Community Server on the virtual machine</span></span>
<span data-ttu-id="6c2cd-121">커뮤니티 버전의 MySQL Server를 설치, 구성 및 실행하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-121">Follow these steps to install, configure, and run the Community version of MySQL Server:</span></span>

> [!NOTE]
> <span data-ttu-id="6c2cd-122">Internet Explorer를 사용하여 항목을 다운로드할 때 IE **강화된 보안 구성**을 Off로 설정하고 다운로드 프로세스를 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-122">When downloading items using Internet Explorer, you can set the IE **Enhanced Security Configuration** to Off, and simplify the downloading process.</span></span> <span data-ttu-id="6c2cd-123">시작 메뉴에서 관리 도구/서버 관리자/로컬 서버를 클릭한 다음 IE **강화된 보안 구성**을 클릭하고 구성을 Off로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-123">From the Start menu, click Administrative Tools/Server Manager/Local Server, then click IE **Enhanced Security Configuration** and set the configuration to Off).</span></span>
>
>

1. <span data-ttu-id="6c2cd-124">원격 데스크톱을 사용하여 가상 컴퓨터에 연결한 후 시작 화면에서 **Internet Explorer** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-124">After you've connected to the virtual machine using Remote Desktop, click **Internet Explorer** from the start screen.</span></span>
2. <span data-ttu-id="6c2cd-125">오른쪽 위에 있는 **도구** 단추(톱니바퀴 아이콘)를 선택하고 **인터넷 옵션**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-125">Select the **Tools** button in the upper-right corner (the cogged wheel icon), and then click **Internet Options**.</span></span> <span data-ttu-id="6c2cd-126">**보안** 탭을 클릭하고 **신뢰할 수 있는 사이트** 아이콘, **사이트** 단추를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-126">Click the **Security** tab, click the **Trusted Sites** icon, and then click the **Sites** button.</span></span> <span data-ttu-id="6c2cd-127">신뢰할 수 있는 사이트 목록에 http://*.mysql.com을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-127">Add http://*.mysql.com to the list of trusted sites.</span></span> <span data-ttu-id="6c2cd-128">**닫기**를 클릭한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-128">Click **Close**, and then click **OK**.</span></span>
3. <span data-ttu-id="6c2cd-129">Internet Explorer 주소 표시줄에 https://dev.mysql.com/downloads/mysql/을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-129">In the address bar of Internet Explorer, type https://dev.mysql.com/downloads/mysql/.</span></span>
4. <span data-ttu-id="6c2cd-130">MySQL 사이트를 사용하여 최신 버전의 Windows용 MySQL Installer를 찾아서 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-130">Use the MySQL site to locate and download the latest version of the MySQL Installer for Windows.</span></span> <span data-ttu-id="6c2cd-131">MySQL Installer를 선택한 경우 전체 파일 집합이 있는 버전(예: 파일 크기가 352.8MB인 mysql-installer-community-5.7.18.0.msi)을 다운로드하고 설치 관리자를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-131">When choosing the MySQL Installer, download the version that has the complete file set (for example, the mysql-installer-community-5.7.18.0.msi with a file size of 352.8 MB), and save the installer.</span></span>
5. <span data-ttu-id="6c2cd-132">설치 관리자가 다운로드를 마치면 **실행** 을 클릭하여 설정을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-132">When the installer has finished downloading, click **Run** to launch setup.</span></span>
6. <span data-ttu-id="6c2cd-133">**사용권 계약** 페이지에서 사용권 계약에 동의하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-133">On the **License Agreement** page, accept the license agreement and click **Next**.</span></span>
7. <span data-ttu-id="6c2cd-134">**설치 유형 선택** 페이지에서 원하는 설치 유형을 클릭한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-134">On the **Choosing a Setup Type** page, click the setup type that you want, and then click **Next**.</span></span> <span data-ttu-id="6c2cd-135">다음 단계에서는 **서버만** 설치 유형을 선택한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-135">The following steps assume the selection of the **Server only** setup type.</span></span>
8. <span data-ttu-id="6c2cd-136">**요구 사항 확인** 페이지가 표시되는 경우 **실행**을 클릭하여 설치 관리자가 누락된 구성 요소를 설치하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-136">If the **Check Requirements** page displays, click **Execute** to let the installer install any missing components.</span></span> <span data-ttu-id="6c2cd-137">C++ 재배포 가능 패키지 런타임과 같이 표시되는 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-137">Follow any instructions that display, such as the C++ Redistributable runtime.</span></span>
9. <span data-ttu-id="6c2cd-138">**설치** 페이지에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-138">On the **Installation** page, click **Execute**.</span></span> <span data-ttu-id="6c2cd-139">설치가 완료되면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-139">When installation is complete, click **Next**.</span></span>

10. <span data-ttu-id="6c2cd-140">**제품 구성** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-140">On the **Product Configuration** page, click **Next**.</span></span>

11. <span data-ttu-id="6c2cd-141">**유형 및 네트워킹** 페이지에서 원하는 구성 유형 및 연결 옵션을 지정합니다(필요한 경우 TCP 포트 포함).</span><span class="sxs-lookup"><span data-stu-id="6c2cd-141">On the **Type and Networking** page, specify your desired configuration type and connectivity options, including the TCP port if needed.</span></span> <span data-ttu-id="6c2cd-142">**고급 옵션 표시**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-142">Select **Show Advanced Options**, and then click **Next**.</span></span>
    ![](./media/mysql-2008r2/MySQL_TypeNetworking.png)

12. <span data-ttu-id="6c2cd-143">**계정 및 역할** 페이지에서 강력한 MySQL 루트 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-143">On the **Accounts and Roles** page, specify a strong MySQL root password.</span></span> <span data-ttu-id="6c2cd-144">필요에 따라 추가 MySQL 사용자 계정을 추가하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-144">Add additional MySQL user accounts as needed, and then click **Next**.</span></span>

    ![](./media/mysql-2008r2/MySQL_AccountsRoles_Filled.png)
13. <span data-ttu-id="6c2cd-145">**Windows 서비스** 페이지에서 필요에 따라 Windows 서비스로 실행 중인 MySQL Server에 대한 기본 설정을 변경하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-145">On the **Windows Service** page, specify changes to the default settings for running the MySQL Server as a Windows service as needed, and then click **Next**.</span></span>

    ![](./media/mysql-2008r2/MySQL_WindowsService.png)
14. <span data-ttu-id="6c2cd-146">**플러그 인 및 확장** 페이지에서의 선택 항목은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-146">The choices on the **Plugins and Extensions** page are optional.</span></span> <span data-ttu-id="6c2cd-147">**다음**을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-147">Click **Next** to continue.</span></span>
15. <span data-ttu-id="6c2cd-148">**고급 옵션** 페이지에서 필요에 따라 로깅 옵션을 변경하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-148">On the **Advanced Options** page, specify changes to logging options as needed, and then click **Next**.</span></span>

    ![](./media/mysql-2008r2/MySQL_AdvOptions.png)
16. <span data-ttu-id="6c2cd-149">**서버 구성 적용** 페이지에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-149">On the **Apply Server Configuration** page, click **Execute**.</span></span> <span data-ttu-id="6c2cd-150">구성 단계가 완료되면 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-150">When the configuration steps are complete, click **Finish**.</span></span>
17. <span data-ttu-id="6c2cd-151">**제품 구성** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-151">On the **Product Configuration** page, click **Next**.</span></span>
18. <span data-ttu-id="6c2cd-152">나중에 검사하려는 경우 **설치 완료** 페이지에서 **클립보드에 로그 복사**를 클릭한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-152">On the **Installation Complete** page, click **Copy Log to Clipboard** if you want to examine it later, and then click **Finish**.</span></span>
19. <span data-ttu-id="6c2cd-153">시작 화면에서 **mysql**을 입력하고 **MySQL 5.7 명령줄 클라이언트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-153">From the start screen, type **mysql**, and then click **MySQL 5.7 Command-Line Client**.</span></span>
20. <span data-ttu-id="6c2cd-154">12단계에서 지정한 루트 암호를 입력하면 명령을 실행하여 MySQL을 구성할 수 있는 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-154">Enter the root password that you specified in step 12 and you are presented with a prompt where you can issue commands to configure MySQL.</span></span> <span data-ttu-id="6c2cd-155">명령 및 구문에 대한 자세한 내용은 [MySQL 참조 설명서](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-155">For the details of commands and syntax, see [MySQL Reference Manuals](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html).</span></span>

    ![](./media/mysql-2008r2/MySQL_CommandPrompt.png)
21. <span data-ttu-id="6c2cd-156">기본/데이터 디렉터리 및 드라이브 같은 서버 구성 기본 설정을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-156">You can also configure server configuration default settings, such as the base and data directories and drives.</span></span> <span data-ttu-id="6c2cd-157">자세한 내용은 [6.1.2 서버 구성 기본값](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-157">For more information, see [6.1.2 Server Configuration Defaults](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html).</span></span>

## <a name="configure-endpoints"></a><span data-ttu-id="6c2cd-158">끝점 구성</span><span class="sxs-lookup"><span data-stu-id="6c2cd-158">Configure endpoints</span></span>

<span data-ttu-id="6c2cd-159">인터넷상의 클라이언트 컴퓨터에 사용 가능한 MySQL 서비스의 경우 TCP 포트에 대한 끝점을 구성하고 Windows 방화벽 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-159">For the MySQL service to be available to client computers on the Internet, you must configure an endpoint for the TCP port and create a Windows Firewall rule.</span></span> <span data-ttu-id="6c2cd-160">MySQL Server 서비스가 MySQL 클라이언트에 대해 수신하는 기본 포트 값은 3306입니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-160">The default port value on which the MySQL Server service listens for MySQL clients is 3306.</span></span> <span data-ttu-id="6c2cd-161">**유형 및 네트워킹** 페이지(이전 절차의 11단계)에서 제공된 값과 일치하는 한 다른 포트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-161">You can specify another port, as long as the port is consistent with the value supplied on the **Type and Networking** page (step 11 of the previous procedure).</span></span>

> [!NOTE]
> <span data-ttu-id="6c2cd-162">프로덕션 사용의 경우 인터넷상의 모든 컴퓨터가 MySQL Server 서비스를 사용할 수 있으므로 보안 영향을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-162">For production use, consider the security implications of making the MySQL Server service available to all computers on the Internet.</span></span> <span data-ttu-id="6c2cd-163">ACL(액세스 제어 목록)에서 끝점을 사용할 수 있는 원본 IP 주소 집합을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-163">You can define the set of source IP addresses that are allowed to use the endpoint with an Access Control List (ACL).</span></span> <span data-ttu-id="6c2cd-164">자세한 내용은 [가상 컴퓨터로 끝점을 설정하는 방법](setup-endpoints.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-164">For more information, see [How to Set Up Endpoints to a Virtual Machine](setup-endpoints.md).</span></span>
>
>

<span data-ttu-id="6c2cd-165">MySQL Server 서비스의 끝점을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="6c2cd-165">To configure an endpoint for the MySQL Server service:</span></span>

1. <span data-ttu-id="6c2cd-166">Azure Portal에서 **Virtual Machines(클래식)**을 클릭하고 MySQL 가상 컴퓨터의 이름을 클릭한 다음 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-166">In the Azure portal, click **Virtual Machines (classic)**, click the name of your MySQL virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="6c2cd-167">명령 모음에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-167">In the command bar, click **Add**.</span></span>
3. <span data-ttu-id="6c2cd-168">**끝점 추가** 페이지에서 **이름**에 고유 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-168">On the **Add endpoint** page, type a unique name for **Name**.</span></span>
4. <span data-ttu-id="6c2cd-169">프로토콜로 **TCP**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-169">Select **TCP** as the protocol.</span></span>
5. <span data-ttu-id="6c2cd-170">**공용 포트** 및 **개인 포트** 둘 다에 **3306**과 같은 포트 번호를 입력한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-170">Type the port number, such as **3306**, in both **Public Port** and **Private Port**, and then click **OK**.</span></span>

## <a name="add-a-windows-firewall-rule-to-allow-mysql-traffic"></a><span data-ttu-id="6c2cd-171">MySQL 트래픽을 허용하도록 Windows 방화벽 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="6c2cd-171">Add a Windows Firewall rule to allow MySQL traffic</span></span>
<span data-ttu-id="6c2cd-172">인터넷에서의 MySQL 트래픽을 허용하는 Windows 방화벽 규칙을 추가하려면 MySQL 서버 가상 컴퓨터의 _관리자 권한 Windows PowerShell 명령 프롬프트_에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-172">To add a Windows Firewall rule that allows MySQL traffic from the Internet, run the following command at an _elevated Windows PowerShell command prompt_ on the MySQL server virtual machine.</span></span>

    New-NetFirewallRule -DisplayName "MySQL57" -Direction Inbound –Protocol TCP –LocalPort 3306 -Action Allow -Profile Public

## <a name="test-your-remote-connection"></a><span data-ttu-id="6c2cd-173">원격 연결 테스트</span><span class="sxs-lookup"><span data-stu-id="6c2cd-173">Test your remote connection</span></span>
<span data-ttu-id="6c2cd-174">MySQL Server 서비스를 실행하는 Azure VM에 원격 연결을 테스트하려면 VN를 포함하는 클라우드 서비스의 DNS 이름을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-174">To test your remote connection to the Azure VM running the MySQL Server service, you must provide the DNS name of the cloud service containing the VN.</span></span>

1. <span data-ttu-id="6c2cd-175">Azure 포털에서 **Virtual Machines(클래식)**을 클릭하고 MySQL 서버 가상 컴퓨터의 이름을 클릭한 다음 **개요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-175">In the Azure portal, click **Virtual Machines (classic)**, click the name of your MySQL server virtual machine, and then click **Overview**.</span></span>
2. <span data-ttu-id="6c2cd-176">가상 컴퓨터 대시보드에서 **DNS 이름** 값을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-176">From the virtual machine dashboard, note the **DNS Name** value.</span></span> <span data-ttu-id="6c2cd-177">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-177">Here is an example:</span></span>

   ![](media/mysql-2008r2/MySQL_DNSName.png)
3. <span data-ttu-id="6c2cd-178">MySQL을 실행 중인 로컬 컴퓨터 또는 MySQL 클라이언트에서 다음 명령을 실행하여 MySQL 사용자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-178">From a local computer running MySQL or the MySQL client, run the following command to log in as a MySQL user.</span></span>

     <span data-ttu-id="6c2cd-179">mysql -u <yourMysqlUsername> -p -h <yourDNSname></span><span class="sxs-lookup"><span data-stu-id="6c2cd-179">mysql -u <yourMysqlUsername> -p -h <yourDNSname></span></span>

   <span data-ttu-id="6c2cd-180">예를 들어 MySQL 사용자 이름이 _dbadmin3_이고 가상 컴퓨터의 DNS 이름이 _testmysql.cloudapp.net_인 경우 다음의 명령을 사용하여 MySQL을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-180">For example, using the MySQL user name _dbadmin3_ and the _testmysql.cloudapp.net_ DNS name for the virtual machine, you could start MySQL using the following command:</span></span>

     <span data-ttu-id="6c2cd-181">mysql -u dbadmin3 -p -h testmysql.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="6c2cd-181">mysql -u dbadmin3 -p -h testmysql.cloudapp.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c2cd-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c2cd-182">Next steps</span></span>
<span data-ttu-id="6c2cd-183">MySQL 실행에 대한 자세한 내용은 [MySQL 설명서](http://dev.mysql.com/doc/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c2cd-183">To learn more about running MySQL, see the [MySQL Documentation](http://dev.mysql.com/doc/).</span></span>
