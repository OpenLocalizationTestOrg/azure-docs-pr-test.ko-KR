---
title: "Azure에서 Service Fabric 클러스터 만들기 | Microsoft Docs"
description: "PowerShell을 사용하여 Azure에서 Windows 또는 Linux Service Fabric 클러스터를 만드는 방법을 알아봅니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: f62249417552b9cf840bfac3b94c27f63bd7064e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="03eb0-103">PowerShell을 사용하여 Azure에서 보안 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="03eb0-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="03eb0-104">이 자습서에서는 Azure에서 실행되는 Service Fabric 클러스터(Windows 또는 Linux)를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-104">This tutorial shows you how to create a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="03eb0-105">작업이 완료되면 응용 프로그램을 배포할 수 있는, 클라우드에서 실행되는 클러스터가 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-105">When you're finished, you have a cluster running in the cloud that you can deploy applications to.</span></span>

<span data-ttu-id="03eb0-106">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="03eb0-107">PowerShell을 사용하여 Azure에서 안전한 Service Fabric 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="03eb0-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="03eb0-108">X.509 인증서를 사용하여 클러스터 보호</span><span class="sxs-lookup"><span data-stu-id="03eb0-108">Secure the cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="03eb0-109">PowerShell을 사용하여 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="03eb0-109">Connect to the cluster using PowerShell</span></span>
> * <span data-ttu-id="03eb0-110">클러스터 제거</span><span class="sxs-lookup"><span data-stu-id="03eb0-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03eb0-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="03eb0-111">Prerequisites</span></span>
<span data-ttu-id="03eb0-112">이 자습서를 시작하기 전에:</span><span class="sxs-lookup"><span data-stu-id="03eb0-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="03eb0-113">Azure 구독이 없는 경우 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="03eb0-114">[Service Fabric SDK 및 PowerShell 모듈](service-fabric-get-started.md)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-114">Install the [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="03eb0-115">[Azure PowerShell 모듈 버전 4.1 이상](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-115">Install the [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="03eb0-116">다음 절차에서는 단일 노드(단일 가상 컴퓨터) 미리 보기 Service Fabric 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-116">The following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="03eb0-117">클러스터는 클러스터와 함께 생성된 다음 키 자격 증명 모음에 배치되는 자체 서명된 인증서에 의해 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-117">The cluster is secured by a self-signed certificate that gets created along with the cluster and then placed in a key vault.</span></span> <span data-ttu-id="03eb0-118">단일 노드 클러스터는 여러 가상 컴퓨터로 확장할 수 없으며 미리 보기 클러스터는 새 버전으로 업그레이드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded to newer versions.</span></span>

<span data-ttu-id="03eb0-119">Azure에서 Service Fabric 클러스터를 실행할 때 발생하는 비용을 계산하려면 [Azure 가격 계산기](https://azure.microsoft.com/pricing/calculator/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-119">To calculate cost incurred by running a Service Fabric cluster in Azure use the [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="03eb0-120">Service Fabric 클러스터를 만드는 방법에 대한 자세한 내용은 [Azure Resource Manager를 사용하여 Service Fabric 클러스터 만들기](service-fabric-cluster-creation-via-arm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03eb0-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-the-cluster-using-azure-powershell"></a><span data-ttu-id="03eb0-121">Azure PowerShell을 사용하여 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="03eb0-121">Create the cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="03eb0-122">[Service Fabric용 Azure Resource Manager 템플릿](https://aka.ms/securepreviewonelineclustertemplate) GitHub 리포지토리에서 Azure Resource Manager 템플릿 및 매개 변수 파일의 로컬 복사본을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-122">Download a local copy of the Azure Resource Manager template and the parameter file from the [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="03eb0-123">*azuredeploy.json*은 Service Fabric 클러스터를 정의하는 Azure Resource Manager 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-123">*azuredeploy.json* is the Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="03eb0-124">*azuredeploy.parameters.json*은 클러스터 배포를 사용자 지정하는 데 사용할 매개 변수 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-124">*azuredeploy.parameters.json* is a parameters file for you to customize the cluster deployment.</span></span>

2. <span data-ttu-id="03eb0-125">*azuredeploy.parameters.json* 매개 변수 파일에서 다음 매개 변수를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-125">Customize the following parameters in the *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="03eb0-126">매개 변수</span><span class="sxs-lookup"><span data-stu-id="03eb0-126">Parameter</span></span>       | <span data-ttu-id="03eb0-127">설명</span><span class="sxs-lookup"><span data-stu-id="03eb0-127">Description</span></span> | <span data-ttu-id="03eb0-128">제안 값</span><span class="sxs-lookup"><span data-stu-id="03eb0-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="03eb0-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="03eb0-129">clusterLocation</span></span> | <span data-ttu-id="03eb0-130">클러스터를 배포할 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-130">The Azure region to which to deploy the cluster.</span></span> | <span data-ttu-id="03eb0-131">*예: westeurope, eastasia, eastus*</span><span class="sxs-lookup"><span data-stu-id="03eb0-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="03eb0-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="03eb0-132">clusterName</span></span>     | <span data-ttu-id="03eb0-133">만들려는 클러스터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-133">Name of the cluster you want to create.</span></span> | <span data-ttu-id="03eb0-134">*예: bobs-sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="03eb0-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="03eb0-135">adminUserName</span><span class="sxs-lookup"><span data-stu-id="03eb0-135">adminUserName</span></span>   | <span data-ttu-id="03eb0-136">클러스터 가상 컴퓨터의 로컬 관리자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-136">The local admin account on the cluster virtual machines.</span></span> | <span data-ttu-id="03eb0-137">*모든 유효한 Windows Server 사용자 이름*</span><span class="sxs-lookup"><span data-stu-id="03eb0-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="03eb0-138">adminPassword</span><span class="sxs-lookup"><span data-stu-id="03eb0-138">adminPassword</span></span>   | <span data-ttu-id="03eb0-139">클러스터 가상 컴퓨터의 로컬 관리자 계정 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-139">Password of the local admin account on the cluster virtual machines.</span></span> | <span data-ttu-id="03eb0-140">*모든 유효한 Windows Server 암호*</span><span class="sxs-lookup"><span data-stu-id="03eb0-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="03eb0-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="03eb0-141">clusterCodeVersion</span></span> | <span data-ttu-id="03eb0-142">실행할 Service Fabric 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-142">The Service Fabric version to run.</span></span> <span data-ttu-id="03eb0-143">(미리 보기 버전은 255.255.X.255)</span><span class="sxs-lookup"><span data-stu-id="03eb0-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="03eb0-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="03eb0-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="03eb0-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="03eb0-145">vmInstanceCount</span></span> | <span data-ttu-id="03eb0-146">클러스터의 가상 컴퓨터 수(1 또는 3-99일 수 있음)입니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-146">The number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="03eb0-147">**1**</span><span class="sxs-lookup"><span data-stu-id="03eb0-147">**1**</span></span> | <span data-ttu-id="03eb0-148">*미리 보기 클러스터에 하나의 가상 컴퓨터를 지정합니다.*</span><span class="sxs-lookup"><span data-stu-id="03eb0-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="03eb0-149">PowerShell 콘솔을 열고 Azure에 로그인한 다음 클러스터를 배포할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-149">Open a PowerShell console, login to Azure, and select the subscription you want to deploy the cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="03eb0-150">Service Fabric에서 사용되는 인증서의 암호를 만들고 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-150">Create and encrypt a password for the certificate to be used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="03eb0-151">다음 명령을 실행하여 클러스터 및 해당 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-151">Create the cluster and its certificate by running the following command:</span></span>

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   ><span data-ttu-id="03eb0-152">`-CertificateSubjectName` 매개 변수는 매개 변수 파일에 지정된 clusterName 매개 변수와 일치해야 하며, 도메인은 선택한 Azure 지역(예: `clustername.eastus.cloudapp.azure.com`)에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-152">The `-CertificateSubjectName` parameter should align with the clusterName parameter specified in the parameters file, as well as the domain tied to the Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="03eb0-153">구성이 완료되면 Azure에서 만든 클러스터에 대한 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-153">Once the configuration finishes, it outputs information about the cluster created in Azure.</span></span> <span data-ttu-id="03eb0-154">또한 클러스터 인증서를 이 매개 변수에 지정한 경로의 CertificateOutputFolder 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-154">It also copies the cluster certificate to the -CertificateOutputFolder directory on the path you specified for this parameter.</span></span> <span data-ttu-id="03eb0-155">Service Fabric Explorer에 액세스하고 클러스터의 상태를 확인하려면 이 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-155">You need this certificate to access Service Fabric Explorer and view the health of your cluster.</span></span>

<span data-ttu-id="03eb0-156">다음 URL과 유사한 클러스터의 URL을 기록해 둡니다. *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="03eb0-156">Take note of the URL for your cluster, which may be similar to the following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-the-certificate--access-service-fabric-explorer"></a><span data-ttu-id="03eb0-157">인증서 수정 및 Service Fabric Explorer에 액세스</span><span class="sxs-lookup"><span data-stu-id="03eb0-157">Modify the certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="03eb0-158">인증서를 두 번 클릭하여 인증서 가져오기 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-158">Double-click the certificate to open the Certificate Import Wizard.</span></span>

2. <span data-ttu-id="03eb0-159">기본 설정을 사용하지만 **이 키를 내보낼 수 있도록 표시**</span><span class="sxs-lookup"><span data-stu-id="03eb0-159">Use default settings, but make sure to check the **Mark this key as exportable.**</span></span> <span data-ttu-id="03eb0-160">확인란을 **개인 키 보호** 단계에서 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-160">check box, in the **private key protection** step.</span></span> <span data-ttu-id="03eb0-161">이 자습서의 뒷부분에 나오는 Azure Container Registry를 Service Fabric 클러스터 인증으로 구성할 때 Visual Studio에서 인증서를 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-161">Visual Studio needs to export the certificate when configuring Azure Container Registry to Service Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="03eb0-162">이제 브라우저에서 Service Fabric Explorer를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="03eb0-163">이렇게 하려면 웹 브라우저를 사용하여 클러스터에 대한 **ManagementEndpoint** URL로 이동하고 컴퓨터에 저장된 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-163">To do so, navigate to the **ManagementEndpoint** URL for your cluster using a web browser, and select the certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="03eb0-164">Service Fabric Explorer를 열면 인증서 오류가 표시되는데 이는 자체 서명된 인증서를 사용하고 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="03eb0-165">Edge에서는 *세부 정보*를 클릭한 다음 *웹 페이지로 이동* 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-165">In Edge, you have to click *Details* and then the *Go on to the webpage* link.</span></span> <span data-ttu-id="03eb0-166">Chrome에서는 *고급* 및 *진행* 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-166">In Chrome, you have to click *Advanced* and then the *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="03eb0-167">클러스터 작성이 실패한 경우 이미 배포된 리소스를 업데이트하는 명령을 언제든지 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-167">If the cluster creation fails, you can always rerun the command, which updates the resources already deployed.</span></span> <span data-ttu-id="03eb0-168">실패한 배포의 일부로 인증서가 만들어진 경우 새 인증서가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-168">If a certificate was created as part of the failed deployment, a new one is generated.</span></span> <span data-ttu-id="03eb0-169">클러스터 만들기 문제를 해결하려면 [Azure Resource Manager를 사용하여 Service Fabric 클러스터 만들기](service-fabric-cluster-creation-via-arm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03eb0-169">To troubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-to-the-secure-cluster"></a><span data-ttu-id="03eb0-170">보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="03eb0-170">Connect to the secure cluster</span></span>
<span data-ttu-id="03eb0-171">Service Fabric SDK가 설치된 Service Fabric PowerShell 모듈을 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-171">Connect to the cluster using the Service Fabric PowerShell module installed with the Service Fabric SDK.</span></span>  <span data-ttu-id="03eb0-172">먼저 사용자 컴퓨터에서 현재 사용자의 개인(내) 저장소에 인증서를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-172">First, install the certificate into the Personal (My) store of the current user on your computer.</span></span>  <span data-ttu-id="03eb0-173">다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-173">Run the following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="03eb0-174">이제 보안 클러스터에 연결할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-174">You are now ready to connect to your secure cluster.</span></span>

<span data-ttu-id="03eb0-175">**Service Fabric** PowerShell 모듈은 Service Fabric 클러스터, 응용 프로그램 및 서비스를 관리하기 위한 많은 cmdlet을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-175">The **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="03eb0-176">[Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet을 사용하여 보안 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-176">Use the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet to connect to the secure cluster.</span></span> <span data-ttu-id="03eb0-177">인증서 지문 및 연결 끝점 세부 정보는 이전 단계의 출력에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-177">The certificate thumbprint and connection endpoint details are found in the output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="03eb0-178">[Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet을 사용하여 사용자가 연결되어 있고 클러스터가 정상 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-178">Check that you are connected and the cluster is healthy using the [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="03eb0-179">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="03eb0-179">Clean up resources</span></span>

<span data-ttu-id="03eb0-180">클러스터는 클러스터 리소스 외에도 다른 Azure 리소스로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-180">A cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="03eb0-181">클러스터 및 클러스터에서 사용하는 모든 리소스를 삭제하는 가장 간단한 방법은 리소스 그룹을 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-181">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span>

<span data-ttu-id="03eb0-182">Azure에 로그인하고 클러스터를 제거할 구독 ID를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-182">Log in to Azure and select the subscription ID with which you want to remove the cluster.</span></span>  <span data-ttu-id="03eb0-183">[Azure Portal](http://portal.azure.com)에 로그인하여 구독 ID를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-183">You can find your subscription ID by logging in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="03eb0-184">[Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup)을 사용하여 리소스 그룹 및 모든 클러스터 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-184">Delete the resource group and all the cluster resources using the [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="03eb0-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03eb0-185">Next steps</span></span>
<span data-ttu-id="03eb0-186">이 자습서에서는 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="03eb0-187">Azure에서 Service Fabric 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="03eb0-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="03eb0-188">X.509 인증서를 사용하여 클러스터 보호</span><span class="sxs-lookup"><span data-stu-id="03eb0-188">Secure the cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="03eb0-189">PowerShell을 사용하여 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="03eb0-189">Connect to the cluster using PowerShell</span></span>
> * <span data-ttu-id="03eb0-190">클러스터 제거</span><span class="sxs-lookup"><span data-stu-id="03eb0-190">Remove a cluster</span></span>

<span data-ttu-id="03eb0-191">이제 다음 자습서로 이동하여 기존 응용 프로그램을 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="03eb0-191">Next, advance to the following tutorial to learn how to deploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="03eb0-192">Docker Compose를 사용하여 기존 .NET 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="03eb0-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)
