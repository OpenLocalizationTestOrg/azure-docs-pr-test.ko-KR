---
title: "SQL Server 가상 컴퓨터를 IPython Notebook 서버로 설정 | Microsoft Docs"
description: "SQL Server 및 IPython 서버를 사용하여 데이터 과학 가상 컴퓨터를 설정합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1fd6014a-d180-4558-b4eb-d9b5a331a99f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 8a151a6a15d4d000a774e3ec4e38bfa0e58ca33b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-an-azure-sql-server-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a><span data-ttu-id="9b8c3-103">고급 분석을 위해 Azure SQL Server 가상 컴퓨터를 IPython Notebook으로 설정</span><span class="sxs-lookup"><span data-stu-id="9b8c3-103">Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics</span></span>
<span data-ttu-id="9b8c3-104">이 토픽에서는 클라우드 기반 데이터 과학 환경의 일부로 사용할 SQL Server 가상 컴퓨터를 프로비전 및 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-104">This topic shows how to provision and configure an SQL Server virtual machine to be used as part of a cloud-based data science environment.</span></span> <span data-ttu-id="9b8c3-105">Windows 가상 컴퓨터는 IPython Notebook, Azure Storage Explorer 및 AzCopy와 같은 지원 도구뿐만 아니라 데이터 과학 프로젝트에 유용한 기타 유틸리티로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-105">The Windows virtual machine is configured with supporting tools such as IPython Notebook, Azure Storage Explorer, and AzCopy, as well as other utilities that are useful for data science projects.</span></span> <span data-ttu-id="9b8c3-106">예를 들어 Azure 저장소 탐색기와 AzCopy는 로컬 컴퓨터에서 Azure Blob 저장소로 데이터를 업로드하거나 Blob 저장소에서 로컬 컴퓨터로 데이터를 다운로드하는 데 편리한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-106">Azure Storage Explorer and AzCopy, for example, provide convenient ways to upload data to Azure blob storage from your local machine or to download it to your local machine from blob storage.</span></span>

<span data-ttu-id="9b8c3-107">Azure 가상 컴퓨터 갤러리에는 Microsoft SQL Server가 포함된 몇 개의 이미지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-107">The Azure virtual machine gallery includes several images that contain Microsoft SQL Server.</span></span> <span data-ttu-id="9b8c3-108">데이터 요구 사항에 적합한 SQL Server VM 이미지를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-108">Select an SQL Server VM image that is suitable for your data needs.</span></span> <span data-ttu-id="9b8c3-109">권장 이미지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-109">Recommended images are:</span></span>

* <span data-ttu-id="9b8c3-110">중소 규모 데이터의 경우 SQL Server 2012 SP2 Enterprise</span><span class="sxs-lookup"><span data-stu-id="9b8c3-110">SQL Server 2012 SP2 Enterprise for small to medium data sizes</span></span>
* <span data-ttu-id="9b8c3-111">대규모 데이터의 경우 SQL Server 2012 SP2 Enterprise Optimized for DataWarehousing Workloads</span><span class="sxs-lookup"><span data-stu-id="9b8c3-111">SQL Server 2012 SP2 Enterprise Optimized for DataWarehousing Workloads for large to very large data sizes</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="9b8c3-112">SQL Server 2012 SP2 Enterprise 이미지에는 **데이터 디스크가 포함되어 있지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-112">SQL Server 2012 SP2 Enterprise image **does not include a data disk**.</span></span> <span data-ttu-id="9b8c3-113">데이터를 저장할 하나 이상의 가상 하드 디스크를 추가 및/또는 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-113">You will need to add and/or attach one or more virtual hard disks to store your data.</span></span> <span data-ttu-id="9b8c3-114">Azure 가상 컴퓨터를 만들면 C 드라이브에 매핑되는 운영 체제용 디스크와 D 드라이브에 매핑되는 임시 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-114">When you create an Azure virtual machine, it has a disk for the operating system mapped to the C drive and a temporary disk mapped to the D drive.</span></span> <span data-ttu-id="9b8c3-115">D 드라이브는 데이터 저장에 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-115">Do not use the D drive to store data.</span></span> <span data-ttu-id="9b8c3-116">이름이 의미하는 것과 같이 D 드라이브는 임시 저장소만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-116">As the name implies, it provides temporary storage only.</span></span> <span data-ttu-id="9b8c3-117">Azure 저장소에 상주하지 않으므로 중복성이나 백업을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-117">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
  > 
  > 

## <span data-ttu-id="9b8c3-118"><a name="Provision"></a>Azure 클래식 포털에 연결 및 SQL Server 가상 컴퓨터 프로비전</span><span class="sxs-lookup"><span data-stu-id="9b8c3-118"><a name="Provision"></a>Connect to the Azure Classic Portal and provision an SQL Server virtual machine</span></span>
1. <span data-ttu-id="9b8c3-119">사용자 계정을 사용하여 [Azure 클래식 포털](http://manage.windowsazure.com/) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-119">Log in to the [Azure Classic portal](http://manage.windowsazure.com/) using your account.</span></span>
   <span data-ttu-id="9b8c3-120">Azure 계정이 없는 경우 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-120">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="9b8c3-121">Azure 클래식 포털 웹 페이지의 왼쪽 아래에서 **+새로 만들기**, **계산**, **가상 컴퓨터**, **갤러리에서**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-121">On the Azure Classic portal, at the bottom left of the web page, click **+NEW**, click **COMPUTE**, click **VIRTUAL MACHINE**, and then click **FROM GALLERY**.</span></span>
3. <span data-ttu-id="9b8c3-122">**가상 컴퓨터 만들기** 페이지에서 데이터 요구 사항에 따라 SQL Server가 포함된 가상 컴퓨터 이미지를 선택한 후 페이지의 오른쪽 아래에서 다음 화살표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-122">On the **Create a Virtual Machine** page, select a virtual machine image containing SQL Server based on your data needs, and then click the next arrow at the bottom right of the page.</span></span> <span data-ttu-id="9b8c3-123">Azure에서 지원되는 SQL Server 이미지에 대한 최신 정보는 [Azure Virtual Machines의 SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=294719) 문서 집합의 [Azure Virtual Machines에서 SQL Server 시작](http://go.microsoft.com/fwlink/p/?LinkId=294720) 토픽을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-123">For the most up-to-date information on the supported SQL Server images on Azure, see [Getting Started with SQL Server in Azure Virtual Machines](http://go.microsoft.com/fwlink/p/?LinkId=294720) topic in the [SQL Server in Azure Virtual Machines](http://go.microsoft.com/fwlink/p/?LinkId=294719) documentation set.</span></span>
   
   ![SQL Server VM 선택][1]
4. <span data-ttu-id="9b8c3-125">첫 번째 **가상 컴퓨터 구성** 페이지에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-125">On the first **Virtual Machine Configuration** page, provide the following information:</span></span>
   
   * <span data-ttu-id="9b8c3-126">**가상 컴퓨터 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-126">Provide a **VIRTUAL MACHINE NAME**.</span></span>
   * <span data-ttu-id="9b8c3-127">**새 사용자 이름** 상자에 VM 로컬 관리자 계정의 고유한 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-127">In the **NEW USER NAME** box, type unique user name for the VM local administrator account.</span></span>
   * <span data-ttu-id="9b8c3-128">**새 암호** 상자에 강력한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-128">In the **NEW PASSWORD** box, type a strong password.</span></span> <span data-ttu-id="9b8c3-129">자세한 내용은 [강력한 암호](http://msdn.microsoft.com/library/ms161962.aspx)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-129">For more information, see [Strong Passwords](http://msdn.microsoft.com/library/ms161962.aspx).</span></span>
   * <span data-ttu-id="9b8c3-130">**암호 확인** 상자에 암호를 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-130">In the **CONFIRM PASSWORD** box, retype the password.</span></span>
   * <span data-ttu-id="9b8c3-131">드롭다운 목록에서 적절한 **크기** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-131">Select the appropriate **SIZE** from the drop down list.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="9b8c3-132">프로비전하는 동안 가상 컴퓨터의 크기가 지정됩니다. A2는 프로덕션 작업에 권장 되는 가장 작은 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-132">The size of the virtual machine is specified during provisioning: A2 is the smallest size recommended for production workloads.</span></span> <span data-ttu-id="9b8c3-133">SQL Server Enterprise Edition을 사용할 경우 가상 컴퓨터의 최소 권장 크기는 A3입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-133">The minimum recommended size for a virtual machine is A3 when using SQL Server Enterprise Edition.</span></span> <span data-ttu-id="9b8c3-134">SQL Server Enterprise Edition을 사용할 경우 A3 이상을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-134">Select A3 or higher when using SQL Server Enterprise Edition.</span></span> <span data-ttu-id="9b8c3-135">트랜잭션 작업 이미지에 최적화된 SQL Server 2012 또는 2014 Enterprise를 사용할 때는 A4를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-135">Select A4 when using SQL Server 2012 or 2014 Enterprise Optimized for Transactional Workloads images.</span></span>
     > <span data-ttu-id="9b8c3-136">데이터 웨어하우스 작업 이미지에 최적화된 SQL Server 2012 또는 2014 Enterprise를 사용할 때는 A7을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-136">Select A7 when using SQL Server 2012 or 2014 Enterprise Optimized for Data Warehousing Workloads images.</span></span> <span data-ttu-id="9b8c3-137">선택한 크기는 구성할 수 있는 데이터 디스크 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-137">The size selected limits the number of data disks you can configure.</span></span> <span data-ttu-id="9b8c3-138">사용 가능한 가상 컴퓨터 크기 및 가상 컴퓨터에 연결할 수 있는 데이터 디스크 수에 대한 최신 정보는 [Azure의 가상 컴퓨터 크기](http://msdn.microsoft.com/library/azure/dn197896.aspx)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-138">For most up-to-date information on available virtual machine sizes and the number of data disks that you can attach to a virtual machine, see [Virtual Machine Sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="9b8c3-139">가격 책정 정보는 [가상 컴퓨터 가격 책정](https://azure.microsoft.com/pricing/details/virtual-machines/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-139">For pricing information, see [VIrtual Macines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
     > 
     > 
   
   <span data-ttu-id="9b8c3-140">오른쪽 아래에 있는 다음 화살표를 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-140">Click the next arrow on the bottom right to continue.</span></span>
   
   ![VM 구성][2]
5. <span data-ttu-id="9b8c3-142">두 번째 **가상 컴퓨터 구성** 페이지에서 네트워킹, 저장소 및 가용성에 대한 리소스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-142">On the second **Virtual machine configuration** page, configure resources for networking, storage, and availability:</span></span>
   
   * <span data-ttu-id="9b8c3-143">**클라우드 서비스** 상자에서 **새 클라우드 서비스 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-143">In the **Cloud Service** box, choose **Create a new cloud service**.</span></span>
   * <span data-ttu-id="9b8c3-144">**클라우드 서비스 DNS 이름** 상자에 **TESTNAME.cloudapp.net** 형식으로 이름이 완성되도록 선택한 DNS 이름의 첫 번째 부분을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-144">In the **Cloud Service DNS Name** box, provide the first portion of a DNS name of your choice, so that it completes a name in the format **TESTNAME.cloudapp.net**</span></span>
   * <span data-ttu-id="9b8c3-145">**지역/선호도 그룹/가상 네트워크** 상자에서 이 가상 이미지를 호스트할 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-145">In the **REGION/AFFINITY GROUP/VIRTUAL NETWORK** box, select a region where this virtual image will be hosted.</span></span>
   * <span data-ttu-id="9b8c3-146">**저장소 계정**에서 기존 저장소 계정 또는 자동으로 생성된 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-146">In the **Storage Account**, select an existing storage account or select an automatically generated one.</span></span>
   * <span data-ttu-id="9b8c3-147">**가용성 집합** 상자에서 **(없음)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-147">In the **AVAILABILITY SET** box, select **(none)**.</span></span>
   * <span data-ttu-id="9b8c3-148">가격 정보를 읽고 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-148">Read and accept the pricing information.</span></span>
6. <span data-ttu-id="9b8c3-149">**끝점** 섹션에서 **이름** 아래에 있는 빈 드롭다운을 클릭하고 **MSSQL**을 선택한 다음 데이터베이스 엔진 인스턴스의 포트 번호(기본 인스턴스의 경우 **1433**)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-149">In the **ENDPOINTS** section, click in the empty dropdown under **NAME**, and select **MSSQL**  then type the port number of the instance of the Database Engine (**1433** for the default instance).</span></span>
7. <span data-ttu-id="9b8c3-150">SQL Server VM을 IPython Notebook 서버로 사용할 수도 있습니다. 이는 이후 단계에서 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-150">Your SQL Server VM can also serve as an IPython Notebook Server, which will be configured in a later step.</span></span>
   <span data-ttu-id="9b8c3-151">새 끝점을 추가하여 IPython Notebook 서버에 사용할 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-151">Add a new endpoint to specify the port to use for your IPython Notebook server.</span></span> <span data-ttu-id="9b8c3-152">**이름** 열에 이름을 입력하고 공용 포트에 대해 원하는 포트 번호를 선택하고 개인 포트에 대해 9999를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-152">Enter a name in the **NAME** column,    select a port number of your choice for the public port, and 9999 for the private port.</span></span>
   
   <span data-ttu-id="9b8c3-153">오른쪽 아래에 있는 다음 화살표를 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-153">Click the next arrow on the bottom right to continue.</span></span>
   
   ![MSSQL 및 IPython 포트 선택][3]
8. <span data-ttu-id="9b8c3-155">기본 **VM 에이전트 설치** 옵션을 선택된 채로 두고 마법사의 오른쪽 아래에 있는 확인 표시를 클릭하여 VM 프로비저닝 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-155">Accept the default **Install VM agent** option checked and click the the check mark in the bottom right corner of the wizard to complete the VM provisioning process.</span></span>
   
   `![VM 최종 옵션][4]
9. <span data-ttu-id="9b8c3-157">Azure에서 가상 컴퓨터를 준비하는 동안 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-157">Wait while Azure prepares your virtual machine.</span></span> <span data-ttu-id="9b8c3-158">다음을 통해 진행할 가상 컴퓨터 상태를 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-158">Expect the virtual machine status to proceed through:</span></span>
   
   * <span data-ttu-id="9b8c3-159">시작 중(프로비전 중)</span><span class="sxs-lookup"><span data-stu-id="9b8c3-159">Starting (Provisioning)</span></span>
   * <span data-ttu-id="9b8c3-160">중지됨</span><span class="sxs-lookup"><span data-stu-id="9b8c3-160">Stopped</span></span>
   * <span data-ttu-id="9b8c3-161">시작 중(프로비전 중)</span><span class="sxs-lookup"><span data-stu-id="9b8c3-161">Starting (Provisioning)</span></span>
   * <span data-ttu-id="9b8c3-162">실행 중(프로비전 중)</span><span class="sxs-lookup"><span data-stu-id="9b8c3-162">Running (Provisioning)</span></span>
   * <span data-ttu-id="9b8c3-163">실행 중</span><span class="sxs-lookup"><span data-stu-id="9b8c3-163">Running</span></span>

## <span data-ttu-id="9b8c3-164"><a name="RemoteDesktop"></a>원격 데스크톱을 사용하여 가상 컴퓨터 열기 및 설치 완료</span><span class="sxs-lookup"><span data-stu-id="9b8c3-164"><a name="RemoteDesktop"></a>Open the virtual machine using Remote Desktop and complete setup</span></span>
1. <span data-ttu-id="9b8c3-165">프로비전이 완료되면 가상 컴퓨터의 이름을 클릭하여 대시보드 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-165">When provisioning completes, click on the name of your virtual machine to go to the DASHBOARD page.</span></span> <span data-ttu-id="9b8c3-166">페이지 맨 아래에 있는 **Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-166">At the bottom of the page, click **Connect**.</span></span>
2. <span data-ttu-id="9b8c3-167">Windows 원격 데스크톱 프로그램(`%windir%\system32\mstsc.exe`)을 사용하여 rpd 파일을 열도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-167">Choose to open the rpd file using the Windows Remote Desktop program (`%windir%\system32\mstsc.exe`).</span></span>
3. <span data-ttu-id="9b8c3-168">**Windows 보안** 대화 상자에서, 이전 단계에서 지정한 로컬 관리자 계정의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-168">At the **Windows Security** dialog box, provide the password for the local administrator account that you specified in an earlier step.</span></span>
   <span data-ttu-id="9b8c3-169">가상 컴퓨터의 자격 증명을 확인하도록 요청될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-169">(You might be asked to verify the credentials of the virtual machine.)</span></span>
4. <span data-ttu-id="9b8c3-170">이 가상 컴퓨터에 처음 로그온하는 경우 데스크톱 설정, Windows 업데이트 및 Windows 초기 구성 작업(sysprep) 완료를 포함하여 여러 프로세스를 완료해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-170">The first time you log on to this virtual machine, several processes may need to complete, including setup of your desktop, Windows updates, and completion of the Windows initial configuration tasks (sysprep).</span></span> <span data-ttu-id="9b8c3-171">Windows sysprep가 완료되면 SQL Server 설치 프로세스에서 구성 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-171">After Windows sysprep completes, SQL Server setup completes configuration tasks.</span></span> <span data-ttu-id="9b8c3-172">이러한 작업으로 인해 완료되는 동안 잠시 지연이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-172">These tasks may cause a delay of a few minutes while they complete.</span></span> <span data-ttu-id="9b8c3-173">`SELECT @@SERVERNAME` 에서 올바른 이름을 반환하지 못할 수 있으며, SQL Server Management Studio가 시작 페이지에 표시되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-173">`SELECT @@SERVERNAME` may not return the correct name until SQL Server setup completes, and SQL Server Management Studio may not be visable on the start page.</span></span>

<span data-ttu-id="9b8c3-174">Windows 원격 데스크톱을 사용하여 가상 컴퓨터에 연결된 후 가상 컴퓨터는 다른 컴퓨터와 상당히 유사하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-174">Once you are connected to the virtual machine with Windows Remote Desktop, the virtual machine works much like any other computer.</span></span> <span data-ttu-id="9b8c3-175">SQL Server Management Studio(가상 컴퓨터에서 실행 중인)가 설치되어 있는 기본 SQL Server 인스턴스에 일반적인 방식으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-175">Connect to the default instance of SQL Server with SQL Server Management Studio (running on the virtual machine) in the normal way.</span></span>

## <span data-ttu-id="9b8c3-176"><a name="InstallIPython"></a>IPython Notebook 및 기타 지원 도구 설치</span><span class="sxs-lookup"><span data-stu-id="9b8c3-176"><a name="InstallIPython"></a>Install IPython Notebook and other supporting tools</span></span>
<span data-ttu-id="9b8c3-177">IPython Notebook 서버 역할을 하도록 새 SQL Server VM을 구성하고 AzCopy, Azure 저장소 탐색기, 유용한 데이터 과학 Python 패키지 등의 추가 지원 도구를 설치할 수 있도록 특별한 사용자 지정 스크립트가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-177">To configure your new SQL Server VM to serve as an IPython Notebook server, and install additional supporting tools such AzCopy, Azure Storage Explorer, useful Data Science Python packages, and others, a special customization script is provided to you.</span></span> <span data-ttu-id="9b8c3-178">설치하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-178">To install:</span></span>

1. <span data-ttu-id="9b8c3-179">**Windows 시작** 아이콘을 마우스 오른쪽 단추로 클릭하고 **명령 프롬프트(관리자)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-179">Right-click the **Windows Start** icon and click **Command Prompt (Admin)**</span></span>
2. <span data-ttu-id="9b8c3-180">다음 명령을 복사하여 명령 프롬프트에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-180">Copy the following commands and paste at the command prompt.</span></span>
  
        set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"
3. <span data-ttu-id="9b8c3-181">메시지가 표시되면 IPython Notebook 서버에 대한 원하는 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-181">When prompted, enter a password of your choice for the IPython Notebook server.</span></span>
4. <span data-ttu-id="9b8c3-182">사용자 지정 스크립트는 다음과 같은 여러 설치 후 절차를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-182">The customization script automates several post-install procedures, which include:</span></span>
    * <span data-ttu-id="9b8c3-183">IPython Notebook 서버 설치 및 설정</span><span class="sxs-lookup"><span data-stu-id="9b8c3-183">Installation and setup of IPython Notebook server</span></span>
    * <span data-ttu-id="9b8c3-184">이전에 만든 끝점에 대해 Windows 방화벽에서 TCP 포트 열기</span><span class="sxs-lookup"><span data-stu-id="9b8c3-184">Opening TCP ports in the Windows firewall for the endpoints created earlier:</span></span>
    * <span data-ttu-id="9b8c3-185">SQL Server 원격 연결</span><span class="sxs-lookup"><span data-stu-id="9b8c3-185">For SQL Server remote connectivity</span></span>
    * <span data-ttu-id="9b8c3-186">IPython Notebook 서버 원격 연결</span><span class="sxs-lookup"><span data-stu-id="9b8c3-186">For IPython Notebook server remote connectivity</span></span>
    * <span data-ttu-id="9b8c3-187">샘플 IPython Notebook 및 SQL 스크립트 가져오기</span><span class="sxs-lookup"><span data-stu-id="9b8c3-187">Fetching sample IPython notebooks and SQL scripts</span></span>
    * <span data-ttu-id="9b8c3-188">유용한 데이터 과학 Python 패키지 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="9b8c3-188">Downloading and installing useful Data Science Python packages</span></span>
    * <span data-ttu-id="9b8c3-189">AzCopy 및 Azure 저장소 탐색기 와 같은 Azure 도구 다운로드 및 설치 </span><span class="sxs-lookup"><span data-stu-id="9b8c3-189">Downloading and installing Azure tools such as AzCopy and Azure Storage Explorer</span></span>  
    <br>
5. <span data-ttu-id="9b8c3-190">모든 로컬 또는 원격 브라우저에서(여기서 port는 가상 컴퓨터를 프로비전하는 동안 선택한 IPython 공용 포트) `https://<virtual_machine_DNS_name>:<port>`형식의 URL을 사용하여 IPython Notebook에 액세스하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-190">You may access and run IPython Notebook from any local or remote browser using a URL of the form `https://<virtual_machine_DNS_name>:<port>`, where port is the IPython public port you selected while provisioning the virtual machine.</span></span>
6. <span data-ttu-id="9b8c3-191">IPython Notebook 서버는 백그라운드 서비스로 실행되며, 가상 컴퓨터를 다시 시작하면 자동으로 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-191">IPython Notebook server is running as a background service and will be restarted automatically when you restart the virtual machine.</span></span>

## <span data-ttu-id="9b8c3-192"><a name="Optional"></a>필요에 따라 데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="9b8c3-192"><a name="Optional"></a>Attach data disk as needed</span></span>
<span data-ttu-id="9b8c3-193">VM 이미지에 데이터 디스크, 즉 C 드라이브(OS 디스크) 및 D 드라이브(임시 디스크) 이외의 디스크가 포함되지 않은 경우 데이터를 저장할 데이터 디스크를 하나 이상 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-193">If your VM image does not include data disks, i.e., disks other than C drive (OS disk) and D drive (temporary disk), you need to add one or more data disks to store your data.</span></span> <span data-ttu-id="9b8c3-194">SQL Server 2012 SP2 Enterprise Optimized for DataWarehousing Workloads용 VM 이미지는 SQL Server 데이터 및 로그 파일용 추가 디스크로 미리 구성된 상태로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-194">The VM image for SQL Server 2012 SP2 Enterprise Optimized for DataWarehousing Workloads comes pre-configured with additional disks for SQL Server data and log files.</span></span>

> [!NOTE]
> <span data-ttu-id="9b8c3-195">D 드라이브는 데이터 저장에 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-195">Do not use the D drive to store data.</span></span> <span data-ttu-id="9b8c3-196">이름이 의미하는 것과 같이 D 드라이브는 임시 저장소만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-196">As the name implies, it provides temporary storage only.</span></span> <span data-ttu-id="9b8c3-197">Azure 저장소에 상주하지 않으므로 중복성이나 백업을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-197">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> 
> 

<span data-ttu-id="9b8c3-198">추가 데이터 디스크를 연결하려면 다음 과정을 안내하는 [Windows 가상 컴퓨터에 데이터 디스크를 연결하는 방법](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)에 설명된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-198">To attach additional data disks, follow the steps described in [How to Attach a Data Disk to a Windows Virtual Machine](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), which will guide you through:</span></span>

1. <span data-ttu-id="9b8c3-199">이전 단계에서 프로비전한 가상 컴퓨터에 빈 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="9b8c3-199">Attaching empty disk(s) to the virtual machine provisioned in earlier steps</span></span>
2. <span data-ttu-id="9b8c3-200">가상 컴퓨터에서 새 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="9b8c3-200">Initialization of the new disk(s) in the virtual machine</span></span>

## <span data-ttu-id="9b8c3-201"><a name="SSMS"></a>SQL Server Management Studio에 연결하여 혼합 모드 인증 설정</span><span class="sxs-lookup"><span data-stu-id="9b8c3-201"><a name="SSMS"></a>Connect to SQL Server Management Studio and enable mixed mode authentication</span></span>
<span data-ttu-id="9b8c3-202">SQL Server 데이터베이스 엔진은 도메인 환경에서만 Windows 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-202">The SQL Server Database Engine cannot use Windows Authentication without domain environment.</span></span> <span data-ttu-id="9b8c3-203">다른 컴퓨터에서 데이터베이스 엔진에 연결하려면 혼합 모드 인증을 위해 SQL Server를 구성하십시오.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-203">To connect to the Database Engine from another computer, configure SQL Server for mixed mode authentication.</span></span> <span data-ttu-id="9b8c3-204">혼합 모드 인증은 SQL Server 인증과 Windows 인증을 모두 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-204">Mixed mode authentication allows both SQL Server Authentication and Windows Authentication.</span></span> <span data-ttu-id="9b8c3-205">SQL 인증 모드는 데이터 가져오기 모듈을 사용하여 [Azure 기계 학습 스튜디오](https://studio.azureml.net) 의 SQL Server VM 데이터베이스에서 직접 데이터를 수집하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-205">SQL authentication mode is required in order to ingest data directly from your SQL Server VM databases in the [Azure Machine Learning Studio](https://studio.azureml.net) using the Import Data module.</span></span>

1. <span data-ttu-id="9b8c3-206">원격 데스크톱을 사용하여 가상 컴퓨터에 연결되어 있는 동안 Windows **검색** 창에 SMSS(**SQL Server Management Studio**)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-206">While connected to the virtual machine by using Remote Desktop, use the Windows **Search** pane and type **SQL Server Management Studio** (SMSS).</span></span> <span data-ttu-id="9b8c3-207">SSMS(SQL Server Management Studio)를 클릭하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-207">Click to start the SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="9b8c3-208">나중에 사용하기 위해 바탕 화면에 SSMS의 바로 가기를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-208">You may want to add a shortcut to SSMS on your Desktop for future use.</span></span>
   
   ![SSMS 시작][5]
   
   <span data-ttu-id="9b8c3-210">처음으로 Management Studio를 열 때 사용자 Management Studio 환경이 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-210">The first time you open Management Studio it must create the users Management Studio environment.</span></span> <span data-ttu-id="9b8c3-211">어느 정도 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-211">This may take a few moments.</span></span>
2. <span data-ttu-id="9b8c3-212">Management Studio를 열면 **서버에 연결** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-212">When opening, Management Studio presents the **Connect to Server** dialog box.</span></span> <span data-ttu-id="9b8c3-213">**서버 이름** 상자에, 개체 탐색기를 사용하여 데이터베이스 엔진에 연결할 가상 컴퓨터의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-213">In the **Server name** box, type the name of the virtual machine to connect to the Database Engine with the Object Explorer.</span></span>
   <span data-ttu-id="9b8c3-214">가상 컴퓨터 이름 대신 **(로컬)** 또는 단일 기간을 **서버 이름**으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-214">(Instead of the virtual machine name you can also use **(local)** or a single period as the **Server name**.</span></span> <span data-ttu-id="9b8c3-215">**Windows 인증**을 선택하고, **사용자 이름** 상자의 ***your\_VM\_name*\\your\_local\_administrator**를 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-215">Select **Windows Authentication**, and leave ***your\_VM\_name*\\your\_local\_administrator** in the **User name** box.</span></span> <span data-ttu-id="9b8c3-216">**연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-216">Click **Connect**.</span></span>
   
   ![서버에 연결][6]
   
   <br>
   
   > [!TIP]
   > <span data-ttu-id="9b8c3-218">Windows 레지스트리 키 변경 또는 SQL Server Management Studio를 사용하여 SQL Server 인증 모드를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-218">You may change the SQL Server authentication mode using a Windows registry key change or using the SQL Server Management Studio.</span></span> <span data-ttu-id="9b8c3-219">Windows 레지스트리 키 변경을 사용하여 인증 모드를 변경하려면 **새 쿼리** 를 시작하고 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-219">To change authentication mode using the registry key change, start a **New Query** and execute the following script:</span></span>
   > 
   > 
   
       USE master
       go
   
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
       go

    <span data-ttu-id="9b8c3-220">SQL Server Management Studio를 사용하여 인증 모드를 변경하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-220">To change the authentication mode using SQL Server management Studio:</span></span>

1. <span data-ttu-id="9b8c3-221">**SQL Server Management Studio 개체 탐색기**에서 SQL Server 인스턴스의 이름(가상 컴퓨터 이름)을 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-221">In **SQL Server Management Studio Object Explorer**, right-click the name of the instance of SQL Server (the virtual machine name), and then click **Properties**.</span></span>
   
   ![서버 속성][7]
2. <span data-ttu-id="9b8c3-223">**보안** 페이지의 **서버 인증**에서 **SQL Server 및 Windows 인증 모드**를 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-223">On the **Security** page, under **Server authentication**, select **SQL Server and Windows Authentication mode**, and then click **OK**.</span></span>
   
   ![인증 모드 선택][8]
3. <span data-ttu-id="9b8c3-225">**SQL Server Management Studio** 대화 상자에서 **확인**을 클릭하여 SQL Server를 다시 시작해야 하는 요구 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-225">In the **SQL Server Management Studio** dialog box, click **OK** to acknowledge the requirement to restart SQL Server.</span></span>
4. <span data-ttu-id="9b8c3-226">**개체 탐색기**에서 서버를 마우스 오른쪽 단추로 클릭한 후 **다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-226">In **Object Explorer**, right-click your server, and then click **Restart**.</span></span> <span data-ttu-id="9b8c3-227">SQL Server 에이전트가 실행 중인 경우 에이전트도 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-227">(If SQL Server Agent is running, it must also be restarted.)</span></span>
   
   ![다시 시작][9]
5. <span data-ttu-id="9b8c3-229">**SQL Server Management Studio** 대화 상자에서 **예**를 클릭하여 SQL Server를 다시 시작한다는 데 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-229">In the **SQL Server Management Studio** dialog box, click **Yes** to agree that you want to restart SQL Server.</span></span>

## <span data-ttu-id="9b8c3-230"><a name="Logins"></a>SQL Server 인증 로그인 만들기</span><span class="sxs-lookup"><span data-stu-id="9b8c3-230"><a name="Logins"></a>Create SQL Server authentication logins</span></span>
<span data-ttu-id="9b8c3-231">다른 컴퓨터에서 데이터베이스 엔진에 연결하려면 SQL Server 인증 로그인을 하나 이상 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-231">To connect to the Database Engine from another computer, you must create at least one SQL Server authentication login.</span></span>  

<span data-ttu-id="9b8c3-232">SQL Server Management Studio를 사용하거나 프로그래밍 방식으로 새 SQL Server 로그인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-232">You may create new SQL Server logins programmatically or using the SQL Server Management Studio.</span></span> <span data-ttu-id="9b8c3-233">SQL 인증을 사용하는 새 sysadmin 사용자를 프로그래밍 방식으로 만들려면 **새 쿼리** 를 시작하고 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-233">To create a new sysadmin user with SQL authentication programmatically, start a **New Query** and execute the following script.</span></span> <span data-ttu-id="9b8c3-234"><새 사용자 이름\> 및 <새 암호\>를 원하는 *사용자 이름* 및 *암호*로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-234">Replace <new user name\> and <new password\> with your choice of *user name* and *password*.</span></span> 

    USE master
    go

    CREATE LOGIN <new user name> WITH PASSWORD = N'<new password>',
        CHECK_POLICY = OFF,
        CHECK_EXPIRATION = OFF;

    EXEC sp_addsrvrolemember @loginame = N'<new user name>', @rolename = N'sysadmin';


<span data-ttu-id="9b8c3-235">필요에 따라 암호 정책을 조정합니다(샘플 코드에서는 정책 확인 및 암호 만료를 해제함).</span><span class="sxs-lookup"><span data-stu-id="9b8c3-235">Adjust the password policy as needed (the sample code turns off policy checking and password expiration).</span></span> <span data-ttu-id="9b8c3-236">SQL Server 로그인에 대한 자세한 내용은 [로그인 만들기](http://msdn.microsoft.com/library/aa337562.aspx)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-236">For more information about SQL Server logins, see [Create a Login](http://msdn.microsoft.com/library/aa337562.aspx).</span></span>  

<span data-ttu-id="9b8c3-237">SQL Server Management Studio를 사용하여 새 SQL Server 로그인을 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-237">To create new SQL Server logins using the SQL Server Management Studio:</span></span>

1. <span data-ttu-id="9b8c3-238">**SQL Server Management Studio 개체 탐색기**에서 새 로그인을 만들 서버 인스턴스의 폴더를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-238">In **SQL Server Management Studio Object Explorer**, expand the folder of the server instance in which you want to create the new login.</span></span>
2. <span data-ttu-id="9b8c3-239">**보안** 폴더를 마우스 오른쪽 단추로 클릭하고, **새로 만들기**를 가리키고 **로그인...**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-239">Right-click the **Security** folder, point to **New**, and select **Login…**.</span></span>
   
   ![새 로그인][10]
3. <span data-ttu-id="9b8c3-241">**로그인 - 신규** 대화 상자의 **일반** 페이지에 있는 **로그인 이름** 상자에 새 사용자의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-241">In the **Login - New** dialog box, on the **General** page, enter the name of the new user in the **Login name** box.</span></span>
4. <span data-ttu-id="9b8c3-242">**SQL Server 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-242">Select **SQL Server authentication**.</span></span>
5. <span data-ttu-id="9b8c3-243">**암호** 상자에 새 사용자의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-243">In the **Password** box, enter a password for the new user.</span></span> <span data-ttu-id="9b8c3-244">**암호 확인** 상자에 암호를 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-244">Enter that password again into the **Confirm Password** box.</span></span>
6. <span data-ttu-id="9b8c3-245">복잡성 및 강제성에 대한 암호 정책 옵션을 적용하려면 **암호 정책 강제 적용** (권장)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-245">To enforce password policy options for complexity and enforcement, select **Enforce password policy** (recommended).</span></span> <span data-ttu-id="9b8c3-246">SQL Server 인증을 선택할 경우 이 항목은 기본 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-246">This is a default option when SQL Server authentication is selected.</span></span>
7. <span data-ttu-id="9b8c3-247">만료에 대한 암호 정책 옵션을 적용하려면 **암호 만료 강제 적용** (권장)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-247">To enforce password policy options for expiration, select **Enforce password expiration** (recommended).</span></span> <span data-ttu-id="9b8c3-248">이 확인란을 사용하려면 먼저 암호 정책 강제 적용을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-248">Enforce password policy must be selected to enable this checkbox.</span></span> <span data-ttu-id="9b8c3-249">SQL Server 인증을 선택할 경우 이 항목은 기본 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-249">This is a default option when SQL Server authentication is selected.</span></span>
8. <span data-ttu-id="9b8c3-250">처음으로 로그인을 사용한 후 사용자가 새 암호를 만들도록 강제하려면 **다음 로그인할 때 반드시 암호 변경**을 선택합니다. 다른 사용자가 이 로그인을 사용할 경우에 이 옵션을 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-250">To force the user to create a new password after the first time the login is used, select **User must change password at next login** (Recommended if this login is for someone else to use.</span></span> <span data-ttu-id="9b8c3-251">사용자만 이 로그인을 사용하는 경우에는 이 옵션을 선택하지 마십시오. 이 확인란을 사용하려면 먼저 암호 만료 강제 적용을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-251">If the login is for your own use, do not select this option.) Enforce password expiration must be selected to enable this checkbox.</span></span> <span data-ttu-id="9b8c3-252">SQL Server 인증을 선택할 경우 이 항목은 기본 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-252">This is a default option when SQL Server authentication is selected.</span></span>
9. <span data-ttu-id="9b8c3-253">**기본 데이터베이스** 목록에서 로그인의 기본 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-253">From the **Default database** list, select a default database for the login.</span></span> <span data-ttu-id="9b8c3-254">**master** 가 이 옵션의 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-254">**master** is the default for this option.</span></span> <span data-ttu-id="9b8c3-255">사용자 데이터베이스를 아직 만들지 않은 경우 **master**로 설정된 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-255">If you have not yet created a user database, leave this set to **master**.</span></span>
10. <span data-ttu-id="9b8c3-256">**기본 언어** 목록에서 **기본값**을 선택 값으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-256">In the **Default language** list, leave **default** as the value.</span></span>
    
    ![로그인 속성][11]
11. <span data-ttu-id="9b8c3-258">처음 로그인을 만드는 경우 이 로그인을 SQL Server 관리자로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-258">If this is the first login you are creating, you may want to designate this login as a SQL Server administrator.</span></span> <span data-ttu-id="9b8c3-259">그렇게 하는 경우 **서버 역할** 페이지에서 **sysadmin**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-259">If so, on the **Server Roles** page, check **sysadmin**.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="9b8c3-260">sysadmin 고정 서버 역할의 구성원은 데이터베이스 엔진을 완전히 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-260">Members of the sysadmin fixed server role have complete control of the Database Engine.</span></span> <span data-ttu-id="9b8c3-261">보안상의 이유로 이 역할의 구성원은 신중하게 제한해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-261">For security reasons, you should carefully restrict membership in this role.</span></span>
    > 
    > 
    
    ![sysadmin][12]
12. <span data-ttu-id="9b8c3-263">확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-263">Click OK.</span></span>

## <span data-ttu-id="9b8c3-264"><a name="DNS"></a>가상 컴퓨터의 DNS 이름 확인</span><span class="sxs-lookup"><span data-stu-id="9b8c3-264"><a name="DNS"></a>Determine the DNS name of the virtual machine</span></span>
<span data-ttu-id="9b8c3-265">다른 컴퓨터에서 SQL Server 데이터베이스 엔진에 연결하려면 가상 컴퓨터의 DNS(Domain Name System) 이름을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-265">To connect to the SQL Server Database Engine from another computer, you must know the Domain Name System (DNS) name of the virtual machine.</span></span>

<span data-ttu-id="9b8c3-266">이 이름은 인터넷에서 가상 컴퓨터를 식별하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-266">(This is the name the internet uses to identify the virtual machine.</span></span> <span data-ttu-id="9b8c3-267">IP 주소를 사용할 수 있지만 Azure가 중복 또는 유지 관리를 위해 리소스를 이동할 경우 IP 주소가 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-267">You can use the IP address, but the IP address might change when Azure moves resources for redundancy or maintenance.</span></span> <span data-ttu-id="9b8c3-268">DNS 이름은 새 IP 주소로 리디렉션할 수 있으므로 안정적입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-268">The DNS name will be stable because it can be redirected to a new IP address.)</span></span>

1. <span data-ttu-id="9b8c3-269">Azure 클래식 포털(또는 이전 단계)에서 **가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-269">In the Azure Classic Portal (or from the previous step), select **VIRTUAL MACHINES**.</span></span>
2. <span data-ttu-id="9b8c3-270">**가상 컴퓨터 인스턴스** 페이지의 **DNS 이름** 열에서, **http://**로 시작하는 가상 컴퓨터의 DNS 이름을 찾아서 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-270">On the **VIRTUAL MACHINE INSTANCES** page, in the **DNS NAME** column, find and copy the DNS name for the virtual machine which appears preceded by **http://**.</span></span> <span data-ttu-id="9b8c3-271">사용자 인터페이스에 전체 이름이 표시되지 않을 수도 있지만 이름을 마우스 오른쪽 단추로 클릭하고 복사를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-271">(The user interface might not display the entire name, but you can right-click on it, and select copy.)</span></span>

## <span data-ttu-id="9b8c3-272"><a name="cde"></a>다른 컴퓨터에서 데이터베이스 엔진에 연결</span><span class="sxs-lookup"><span data-stu-id="9b8c3-272"><a name="cde"></a>Connect to the Database Engine from another computer</span></span>
1. <span data-ttu-id="9b8c3-273">인터넷에 연결된 컴퓨터에서 SQL Server Management Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-273">On a computer connected to the internet, open SQL Server Management Studio.</span></span>
2. <span data-ttu-id="9b8c3-274">**서버에 연결** 또는 **데이터베이스 엔진에 연결** 대화 상자의 **서버 이름** 상자에 가상 컴퓨터의 DNS 이름(이전 작업에서 확인된 이름) 및 공개 끝점 포트 번호를 *DNS이름,포트번호* 형식(예: **tutorialtestVM.cloudapp.net,57500**)으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-274">In the **Connect to Server** or **Connect to Database Engine** dialog box, in the **Server name** box, enter the DNS name of the virtual machine (determined in the previous task) and a public endpoint port number in the format of *DNSName,portnumber* such as **tutorialtestVM.cloudapp.net,57500**.</span></span>
3. <span data-ttu-id="9b8c3-275">**인증** 상자에 **SQL Server 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-275">In the **Authentication** box, select **SQL Server Authentication**.</span></span>
4. <span data-ttu-id="9b8c3-276">**로그인** 상자에, 이전 작업에서 만든 로그인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-276">In the **Login** box, type the name of a login that you created in an earlier task.</span></span>
5. <span data-ttu-id="9b8c3-277">**암호** 상자에, 이전 작업에서 만든 로그인의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-277">In the **Password** box, type the password of the login that you create in an earlier task.</span></span>
6. <span data-ttu-id="9b8c3-278">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-278">Click **Connect**.</span></span>

## <span data-ttu-id="9b8c3-279"><a name="amlconnect"></a>Azure 기계 학습에서 데이터베이스 엔진에 연결</span><span class="sxs-lookup"><span data-stu-id="9b8c3-279"><a name="amlconnect"></a>Connect to the Database Engine from Azure Machine Learning</span></span>
<span data-ttu-id="9b8c3-280">팀 데이터 과학 프로세스의 이후 단계에서는 [Azure 기계 학습 스튜디오](https://studio.azureml.net) 를 사용하여 기계 학습 모델을 빌드 및 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-280">In later stages of the Team Data Science Process, you will use the [Azure Machine Learning Studio](https://studio.azureml.net) to build and deploy machine learning models.</span></span> <span data-ttu-id="9b8c3-281">학습 또는 점수 매기기를 위해 SQL Server VM 데이터베이스에서 직접 Azure 기계 학습으로 데이터를 수집하려면 새 **Azure 기계 학습 스튜디오** 실험에서 [데이터 가져오기](https://studio.azureml.net) 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-281">To ingest data from your SQL Server VM databases directly into Azure Machine Learning for training or scoring, use the **Import Data** module in a new [Azure Machine Learning Studio](https://studio.azureml.net) experiment.</span></span> <span data-ttu-id="9b8c3-282">이 토픽은 팀 데이터 과학 프로세스 가이드 링크를 통해 보다 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-282">This topic is covered in more details through the Team Data Science Process guide links.</span></span> <span data-ttu-id="9b8c3-283">지침은 [Azure 기계 학습 스튜디오란?](machine-learning-what-is-ml-studio.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-283">For an introduction, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md).</span></span>

1. <span data-ttu-id="9b8c3-284">[데이터 가져오기 모듈](https://msdn.microsoft.com/library/azure/dn905997.aspx)의 **속성** 창에 있는 **데이터 원본** 드롭다운 목록에서 **Azure SQL Database**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-284">In the **Properties** pane of the [Import Data module](https://msdn.microsoft.com/library/azure/dn905997.aspx), select **Azure SQL Database** from the **Data Source**     dropdown list.</span></span>
2. <span data-ttu-id="9b8c3-285">**데이터베이스 서버 이름** 텍스트 상자에 `tcp:<DNS name of your virtual machine>,1433`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-285">In the **Database server name** text box, enter `tcp:<DNS name of your virtual machine>,1433`</span></span>
3. <span data-ttu-id="9b8c3-286">**서버 사용자 계정 이름** 텍스트 상자에 SQL 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-286">Enter the SQL user name in the **Server user account name** text box.</span></span>
4. <span data-ttu-id="9b8c3-287">**서버 사용자 계정 암호** 텍스트 상자에 SQL 사용자의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-287">Enter the sql user's password in the **Server user account password** text box.</span></span>
   
   ![Azure 기계 학습 데이터 가져오기][13]

## <span data-ttu-id="9b8c3-289"><a name="shutdown"></a>사용하지 않을 때 가상 컴퓨터 종료 및 할당 해제</span><span class="sxs-lookup"><span data-stu-id="9b8c3-289"><a name="shutdown"></a>Shutdown and deallocate virtual machine when not in use</span></span>
<span data-ttu-id="9b8c3-290">Azure 가상 컴퓨터는 **종량제**로 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-290">Azure Virtual Machines are priced as **pay only for what you use**.</span></span> <span data-ttu-id="9b8c3-291">가상 컴퓨터를 사용하지 않을 때 비용이 청구되지 않도록 하려면 **중지(할당 해제)** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-291">To ensure that you are not being billed when not using your virtual machine, it has to be in the **Stopped (Deallocated)** state.</span></span>

> [!NOTE]
> <span data-ttu-id="9b8c3-292">Windows 전원 옵션을 사용하여 내부에서 가상 컴퓨터를 종료하면 VM이 중지되지만 여전히 할당된 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-292">Shutting down the virtual machine from inside (using Windows power options), the VM is stopped but remains allocated.</span></span> <span data-ttu-id="9b8c3-293">비용이 청구되지 않도록 하려면 항상 [Azure 클래식 포털](http://manage.windowsazure.com/)에서 가상 컴퓨터를 중지하세요.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-293">To ensure you’re not being billed, always stop virtual machines from the [Azure Classic Portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="9b8c3-294">"PostShutdownAction"이 "StoppedDeallocated"와 동일한 ShutdownRoleOperation을 호출하여 Powershell을 통해 VM을 중지할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-294">You can also stop the VM through Powershell by calling ShutdownRoleOperation with "PostShutdownAction" equal to "StoppedDeallocated".</span></span>
> 
> 

<span data-ttu-id="9b8c3-295">가상 컴퓨터를 종료하고 할당을 해제하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-295">To shutdown and deallocate the virtual machine:</span></span>

1. <span data-ttu-id="9b8c3-296">사용자 계정을 사용하여 [Azure 클래식 포털](http://manage.windowsazure.com/) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-296">Log in to the [Azure Classic Portal](http://manage.windowsazure.com/) using your account.</span></span>  
2. <span data-ttu-id="9b8c3-297">왼쪽 탐색 모음에서 **가상 컴퓨터** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-297">Select **VIRTUAL MACHINES** from the left navigation bar.</span></span>
3. <span data-ttu-id="9b8c3-298">가상 컴퓨터 목록에서 가상 컴퓨터의 이름을 클릭하여 **대시보드** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-298">In the list of virtual machines, click on the name of your virtual machine then go to the **DASHBOARD** page.</span></span>
4. <span data-ttu-id="9b8c3-299">페이지 아래쪽에서 **종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-299">At the bottom of the page, click **SHUTDOWN**.</span></span>

![VM 종료][15]

<span data-ttu-id="9b8c3-301">가상 컴퓨터가 할당 해제되지만 삭제되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-301">The virtual machine will be deallocated but not deleted.</span></span> <span data-ttu-id="9b8c3-302">Azure 클래식 포털에서 언제든지 가상 컴퓨터를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-302">You may restart your virtual machine at any time from the Azure Classic Portal.</span></span>

## <a name="your-azure-sql-server-vm-is-ready-to-use-whats-next"></a><span data-ttu-id="9b8c3-303">Azure SQL Server VM을 사용할 준비가 되었습니다. 다음 단계는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="9b8c3-303">Your Azure SQL Server VM is ready to use: what's next?</span></span>
<span data-ttu-id="9b8c3-304">이제 데이터 과학 연습에서 가상 컴퓨터를 사용할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-304">Your virtual machine is now ready to use in your data science exercises.</span></span> <span data-ttu-id="9b8c3-305">또한 데이터 탐색 및 처리, Azure 기계 학습 및 TDSP(팀 데이터 과학 프로세스)와 함께 수행할 다른 작업 등에 가상 컴퓨터를 IPython Notebook 서버로 사용할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-305">The virtual machine is also ready for use as an IPython Notebook server for the exploration and processing of data, and other tasks in conjunction with Azure Machine Learning and the Team Data Science Process (TDSP).</span></span>

<span data-ttu-id="9b8c3-306">데이터 과학 프로세스의 다음 단계는 [TDSP(팀 데이터 과학 프로세스)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) 에서 매핑되며, 데이터를 HDInsight로 이동한 후 Azure 기계 학습에서 데이터를 통해 학습할 준비를 수행하면서 데이터를 처리 및 샘플링하는 단계를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c3-306">The next steps in the data science process are mapped in the [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, process and sample it there in preparation for learning from the data with Azure Machine Learning.</span></span>

[1]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/selectsqlvmimg.png
[2]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/4vm-config.png
[3]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/sqlvmports.png
[4]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmpostopts.png
[5]:./media/machine-learning-data-science-setup-sql-server-virtual-machine/searchssms.png
[6]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/19connect-to-server.png
[7]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/20server-properties.png
[8]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/21mixed-mode.png
[9]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/22restart2.png
[10]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/23new-login.png
[11]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/24test-login.png
[12]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/25sysadmin.png
[13]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/amlreader.png
[15]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmshutdown.png

