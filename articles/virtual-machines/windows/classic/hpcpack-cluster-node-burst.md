---
title: "HPC 팩 클러스터에 버스트 노드 추가 | Microsoft Docs"
description: "클라우드 서비스에서 실행되는 작업자 역할 인스턴스를 추가하여 요청에 따라 HPC Pack 클러스터를 확장하는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 24b79a8a-24ad-4002-ae76-75abc9b28c83
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 9336743b92130e37b1df2992aab806696f8276aa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-on-demand-burst-nodes-to-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="dd066-103">Azure의 HPC 팩 클러스터에 주문형 "버스트" 노드 추가</span><span class="sxs-lookup"><span data-stu-id="dd066-103">Add on-demand "burst" nodes to an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="dd066-104">Azure에서 [Microsoft HPC 팩](https://technet.microsoft.com/library/cc514029) 클러스터를 설정하는 경우 미리 구성된 계산 노드 VM을 유지하지 않고 클러스터 용량을 신속하게 확장 또는 축소할 수 있는 방법을 원할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-104">If you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure, you might want a way to quickly scale the cluster capacity up or down, without maintaining a set of preconfigured compute node VMs.</span></span> <span data-ttu-id="dd066-105">이 문서에서는 "버스트" 노드(클라우드 서비스에서 실행되는 작업자 역할 인스턴스)를 Azure의 헤드 노드에 계산 리소스로 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-105">This article shows you how to add on-demand "burst" nodes (worker role instances running in a cloud service) as compute resources to a head node in Azure.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="dd066-106">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="dd066-107">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="dd066-108">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

![버스트 노드][burst]

<span data-ttu-id="dd066-110">이 문서의 단계를 통해 Azure 노드를 클라우드 기반 HPC 팩 헤드 노드 VM에 빠르게 추가하여 테스트 또는 개념 증명 배포를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-110">The steps in this article help you add Azure nodes quickly to a cloud-based HPC Pack head node VM for a test or proof-of-concept deployment.</span></span> <span data-ttu-id="dd066-111">전체적인 단계는 "Azure로 버스트"하여 온-프레미스 HPC 팩 클러스터에 클라우드 계산 용량을 추가하는 단계와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-111">The high-level steps are the same as the steps to “burst to Azure” to add cloud compute capacity to an on-premises HPC Pack cluster.</span></span> <span data-ttu-id="dd066-112">자습서를 보려면 [Microsoft HPC 팩을 사용하여 하이브리드 계산 클러스터 설정](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd066-112">For a tutorial, see [Set up a hybrid compute cluster with Microsoft HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md).</span></span> <span data-ttu-id="dd066-113">프로덕션 배포에 대한 자세한 지침과 고려 사항을 보려면 [Microsoft HPC 팩을 사용하여 Azure로 버스트](https://technet.microsoft.com/library/gg481749.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd066-113">For detailed guidance and considerations for production deployments, see [Burst to Azure with Microsoft HPC Pack](https://technet.microsoft.com/library/gg481749.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd066-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dd066-114">Prerequisites</span></span>
* <span data-ttu-id="dd066-115">**Azure VM에 배포된 HPC Pack 헤드 노드** - 독립 실행형 헤드 노드 VM 또는 더 큰 클러스터의 일부인 VM을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-115">**HPC Pack head node deployed in an Azure VM** - You can use a stand-alone head node VM or one that is part of a larger cluster.</span></span> <span data-ttu-id="dd066-116">독립 실행형 헤드 노드를 만들려면 [Azure VM에서 HPC Pack 헤드 노드 배포](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-116">To create a stand-alone head node, see [Deploy an HPC Pack Head Node in an Azure VM](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="dd066-117">자동화된 HPC Pack 클러스트 배포 옵션에 대한 자세한 내용은 [Microsoft HPC Pack을 사용하여 Azure에서 Windows HPC 클러스터를 만들고 관리하는 옵션](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd066-117">For automated HPC Pack cluster deployment options, see [Options to create and manage a Windows HPC cluster in Azure with Microsoft HPC Pack](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
  > [!TIP]
  > <span data-ttu-id="dd066-118">[HPC 팩 IaaS 배포 스크립트](hpcpack-cluster-powershell-script.md) 를 사용하여 Azure에 클러스터를 만들 경우 자동 배포에 Azure 버스트 노드를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-118">If you use the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to create the cluster in Azure, you can include Azure burst nodes in your automated deployment.</span></span> <span data-ttu-id="dd066-119">해당 문서에서 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd066-119">See the examples in that article.</span></span>
  > 
  > 
* <span data-ttu-id="dd066-120">**Azure 구독** - Azure 노드를 추가하려는 경우 헤드 노드 VM을 배포하는 데 사용하는 것과 동일한 구독 또는 다른 구독을 하나 이상 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-120">**Azure subscription** - To add Azure nodes, you can choose the same subscription used to deploy the head node VM, or a different subscription (or subscriptions).</span></span>
* <span data-ttu-id="dd066-121">**코어 할당량** - 멀티 코어 크기를 사용하여 여러 Azure 노드를 배포하려는 경우 특히 코어 할당량을 늘려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-121">**Cores quota** - You might need to increase the quota of cores, especially if you choose to deploy several Azure nodes with multicore sizes.</span></span> <span data-ttu-id="dd066-122">할당량을 늘리려면 무료로 [온라인 고객 지원 요청을 개설](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-122">To increase a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>

## <a name="step-1-create-a-cloud-service-and-a-storage-account-for-the-azure-nodes"></a><span data-ttu-id="dd066-123">1단계: Azure 노드에 대한 클라우드 서비스 및 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="dd066-123">Step 1: Create a cloud service and a storage account for the Azure nodes</span></span>
<span data-ttu-id="dd066-124">Azure 클래식 포털 또는 동급의 도구를 사용하여 Azure 노드 배포에 필요한 다음 리소스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-124">Use the Azure classic portal or equivalent tools to configure the following resources that are needed to deploy your Azure nodes:</span></span>

* <span data-ttu-id="dd066-125">새 Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="dd066-125">A new Azure cloud service</span></span>
* <span data-ttu-id="dd066-126">새 Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="dd066-126">A new Azure storage account</span></span>

> [!NOTE]
> <span data-ttu-id="dd066-127">구독에서 기존 클라우드 서비스를 다시 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="dd066-127">Don't reuse an existing cloud service in your subscription.</span></span> 
> 
> 

<span data-ttu-id="dd066-128">**고려 사항**</span><span class="sxs-lookup"><span data-stu-id="dd066-128">**Considerations**</span></span>

* <span data-ttu-id="dd066-129">만들려는 각 Azure 노드 템플릿에 대해 별도의 클라우드 서비스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-129">Configure a separate cloud service for each Azure node template that you plan to create.</span></span> <span data-ttu-id="dd066-130">하지만 여러 노드 템플릿에 대해 동일한 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-130">However, you can use the same storage account for multiple node templates.</span></span>
* <span data-ttu-id="dd066-131">동일한 Azure 지역에서 배포하는 데 사용할 저장소 계정과 클라우드 서비스를 찾는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-131">We recommend that you locate the cloud service and the storage account for the deployment in the same Azure region.</span></span>

## <a name="step-2-configure-an-azure-management-certificate"></a><span data-ttu-id="dd066-132">2단계: Azure 관리 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="dd066-132">Step 2: Configure an Azure management certificate</span></span>
<span data-ttu-id="dd066-133">Azure 노드를 계산 리소스로 추가하려면 헤드 노드에 관리 인증서를 추가하고 해당 인증서를 배포에 사용한 Azure 구독에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-133">To add Azure nodes as compute resources, you need a management certificate on the head node and upload a corresponding certificate to the Azure subscription used for the deployment.</span></span>

<span data-ttu-id="dd066-134">이 시나리오의 경우 HPC 팩에서 설치한 **기본 HPC Azure 관리 인증서** 를 선택하고 헤드 노드에 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-134">For this scenario, you can choose the **Default HPC Azure Management Certificate** that HPC Pack installs and configures automatically on the head node.</span></span> <span data-ttu-id="dd066-135">이 인증서는 테스트 목적 및 개념 증명 배포에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-135">This certificate is useful for testing purposes and proof-of-concept deployments.</span></span> <span data-ttu-id="dd066-136">이 인증서를 사용하려면 헤드 노드 VM에서 구독으로 C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-136">To use this certificate, upload the file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer from the head node VM to the subscription.</span></span> <span data-ttu-id="dd066-137">[Azure 클래식 포털](https://manage.windowsazure.com)에서 인증서를 업로드하려면 **설정** > **관리 인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-137">To upload the certificate in the [Azure classic portal](https://manage.windowsazure.com), click **Settings** > **Management Certificates**.</span></span>

<span data-ttu-id="dd066-138">관리 인증서 구성에 대한 추가 옵션을 보려면 [Azure 버스트 배포를 위한 Azure 관리 인증서 구성 시나리오](http://technet.microsoft.com/library/gg481759.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd066-138">For additional options to configure the management certificate, see [Scenarios to Configure the Azure Management Certificate for Azure Burst Deployments](http://technet.microsoft.com/library/gg481759.aspx).</span></span>

## <a name="step-3-deploy-azure-nodes-to-the-cluster"></a><span data-ttu-id="dd066-139">단계 3: 클러스터에 Azure 노드 배포</span><span class="sxs-lookup"><span data-stu-id="dd066-139">Step 3: Deploy Azure nodes to the cluster</span></span>
<span data-ttu-id="dd066-140">이 시나리오에서 Azure 노드를 추가 및 시작하는 단계는 온-프레미스 헤드 노드의 단계와 일반적으로 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-140">The steps to add and start Azure nodes in this scenario are generally the same as the steps with an on-premises head node.</span></span> <span data-ttu-id="dd066-141">자세한 내용은 [Microsoft HPC 팩을 사용하여 Azure 노드를 배포하는 단계](https://technet.microsoft.com/library/gg481758.aspx)에서 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd066-141">For more information, see the following sections in [Steps to Deploy Azure Nodes with Microsoft HPC Pack](https://technet.microsoft.com/library/gg481758.aspx):</span></span>

* <span data-ttu-id="dd066-142">Azure 노드 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="dd066-142">Create an Azure node template</span></span>
* <span data-ttu-id="dd066-143">Windows HPC 클러스터에 Azure 노드 추가</span><span class="sxs-lookup"><span data-stu-id="dd066-143">Add Azure nodes to the Windows HPC cluster</span></span>
* <span data-ttu-id="dd066-144">Azure 노드 시작(프로비전)</span><span class="sxs-lookup"><span data-stu-id="dd066-144">Start (provision) the Azure nodes</span></span>

<span data-ttu-id="dd066-145">노드를 추가 및 시작하면 클러스터 작업을 실행하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd066-145">After you add and start the nodes, they are ready for you to use to run cluster jobs.</span></span>

<span data-ttu-id="dd066-146">Azure 노드를 배포할 때 문제가 발생할 경우 [Microsoft HPC Pack을 사용하여 Azure 노드 배포 시 문제 해결](http://technet.microsoft.com/library/jj159097.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd066-146">If you encounter problems when deploying Azure nodes, see [Troubleshoot Deployments of Azure Nodes with Microsoft HPC Pack](http://technet.microsoft.com/library/jj159097.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd066-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd066-147">Next steps</span></span>
* <span data-ttu-id="dd066-148">버스트 노드에 계산 집약적 인스턴스 크기를 사용하려는 경우 [고성능 계산 VM 크기](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)의 고려 사항을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd066-148">To use a compute-intensive instance size for the burst nodes, see the considerations in [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="dd066-149">Azure 컴퓨팅 리소스를 클러스터 워크로드에 따라 자동으로 증가 또는 축소하려는 경우 [HPC Pack 클러스터에서 Azure 계산 리소스를 자동으로 증가 및 축소](hpcpack-cluster-node-autogrowshrink.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd066-149">If you want to automatically grow or shrink the Azure computing resources according to the cluster workload, see [Automatically grow and shrink Azure compute resources in an HPC Pack cluster](hpcpack-cluster-node-autogrowshrink.md).</span></span>

<!--Image references-->
[burst]: ./media/hpcpack-cluster-node-burst/burst.png
