---
title: "HPC 팩 클러스터 노드 자동 크기 조정 | Microsoft Docs"
description: "Azure에서 HPC 팩 클러스터 계산 노드 수를 자동으로 증가 및 축소"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0dc0d15c64d8951c3c457df73588c37418a3c8a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-grow-and-shrink-the-hpc-pack-cluster-resources-in-azure-according-to-the-cluster-workload"></a><span data-ttu-id="95fa1-103">클러스터 워크로드에 따라 Azure에서 HPC 팩 클러스터 리소스를 자동으로 증가 및 축소</span><span class="sxs-lookup"><span data-stu-id="95fa1-103">Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload</span></span>
<span data-ttu-id="95fa1-104">HPC 팩 클러스터에 Azure "버스트" 노드를 배포하거나 Azure VM에 HPC 팩 클러스터를 만드는 경우 클러스터의 현재 워크로드에 따라 노드 또는 코어 등과 같은 클러스터 리소스를 자동으로 증가 또는 축소하려는 방법이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink the cluster resources such as nodes or cores according to the workload on the cluster.</span></span> <span data-ttu-id="95fa1-105">이렇게 클러스터 리소스의 크기를 조정하면 Azure 리소스를 더욱 효율적으로 사용하고 비용을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-105">Scaling the cluster resources in this way allows you to use your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="95fa1-106">이 문서에서는 HPC 팩에서 계산 리소스의 자동 크기 조정에 제공하는 두 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-106">This article shows you two ways that HPC Pack provides to autoscale compute resources:</span></span>

* <span data-ttu-id="95fa1-107">HPC 팩 클러스터 속성 **AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="95fa1-107">The HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="95fa1-108">**AzureAutoGrowShrink.ps1** HPC PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="95fa1-108">The **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="95fa1-109">현재 Windows Server 운영 체제를 실행하는 HPC 팩 계산 리소스만 자동으로 증가 및 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-the-autogrowshrink-cluster-property"></a><span data-ttu-id="95fa1-110">AutoGrowShrink 클러스터 속성 설정</span><span class="sxs-lookup"><span data-stu-id="95fa1-110">Set the AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="95fa1-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="95fa1-111">Prerequisites</span></span>

* <span data-ttu-id="95fa1-112">**HPC 팩 2012 R2 업데이트 2 또는 이후 버전 클러스터** - 클러스터 헤드 노드는 온-프레미스 또는 Azure VM에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-112">**HPC Pack 2012 R2 Update 2 or later cluster** - The cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="95fa1-113">온-프레미스 헤드 노드 및 Azure "버스트" 노드로 시작하려면 [HPC 팩으로 하이브리드 클러스터 설정](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95fa1-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="95fa1-114">Azure VM에 HPC 팩 클러스터를 빠르게 배포하려면 [HPC 팩 IaaS 배포 스크립트](hpcpack-cluster-powershell-script.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95fa1-114">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="95fa1-115">**Azure Resource Manager 배포 모델에서 헤드 노드를 사용하는 클러스터의 경우** - HPC 팩 2016부터 Azure Active Directory 응용 프로그램의 인증서 인증은 Azure Resource Manager를 사용하여 배포된 클러스터 VM을 자동으로 증가 및 축소시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="95fa1-116">인증서를 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="95fa1-117">클러스터 배포 후에 원격 데스크톱에 의해 하나의 헤드 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-117">After cluster deployment, connect by Remote Desktop to one head node.</span></span>

  2. <span data-ttu-id="95fa1-118">각 헤드 노드에 대한 인증서(개인 키를 포함한 PFX 형식)를 업로드하고 Cert:\LocalMachine\My and Cert:\LocalMachine\Root에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-118">Upload the certificate (PFX format with private key) to each head node and install to Cert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="95fa1-119">Azure PowerShell을 관리자로 시작하고 하나의 헤드 노드에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-119">Start Azure PowerShell as an administrator and run the following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="95fa1-120">계정이 둘 이상의 Azure Active Directory 테넌트 또는 Azure 구독에 포함된 경우 다음 명령을 실행해 올바른 테넌트 및 구독을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run the following command to select the correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="95fa1-121">현재 선택된 테넌트와 구독을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-121">Run the following command to view the currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="95fa1-122">다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-122">Run the following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="95fa1-123">여기서,</span><span class="sxs-lookup"><span data-stu-id="95fa1-123">where</span></span>

    <span data-ttu-id="95fa1-124">**DisplayName** - Azure 활성 응용 프로그램 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="95fa1-125">응용 프로그램이 없는 경우 Azure Active Directory에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-125">If the application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="95fa1-126">**HomePage** - 응용 프로그램의 홈 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-126">**HomePage** - The home page of the application.</span></span> <span data-ttu-id="95fa1-127">앞의 예제에서와 같이 더미 URL을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-127">You can configure a dummy URL, as in the preceding example.</span></span>

    <span data-ttu-id="95fa1-128">**IdentifierUri** - 응용 프로그램의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-128">**IdentifierUri** - Identifier of the application.</span></span> <span data-ttu-id="95fa1-129">앞의 예제에서와 같이 더미 URL을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-129">You can configure a dummy URL, as in the preceding example.</span></span>

    <span data-ttu-id="95fa1-130">**CertificateThumbprint** -1단계에서 헤드 노드에 설치한 인증서의 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-130">**CertificateThumbprint** - Thumbprint of the certificate you installed on the head node in Step 1.</span></span>

    <span data-ttu-id="95fa1-131">**TenantId** - Azure Active Directory의 테넌트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="95fa1-132">Azure Active Directory 포털 **속성** 페이지에서 테넌트 ID를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-132">You can get the Tenant ID from the Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="95fa1-133">**ConfigARMAutoGrowShrinkCert.ps1**에 대한 자세한 내용은 `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="95fa1-134">**Azure 클래식 배포 모델에 헤드 노드를 가진 클러스터** - HPC 팩 IaaS 배포 스크립트를 사용하여 클러스터를 만드는 경우 클러스터 구성 파일의 AutoGrowShrink 옵션을 설정하여 **AutoGrowShrink** 클러스터 속성을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use the HPC Pack IaaS deployment script to create the cluster in the classic deployment model, enable the **AutoGrowShrink** cluster property by setting the AutoGrowShrink option in the cluster configuration file.</span></span> <span data-ttu-id="95fa1-135">자세한 내용은 [스크립트 다운로드](https://www.microsoft.com/download/details.aspx?id=44949)와 함께 제공되는 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95fa1-135">For details, see the documentation accompanying the [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="95fa1-136">또는 다음 섹션에서 설명하는 HPC PowerShell 명령을 사용하여 클러스터를 배포한 후 **AutoGrowShrink** 클러스터 속성을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-136">Alternatively, enable the **AutoGrowShrink** cluster property after you deploy the cluster by using HPC PowerShell commands described in the following section.</span></span> <span data-ttu-id="95fa1-137">이를 준비하려면 먼저 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-137">To prepare for this, first complete the following steps:</span></span>

  1. <span data-ttu-id="95fa1-138">헤드 노드 및 Azure 구독에서 Azure 관리 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-138">Configure an Azure management certificate on the head node and in the Azure subscription.</span></span> <span data-ttu-id="95fa1-139">테스트 배포의 경우 HPC 팩이 헤드 노드에 설치하는 기본 Microsoft HPC Azure 자체 서명 인증서를 사용하고 이 인증서를 Azure 구독에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-139">For a test deployment, you can use the Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on the head node, and then upload that certificate to your Azure subscription.</span></span> <span data-ttu-id="95fa1-140">옵션 및 단계는 [TechNet 라이브러리 지침](https://technet.microsoft.com/library/gg481759.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95fa1-140">For options and steps, see the [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="95fa1-141">헤드 노드에서 **regedit**을 실행하고 HKLM\SOFTWARE\Micorsoft\HPC\IaasInfo로 이동한 다음 문자열 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-141">Run **regedit** on the head node, go to HKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="95fa1-142">값 이름을 “ThumbPrint”로 설정하고 값 데이터를 1단계의 인증서 지문으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-142">Set the Value name to “ThumbPrint”, and Value data to the thumbprint of the certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-to-set-the-autogrowshrink-property"></a><span data-ttu-id="95fa1-143">AutoGrowShrink 속성을 설정하는 HPC PowerShell 명령</span><span class="sxs-lookup"><span data-stu-id="95fa1-143">HPC PowerShell commands to set the AutoGrowShrink property</span></span>
<span data-ttu-id="95fa1-144">다음은 **AutoGrowShrink** 를 설정하고 추가 매개 변수를 통해 해당 동작을 조정하는 샘플 HPC PowerShell 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-144">Following are sample HPC PowerShell commands to set **AutoGrowShrink** and to tune its behavior with additional parameters.</span></span> <span data-ttu-id="95fa1-145">전체 설정 목록은 이 문서의 뒷부분에 나오는 [AutoGrowShrink 매개 변수](#AutoGrowShrink-parameters) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95fa1-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for the complete list of settings.</span></span>

<span data-ttu-id="95fa1-146">이 명령을 시작하려면 관리자 권한으로 클러스터 헤드 노드에서 HPC PowerShell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-146">To run these commands, start HPC PowerShell on the cluster head node as an administrator.</span></span>

<span data-ttu-id="95fa1-147">**AutoGrowShrink 속성을 사용하도록 설정하려면**</span><span class="sxs-lookup"><span data-stu-id="95fa1-147">**To enable the AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="95fa1-148">**AutoGrowShrink 속성을 사용하지 않도록 설정하려면**</span><span class="sxs-lookup"><span data-stu-id="95fa1-148">**To disable the AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="95fa1-149">**분 단위로 증가 간격을 변경하려면**</span><span class="sxs-lookup"><span data-stu-id="95fa1-149">**To change the grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="95fa1-150">**분 단위로 축소 간격을 변경하려면**</span><span class="sxs-lookup"><span data-stu-id="95fa1-150">**To change the shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="95fa1-151">**AutoGrowShrink의 현재 구성을 보려면**</span><span class="sxs-lookup"><span data-stu-id="95fa1-151">**To view the current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="95fa1-152">**AutoGrowShrink에서 노드 그룹을 제외하려면**</span><span class="sxs-lookup"><span data-stu-id="95fa1-152">**To exclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="95fa1-153">이 매개 변수는 HPC 팩 2016부터 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="95fa1-154">AutoGrowShrink 매개 변수</span><span class="sxs-lookup"><span data-stu-id="95fa1-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="95fa1-155">다음은 **Set-HpcClusterProperty** 명령을 사용하여 수정할 수 있는 AutoGrowShrink 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-155">The following are AutoGrowShrink parameters that you can modify by using the **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="95fa1-156">**EnableGrowShrink** - **AutoGrowShrink** 속성을 사용하도록 또는 사용하지 않도록 설정하는 스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-156">**EnableGrowShrink** - Switch to enable or disable the **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="95fa1-157">**ParamSweepTasksPerCore** - 한 코어를 확장하기 위한 매개 변수 스위프 태스크 수입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks to grow one core.</span></span> <span data-ttu-id="95fa1-158">기본값은 태스크당 코어 한 개를 증가시키는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-158">The default is to grow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="95fa1-159">HPC 팩 QFE KB3134307은 **ParamSweepTasksPerCore**를 **TasksPerResourceUnit**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** to **TasksPerResourceUnit**.</span></span> <span data-ttu-id="95fa1-160">이는 작업 리소스 유형을 기반으로 하며 노드, 소켓 또는 코어일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-160">It is based on the job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="95fa1-161">**GrowThreshold** - 자동 증가를 트리거하도록 대기열에 저장된 태스크의 임계값입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-161">**GrowThreshold** - Threshold of queued tasks to trigger automatic growth.</span></span> <span data-ttu-id="95fa1-162">기본값은 1이며, 이는 태스크 1 개 이상이 대기열에 저장된 상태이면 자동으로 노드를 증가한다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-162">The default is 1, which means that if there are 1 or more tasks in the queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="95fa1-163">**GrowInterval** - 자동 증가를 트리거하는 분 단위의 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-163">**GrowInterval** - Interval in minutes to trigger automatic growth.</span></span> <span data-ttu-id="95fa1-164">기본 간격은 5 분입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-164">The default interval is 5 minutes.</span></span>
* <span data-ttu-id="95fa1-165">**ShrinkInterval** - 자동 축소를 트리거하는 분 단위의 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-165">**ShrinkInterval** - Interval in minutes to trigger automatic shrinking.</span></span> <span data-ttu-id="95fa1-166">기본 간격은 5 분입니다.|</span><span class="sxs-lookup"><span data-stu-id="95fa1-166">The default interval is 5 minutes.|</span></span>
* <span data-ttu-id="95fa1-167">**ShrinkIdleTimes** - 노드가 유휴 상태임을 나타내도록 축소하는 연속 검사 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-167">**ShrinkIdleTimes** - Number of continuous checks to shrink to indicate the nodes are idle.</span></span> <span data-ttu-id="95fa1-168">기본값은 3회입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-168">The default is 3 times.</span></span> <span data-ttu-id="95fa1-169">예를 들어 **ShrinkInterval** 이 5 분인 경우 HPC 팩은 매 5 분마다 노드가 유휴 상태인지 여부를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-169">For example, if the **ShrinkInterval** is 5 minutes, HPC Pack checks whether the node is idle every 5 minutes.</span></span> <span data-ttu-id="95fa1-170">노드가 연속 3회 검사(15 분) 후 유휴 상태에 있으면 HPC 팩이 해당 노드를 축소합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-170">If the nodes are in the idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="95fa1-171">**ExtraNodesGrowRatio** - 메시지 전달 인터페이스(MPI) 작업에 대해 증가할 노드의 추가 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-171">**ExtraNodesGrowRatio** - Additional percentage of nodes to grow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="95fa1-172">기본값은 1이며, 이는 HPC 팩이 MPI 작업에 대해 노드 1%를 증가시킨다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-172">The default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="95fa1-173">**GrowByMin** - 자동 증가 정책이 작업에 필요한 최소 리소스를 기반으로 하는지 여부를 나타내는 스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-173">**GrowByMin** - Switch to indicate whether the autogrow policy is based on the minimum resources required for the job.</span></span> <span data-ttu-id="95fa1-174">기본값은 False이며, 이는 HPC 팩이 작업에 필요한 최대 리소스를 기반으로 작업에 대한 노드를 증가시킨다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-174">The default is false, which means that HPC Pack grows nodes for jobs based on the maximum resources required for the jobs.</span></span>
* <span data-ttu-id="95fa1-175">**SoaJobGrowThreshold** - 자동 증가 프로세스를 트리거하는 수신 SQA 요청의 임계값입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests to trigger the automatic grow process.</span></span> <span data-ttu-id="95fa1-176">기본값은 50000입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-176">The default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="95fa1-177">이 매개 변수는 HPC 팩 2012 R2 업데이트 3부터 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="95fa1-178">**SoaRequestsPerCore** - 코어 한 개를 증가시키기 위한 수신 SOA 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-178">**SoaRequestsPerCore** -Number of incoming SOA requests to grow one core.</span></span> <span data-ttu-id="95fa1-179">기본값은 20000입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-179">The default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="95fa1-180">이 매개 변수는 HPC 팩 2012 R2 업데이트 3부터 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="95fa1-181">**ExcludeNodeGroups** – 지정된 노드 그룹의 노드는 자동으로 확장 및 축소되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-181">**ExcludeNodeGroups** – Nodes in the specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="95fa1-182">이 매개 변수는 HPC 팩 2016부터 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="95fa1-183">MPI 예제</span><span class="sxs-lookup"><span data-stu-id="95fa1-183">MPI example</span></span>
<span data-ttu-id="95fa1-184">기본적으로 HPC 팩은 MPI 작업에 대한 추가 노드를 1% 증가시킵니다(**ExtraNodesGrowRatio** 가 1로 설정됨).</span><span class="sxs-lookup"><span data-stu-id="95fa1-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set to 1).</span></span> <span data-ttu-id="95fa1-185">그 이유는 MPI 노드에 노드 여러 개가 필요할 수 있고 모든 노드가 준비되어야만 작업을 실행할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-185">The reason is that MPI may require multiple nodes, and the job can only run when all nodes are ready.</span></span> <span data-ttu-id="95fa1-186">Azure 노드를 시작할 때 경우에 따라 어떤 노드가 다른 노드보다 시작하기 위해 더 많은 시간이 필요하기 때문에 해당 노드가 준비가 될 때까지 다른 노드가 유휴 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-186">When Azure starts nodes, occasionally one node might need more time to start than others, causing other nodes to be idle while waiting for that node to get ready.</span></span> <span data-ttu-id="95fa1-187">HPC 팩은 추가 노드를 증가시켜 이 리소스 대기 시간을 줄이며 잠재적으로 비용을 절감합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="95fa1-188">MPI 작업에 대한 추가 노드의 비율을 증가시키려면(예를 들어 10%) 다음과 유사한 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-188">To increase the percentage of extra nodes for MPI jobs (for example, to 10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="95fa1-189">SOA 예제</span><span class="sxs-lookup"><span data-stu-id="95fa1-189">SOA example</span></span>
<span data-ttu-id="95fa1-190">기본적으로 **SoaJobGrowThreshold**는 50000으로 설정되며 **SoaRequestsPerCore**는 200000으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-190">By default, **SoaJobGrowThreshold** is set to 50000 and **SoaRequestsPerCore** is set to 200000.</span></span> <span data-ttu-id="95fa1-191">70000개의 요청을 가진 하나의 SOA 작업을 제출하는 경우 대기열에 저장된 하나의 태스크가 있으며 수신 요청 수는 70000개입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="95fa1-192">이 경우 HPC 팩은 대기열에 저장된 태스크에 대해 코어 1개를 증가시키며 수신 요청의 경우 (70000-50000)/20000 = 1개의 코어가 증가하므로 모두 합해서 이 SOA 작업에 대해 코어 2개가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-192">In this case HPC Pack grows 1 core for the queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-the-azureautogrowshrinkps1-script"></a><span data-ttu-id="95fa1-193">AzureAutoGrowShrink.ps1 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="95fa1-193">Run the AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="95fa1-194">필수 조건</span><span class="sxs-lookup"><span data-stu-id="95fa1-194">Prerequisites</span></span>

* <span data-ttu-id="95fa1-195">**HPC 팩 2012 R2 업데이트 1 이상 클러스터** - **AzureAutoGrowShrink.ps1** 스크립트는 %CCP_HOME%bin 폴더에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-195">**HPC Pack 2012 R2 Update 1 or later cluster** - The **AzureAutoGrowShrink.ps1** script is installed in the %CCP_HOME%bin folder.</span></span> <span data-ttu-id="95fa1-196">클러스터 헤드 노드는 온-프레미스 또는 Azure VM에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-196">The cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="95fa1-197">온-프레미스 헤드 노드 및 Azure "버스트" 노드로 시작하려면 [HPC 팩으로 하이브리드 클러스터 설정](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95fa1-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="95fa1-198">Azure VM에 HPC 팩 클러스터를 빠르게 배포하려면 [HPC 팩 IaaS 배포 스크립트](hpcpack-cluster-powershell-script.md)를 참조하세요. 또는 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/)을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="95fa1-198">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="95fa1-199">**Azure PowerShell 1.4.0** - 현재 스크립트는 이 특정 버전의 Azure PowerShell에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-199">**Azure PowerShell 1.4.0** - The script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="95fa1-200">**Azure 버스트 노드가 포함된 클러스터의 경우** - HPC 팩이 설치된 클라이언트 컴퓨터 또는 헤드 노드에서 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-200">**For a cluster with Azure burst nodes** - Run the script on a client computer where HPC Pack is installed, or on the head node.</span></span> <span data-ttu-id="95fa1-201">클라이언트 컴퓨터에서 실행할 경우 $env:CCP_SCHEDULER 변수가 헤드 노드를 가리키도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-201">If running on a client computer, ensure that you set the variable $env:CCP_SCHEDULER to point to the head node.</span></span> <span data-ttu-id="95fa1-202">Azure "버스트" 노드는 클러스터에 추가되어 있어야 하지만, 배포되지 않음 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-202">The Azure “burst” nodes must be added to the cluster, but they may be in the Not-Deployed state.</span></span>
* <span data-ttu-id="95fa1-203">**Azure VM Resource Manager 배포 모델에서 배포된 클러스터의 경우** - Resource Manager 배포 모델에 배포된 Azure VM 클러스터의 경우 스크립트는 Azure 인증을 위한 두 가지 방법을 지원합니다. `Login-AzureRmAccount`을 실행하여 스크립트를 실행할 때마다 Azure 계정에 로그인하거나 서비스 주체가 인증서를 사용하여 인증하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in the Resource Manager deployment model, the script supports two methods for Azure authentication: sign in to your Azure account to run the script every time (by running `Login-AzureRmAccount`, or configure a service principal to authenticate with a certificate.</span></span> <span data-ttu-id="95fa1-204">HPC 팩은 **ConfigARMAutoGrowShrinkCert.ps** 스크립트를 제공하여 인증서를 가진 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-204">HPC Pack provides the script **ConfigARMAutoGrowShrinkCert.ps** to create a service principal with certificate.</span></span> <span data-ttu-id="95fa1-205">스크립트는 Azure AD(Azure Active Directory) 응용 프로그램 및 서비스 주체를 만들고 서비스 주체에 참가자 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-205">The script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns the Contributor role to the service principal.</span></span> <span data-ttu-id="95fa1-206">스크립트를 실행하려면 Azure PowerShell을 관리자로 시작하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-206">To run the script, start Azure PowerShell  as administrator and run the following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="95fa1-207">**ConfigARMAutoGrowShrinkCert.ps1**에 대한 자세한 내용은 `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="95fa1-208">**Azure VM 클래식 배포 모델에 배포된 클러스터의 경우** - 여기에 설치된 **Start-HpcIaaSNode.ps1** 및 **Stop-HpcIaaSNode.ps1** 스크립트에 따라 다라지므로 헤드 노드 VM에서 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run the script on the head node VM, because it depends on the **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="95fa1-209">이러한 스크립트는 추가적으로 Azure 관리 인증서 또는 게시 설정 파일이 필요합니다( [Azure의 HPC 팩 클러스터에서 계산 노드 관리](hpcpack-cluster-node-manage.md)참조).</span><span class="sxs-lookup"><span data-stu-id="95fa1-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="95fa1-210">필요한 모든 컴퓨터 노드 VM이 클러스터에 이미 추가되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-210">Make sure all the compute node VMs you need are already added to the cluster.</span></span> <span data-ttu-id="95fa1-211">중지된 상태에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-211">They may be in the Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="95fa1-212">구문</span><span class="sxs-lookup"><span data-stu-id="95fa1-212">Syntax</span></span>
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="95fa1-213">매개 변수</span><span class="sxs-lookup"><span data-stu-id="95fa1-213">Parameters</span></span>
* <span data-ttu-id="95fa1-214">**NodeTemplates** - 노드의 증가 및 축소 범위를 정의하는 노드 템플릿의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-214">**NodeTemplates** - Names of the node templates to define the scope for the nodes to grow and shrink.</span></span> <span data-ttu-id="95fa1-215">이 매개 변수를 지정하지 않을 경우(기본값은 @()) **NodeType** 값이 AzureNodes이면 **AzureNodes** 노드 그룹의 모든 노드가 범위에 포함되고 **NodeType** 값이 ComputeNodes이면 **ComputeNodes** 노드 그룹의 모든 노드가 범위에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-215">If not specified (the default value is @()), all nodes in the **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in the **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="95fa1-216">**JobTemplates** - 노드의 증가 범위를 정의하는 작업 템플릿의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-216">**JobTemplates** - Names of the job templates to define the scope for the nodes to grow.</span></span>
* <span data-ttu-id="95fa1-217">**NodeType** - 증가 및 축소할 노드의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-217">**NodeType** - The type of node to grow and shrink.</span></span> <span data-ttu-id="95fa1-218">지원되는 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-218">Supported values are:</span></span>

  * <span data-ttu-id="95fa1-219">**AzureNodes** – 온-프레미스 또는 Azure IaaS 클러스터의 Azure PaaS(버스트) 노드에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="95fa1-220">**ComputeNodes** - Azure IaaS 클러스터의 계산 노드 VM에만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="95fa1-221">**NumOfQueuedJobsPerNodeToGrow** - 한 개 노드를 증가하는 데 필요한 큐 작업의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required to grow one node.</span></span>
* <span data-ttu-id="95fa1-222">**NumOfQueuedJobsToGrowThreshold** - 증가 프로세스를 시작하기 위한 큐 작업 수의 임계치입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-222">**NumOfQueuedJobsToGrowThreshold** - The threshold number of queued jobs to start the grow process.</span></span>
* <span data-ttu-id="95fa1-223">**NumOfActiveQueuedTasksPerNodeToGrow** - 한 개 노드를 증가하는 데 필요한 활성 큐 작업의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-223">**NumOfActiveQueuedTasksPerNodeToGrow** - The number of active queued tasks required to grow one node.</span></span> <span data-ttu-id="95fa1-224">**NumOfQueuedJobsPerNodeToGrow** 가 0보다 큰 값으로 지정된 경우 이 매개 변수가 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="95fa1-225">**NumOfActiveQueuedTasksToGrowThreshold** - 증가 프로세스를 시작하기 위한 활성 큐 작업 수의 임계치입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-225">**NumOfActiveQueuedTasksToGrowThreshold** - The threshold number of active queued tasks to start the grow process.</span></span>
* <span data-ttu-id="95fa1-226">**NumOfInitialNodesToGrow** - 범위 내 모든 노드가 **배포되지 않음** 또는 **중지(할당 해제)**일 경우 증가할 초기의 최소 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-226">**NumOfInitialNodesToGrow** - The initial minimum number of nodes to grow if all the nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="95fa1-227">**GrowCheckIntervalMins** - 검사 간 증가할 간격(분)입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-227">**GrowCheckIntervalMins** - The interval in minutes between checks to grow.</span></span>
* <span data-ttu-id="95fa1-228">**ShrinkCheckIntervalMins** - 검사 간 축소할 간격(분)입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-228">**ShrinkCheckIntervalMins** - The interval in minutes between checks to shrink.</span></span>
* <span data-ttu-id="95fa1-229">**ShrinkCheckIdleTimes** - 노드가 유휴 상태임을 나타낼 연속적 축소 검사의 수(**ShrinkCheckIntervalMins**로 구분)입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-229">**ShrinkCheckIdleTimes** - The number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) to indicate the nodes are idle.</span></span>
* <span data-ttu-id="95fa1-230">**UseLastConfigurations** - 인수 파일에 저장된 이전 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-230">**UseLastConfigurations** - The previous configurations saved in the argument file.</span></span>
* <span data-ttu-id="95fa1-231">**ArgFile**- 스크립트를 실행하기 위해 구성을 저장 및 업데이트하는 데 사용한 인수 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-231">**ArgFile**- The name of the argument file used to save and update the configurations to run the script.</span></span>
* <span data-ttu-id="95fa1-232">**LogFilePrefix** - 로그 파일의 접두사 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-232">**LogFilePrefix** - The prefix name of the log file.</span></span> <span data-ttu-id="95fa1-233">경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-233">You can specify a path.</span></span> <span data-ttu-id="95fa1-234">기본적으로 로그는 현재 작업 디렉터리에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-234">By default the log is written to the current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="95fa1-235">예 1</span><span class="sxs-lookup"><span data-stu-id="95fa1-235">Example 1</span></span>
<span data-ttu-id="95fa1-236">다음 예제는 자동으로 증가 및 축소하는 기본 AzureNode 템플릿을 배포된 Azure 버스트 노드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-236">The following example configures the Azure burst nodes deployed with the Default AzureNode Template to grow and shrink automatically.</span></span> <span data-ttu-id="95fa1-237">모든 노드가 초기에 **배포되지 않음** 상태인 경우 최소 3개 노드가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-237">If all the nodes are initially in the **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="95fa1-238">큐 작업 수가 8개를 초과할 경우 노드 수가 큐 작업 수 대 **NumOfQueuedJobsPerNodeToGrow**의 비율을 초과할 때까지 스크립트에서 노드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-238">If the number of queued jobs exceeds 8, the script starts nodes until their number exceeds the ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="95fa1-239">노드가 연속 3회 이상 유휴 상태인 것으로 확인되면 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-239">If a node is found to be idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="95fa1-240">예 2</span><span class="sxs-lookup"><span data-stu-id="95fa1-240">Example 2</span></span>
<span data-ttu-id="95fa1-241">다음 예제는 자동으로 증가 및 축소하는 기본 ComputeNode 템플릿을 배포된 Azure 계산 노드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-241">The following example configures the Azure compute node VMs deployed with the Default ComputeNode Template to grow and shrink automatically.</span></span>
<span data-ttu-id="95fa1-242">기본 작업 템플릿으로 구성된 작업은 클러스터에 워크로드 범위를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-242">The jobs configured by the Default job template define the scope of the workload on the cluster.</span></span> <span data-ttu-id="95fa1-243">모든 노드가 초기에 중지되어 있으면 최소 5개 노드가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-243">If all the nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="95fa1-244">활성 큐 작업 수가 15개를 초과할 경우 노드 수가 활성 큐 작업 수 대 **NumOfActiveQueuedTasksPerNodeToGrow**의 비율을 초과할 때까지 스크립트에서 노드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-244">If the number of active queued tasks exceeds 15, the script starts nodes until their number exceeds the ratio of active queued tasks to **NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="95fa1-245">노드가 연속 10회 이상 유휴 상태인 것으로 확인되면 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fa1-245">If a node is found to be idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
