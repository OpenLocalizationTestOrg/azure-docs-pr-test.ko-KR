---
title: "Azure에서 하이브리드 HPC Pack 클러스터 설정 | Microsoft Docs"
description: "Microsoft HPC Pack 및 Azure를 사용하여 소규모 하이브리드 HPC(고성능 컴퓨팅) 클러스터를 설정하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: f6dc9657e64160be1e68a7356863b53131e9b3c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="9c505-103">Microsoft HPC(고성능 컴퓨팅) Pack 및 주문형 Azure 계산 노드를 사용하여 하이브리드 HPC 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="9c505-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="9c505-104">Microsoft HPC Pack 2012 R2 및 Azure를 사용하여 소규모 하이브리드 HPC(고성능 컴퓨팅) 클러스터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-104">Use Microsoft HPC Pack 2012 R2 and Azure to set up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="9c505-105">이 문서에 표시된 클러스터는 온-프레미스 HPC Pack 헤드 노드와 Azure Cloud Service에서 주문형으로 배포되는 일부 계산 노드로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-105">The cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="9c505-106">그런 다음 하이브리드 클러스터에서 계산 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-106">You can then run compute jobs on the hybrid cluster.</span></span>

![하이브리드 HPC 클러스터][Overview] 

<span data-ttu-id="9c505-108">이 자습서에서는 Azure의 확장성 있는 주문형 리소스를 사용하여 계산이 많이 사용되는 응용 프로그램을 실행하는 방법을 보여 줍니다. 이 방법을 클러스터 “클라우드로 버스트”라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-108">This tutorial shows one approach, sometimes called cluster "burst to the cloud," to use scalable, on-demand Azure resources to run compute-intensive applications.</span></span>

<span data-ttu-id="9c505-109">이 자습서는 이전에 계산 클러스터나 HPC 팩을 사용한 경험이 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="9c505-110">데모를 위해 하이브리드 계산 클러스터를 신속하게 배포하도록 도와주는 역할만 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-110">It is intended only to help you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="9c505-111">하이브리드 HPC Pack 클러스터를 프로덕션 환경에 대규모로 배포하거나 HPC Pack 2016을 사용하는 단계 및 고려 사항은 [자세한 지침](http://go.microsoft.com/fwlink/p/?LinkID=200493)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c505-111">For considerations and steps to deploy a hybrid HPC Pack cluster at greater scale in a production environment, or to use HPC Pack 2016, see the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="9c505-112">Azure Virtual Machine의 자동화된 클러스터 배포를 포함한 HPC Pack을 사용한 다른 시나리오의 경우 [Azure에서 Microsoft HPC Pack을 사용하는 HPC 클러스터 옵션](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c505-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c505-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9c505-113">Prerequisites</span></span>
* <span data-ttu-id="9c505-114">**Azure 구독** - Azure 구독이 없는 경우 몇 분 만에 [무료 계정](https://azure.microsoft.com/free/) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="9c505-115">**Windows Server 2012 R2 또는 Windows Server 2012가 실행되는 온-프레미스 컴퓨터** - 이 컴퓨터는 HPC 클러스터의 헤드 노드로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as the head node of the HPC cluster.</span></span> <span data-ttu-id="9c505-116">Windows Server가 아직 실행되지 않는 경우 [평가판](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2)을 다운로드하고 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="9c505-117">Active Directory 도메인에 컴퓨터를 가입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-117">The computer must be joined to an Active Directory domain.</span></span> <span data-ttu-id="9c505-118">테스트를 위해, 헤드 노드 컴퓨터를 도메인 컨트롤러로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-118">For test purposes, you can configure the head node computer as a domain controller.</span></span> <span data-ttu-id="9c505-119">Active Directory Domain Services 서버 역할을 추가하고 헤드 노드 컴퓨터를 도메인 컨트롤러로 수준을 올리려면 Windows Server에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c505-119">To add the Active Directory Domain Services server role and promote the head node computer as a domain controller, see the documentation for Windows Server.</span></span>
  * <span data-ttu-id="9c505-120">HPC 팩을 지원하려면 운영 체제가 영어, 일본어 또는 중국어(간체) 언어 중 하나로 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-120">To support HPC Pack, the operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="9c505-121">중요 업데이트가 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="9c505-122">**HPC Pack 2012 R2** - 최신 버전의 평가판 설치 패키지를 [다운로드](http://go.microsoft.com/fwlink/p/?linkid=328024)하고 헤드 노드 컴퓨터에 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) the installation package for the latest version free of charge and copy the files to the head node computer.</span></span> <span data-ttu-id="9c505-123">Windows Server 설치와 동일한 언어의 설치 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-123">Choose installation files in the same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="9c505-124">HPC Pack 2012 R2 대신 HPC Pack 2016을 사용하려는 경우 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-124">If you want to use HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="9c505-125">[자세한 지침](http://go.microsoft.com/fwlink/p/?LinkID=200493)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c505-125">See the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="9c505-126">**도메인 계정** - HPC Pack을 설치하려면 헤드 노드에서 로컬 관리자 권한으로 이 계정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-126">**Domain account** - This account must be configured with local Administrator permissions on the head node to install HPC Pack.</span></span>
* <span data-ttu-id="9c505-127">**포트 443의 헤드 노드와 Azure 간 TCP 연결**</span><span class="sxs-lookup"><span data-stu-id="9c505-127">**TCP connectivity on port 443** from the head node to Azure.</span></span>

## <a name="install-hpc-pack-on-the-head-node"></a><span data-ttu-id="9c505-128">헤드 노드에 HPC 팩 설치</span><span class="sxs-lookup"><span data-stu-id="9c505-128">Install HPC Pack on the head node</span></span>
<span data-ttu-id="9c505-129">먼저 Windows Server를 실행하는 온-프레미스 컴퓨터에 Microsoft HPC Pack을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="9c505-130">이 컴퓨터는 클러스터의 헤드 노드가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-130">This computer becomes the head node of the cluster.</span></span>

1. <span data-ttu-id="9c505-131">로컬 관리자 권한을 가진 도메인 계정을 사용하여 헤드 노드에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-131">Log on to the head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="9c505-132">HPC 팩 설치 파일에서 Setup.exe를 실행하여 HPC Pack Installation Wizard를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-132">Start the HPC Pack Installation Wizard by running Setup.exe from the HPC Pack installation files.</span></span>

3. <span data-ttu-id="9c505-133">**HPC Pack 2012 R2 Setup** 화면에서 **New installation or add new features to an existing installation**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-133">On the **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features to an existing installation**.</span></span>

    ![HPC Pack 2012 설치][install_hpc1]

4. <span data-ttu-id="9c505-135">**Microsoft Software User Agreement page** 페이지에서 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-135">On the **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="9c505-136">**Select Installation Type** 페이지에서 **Create a new HPC cluster by creating a head node**를 클릭한 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-136">On the **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="9c505-137">마법사에서 여러 개의 사전 설치 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-137">The wizard runs several pre-installation tests.</span></span> <span data-ttu-id="9c505-138">테스트를 모두 통과한 경우 **Next** on the **Next** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-138">Click **Next** on the **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="9c505-139">그렇지 않으면 제공된 정보를 검토하고 필요에 따라 환경을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-139">Otherwise, review the information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="9c505-140">다시 테스트를 실행하거나 필요한 경우 Installation Wizard를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-140">Then run the tests again or if necessary start the Installation Wizard again.</span></span>
7. <span data-ttu-id="9c505-141">**HPC DB Configuration** 페이지에서 모든 HPC 데이터베이스에 대해 **Head Node**가 선택되었는지 확인한 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-141">On the **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![DB 구성][install_hpc4]

8. <span data-ttu-id="9c505-143">마법사의 나머지 페이지에서 기본 선택을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-143">Accept default selections on the remaining pages of the wizard.</span></span> <span data-ttu-id="9c505-144">**Install Required Components** 페이지에서 **Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-144">On the **Install Required Components** page, click **Install**.</span></span>
   
    ![Install][install_hpc6]

9. <span data-ttu-id="9c505-146">설치가 완료되면 **Start HPC Cluster Manager**를 선택 취소하고 **Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-146">After the installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="9c505-147">(이후 단계에서 HPC 클러스터 관리자를 시작합니다.)</span><span class="sxs-lookup"><span data-stu-id="9c505-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![Finish][install_hpc7]

## <a name="prepare-the-azure-subscription"></a><span data-ttu-id="9c505-149">Azure 구독 준비</span><span class="sxs-lookup"><span data-stu-id="9c505-149">Prepare the Azure subscription</span></span>
<span data-ttu-id="9c505-150">[Azure Portal](https://portal.azure.com)에서 Azure 구독으로 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-150">Perform the following steps in the [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="9c505-151">이러한 단계를 완료한 후에는 온-프레미스 헤드 노드에서 Azure 노드를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-151">After completing these steps, you can deploy Azure nodes from the on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="9c505-152">또한 나중에 필요한 Azure 구독 ID를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="9c505-153">포털의 **구독**에서 ID를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-153">Find the ID in **Subscriptions** in the portal.</span></span>
  > 

### <a name="upload-the-default-management-certificate"></a><span data-ttu-id="9c505-154">기본 관리 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="9c505-154">Upload the default management certificate</span></span>
<span data-ttu-id="9c505-155">HPC 팩은 Azure 관리 인증서로 업로드할 수 있는 자체 서명된 인증서(기본 Microsoft HPC Azure 관리 인증서라고 함)를 헤드 노드에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-155">HPC Pack installs a self-signed certificate on the head node, called the Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="9c505-156">이 인증서는 테스트 및 개념 증명 배포를 위해 제공되며 헤드 노드와 Azure 간의 연결에 보안을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-156">This certificate is provided for testing and proof-of-concept deployments to secure the connection between the head node and Azure.</span></span>

1. <span data-ttu-id="9c505-157">헤드 노드 컴퓨터에서 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-157">From the head node computer, sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="9c505-158">**구독** > *your_subscription_name*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="9c505-159">**관리 인증서** > **업로드**.4를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="9c505-160">헤드 노드에서 C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer 파일을 찾은 다음</span><span class="sxs-lookup"><span data-stu-id="9c505-160">Browse on the head node for the file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="9c505-161">**업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="9c505-162">관리 인증서 목록에 **기본 HPC Azure 관리** 인증서가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-162">The **Default HPC Azure Management** certificate appears in the list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="9c505-163">Azure 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="9c505-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="9c505-164">최상의 성능을 얻으려면 동일한 지역에 클라우드 서비스와 저장소 계정을 만듭니다(이후 단계에서).</span><span class="sxs-lookup"><span data-stu-id="9c505-164">For best performance, create the cloud service and the storage account (in a later step) in the same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="9c505-165">포털에서 **Cloud Services(클래식)** > **+추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-165">In the portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="9c505-166">서비스에 대한 DNS 이름을 입력하고 리소스 그룹 및 위치를 선택한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-166">Type a DNS name for the service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="9c505-167">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="9c505-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="9c505-168">포털에서 **Storage 계정(클래식)** > **+추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-168">In the portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="9c505-169">계정에 대한 이름을 입력하고 **클래식** 배포 모델을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-169">Type a name for the account, and select the **Classic** deployment model.</span></span>

3. <span data-ttu-id="9c505-170">리소스 그룹 및 위치를 선택하고 다른 설정을 기본값 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="9c505-171">그런 다음 **Create**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-171">Then click **Create**.</span></span>

## <a name="configure-the-head-node"></a><span data-ttu-id="9c505-172">헤드 노드 구성</span><span class="sxs-lookup"><span data-stu-id="9c505-172">Configure the head node</span></span>
<span data-ttu-id="9c505-173">HPC Cluster Manager를 사용하여 Azure 노드를 배포하고 작업을 제출하려면 먼저 필요한 클러스터 구성 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-173">To use HPC Cluster Manager to deploy Azure nodes and to submit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="9c505-174">헤드 노드에서 HPC Cluster Manager를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-174">On the head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="9c505-175">**Select Head Node** 대화 상자가 표시되면 **Local Computer**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-175">If the **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="9c505-176">**Deployment To-do List** 가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-176">The **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="9c505-177">**Required deployment tasks**에서 **Configure your network**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![네트워크 구성][config_hpc2]

3. <span data-ttu-id="9c505-179">Network Configuration Wizard에서 **All nodes only on an enterprise network** (Topology 5)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-179">In the Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="9c505-180">이 네트워크 구성은 가장 간단한 예시입니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-180">This network configuration is the simplest for demonstration purposes.</span></span>
   
    ![토폴로지 5][config_hpc3]
   
4. <span data-ttu-id="9c505-182">마법사의 나머지 페이지에서 **Next** 를 클릭하여 기본값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-182">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="9c505-183">**Review** 탭에서 **Configure**를 클릭하여 네트워크 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-183">Then, on the **Review** tab, click **Configure** to complete the network configuration.</span></span>

5. <span data-ttu-id="9c505-184">**Deployment To-do List**에서 **Provide installation credentials**을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9c505-184">In the **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="9c505-185">**Installation Credentials** 대화 상자에서 HPC 팩을 설치하는 데 사용한 도메인 계정의 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-185">In the **Installation Credentials** dialog box, type the credentials of the domain account that you used to install HPC Pack.</span></span> <span data-ttu-id="9c505-186">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-186">Then click **OK**.</span></span> 
   
    ![Installation Credentials][config_hpc6]
   
7. <span data-ttu-id="9c505-188">**Deployment To-do List**에서 **Configure the naming of new nodes**을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9c505-188">In the **Deployment To-do List**, click **Configure the naming of new nodes**.</span></span>

8. <span data-ttu-id="9c505-189">**Specify Node Naming Series** 대화 상자에서 기본 이름 지정 시리즈를 적용하고 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-189">In the **Specify Node Naming Series** dialog box, accept the default naming series and click **OK**.</span></span> <span data-ttu-id="9c505-190">이 자습서에서 추가한 Azure 노드가 자동으로 이름이 지정되었더라도 이 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-190">Complete this step even though the Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![노드 이름 지정][config_hpc8]
   
9. <span data-ttu-id="9c505-192">**Deployment To-do List**에서 **Create a node template**을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9c505-192">In the **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="9c505-193">자습서의 뒷부분에서는 노드 템플릿을 사용하여 클러스터에 Azure 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-193">Later in the tutorial, you use the node template to add Azure nodes to the cluster.</span></span>

10. <span data-ttu-id="9c505-194">Create Node Template Wizard에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-194">In the Create Node Template Wizard, do the following:</span></span>
    
    <span data-ttu-id="9c505-195">a.</span><span class="sxs-lookup"><span data-stu-id="9c505-195">a.</span></span> <span data-ttu-id="9c505-196">**노드 템플릿 유형 선택** 페이지에서 **Windows Azure 노드 템플릿**을 클릭한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-196">On the **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![노드 템플릿][config_hpc10]
    
    <span data-ttu-id="9c505-198">b.</span><span class="sxs-lookup"><span data-stu-id="9c505-198">b.</span></span> <span data-ttu-id="9c505-199">**다음** 을 클릭하여 기본 템플릿 이름을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-199">Click **Next** to accept the default template name.</span></span>
    
    <span data-ttu-id="9c505-200">c.</span><span class="sxs-lookup"><span data-stu-id="9c505-200">c.</span></span> <span data-ttu-id="9c505-201">**구독 정보 제공** 페이지에서 Azure 구독 ID(Azure 계정 정보에서 사용 가능)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-201">On the **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="9c505-202">그런 후 **관리 인증서**에서 **기본 Microsoft HPC Azure 관리**를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="9c505-203">그런 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-203">Then click **Next**.</span></span>
    
    ![노드 템플릿][config_hpc12]
    
    <span data-ttu-id="9c505-205">d.</span><span class="sxs-lookup"><span data-stu-id="9c505-205">d.</span></span> <span data-ttu-id="9c505-206">**서비스 정보 제공** 페이지에서 이전 단계를 통해 만든 클라우드 서비스와 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-206">On the **Provide Service Information** page, select the cloud service and the storage account that you created in a previous step.</span></span> <span data-ttu-id="9c505-207">그런 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-207">Then click **Next**.</span></span>
    
    ![노드 템플릿][config_hpc13]
    
    <span data-ttu-id="9c505-209">e.</span><span class="sxs-lookup"><span data-stu-id="9c505-209">e.</span></span> <span data-ttu-id="9c505-210">마법사의 나머지 페이지에서 **Next** 를 클릭하여 기본값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-210">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="9c505-211">**Review** 탭에서 **Create**를 클릭하여 노드 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-211">Then, on the **Review** tab, click **Create** to create the node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="9c505-212">기본적으로 Azure 노드 템플릿에는 HPC 클러스터 관리자를 사용하여 수동으로 노드를 시작(프로비전) 및 중지하기 위한 설정이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-212">By default, the Azure node template includes settings for you to start (provision) and stop the nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="9c505-213">Azure 노드를 자동으로 시작 및 중지하도록 일정을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-213">You can optionally configure a schedule to start and stop the Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-to-the-cluster"></a><span data-ttu-id="9c505-214">클러스터에 Azure 노드 추가</span><span class="sxs-lookup"><span data-stu-id="9c505-214">Add Azure nodes to the cluster</span></span>
<span data-ttu-id="9c505-215">이제 노드 템플릿을 사용하여 클러스터에 Azure 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-215">Now use the node template to add Azure nodes to the cluster.</span></span> <span data-ttu-id="9c505-216">클러스터에 노드를 추가하면 해당 구성 정보가 저장되므로 언제든지 클라우드 서비스에서 노드를 시작(프로비전)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-216">Adding the nodes to the cluster stores their configuration information so that you can start (provision) them at any time in the cloud service.</span></span> <span data-ttu-id="9c505-217">클라우드 서비스에서 인스턴스가 실행되는 경우 Azure 노드에 대해서만 구독에 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-217">Your subscription only gets charged for Azure nodes after the instances are running in the cloud service.</span></span>

<span data-ttu-id="9c505-218">두 개의 작은 노드를 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-218">Follow these steps to add two Small nodes.</span></span>

1. <span data-ttu-id="9c505-219">HPC 클러스터 관리자에서 **노드 관리**(최신 버전의 HPC Pack에서 **리소스 관리**) > **노드 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![노드 추가][add_node1]

2. <span data-ttu-id="9c505-221">Add Node Wizard의 **Select Deployment Method** 페이지에서 **Add Windows Azure nodes**를 클릭한 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-221">In the Add Node Wizard, on the **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Azure 노드 추가][add_node1_1]

3. <span data-ttu-id="9c505-223">**Specify New Nodes** 페이지에서 이전에 만든 Azure 노드 템플릿(기본적으로 **Default AzureNode Template**)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-223">On the **Specify New Nodes** page, select the Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="9c505-224">크기가 **Small**인 노드 **2**개를 지정하고 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![노드 지정][add_node2]
   
4. <span data-ttu-id="9c505-226">**Completing the Add Node Wizard** 페이지에서 **Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-226">On the **Completing the Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="9c505-227">이제 **AzureCN-0001** 및 **AzureCN-0002**라는 Azure 노드 2개가 HPC Cluster Manager에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="9c505-228">둘 다 **배포되지 않음** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-228">Both are in the **Not-Deployed** state.</span></span>
   
    ![추가된 노드][add_node3]

## <a name="start-the-azure-nodes"></a><span data-ttu-id="9c505-230">Azure 노드 시작</span><span class="sxs-lookup"><span data-stu-id="9c505-230">Start the Azure nodes</span></span>
<span data-ttu-id="9c505-231">Azure에서 클러스터 리소스를 사용하려면 HPC Cluster Manager를 통해 Azure 노드를 시작(프로비전)하고 온라인 상태로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-231">When you want to use the cluster resources in Azure, use HPC Cluster Manager to start (provision) the Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="9c505-232">HPC 클러스터 관리자에서 **노드 관리**(최신 버전의 HPC Pack에서 **리소스 관리**)를 클릭하고 [Azure 노드]를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select the Azure nodes.</span></span>

2. <span data-ttu-id="9c505-233">**시작**을 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-233">Click **Start**, and then click **OK**.</span></span>
   
   ![노드 시작][add_node4]
   
    <span data-ttu-id="9c505-235">노드가 **Provisioning** 상태로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-235">The nodes transition to the **Provisioning** state.</span></span> <span data-ttu-id="9c505-236">프로비전 로그를 보고 프로비전 진행 상태를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-236">View the provisioning log to track the provisioning progress.</span></span>
   
    ![노드 프로비전][add_node6]

3. <span data-ttu-id="9c505-238">몇 분 후에 Azure 노드가 프로비전을 완료하고 **Offline** 상태로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-238">After a few minutes, the Azure nodes finish provisioning and are in the **Offline** state.</span></span> <span data-ttu-id="9c505-239">이 상태에서는 역할 인스턴스가 실행되지만 클러스터 작업을 수락할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-239">In this state, the role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="9c505-240">역할 인스턴스가 실행되고 있는지 확인하려면 Azure Portal에서 **Cloud Services(클래식)** > *your_cloud_service_name*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-240">To confirm that the role instances are running, in the Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="9c505-241">두 개의 **HpcWorkerRole** 인스턴스(노드)가 서비스에서 실행 중인 것으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-241">You should see two **HpcWorkerRole** instances (nodes) running in the service.</span></span> <span data-ttu-id="9c505-242">또한 HPC 팩은 헤드 노드와 Azure 간의 통신을 처리하기 위해 **HpcProxy** 인스턴스(중간 크기) 두 개를 자동으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) to handle communication between the head node and Azure.</span></span>

   ![실행 중인 인스턴스][view_instances1]

5. <span data-ttu-id="9c505-244">클러스터 작업을 실행하기 위해 Azure 노드를 온라인 상태로 전환하려면 노드를 선택하고 마우스 오른쪽 단추를 클릭한 후 **Bring Online**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-244">To bring the Azure nodes online to run cluster jobs, select the nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![오프라인 노드][add_node7]
   
    <span data-ttu-id="9c505-246">HPC Cluster Manager에서 노드가 **Online** 상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-246">HPC Cluster Manager indicates that the nodes are in the **Online** state.</span></span>

## <a name="run-a-command-across-the-cluster"></a><span data-ttu-id="9c505-247">클러스터에서 명령 실행</span><span class="sxs-lookup"><span data-stu-id="9c505-247">Run a command across the cluster</span></span>
<span data-ttu-id="9c505-248">설치를 확인하려면 HPC Pack **clusrun** 명령을 사용하여 하나 이상의 클러스터 노드에서 명령이나 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-248">To check the installation, use the HPC Pack **clusrun** command to run a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="9c505-249">간단한 예로 **clusrun** 을 사용하여 Azure 노드의 IP 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-249">As a simple example, use **clusrun** to get the IP configuration of the Azure nodes.</span></span>

1. <span data-ttu-id="9c505-250">헤드 노드에서 관리자 권한으로 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-250">On the head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="9c505-251">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-251">Type the following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="9c505-252">메시지가 표시되면 클러스터 관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="9c505-253">다음과 유사한 명령 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-253">You should see command output similar to the following.</span></span>
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="9c505-255">테스트 작업 실행</span><span class="sxs-lookup"><span data-stu-id="9c505-255">Run a test job</span></span>
<span data-ttu-id="9c505-256">이제 하이브리드 클러스터에서 실행되는 테스트 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-256">Now submit a test job that runs on the hybrid cluster.</span></span> <span data-ttu-id="9c505-257">이 예제는 간단한 매개 변수 스윕 작업(본질적으로 병렬 계산 형식)입니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="9c505-258">이 예제는 **set/a** 명령을 사용하여 자체적으로 정수를 추가하는 하위 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-258">This example runs subtasks that add an integer to itself by using the **set /a** command.</span></span> <span data-ttu-id="9c505-259">클러스터의 모든 노드는 1에서 100까지 정수의 하위 작업을 마치는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-259">All the nodes in the cluster contribute to finishing the subtasks for integers from 1 to 100.</span></span>

1. <span data-ttu-id="9c505-260">HPC 클러스터 관리자에서 **작업 관리** > **New Parametric Sweep Job(새 매개 변수 스윕 작업)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![새 작업][test_job1]

2. <span data-ttu-id="9c505-262">**New Parametric Sweep Job** 대화 상자의 **Command line**에 `set /a *+*`를 입력합니다(표시되는 기본 명령줄을 덮어씀).</span><span class="sxs-lookup"><span data-stu-id="9c505-262">In the **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting the default command line that appears).</span></span> <span data-ttu-id="9c505-263">나머지 설정은 기본값을 그대로 두고 **Submit** 를 클릭하여 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-263">Leave default values for the remaining settings, and then click **Submit** to submit the job.</span></span>
   
    ![매개 변수 스윕][param_sweep1]

3. <span data-ttu-id="9c505-265">작업이 완료되면 **My Sweep Task** 작업을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-265">When the job is finished, double-click the **My Sweep Task** job.</span></span>

4. <span data-ttu-id="9c505-266">**View Tasks**를 클릭한 후 하위 작업을 클릭하여 해당 하위 작업의 계산된 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-266">Click **View Tasks**, and then click a subtask to view the calculated output of that subtask.</span></span>
   
    ![작업 결과][view_job361]

5. <span data-ttu-id="9c505-268">하위 작업에 대한 계산을 수행한 노드를 보려면 **Allocated Nodes**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-268">To see which node performed the calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="9c505-269">클러스터에서 다른 노드 이름이 표시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-269">(Your cluster might show a different node name.)</span></span>
   
    ![작업 결과][view_job362]

## <a name="stop-the-azure-nodes"></a><span data-ttu-id="9c505-271">Azure 노드 중지</span><span class="sxs-lookup"><span data-stu-id="9c505-271">Stop the Azure nodes</span></span>
<span data-ttu-id="9c505-272">클러스터를 시도한 후 계정에 대한 불필요한 요금 부과를 피하기 위해 Azure 노드를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-272">After you try out the cluster, stop the Azure nodes to avoid unnecessary charges to your account.</span></span> <span data-ttu-id="9c505-273">이 단계로 클라우드 서비스가 중지되고 Azure 역할 인스턴스가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-273">This step stops the cloud service and removes the Azure role instances.</span></span>

1. <span data-ttu-id="9c505-274">HPC 클러스터 관리자의 **노드 관리**(이전 버전의 HPC Pack에서 **리소스 관리**)에서 두 Azure 노드를 모두 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="9c505-275">그런 다음 **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-275">Then, click **Stop**.</span></span>
   
    ![노드 중지][stop_node1]

2. <span data-ttu-id="9c505-277">**Stop Windows Azure nodes** 대화 상자에서 **Stop**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-277">In the **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="9c505-278">노드가 **Stopping** 상태로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-278">The nodes transition to the **Stopping** state.</span></span> <span data-ttu-id="9c505-279">몇 분 후에 HPC Cluster Manager에서 노드가 **Not-Deployed**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-279">After a few minutes, HPC Cluster Manager shows that the nodes are **Not-Deployed**.</span></span>
   
    ![배포되지 않은 노드][stop_node4]

4. <span data-ttu-id="9c505-281">역할 인스턴스가 Azure에서 더 이상 실행되지 않는지 확인하려면 Azure Portal에서 **Cloud Services(클래식)** > *your_cloud_service_name*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-281">To confirm that the role instances are no longer running in Azure, in the Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="9c505-282">프로덕션 환경에는 인스턴스가 배포되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-282">No instances are deployed in the production environment.</span></span> 
   
    <span data-ttu-id="9c505-283">이제 자습서를 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="9c505-283">This completes the tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c505-284">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c505-284">Next steps</span></span>
* <span data-ttu-id="9c505-285">[HPC Pack](https://technet.microsoft.com/library/cc514029)설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c505-285">Explore the documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="9c505-286">대규모 하이브리드 HPC Pack 클러스터 배포를 설정하려면 [Microsoft HPC Pack을 사용하여 Azure 작업자 역할 인스턴스로 버스트](http://go.microsoft.com/fwlink/p/?LinkID=200493)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c505-286">To set up a hybrid HPC Pack cluster deployment at greater scale, see [Burst to Azure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="9c505-287">Azure Resource Manager 템플릿 사용 등 Azure에서 HPC Pack 클러스터를 만드는 다른 방법은 [Azure에서 Microsoft HPC Pack을 사용하는 HPC 클러스터 옵션](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c505-287">For other ways to create an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
