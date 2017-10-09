---
title: "클래식 Azure VM aaaCreate MySQL을 실행 | Microsoft Docs"
description: "Windows Server 2012 r 2를 실행 하는 Azure 가상 컴퓨터를 만들고 hello 클래식 배포 모델을 사용 하 여 MySQL 데이터베이스 hello 합니다."
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
ms.openlocfilehash: 2c9564955c2bab197a8e494e939ce16c0b9bb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-created-with-hello-classic-deployment-model-running-windows-server-2016"></a><span data-ttu-id="82356-103">Windows Server 2016을 실행 하는 hello 클래식 배포 모델을 사용 하 여 만든 가상 컴퓨터에서 MySQL을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-103">Install MySQL on a virtual machine created with hello classic deployment model running Windows Server 2016</span></span>
<span data-ttu-id="82356-104">[MySQL](https://www.mysql.com) 은 인기 있는 오픈 소스 SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="82356-104">[MySQL](https://www.mysql.com) is a popular open source, SQL database.</span></span> <span data-ttu-id="82356-105">이 자습서에서는 어떻게 tooinstall 및 실행 hello **커뮤니티 버전의 MySQL 5.7.18** 실행 가상 컴퓨터에서 MySQL 서버와 **Windows Server 2016**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-105">This tutorial shows you how tooinstall and run hello **community version of MySQL 5.7.18** as a MySQL Server on a virtual machine running **Windows Server 2016**.</span></span> <span data-ttu-id="82356-106">다른 버전의 MySQL 또는 Windows Server에서는 작업 단계가 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82356-106">Your experience might be slightly different for other versions of MySQL or Windows Server.</span></span>

<span data-ttu-id="82356-107">Linux에서 MySQL를 설치 하는 방법에 지침은 참조: [어떻게 tooinstall Azure에서 MySQL](../../linux/mysql-install.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-107">For instructions on installing MySQL on Linux, refer to: [How tooinstall MySQL on Azure](../../linux/mysql-install.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82356-108">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82356-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="82356-109">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-109">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="82356-110">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="82356-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="create-a-virtual-machine-running-windows-server-2016"></a><span data-ttu-id="82356-111">Windows Server 2016을 실행하는 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="82356-111">Create a virtual machine running Windows Server 2016</span></span>
<span data-ttu-id="82356-112">Windows Server 2016을 실행 하는 VM이 없는 경우이 사용할 수 있습니다 [자습서](./tutorial.md) toocreate hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="82356-112">If you don't already have a VM running Windows Server 2016, you can use this [tutorial](./tutorial.md) toocreate hello virtual machine.</span></span>

## <a name="attach-a-data-disk"></a><span data-ttu-id="82356-113">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="82356-113">Attach a data disk</span></span>
<span data-ttu-id="82356-114">Hello 가상 컴퓨터를 만든 후 데이터 디스크를 필요에 따라 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82356-114">After hello virtual machine is created, you can optionally attach a data disk.</span></span> <span data-ttu-id="82356-115">Hello 운영 체제 포함 데이터 디스크는 프로덕션 작업 및 운영 체제 드라이브 (c:) hello에 공간이 부족 tooavoid에 권장를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-115">Adding a data disk is recommended for production workloads and tooavoid running out of space on hello OS drive (C:), which includes hello operating system.</span></span>

<span data-ttu-id="82356-116">참조 [tooattach 데이터 tooa Windows 가상 컴퓨터 디스크 하는 방법을](../attach-managed-disk-portal.md) 빈 디스크 연결에 대 한 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="82356-116">See [How tooattach a data disk tooa Windows virtual machine](../attach-managed-disk-portal.md) and follow hello instructions for attaching an empty disk.</span></span> <span data-ttu-id="82356-117">Hello 호스트 캐시 설정 너무 설정**None** 또는 **읽기 전용**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-117">Set hello host cache setting too**None** or **Read-only**.</span></span>

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="82356-118">Toohello 가상 컴퓨터에 로그온</span><span class="sxs-lookup"><span data-stu-id="82356-118">Log on toohello virtual machine</span></span>
<span data-ttu-id="82356-119">[Toohello 가상 컴퓨터에 로그온](./connect-logon.md) MySQL을 설치할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-119">Next, you'll [log on toohello virtual machine](./connect-logon.md) so you can install MySQL.</span></span>

## <a name="install-and-run-mysql-community-server-on-hello-virtual-machine"></a><span data-ttu-id="82356-120">설치 하 고 MySQL Community 서버 hello 가상 컴퓨터에서 실행</span><span class="sxs-lookup"><span data-stu-id="82356-120">Install and run MySQL Community Server on hello virtual machine</span></span>
<span data-ttu-id="82356-121">이러한 단계 tooinstall에 따라, 구성 및 hello 커뮤니티 버전의 MySQL Server를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-121">Follow these steps tooinstall, configure, and run hello Community version of MySQL Server:</span></span>

> [!NOTE]
> <span data-ttu-id="82356-122">Internet Explorer를 사용 하 여 항목을 다운로드할 때 hello IE를 설정할 수 있습니다 **보안 강화 구성** tooOff, 고 hello 다운로드 프로세스를 단순화 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-122">When downloading items using Internet Explorer, you can set hello IE **Enhanced Security Configuration** tooOff, and simplify hello downloading process.</span></span> <span data-ttu-id="82356-123">Hello 시작 메뉴에서 관리 도구/서버 관리자/로컬 서버를 클릭 한 다음 클릭 IE **보안 강화 구성** hello 구성 tooOff 설정).</span><span class="sxs-lookup"><span data-stu-id="82356-123">From hello Start menu, click Administrative Tools/Server Manager/Local Server, then click IE **Enhanced Security Configuration** and set hello configuration tooOff).</span></span>
>
>

1. <span data-ttu-id="82356-124">원격 데스크톱을 사용 하 여 toohello 가상 컴퓨터를 연결한 후 클릭 **Internet Explorer** hello 시작 화면에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-124">After you've connected toohello virtual machine using Remote Desktop, click **Internet Explorer** from hello start screen.</span></span>
2. <span data-ttu-id="82356-125">선택 hello **도구** hello 오른쪽 위 모서리 (hello cogged 휠 아이콘) 단추를 선택한 다음 클릭 **인터넷 옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-125">Select hello **Tools** button in hello upper-right corner (hello cogged wheel icon), and then click **Internet Options**.</span></span> <span data-ttu-id="82356-126">Hello 클릭 **보안** 탭에서 hello **신뢰할 수 있는 사이트** 아이콘을 hello를 클릭 한 다음 **사이트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="82356-126">Click hello **Security** tab, click hello **Trusted Sites** icon, and then click hello **Sites** button.</span></span> <span data-ttu-id="82356-127">신뢰할 수 있는 사이트 http://*.mysql.com toohello 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-127">Add http://*.mysql.com toohello list of trusted sites.</span></span> <span data-ttu-id="82356-128">**닫기**를 클릭한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-128">Click **Close**, and then click **OK**.</span></span>
3. <span data-ttu-id="82356-129">hello 주소 표시줄의 Internet Explorer https://dev.mysql.com/downloads/mysql/를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-129">In hello address bar of Internet Explorer, type https://dev.mysql.com/downloads/mysql/.</span></span>
4. <span data-ttu-id="82356-130">MySQL 사이트 toolocate hello를 사용 하 고 hello hello MySQL Windows 용 설치 관리자의 최신 버전을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-130">Use hello MySQL site toolocate and download hello latest version of hello MySQL Installer for Windows.</span></span> <span data-ttu-id="82356-131">Hello MySQL 설치 관리자를 선택할 때는 hello 파일 집합 (예를 들어 hello mysql-설치 프로그램-커뮤니티-5.7.18.0.msi 352.8 MB의 파일 크기)를 완료 하 고 hello 설치 관리자를 저장 된 hello 버전을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-131">When choosing hello MySQL Installer, download hello version that has hello complete file set (for example, hello mysql-installer-community-5.7.18.0.msi with a file size of 352.8 MB), and save hello installer.</span></span>
5. <span data-ttu-id="82356-132">Hello 설치 관리자 다운로드 완료 되 면 클릭 **실행** toolaunch 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-132">When hello installer has finished downloading, click **Run** toolaunch setup.</span></span>
6. <span data-ttu-id="82356-133">Hello에 **사용권 계약** 페이지 hello 사용권 계약에 동의 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-133">On hello **License Agreement** page, accept hello license agreement and click **Next**.</span></span>
7. <span data-ttu-id="82356-134">Hello에 **설치 유형을 선택 하면** 페이지에서 클릭 하 고 클릭 hello 설치 유형을 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-134">On hello **Choosing a Setup Type** page, click hello setup type that you want, and then click **Next**.</span></span> <span data-ttu-id="82356-135">hello 다음 단계에서는 가정 hello hello 선택을 **서버만** 설치 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="82356-135">hello following steps assume hello selection of hello **Server only** setup type.</span></span>
8. <span data-ttu-id="82356-136">경우 hello **요구 사항 확인** 페이지가 표시를 클릭 **Execute** toolet hello 설치 관리자는 누락 된 구성 요소를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-136">If hello **Check Requirements** page displays, click **Execute** toolet hello installer install any missing components.</span></span> <span data-ttu-id="82356-137">Hello c + + 재배포 가능 런타임과 같이 표시 하는 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="82356-137">Follow any instructions that display, such as hello C++ Redistributable runtime.</span></span>
9. <span data-ttu-id="82356-138">Hello에 **설치** 페이지 **Execute**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-138">On hello **Installation** page, click **Execute**.</span></span> <span data-ttu-id="82356-139">설치가 완료되면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-139">When installation is complete, click **Next**.</span></span>

10. <span data-ttu-id="82356-140">Hello에 **제품 구성** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-140">On hello **Product Configuration** page, click **Next**.</span></span>

11. <span data-ttu-id="82356-141">Hello에 **유형 및 네트워킹** 페이지에서 원하는 구성 유형 및 연결 옵션, 필요한 경우 hello TCP 포트를 포함 하 여 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-141">On hello **Type and Networking** page, specify your desired configuration type and connectivity options, including hello TCP port if needed.</span></span> <span data-ttu-id="82356-142">**고급 옵션 표시**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-142">Select **Show Advanced Options**, and then click **Next**.</span></span>
    ![](./media/mysql-2008r2/MySQL_TypeNetworking.png)

12. <span data-ttu-id="82356-143">Hello에 **계정과 역할** 페이지에서 강력한 MySQL 루트 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-143">On hello **Accounts and Roles** page, specify a strong MySQL root password.</span></span> <span data-ttu-id="82356-144">필요에 따라 추가 MySQL 사용자 계정을 추가하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-144">Add additional MySQL user accounts as needed, and then click **Next**.</span></span>

    ![](./media/mysql-2008r2/MySQL_AccountsRoles_Filled.png)
13. <span data-ttu-id="82356-145">Hello에 **Windows 서비스** 페이지, 필요에 따라 hello MySQL 서버를 Windows 서비스로 실행 하기 위한 변경 toohello 기본 설정을 지정 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-145">On hello **Windows Service** page, specify changes toohello default settings for running hello MySQL Server as a Windows service as needed, and then click **Next**.</span></span>

    ![](./media/mysql-2008r2/MySQL_WindowsService.png)
14. <span data-ttu-id="82356-146">hello에 대 한 선택 사항 hello **플러그 인 및 확장** 페이지는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="82356-146">hello choices on hello **Plugins and Extensions** page are optional.</span></span> <span data-ttu-id="82356-147">클릭 **다음** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-147">Click **Next** toocontinue.</span></span>
15. <span data-ttu-id="82356-148">Hello에 **고급 옵션** 페이지, 필요에 따라 변경 내용을 toologging 옵션을 지정 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-148">On hello **Advanced Options** page, specify changes toologging options as needed, and then click **Next**.</span></span>

    ![](./media/mysql-2008r2/MySQL_AdvOptions.png)
16. <span data-ttu-id="82356-149">Hello에 **서버 구성 적용** 페이지 **Execute**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-149">On hello **Apply Server Configuration** page, click **Execute**.</span></span> <span data-ttu-id="82356-150">Hello 구성 단계가 완료 되 면 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-150">When hello configuration steps are complete, click **Finish**.</span></span>
17. <span data-ttu-id="82356-151">Hello에 **제품 구성** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-151">On hello **Product Configuration** page, click **Next**.</span></span>
18. <span data-ttu-id="82356-152">Hello에 **설치 완료** 페이지 **복사 로그 tooClipboard** 나중 누른 tooexamine 하려는 경우 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-152">On hello **Installation Complete** page, click **Copy Log tooClipboard** if you want tooexamine it later, and then click **Finish**.</span></span>
19. <span data-ttu-id="82356-153">Hello 시작 화면에서 입력 **mysql**, 클릭 하 고 **MySQL 5.7 명령줄 클라이언트**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-153">From hello start screen, type **mysql**, and then click **MySQL 5.7 Command-Line Client**.</span></span>
20. <span data-ttu-id="82356-154">12 단계에서 지정한 hello 루트 암호를 입력 하 고 표시 되는 프롬프트 명령을 tooconfigure MySQL을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82356-154">Enter hello root password that you specified in step 12 and you are presented with a prompt where you can issue commands tooconfigure MySQL.</span></span> <span data-ttu-id="82356-155">명령 및 구문을 hello 세부 정보를 참조 하십시오. [MySQL 참조 설명서](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-155">For hello details of commands and syntax, see [MySQL Reference Manuals](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html).</span></span>

    ![](./media/mysql-2008r2/MySQL_CommandPrompt.png)
21. <span data-ttu-id="82356-156">또한 기본 hello 및 데이터 디렉터리 및 드라이브와 같은 서버 구성 기본 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82356-156">You can also configure server configuration default settings, such as hello base and data directories and drives.</span></span> <span data-ttu-id="82356-157">자세한 내용은 [6.1.2 서버 구성 기본값](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82356-157">For more information, see [6.1.2 Server Configuration Defaults](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html).</span></span>

## <a name="configure-endpoints"></a><span data-ttu-id="82356-158">끝점 구성</span><span class="sxs-lookup"><span data-stu-id="82356-158">Configure endpoints</span></span>

<span data-ttu-id="82356-159">컴퓨터용 hello MySQL 서비스 toobe 사용 가능한 tooclient hello 인터넷에 hello TCP 포트에 대 한 끝점을 구성 하 고 Windows 방화벽 규칙을 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-159">For hello MySQL service toobe available tooclient computers on hello Internet, you must configure an endpoint for hello TCP port and create a Windows Firewall rule.</span></span> <span data-ttu-id="82356-160">hello MySQL 클라이언트에 대 한 수신 대기 서비스는 hello MySQL Server에는 기본 포트 값은 3306 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-160">hello default port value on which hello MySQL Server service listens for MySQL clients is 3306.</span></span> <span data-ttu-id="82356-161">Hello 포트는 hello에 제공 하는 hello 값과 일치으로 다른 포트를 지정할 수 있습니다 **유형 및 네트워킹** (hello 이전 절차의 11 단계) 페이지.</span><span class="sxs-lookup"><span data-stu-id="82356-161">You can specify another port, as long as hello port is consistent with hello value supplied on hello **Type and Networking** page (step 11 of hello previous procedure).</span></span>

> [!NOTE]
> <span data-ttu-id="82356-162">프로덕션 용도로 hello를 hello 인터넷에서 MySQL 서버 hello tooall 사용할 수 있는 컴퓨터에 서비스를 만드는 요소의 보안 문제도 고려해.</span><span class="sxs-lookup"><span data-stu-id="82356-162">For production use, consider hello security implications of making hello MySQL Server service available tooall computers on hello Internet.</span></span> <span data-ttu-id="82356-163">Hello toouse hello 끝점은 액세스 제어 목록 (ACL)를 허용 되는 원본 IP 주소 집합을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82356-163">You can define hello set of source IP addresses that are allowed toouse hello endpoint with an Access Control List (ACL).</span></span> <span data-ttu-id="82356-164">자세한 내용은 참조 [어떻게 tooSet 끝점 tooa 가상 컴퓨터](setup-endpoints.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-164">For more information, see [How tooSet Up Endpoints tooa Virtual Machine](setup-endpoints.md).</span></span>
>
>

<span data-ttu-id="82356-165">tooconfigure hello MySQL Server 서비스에 대 한 끝점:</span><span class="sxs-lookup"><span data-stu-id="82356-165">tooconfigure an endpoint for hello MySQL Server service:</span></span>

1. <span data-ttu-id="82356-166">Hello Azure 포털에서에서 클릭 **가상 컴퓨터 (클래식)**MySQL 가상 컴퓨터의 hello 이름을 클릭 하 고 클릭 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-166">In hello Azure portal, click **Virtual Machines (classic)**, click hello name of your MySQL virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="82356-167">Hello 명령 모음에서 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-167">In hello command bar, click **Add**.</span></span>
3. <span data-ttu-id="82356-168">Hello에 **끝점 추가** 페이지에 대 한 고유한 이름을 입력 합니다 **이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-168">On hello **Add endpoint** page, type a unique name for **Name**.</span></span>
4. <span data-ttu-id="82356-169">선택 **TCP** hello 프로토콜로 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-169">Select **TCP** as hello protocol.</span></span>
5. <span data-ttu-id="82356-170">같은 hello 포트 번호를 입력 **3306**, 둘 다에서 **공용 포트** 및 **개인 포트**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-170">Type hello port number, such as **3306**, in both **Public Port** and **Private Port**, and then click **OK**.</span></span>

## <a name="add-a-windows-firewall-rule-tooallow-mysql-traffic"></a><span data-ttu-id="82356-171">Windows 방화벽 규칙 tooallow MySQL 트래픽 추가</span><span class="sxs-lookup"><span data-stu-id="82356-171">Add a Windows Firewall rule tooallow MySQL traffic</span></span>
<span data-ttu-id="82356-172">hello 다음에서 명령을 실행 하는 hello 인터넷에서에서 MySQL 트래픽을 허용 하는 Windows 방화벽 규칙 tooadd는 _관리자 권한 Windows PowerShell 명령 프롬프트_ hello MySQL 서버 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="82356-172">tooadd a Windows Firewall rule that allows MySQL traffic from hello Internet, run hello following command at an _elevated Windows PowerShell command prompt_ on hello MySQL server virtual machine.</span></span>

    New-NetFirewallRule -DisplayName "MySQL57" -Direction Inbound –Protocol TCP –LocalPort 3306 -Action Allow -Profile Public

## <a name="test-your-remote-connection"></a><span data-ttu-id="82356-173">원격 연결 테스트</span><span class="sxs-lookup"><span data-stu-id="82356-173">Test your remote connection</span></span>
<span data-ttu-id="82356-174">tootest 여 원격 연결 toohello Azure VM 실행 중인 hello MySQL 서버 서비스, VN hello를 포함 하는 hello 클라우드 서비스의 hello DNS 이름을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-174">tootest your remote connection toohello Azure VM running hello MySQL Server service, you must provide hello DNS name of hello cloud service containing hello VN.</span></span>

1. <span data-ttu-id="82356-175">Hello Azure 포털에서에서 클릭 **가상 컴퓨터 (클래식)**MySQL server 가상 컴퓨터의 hello 이름을 클릭 하 고 클릭 **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-175">In hello Azure portal, click **Virtual Machines (classic)**, click hello name of your MySQL server virtual machine, and then click **Overview**.</span></span>
2. <span data-ttu-id="82356-176">Hello 가상 컴퓨터 대시보드에서 hello 참고 **DNS 이름** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="82356-176">From hello virtual machine dashboard, note hello **DNS Name** value.</span></span> <span data-ttu-id="82356-177">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="82356-177">Here is an example:</span></span>

   ![](media/mysql-2008r2/MySQL_DNSName.png)
3. <span data-ttu-id="82356-178">MySQL 사용자로의 명령 toolog 다음 hello MySQL 또는 hello MySQL 클라이언트를 실행 하는 로컬 컴퓨터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-178">From a local computer running MySQL or hello MySQL client, run hello following command toolog in as a MySQL user.</span></span>

     <span data-ttu-id="82356-179">mysql -u <yourMysqlUsername> -p -h <yourDNSname></span><span class="sxs-lookup"><span data-stu-id="82356-179">mysql -u <yourMysqlUsername> -p -h <yourDNSname></span></span>

   <span data-ttu-id="82356-180">예를 들어 MySQL 사용자 이름을 사용 하 여 hello _dbadmin3_ 및 hello _testmysql.cloudapp.net_ hello 가상 컴퓨터에 대 한 DNS 이름, 다음 명령을 hello를 사용 하 여 MySQL을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82356-180">For example, using hello MySQL user name _dbadmin3_ and hello _testmysql.cloudapp.net_ DNS name for hello virtual machine, you could start MySQL using hello following command:</span></span>

     <span data-ttu-id="82356-181">mysql -u dbadmin3 -p -h testmysql.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="82356-181">mysql -u dbadmin3 -p -h testmysql.cloudapp.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="82356-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="82356-182">Next steps</span></span>
<span data-ttu-id="82356-183">MySQL을 실행에 대 한 더 toolearn 참조 hello [MySQL 설명서](http://dev.mysql.com/doc/)합니다.</span><span class="sxs-lookup"><span data-stu-id="82356-183">toolearn more about running MySQL, see hello [MySQL Documentation](http://dev.mysql.com/doc/).</span></span>
