---
title: "Azure에서 HPC 팩 클러스터에 작업 제출 | Microsoft Docs"
description: "Azure에서 HPC 팩 클러스터로 작업을 제출하기 위해 온-프레미스 컴퓨터를 설정하는 방법"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: d5953f1e1dd2deb4d871bd67352a6a5b2ae13dbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-to-an-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="a7524-103">온-프레미스 컴퓨터에서 Azure에 배포된 HPC 팩 클러스터로 HPC 작업 제출</span><span class="sxs-lookup"><span data-stu-id="a7524-103">Submit HPC jobs from an on-premises computer to an HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="a7524-104">Azure의 [Microsoft HPC 팩](https://technet.microsoft.com/library/cc514029) 클러스터로 작업을 제출하도록 온-프레미스 클라이언트 컴퓨터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-104">Configure an on-premises client computer to submit jobs to a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="a7524-105">이 문서에서는 HTTPS를 통해 Azure의 클러스터로 작업을 제출하도록 클라이언트 도구를 사용하여 로컬 컴퓨터를 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-105">This article shows you how to set up a local computer with client tools to submit job over HTTPS to the cluster in Azure.</span></span> <span data-ttu-id="a7524-106">이 방식으로 여러 클러스터 사용자가 헤드 노드 VM에 직접 연결하거나 Azure 구독에 액세스하지 않고도 클라우드 기반 HPC 팩 클러스터로 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-106">In this way, several cluster users can submit jobs to a cloud-based HPC Pack cluster, but without connecting directly to the head node VM or accessing an Azure subscription.</span></span>

![Azure의 클러스터로 작업 제출][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="a7524-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a7524-108">Prerequisites</span></span>
* <span data-ttu-id="a7524-109">**Azure VM에 배포된 HPC 팩 헤드 노드** - [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/) 또는 [Azure PowerShell 스크립트](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)와 같은 자동화된 도구를 사용하여 헤드 노드 및 클러스터를 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to deploy the head node and cluster.</span></span> <span data-ttu-id="a7524-110">이 문서의 단계를 완료하려면 헤드 노드의 DNS 이름 및 클러스터 관리자 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-110">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span></span>
* <span data-ttu-id="a7524-111">**클라이언트 컴퓨터** - HPC 팩 클라이언트 유틸리티를 실행할 수 있는 Windows 또는 Windows Server 클라이언트 컴퓨터가 필요합니다([시스템 요구 사항](https://technet.microsoft.com/library/dn535781.aspx) 참조).</span><span class="sxs-lookup"><span data-stu-id="a7524-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="a7524-112">HPC 팩 웹 포털 또는 REST API를 사용하여 작업을 제출하려는 경우 사용자가 선택한 모든 클라이언트 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-112">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="a7524-113">**HPC 팩 설치 미디어** - HPC Pack 클라이언트 유틸리티를 설치하려면 [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024)에서 최신 버전의 HPC 팩(HPC 팩 2012 R2)용 무료 설치 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-113">**HPC Pack installation media** - To install the HPC Pack client utilities, the free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="a7524-114">헤드 노드 VM에 설치된 HPC 팩과 동일한 버전의 HPC 팩을 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-114">Make sure that you download the same version of HPC Pack that is installed on the head node VM.</span></span>

## <a name="step-1-install-and-configure-the-web-components-on-the-head-node"></a><span data-ttu-id="a7524-115">1단계: 헤드 노드에 웹 구성 요소 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="a7524-115">Step 1: Install and configure the web components on the head node</span></span>
<span data-ttu-id="a7524-116">HTTPS를 통해 클러스터로 작업을 제출하도록 REST 인터페이스를 설정하려면 HPC 팩 헤드 노드에 HPC 팩 웹 구성 요소를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-116">To enable a REST interface to submit jobs to the cluster over HTTPS, ensure that the HPC Pack web components are configured on the HPC Pack head node.</span></span> <span data-ttu-id="a7524-117">아직 설치되지 않았으면 먼저 HpcWebComponents.msi 설치 파일을 실행하여 웹 구성 요소를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-117">If they aren't already installed, first install the web components by running the HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="a7524-118">그런 다음 HPC PowerShell 스크립트 **Set-HPCWebComponents.ps1**을 실행하여 구성 요소를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-118">Then, configure the components by running the HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="a7524-119">자세한 절차는 [Microsoft HPC 팩 웹 구성 요소 설치](http://technet.microsoft.com/library/hh314627.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7524-119">For detailed procedures, see [Install the Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="a7524-120">일부 HPC Pack용 Azure 빠른 시작 템플릿은 웹 구성을 자동으로 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-120">Certain Azure quickstart templates for HPC Pack install and configure the web components automatically.</span></span> <span data-ttu-id="a7524-121">[HPC 팩 IaaS 배포 스크립트](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) 를 사용하여 클러스터를 만드는 경우 배포의 일환으로 웹 구성 요소를 선택적으로 설치 및 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-121">If you use the [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to create the cluster, you can optionally install and configure the web components as part of the deployment.</span></span>
> 
> 

<span data-ttu-id="a7524-122">**웹 구성 요소를 설치하려면**</span><span class="sxs-lookup"><span data-stu-id="a7524-122">**To install the web components**</span></span>

1. <span data-ttu-id="a7524-123">클러스터 관리자의 자격 증명을 사용하여 헤드 노드 VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-123">Connect to the head node VM by using the credentials of a cluster administrator.</span></span>
2. <span data-ttu-id="a7524-124">HPC 팩 설치 폴더에서 헤드 노드에 HpcWebComponents.msi를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-124">From the HPC Pack Setup folder, run HpcWebComponents.msi on the head node.</span></span>
3. <span data-ttu-id="a7524-125">마법사의 단계를 따라 웹 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="a7524-125">Follow the steps in the wizard to install the web components</span></span>

<span data-ttu-id="a7524-126">**웹 구성 요소를 구성하려면**</span><span class="sxs-lookup"><span data-stu-id="a7524-126">**To configure the web components**</span></span>

1. <span data-ttu-id="a7524-127">헤드 노드에서 관리자 권한으로 HPC PowerShell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-127">On the head node, start HPC PowerShell as an administrator.</span></span>
2. <span data-ttu-id="a7524-128">디렉터리를 구성 스크립트의 위치로 변경하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-128">To change directory to the location of the configuration script, type the following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. <span data-ttu-id="a7524-129">REST 인터페이스를 구성하고 HPC 웹 서비스를 시작하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-129">To configure the REST interface and start the HPC Web Service, type the following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. <span data-ttu-id="a7524-130">인증서를 선택하라는 메시지가 표시되면 헤드 노드의 공용 DNS 이름에 해당하는 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-130">When prompted to select a certificate, choose the certificate that corresponds to the public DNS name of the head node.</span></span> <span data-ttu-id="a7524-131">예를 들어 클래식 배포 모델을 사용하여 헤드 노드 VM을 배포하는 경우 인증서 이름은 CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-131">For example, if you deploy the head node VM using the classic deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="a7524-132">Resource Manager 배포 모델을 사용하는 경우 인증서 이름은 CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-132">If you use the Resource Manager deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a7524-133">나중에 온-프레미스 컴퓨터에서 헤드 노드로 작업을 제출할 때 이 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-133">You select this certificate later when you submit jobs to the head node from an on-premises computer.</span></span> <span data-ttu-id="a7524-134">Active Directory 도메인에 있는 헤드 노드의 컴퓨터 이름(예: CN=*MyHPCHeadNode.HpcAzure.local*)에 해당하는 인증서를 선택 또는 구성하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="a7524-134">Don't select or configure a certificate that corresponds to the computer name of the head node in the Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
5. <span data-ttu-id="a7524-135">작업 제출을 위해 웹 포털을 구성하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-135">To configure the web portal for job submission, type the following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. <span data-ttu-id="a7524-136">스크립트가 완료되면 다음 명령을 입력하여 HPC 작업 Scheduler 서비스를 중지했다 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-136">After the script completes, stop and restart the HPC Job Scheduler Service by typing the following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-the-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="a7524-137">2단계: 온-프레미스 컴퓨터에 HPC 팩 클라이언트 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="a7524-137">Step 2: Install the HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="a7524-138">컴퓨터에 HPC Pack 클라이언트 유틸리티를 설치하려면 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=328024)에서 HPC Pack 설치 파일(전체 설치)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-138">If you want to install the HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="a7524-139">설치를 시작할 때 **HPC Pack 클라이언트 유틸리티**에 대한 설정 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-139">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span></span>

<span data-ttu-id="a7524-140">HPC 팩 클라이언트 도구를 사용하여 헤드 노드 VM으로 작업을 제출하려면 헤드 노드에서 인증서를 내보내고 클라이언트 컴퓨터에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-140">To use the HPC Pack client tools to submit jobs to the head node VM, you also need to export a certificate from the head node and install it on the client computer.</span></span> <span data-ttu-id="a7524-141">인증서는 .CER 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-141">The certificate must be in .CER format.</span></span>

<span data-ttu-id="a7524-142">**헤드 노드에서 인증서를 내보내려면**</span><span class="sxs-lookup"><span data-stu-id="a7524-142">**To export the certificate from the head node**</span></span>

1. <span data-ttu-id="a7524-143">헤드 노드에서 로컬 컴퓨터 계정의 Microsoft Management Console에 인증서 스냅인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-143">On the head node, add the Certificates snap-in to a Microsoft Management Console for the Local Computer account.</span></span> <span data-ttu-id="a7524-144">스냅인을 추가하는 단계는 [MMC에 인증서 스냅인 추가](https://technet.microsoft.com/library/cc754431.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7524-144">For steps to add the snap-in, see [Add the Certificates Snap-in to an MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
2. <span data-ttu-id="a7524-145">콘솔 트리에서 **인증서 - 로컬 컴퓨터** > **개인**을 확장한 다음 **인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-145">In the console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
3. <span data-ttu-id="a7524-146">[1단계: 헤드 노드에 웹 구성 요소 설치 및 구성](#step-1:-install-and-configure-the-web-components-on-the-head-node)에서 HPC Pack 웹 구성 요소에 구성한 인증서를 찾습니다(예: CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="a7524-146">Locate the certificate that you configured for the HPC Pack web components in [Step 1: Install and configure the web components on the head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
4. <span data-ttu-id="a7524-147">인증서를 마우스 오른쪽 단추로 클릭하고 **모든 작업** > **내보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-147">Right-click the certificate, and click **All Tasks** > **Export**.</span></span>
5. <span data-ttu-id="a7524-148">인증서 내보내기 마법사에서 **다음**을 클릭하고 **아니요, 개인 키를 내보내지 않습니다.**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-148">In the Certificate Export Wizard, click **Next**, and ensure that **No, do not export the private key** is selected.</span></span>
6. <span data-ttu-id="a7524-149">마법사의 나머지 단계를 따라 인증서를 DER 인코딩 이진 X.509(.CER) 형식으로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-149">Follow the remaining steps of the wizard to export the certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="a7524-150">**클라이언트 컴퓨터로 인증서를 가져오려면**</span><span class="sxs-lookup"><span data-stu-id="a7524-150">**To import the certificate on the client computer**</span></span>

1. <span data-ttu-id="a7524-151">헤드 노드에서 클라이언트 컴퓨터의 폴더로 내보낸 인증서를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-151">Copy the certificate that you exported from the head node to a folder on the client computer.</span></span>
2. <span data-ttu-id="a7524-152">클라이언트 컴퓨터에서 certmgr.msc를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-152">On the client computer, run certmgr.msc.</span></span>
3. <span data-ttu-id="a7524-153">인증서 관리자에서 **인증서 - 현재 사용자** > **신뢰할 수 있는 루트 인증 기관**을 확장한 후 **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업** > **가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
4. <span data-ttu-id="a7524-154">인증서 가져오기 마법사에서 **다음** 을 클릭하고 헤드 노드에서 신뢰할 수 있는 루트 인증 기관 저장소로 내보낸 인증서를 가져오는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-154">In the Certificate Import Wizard, click **Next** and follow the steps to import the certificate that you exported from the head node to the Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="a7524-155">클라이언트 컴퓨터가 헤드 노드의 인증 기관을 인식할 수 없기 때문에 보안 경고가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-155">You might see a security warning, because the certification authority on the head node isn't recognized by the client computer.</span></span> <span data-ttu-id="a7524-156">테스트 목적으로 이 경고를 무시하고 인증서 가져오기를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-156">For testing purposes, you can ignore this warning and complete the certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-the-cluster"></a><span data-ttu-id="a7524-157">3단계: 클러스터에서 테스트 작업 실행</span><span class="sxs-lookup"><span data-stu-id="a7524-157">Step 3: Run test jobs on the cluster</span></span>
<span data-ttu-id="a7524-158">구성을 확인하려면 온-프레미스 컴퓨터에서 Azure의 클러스터에 작업을 실행해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-158">To verify your configuration, try running jobs on the cluster in Azure from the on-premises computer.</span></span> <span data-ttu-id="a7524-159">예를 들어 HPC 팩 GUI 도구 또는 명령줄 명령을 사용하여 클러스터로 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-159">For example, you can use HPC Pack GUI tools or command-line commands to submit jobs to the cluster.</span></span> <span data-ttu-id="a7524-160">웹 기반 포털을 사용하여 작업을 제출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-160">You can also use a web-based portal to submit jobs.</span></span>

<span data-ttu-id="a7524-161">**클라이언트 컴퓨터에서 작업 제출 명령을 실행하려면**</span><span class="sxs-lookup"><span data-stu-id="a7524-161">**To run job submission commands on the client computer**</span></span>

1. <span data-ttu-id="a7524-162">HPC Pack 클라이언트 유틸리티가 설치되어 있는 클라이언트 컴퓨터에서 명령 프롬프트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-162">On a client computer where the HPC Pack client utilities are installed, start a Command Prompt.</span></span>
2. <span data-ttu-id="a7524-163">샘플 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-163">Type a sample command.</span></span> <span data-ttu-id="a7524-164">예를 들어, 클러스터의 모든 작업을 나열하려면, 헤드 노드의 전체 DNS 이름에 따라서 다음 중 하나와 유사한 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-164">For example, to list all jobs on the cluster, type a command similar to one of the following, depending on the full DNS name of the head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="a7524-165">또는</span><span class="sxs-lookup"><span data-stu-id="a7524-165">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="a7524-166">스케줄러 URL에 IP 주소가 아닌 헤드 노드의 전체 DNS 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-166">Use the full DNS name of the head node, not the IP address, in the scheduler URL.</span></span> <span data-ttu-id="a7524-167">IP 주소를 지정할 경우 "서버 인증서에 유효한 신뢰 체인이 있거나 서버 인증서를 신뢰할 수 있는 루트 저장소에 저장해야 합니다."와 유사한 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-167">If you specify the IP address, an error appears similar to "The server certificate needs to either have a valid chain of trust or to be placed in the trusted root store."</span></span>
   > 
   > 
3. <span data-ttu-id="a7524-168">메시지가 표시되면 구성해 놓은 HPC 클러스터 관리자 또는 다른 클러스터 사용자의 사용자 이름(&lt;DomainName&gt;\\&lt;UserName&gt; 형식)과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-168">When prompted, type the user name (in the form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of the HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="a7524-169">추가 작업에 대해 자격 증명을 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-169">You can choose to store the credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="a7524-170">작업 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-170">A list of jobs appears.</span></span>

<span data-ttu-id="a7524-171">**클라이언트 컴퓨터에서 HPC 작업 관리자를 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="a7524-171">**To use HPC Job Manager on the client computer**</span></span>

1. <span data-ttu-id="a7524-172">작업을 제출할 때 이전에 클러스터 사용자의 도메인 자격 증명을 저장해 놓지 경우 자격 증명 관리자에서 자격 증명을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add the credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="a7524-173">a.</span><span class="sxs-lookup"><span data-stu-id="a7524-173">a.</span></span> <span data-ttu-id="a7524-174">클라이언트 컴퓨터의 제어판에서 자격 증명 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-174">In Control Panel on the client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="a7524-175">b.</span><span class="sxs-lookup"><span data-stu-id="a7524-175">b.</span></span> <span data-ttu-id="a7524-176">**Windows 자격 증명** > **일반 자격 증명 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-176">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="a7524-177">c.</span><span class="sxs-lookup"><span data-stu-id="a7524-177">c.</span></span> <span data-ttu-id="a7524-178">구성한 클러스터 관리자 또는 다른 클러스터 사용자의 인터넷 주소(예: https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler 또는 https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler)와 사용자 이름(&lt;도메인 이름&gt;\\&lt;사용자 이름&gt;) 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-178">Specify the Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and the user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of the cluster administrator or another cluster user that you configured.</span></span>
2. <span data-ttu-id="a7524-179">클라이언트 컴퓨터에서 HPC 작업 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-179">On the client computer, start HPC Job Manager.</span></span>
3. <span data-ttu-id="a7524-180">**헤드 노드 선택** 대화 상자에서 Azure 헤드 노드의 URL을 입력합니다(예: https://&lt;HeadNodeDnsName&gt;.cloudapp.net 또는 https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a7524-180">In the **Select Head Node** dialog box, type the URL to the head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="a7524-181">HPC 작업 관리자가 열리고 헤드 노드의 작업 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-181">HPC Job Manager opens and shows a list of jobs on the head node.</span></span>

<span data-ttu-id="a7524-182">**헤드 노드에서 실행되는 웹 포털을 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="a7524-182">**To use the web portal running on the head node**</span></span>

1. <span data-ttu-id="a7524-183">클라이언트 컴퓨터에서 웹 브라우저를 시작하고, 헤드 노드의 전체 DNS 이름에 따라서 다음 주소 중 하나를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-183">Start a web browser on the client computer, and enter one of the following addresses, depending on the full DNS name of the head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="a7524-184">또는</span><span class="sxs-lookup"><span data-stu-id="a7524-184">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. <span data-ttu-id="a7524-185">보안 대화 상자가 나타나면 HPC 클러스터 관리자의 도메인 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-185">In the security dialog box that appears, type the domain credentials of the HPC cluster administrator.</span></span> <span data-ttu-id="a7524-186">(다른 역할의 다른 클러스터 사용자를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-186">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="a7524-187">[클러스터 사용자 관리](https://technet.microsoft.com/library/ff919335.aspx)를 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="a7524-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="a7524-188">웹 포털이 작업 목록 보기로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-188">The web portal opens to the job list view.</span></span>
3. <span data-ttu-id="a7524-189">클러스터에서 "Hello World" 문자열을 반환하는 샘플 작업을 제출하려면 왼쪽 탐색 창에서 **새 작업** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-189">To submit a sample job that returns the string “Hello World” from the cluster, click **New job** in the left-hand navigation.</span></span>
4. <span data-ttu-id="a7524-190">**새 작업** 페이지의 **제출 페이지에서**에서 **HelloWorld**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-190">On the **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="a7524-191">작업 제출 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-191">The job submission page appears.</span></span>
5. <span data-ttu-id="a7524-192">**Submit**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-192">Click **Submit**.</span></span> <span data-ttu-id="a7524-193">메시지가 표시되면 HPC 클러스터 관리자의 도메인 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-193">If prompted, provide the domain credentials of the HPC cluster administrator.</span></span> <span data-ttu-id="a7524-194">작업이 제출되고 **내 작업** 페이지에 작업 ID가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-194">The job is submitted, and the job ID appears on the **My Jobs** page.</span></span>
6. <span data-ttu-id="a7524-195">제출한 작업의 결과를 보려면 작업 ID를 클릭한 다음 **작업 보기**를 클릭하여(**출력**에서) 명령 출력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-195">To view the results of the job that you submitted, click the job ID, and then click **View Tasks** to view the command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7524-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a7524-196">Next steps</span></span>
* <span data-ttu-id="a7524-197">[HPC 팩 REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx)를 사용해도 Azure 클러스터에 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7524-197">You can also submit jobs to the Azure cluster with the [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="a7524-198">Linux 클라이언트에서 클러스터 작업을 제출하려는 경우 [HPC Pack 2012 R2 SDK 및 샘플 코드](https://www.microsoft.com/download/details.aspx?id=41633)의 Python 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7524-198">If you want to submit cluster jobs from a Linux client, see the Python sample in the [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
