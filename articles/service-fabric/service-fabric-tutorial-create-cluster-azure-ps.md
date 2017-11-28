---
title: "Azure에서 aaaCreate 서비스 패브릭 클러스터 | Microsoft Docs"
description: "PowerShell을 사용 하 여 Azure에 있는 toocreate Windows 또는 Linux 서비스 패브릭 클러스터 하는 방법을 알아봅니다."
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
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="50a7c-103">PowerShell을 사용하여 Azure에서 보안 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="50a7c-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="50a7c-104">이 자습서에서는 어떻게 toocreate 서비스 패브릭 클러스터를 실행 (Windows 또는 Linux) Azure에서.</span><span class="sxs-lookup"><span data-stu-id="50a7c-104">This tutorial shows you how toocreate a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="50a7c-105">작업을 완료 하는 경우 응용 프로그램을 배포할 수 있는 hello 클라우드에서 실행 하는 클러스터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-105">When you're finished, you have a cluster running in hello cloud that you can deploy applications to.</span></span>

<span data-ttu-id="50a7c-106">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="50a7c-107">PowerShell을 사용하여 Azure에서 안전한 Service Fabric 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="50a7c-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="50a7c-108">X.509 인증서로 hello 클러스터 보안</span><span class="sxs-lookup"><span data-stu-id="50a7c-108">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="50a7c-109">PowerShell을 사용 하 여 toohello 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="50a7c-109">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="50a7c-110">클러스터 제거</span><span class="sxs-lookup"><span data-stu-id="50a7c-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50a7c-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="50a7c-111">Prerequisites</span></span>
<span data-ttu-id="50a7c-112">이 자습서를 시작하기 전에:</span><span class="sxs-lookup"><span data-stu-id="50a7c-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="50a7c-113">Azure 구독이 없는 경우 [평가판 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="50a7c-114">Hello 설치 [서비스 패브릭 SDK 및 PowerShell 모듈](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="50a7c-114">Install hello [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="50a7c-115">Hello 설치 [Azure Powershell 모듈 버전 4.1 이상](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="50a7c-115">Install hello [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="50a7c-116">절차를 수행 하는 hello 단일 노드 (단일 가상 컴퓨터) 미리 보기 서비스 패브릭 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-116">hello following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="50a7c-117">hello 클러스터 hello 클러스터와 함께 생성를 가져오고 다음 키 자격 증명 모음에 배치 하는 자체 서명 된 인증서에 의해 보안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-117">hello cluster is secured by a self-signed certificate that gets created along with hello cluster and then placed in a key vault.</span></span> <span data-ttu-id="50a7c-118">단일 노드 클러스터의 가상 컴퓨터를 하나 이상 확장할 수 없습니다 및 미리 보기 클러스터 업그레이드 toonewer 버전 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded toonewer versions.</span></span>

<span data-ttu-id="50a7c-119">서비스 패브릭 클러스터를 사용 하 여 Azure hello에서 실행 하 여 발생 하는 toocalculate 비용 [Azure 가격 계산기](https://azure.microsoft.com/pricing/calculator/)합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-119">toocalculate cost incurred by running a Service Fabric cluster in Azure use hello [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="50a7c-120">Service Fabric 클러스터를 만드는 방법에 대한 자세한 내용은 [Azure Resource Manager를 사용하여 Service Fabric 클러스터 만들기](service-fabric-cluster-creation-via-arm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="50a7c-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-hello-cluster-using-azure-powershell"></a><span data-ttu-id="50a7c-121">Azure PowerShell을 사용 하 여 hello 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="50a7c-121">Create hello cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="50a7c-122">Hello에서 hello Azure 리소스 관리자 템플릿 및 hello 매개 변수 파일의 로컬 복사본을 다운로드 [서비스 패브릭 용 Azure 리소스 관리자 템플릿](https://aka.ms/securepreviewonelineclustertemplate) GitHub 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-122">Download a local copy of hello Azure Resource Manager template and hello parameter file from hello [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="50a7c-123">*azuredeploy.json* 서비스 패브릭 클러스터를 정의 하는 hello Azure 리소스 관리자 템플릿이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-123">*azuredeploy.json* is hello Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="50a7c-124">*azuredeploy.parameters.json* toocustomize hello 클러스터 배포는 매개 변수 파일 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-124">*azuredeploy.parameters.json* is a parameters file for you toocustomize hello cluster deployment.</span></span>

2. <span data-ttu-id="50a7c-125">Hello hello에 대 한 매개 변수 뒤에 사용자 지정 *azuredeploy.parameters.json* 매개 변수 파일:</span><span class="sxs-lookup"><span data-stu-id="50a7c-125">Customize hello following parameters in hello *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="50a7c-126">매개 변수</span><span class="sxs-lookup"><span data-stu-id="50a7c-126">Parameter</span></span>       | <span data-ttu-id="50a7c-127">설명</span><span class="sxs-lookup"><span data-stu-id="50a7c-127">Description</span></span> | <span data-ttu-id="50a7c-128">제안 값</span><span class="sxs-lookup"><span data-stu-id="50a7c-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="50a7c-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="50a7c-129">clusterLocation</span></span> | <span data-ttu-id="50a7c-130">hello Azure 지역 toowhich toodeploy hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-130">hello Azure region toowhich toodeploy hello cluster.</span></span> | <span data-ttu-id="50a7c-131">*예: westeurope, eastasia, eastus*</span><span class="sxs-lookup"><span data-stu-id="50a7c-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="50a7c-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="50a7c-132">clusterName</span></span>     | <span data-ttu-id="50a7c-133">이름을 원하는 toocreate hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-133">Name of hello cluster you want toocreate.</span></span> | <span data-ttu-id="50a7c-134">*예: bobs-sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="50a7c-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="50a7c-135">adminUserName</span><span class="sxs-lookup"><span data-stu-id="50a7c-135">adminUserName</span></span>   | <span data-ttu-id="50a7c-136">가상 컴퓨터를 클러스터링 하는 hello에 대 한 hello 로컬 관리자 계정.</span><span class="sxs-lookup"><span data-stu-id="50a7c-136">hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="50a7c-137">*모든 유효한 Windows Server 사용자 이름*</span><span class="sxs-lookup"><span data-stu-id="50a7c-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="50a7c-138">adminPassword</span><span class="sxs-lookup"><span data-stu-id="50a7c-138">adminPassword</span></span>   | <span data-ttu-id="50a7c-139">가상 컴퓨터를 클러스터링 하는 hello에 대 한 hello 로컬 관리자 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-139">Password of hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="50a7c-140">*모든 유효한 Windows Server 암호*</span><span class="sxs-lookup"><span data-stu-id="50a7c-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="50a7c-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="50a7c-141">clusterCodeVersion</span></span> | <span data-ttu-id="50a7c-142">서비스 패브릭 버전 toorun hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-142">hello Service Fabric version toorun.</span></span> <span data-ttu-id="50a7c-143">(미리 보기 버전은 255.255.X.255)</span><span class="sxs-lookup"><span data-stu-id="50a7c-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="50a7c-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="50a7c-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="50a7c-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="50a7c-145">vmInstanceCount</span></span> | <span data-ttu-id="50a7c-146">(1 개 또는 3-99 일 수 있음) 클러스터의 가상 컴퓨터의 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-146">hello number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="50a7c-147">**1**</span><span class="sxs-lookup"><span data-stu-id="50a7c-147">**1**</span></span> | <span data-ttu-id="50a7c-148">*미리 보기 클러스터에 하나의 가상 컴퓨터를 지정합니다.*</span><span class="sxs-lookup"><span data-stu-id="50a7c-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="50a7c-149">PowerShell 콘솔, 로그인 tooAzure 열고 toodeploy hello 클러스터에서 원하는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-149">Open a PowerShell console, login tooAzure, and select hello subscription you want toodeploy hello cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="50a7c-150">페이지를 만들고 서비스 패브릭에서 사용 하는 hello 인증서 toobe에 대 한 암호를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-150">Create and encrypt a password for hello certificate toobe used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="50a7c-151">Hello 다음 명령을 실행 하 여 hello 클러스터 및 해당 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-151">Create hello cluster and its certificate by running hello following command:</span></span>

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
   ><span data-ttu-id="50a7c-152">hello `-CertificateSubjectName` hello 매개 변수 파일에 지정 된 hello clusterName 매개 변수 매개 변수 맞춰짐을도 hello 도메인 연결 toohello Azure 지역으로 선택한와 같은: `clustername.eastus.cloudapp.azure.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-152">hello `-CertificateSubjectName` parameter should align with hello clusterName parameter specified in hello parameters file, as well as hello domain tied toohello Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="50a7c-153">Hello 구성 완료 되 면 Azure에서 만든 hello 클러스터에 대 한 정보를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-153">Once hello configuration finishes, it outputs information about hello cluster created in Azure.</span></span> <span data-ttu-id="50a7c-154">또한이 매개 변수에 대해 지정 된 hello 경로에 hello 클러스터 인증서 toohello-CertificateOutputFolder 디렉터리를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-154">It also copies hello cluster certificate toohello -CertificateOutputFolder directory on hello path you specified for this parameter.</span></span> <span data-ttu-id="50a7c-155">이 인증서 tooaccess 클러스터의 서비스 패브릭 탐색기 및 보기 hello 상태 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-155">You need this certificate tooaccess Service Fabric Explorer and view hello health of your cluster.</span></span>

<span data-ttu-id="50a7c-156">비슷한 toohello 일 수 있는 클러스터에 대 한 hello URL을 기록해 url: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="50a7c-156">Take note of hello URL for your cluster, which may be similar toohello following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a><span data-ttu-id="50a7c-157">서비스 패브릭 탐색기 액세스 및 hello 인증서 수정</span><span class="sxs-lookup"><span data-stu-id="50a7c-157">Modify hello certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="50a7c-158">Hello 인증서 tooopen hello 인증서 가져오기 마법사를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-158">Double-click hello certificate tooopen hello Certificate Import Wizard.</span></span>

2. <span data-ttu-id="50a7c-159">기본 설정을 사용 하지만 있는지 toocheck hello **이 키를 내보낼 수 있도록 표시 합니다.**</span><span class="sxs-lookup"><span data-stu-id="50a7c-159">Use default settings, but make sure toocheck hello **Mark this key as exportable.**</span></span> <span data-ttu-id="50a7c-160">확인란 hello **개인 키 보호** 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-160">check box, in hello **private key protection** step.</span></span> <span data-ttu-id="50a7c-161">이 자습서의 뒷부분에 나오는 Azure 컨테이너 레지스트리 tooService 패브릭 클러스터 인증을 구성할 때 visual Studio tooexport hello 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-161">Visual Studio needs tooexport hello certificate when configuring Azure Container Registry tooService Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="50a7c-162">이제 브라우저에서 Service Fabric Explorer를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="50a7c-163">toodo toohello를 따라서 이동 **ManagementEndpoint** 웹 브라우저를 컴퓨터에 저장 된 select hello 인증서를 사용 하 여 클러스터에 대 한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-163">toodo so, navigate toohello **ManagementEndpoint** URL for your cluster using a web browser, and select hello certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="50a7c-164">Service Fabric Explorer를 열면 인증서 오류가 표시되는데 이는 자체 서명된 인증서를 사용하고 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="50a7c-165">Edge에서는 tooclick 있는 *세부 정보* 다음 hello 및 *toohello 웹 페이지에서 이동* 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-165">In Edge, you have tooclick *Details* and then hello *Go on toohello webpage* link.</span></span> <span data-ttu-id="50a7c-166">Chrome에서는 tooclick 있는 *고급* 다음 hello 및 *계속* 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-166">In Chrome, you have tooclick *Advanced* and then hello *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="50a7c-167">Hello 클러스터 만들기가 실패할 경우에 이미 배포 된 hello 리소스를 업데이트 하는 hello 명령 항상 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-167">If hello cluster creation fails, you can always rerun hello command, which updates hello resources already deployed.</span></span> <span data-ttu-id="50a7c-168">에서 실패 하는 hello 배포의 일부로 인증서를 만든 경우 새로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-168">If a certificate was created as part of hello failed deployment, a new one is generated.</span></span> <span data-ttu-id="50a7c-169">tootroubleshoot 클러스터를 만드는 참조 [Azure 리소스 관리자를 사용 하 여 서비스 패브릭 클러스터를 만들](service-fabric-cluster-creation-via-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-169">tootroubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-toohello-secure-cluster"></a><span data-ttu-id="50a7c-170">Toohello 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="50a7c-170">Connect toohello secure cluster</span></span>
<span data-ttu-id="50a7c-171">서비스 패브릭 SDK hello와 함께 설치 하는 hello 서비스 패브릭 PowerShell 모듈을 사용 하 여 toohello 클러스터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-171">Connect toohello cluster using hello Service Fabric PowerShell module installed with hello Service Fabric SDK.</span></span>  <span data-ttu-id="50a7c-172">첫째, 컴퓨터에 hello 현재 사용자의 개인 (My) 저장소 hello로 hello 인증서를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-172">First, install hello certificate into hello Personal (My) store of hello current user on your computer.</span></span>  <span data-ttu-id="50a7c-173">Hello 다음 PowerShell 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-173">Run hello following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="50a7c-174">준비 tooconnect tooyour 보안 클러스터가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-174">You are now ready tooconnect tooyour secure cluster.</span></span>

<span data-ttu-id="50a7c-175">hello **서비스 패브릭** PowerShell 모듈 서비스 패브릭 클러스터, 응용 프로그램 및 서비스를 관리 하기 위한 많은 cmdlet을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-175">hello **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="50a7c-176">사용 하 여 hello [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello 보안 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-176">Use hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello secure cluster.</span></span> <span data-ttu-id="50a7c-177">인증서 지문을 hello 및 연결 끝점 세부 정보는 이전 단계의 hello 출력에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-177">hello certificate thumbprint and connection endpoint details are found in hello output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="50a7c-178">연결 하 고 hello 클러스터 상태가 정상이 hello를 사용 하 여 확인 [Get ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="50a7c-178">Check that you are connected and hello cluster is healthy using hello [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="50a7c-179">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="50a7c-179">Clean up resources</span></span>

<span data-ttu-id="50a7c-180">클러스터 구성 된 다른 Azure 리소스로 또한 자체 toohello 클러스터 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-180">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="50a7c-181">hello 가장 간단한 방법은 toodelete hello 클러스터와 사용 하는 모든 hello 리소스 toodelete hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-181">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span>

<span data-ttu-id="50a7c-182">TooAzure을 고 tooremove hello 클러스터 할 hello 구독 ID를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-182">Log in tooAzure and select hello subscription ID with which you want tooremove hello cluster.</span></span>  <span data-ttu-id="50a7c-183">Toohello에 로그인 하 여 구독 ID를 찾을 수 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-183">You can find your subscription ID by logging in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="50a7c-184">Hello 리소스 그룹 및 hello를 사용 하 여 모든 hello 클러스터 리소스 삭제 [제거 AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup)합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-184">Delete hello resource group and all hello cluster resources using hello [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="50a7c-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50a7c-185">Next steps</span></span>
<span data-ttu-id="50a7c-186">이 자습서에서는 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="50a7c-187">Azure에서 Service Fabric 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="50a7c-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="50a7c-188">X.509 인증서로 hello 클러스터 보안</span><span class="sxs-lookup"><span data-stu-id="50a7c-188">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="50a7c-189">PowerShell을 사용 하 여 toohello 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="50a7c-189">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="50a7c-190">클러스터 제거</span><span class="sxs-lookup"><span data-stu-id="50a7c-190">Remove a cluster</span></span>

<span data-ttu-id="50a7c-191">다음으로 이동 하는 자습서 toolearn 방법을 따르는 toohello toodeploy 기존 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="50a7c-191">Next, advance toohello following tutorial toolearn how toodeploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="50a7c-192">Docker Compose를 사용하여 기존 .NET 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="50a7c-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)
