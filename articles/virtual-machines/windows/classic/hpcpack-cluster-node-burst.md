---
title: "aaaAdd 버스트 노드 tooan HPC Pack 클러스터 | Microsoft Docs"
description: "Tooexpand HPC Pack 요청 시 Azure에서 클라우드 서비스에서 실행 되는 작업자 역할 인스턴스를 추가 하 여 클러스터링 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 7ec40ffe76485742c9e458ec49e11805990974e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-on-demand-burst-nodes-tooan-hpc-pack-cluster-in-azure"></a><span data-ttu-id="3950f-103">Azure의 주문형 "전환" 노드 tooan HPC Pack 클러스터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-103">Add on-demand "burst" nodes tooan HPC Pack cluster in Azure</span></span>
<span data-ttu-id="3950f-104">설정 하는 경우는 [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) 클러스터에 Azure를 위 또는 아래로 tooquickly 눈금 hello 클러스터 용량 집합을 유지 하지 않고 미리 구성 된 계산 노드 Vm 하는 방법을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-104">If you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure, you might want a way tooquickly scale hello cluster capacity up or down, without maintaining a set of preconfigured compute node VMs.</span></span> <span data-ttu-id="3950f-105">이 문서에서는 어떻게 주문형 tooadd "전환" 노드 (클라우드 서비스에서 실행 중인 작업자 역할 인스턴스)로 계산 리소스 tooa Azure에서 헤드 노드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-105">This article shows you how tooadd on-demand "burst" nodes (worker role instances running in a cloud service) as compute resources tooa head node in Azure.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="3950f-106">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3950f-107">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3950f-108">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

![버스트 노드][burst]

<span data-ttu-id="3950f-110">이 문서의 단계 hello Azure 노드를 신속 하 게 추가 하는 데 도움이 tooa 클라우드 기반 HPC Pack 헤드 노드 VM 테스트 또는 개념 증명 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-110">hello steps in this article help you add Azure nodes quickly tooa cloud-based HPC Pack head node VM for a test or proof-of-concept deployment.</span></span> <span data-ttu-id="3950f-111">hello 대략적인 단계는 hello tooadd 클라우드 계산 용량 tooan 온-프레미스 HPC Pack 클러스터 hello 단계 너무 "전환" tooAzure 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-111">hello high-level steps are hello same as hello steps too“burst tooAzure” tooadd cloud compute capacity tooan on-premises HPC Pack cluster.</span></span> <span data-ttu-id="3950f-112">자습서를 보려면 [Microsoft HPC 팩을 사용하여 하이브리드 계산 클러스터 설정](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3950f-112">For a tutorial, see [Set up a hybrid compute cluster with Microsoft HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md).</span></span> <span data-ttu-id="3950f-113">자세한 지침 및 프로덕션 배포에 대 한 고려 사항에 대 한 참조 [Microsoft HPC Pack을 사용한 tooAzure 버스트](https://technet.microsoft.com/library/gg481749.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-113">For detailed guidance and considerations for production deployments, see [Burst tooAzure with Microsoft HPC Pack](https://technet.microsoft.com/library/gg481749.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3950f-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3950f-114">Prerequisites</span></span>
* <span data-ttu-id="3950f-115">**Azure VM에 배포된 HPC Pack 헤드 노드** - 독립 실행형 헤드 노드 VM 또는 더 큰 클러스터의 일부인 VM을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-115">**HPC Pack head node deployed in an Azure VM** - You can use a stand-alone head node VM or one that is part of a larger cluster.</span></span> <span data-ttu-id="3950f-116">독립 실행형 헤드 노드 toocreate 참조 [Azure VM에서 HPC Pack 헤드 노드 배포](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-116">toocreate a stand-alone head node, see [Deploy an HPC Pack Head Node in an Azure VM](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="3950f-117">자동화 된 HPC 팩 클러스터 배포 옵션에 대 한 참조 [toocreate 옵션 및 Microsoft HPC Pack을 사용 하 여 Azure에서 Windows HPC 클러스터를 관리할](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-117">For automated HPC Pack cluster deployment options, see [Options toocreate and manage a Windows HPC cluster in Azure with Microsoft HPC Pack](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
  > [!TIP]
  > <span data-ttu-id="3950f-118">Hello를 사용 하는 경우 [HPC Pack IaaS 배포 스크립트](hpcpack-cluster-powershell-script.md) toocreate hello Azure에서 클러스터의 경우 자동화 된 배포에 Azure 버스트 노드를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-118">If you use hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) toocreate hello cluster in Azure, you can include Azure burst nodes in your automated deployment.</span></span> <span data-ttu-id="3950f-119">해당 아티클에 있는 hello 예를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3950f-119">See hello examples in that article.</span></span>
  > 
  > 
* <span data-ttu-id="3950f-120">**Azure 구독** -Azure tooadd 선택할 수 노드를 동일한 사용 되는 구독 toodeploy hello 헤드 노드 VM 또는 다른 구독 (또는 구독) hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-120">**Azure subscription** - tooadd Azure nodes, you can choose hello same subscription used toodeploy hello head node VM, or a different subscription (or subscriptions).</span></span>
* <span data-ttu-id="3950f-121">**코어 할당량** -toodeploy 멀티 코어 크기에 따라 여러 Azure 노드를 선택 하는 경우에 특히 tooincrease hello 할당량의 코어를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-121">**Cores quota** - You might need tooincrease hello quota of cores, especially if you choose toodeploy several Azure nodes with multicore sizes.</span></span> <span data-ttu-id="3950f-122">할당량 tooincrease [온라인 고객 지원 요청을 개시](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) 비용 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-122">tooincrease a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>

## <a name="step-1-create-a-cloud-service-and-a-storage-account-for-hello-azure-nodes"></a><span data-ttu-id="3950f-123">1 단계: 클라우드 서비스 및 hello에 대 한 저장소 계정을 Azure 노드 만들기</span><span class="sxs-lookup"><span data-stu-id="3950f-123">Step 1: Create a cloud service and a storage account for hello Azure nodes</span></span>
<span data-ttu-id="3950f-124">Azure 클래식 포털 hello 또는 다음 리소스를 필요한 toodeploy 상응 하는 도구 tooconfigure hello Azure 노드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-124">Use hello Azure classic portal or equivalent tools tooconfigure hello following resources that are needed toodeploy your Azure nodes:</span></span>

* <span data-ttu-id="3950f-125">새 Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="3950f-125">A new Azure cloud service</span></span>
* <span data-ttu-id="3950f-126">새 Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="3950f-126">A new Azure storage account</span></span>

> [!NOTE]
> <span data-ttu-id="3950f-127">구독에서 기존 클라우드 서비스를 다시 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3950f-127">Don't reuse an existing cloud service in your subscription.</span></span> 
> 
> 

<span data-ttu-id="3950f-128">**고려 사항**</span><span class="sxs-lookup"><span data-stu-id="3950f-128">**Considerations**</span></span>

* <span data-ttu-id="3950f-129">각 Azure 노드 템플릿 toocreate 계획에 대 한 별도 클라우드 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-129">Configure a separate cloud service for each Azure node template that you plan toocreate.</span></span> <span data-ttu-id="3950f-130">사용할 수 있습니다 hello 여러 노드 템플릿에 동일한 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-130">However, you can use hello same storage account for multiple node templates.</span></span>
* <span data-ttu-id="3950f-131">Hello 클라우드 서비스 및 hello 배포에 사용할 저장소 계정을 hello hello에서 찾는 것이 좋습니다 동일한 Azure 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-131">We recommend that you locate hello cloud service and hello storage account for hello deployment in hello same Azure region.</span></span>

## <a name="step-2-configure-an-azure-management-certificate"></a><span data-ttu-id="3950f-132">2단계: Azure 관리 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="3950f-132">Step 2: Configure an Azure management certificate</span></span>
<span data-ttu-id="3950f-133">tooadd Azure 노드를 계산 리소스를 toohello hello 배포에 사용 되는 Azure 구독에 인증서를 해당 hello 헤드 노드 및 업로드에 관리 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-133">tooadd Azure nodes as compute resources, you need a management certificate on hello head node and upload a corresponding certificate toohello Azure subscription used for hello deployment.</span></span>

<span data-ttu-id="3950f-134">이 시나리오에 대 한 hello를 선택할 수 있습니다 **기본 HPC Azure 관리 인증서** HPC Pack을 설치 하 고 헤드 노드에서 자동으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-134">For this scenario, you can choose hello **Default HPC Azure Management Certificate** that HPC Pack installs and configures automatically on the head node.</span></span> <span data-ttu-id="3950f-135">이 인증서는 테스트 목적 및 개념 증명 배포에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-135">This certificate is useful for testing purposes and proof-of-concept deployments.</span></span> <span data-ttu-id="3950f-136">toouse 인증서이 hello 헤드 노드 VM toothe 구독에서에서 파일 C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-136">toouse this certificate, upload the file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer from hello head node VM toothe subscription.</span></span> <span data-ttu-id="3950f-137">hello에 tooupload hello 인증서 [Azure 클래식 포털](https://manage.windowsazure.com), 클릭 **설정** > **관리 인증서**합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-137">tooupload hello certificate in hello [Azure classic portal](https://manage.windowsazure.com), click **Settings** > **Management Certificates**.</span></span>

<span data-ttu-id="3950f-138">추가 옵션 tooconfigure hello 관리 인증서에 대 한 참조 [시나리오 tooConfigure hello Azure 버스트 배포용 Azure 관리 인증서](http://technet.microsoft.com/library/gg481759.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-138">For additional options tooconfigure hello management certificate, see [Scenarios tooConfigure hello Azure Management Certificate for Azure Burst Deployments](http://technet.microsoft.com/library/gg481759.aspx).</span></span>

## <a name="step-3-deploy-azure-nodes-toohello-cluster"></a><span data-ttu-id="3950f-139">3 단계: Azure 노드 toohello 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="3950f-139">Step 3: Deploy Azure nodes toohello cluster</span></span>
<span data-ttu-id="3950f-140">단계 tooadd hello 및 Azure를 시작 합니다. 온-프레미스 헤드 노드를 사용 하 여 hello 단계와 동일를이 시나리오에서는 노드는 hello 일반적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-140">hello steps tooadd and start Azure nodes in this scenario are generally hello same as hello steps with an on-premises head node.</span></span> <span data-ttu-id="3950f-141">자세한 내용은 다음 섹션에는 hello 참조 [tooDeploy Microsoft HPC Pack을 사용한 Azure 노드 단계](https://technet.microsoft.com/library/gg481758.aspx):</span><span class="sxs-lookup"><span data-stu-id="3950f-141">For more information, see hello following sections in [Steps tooDeploy Azure Nodes with Microsoft HPC Pack](https://technet.microsoft.com/library/gg481758.aspx):</span></span>

* <span data-ttu-id="3950f-142">Azure 노드 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="3950f-142">Create an Azure node template</span></span>
* <span data-ttu-id="3950f-143">Azure 노드 toohello Windows HPC 클러스터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-143">Add Azure nodes toohello Windows HPC cluster</span></span>
* <span data-ttu-id="3950f-144">시작 (프로 비전) hello Azure 노드</span><span class="sxs-lookup"><span data-stu-id="3950f-144">Start (provision) hello Azure nodes</span></span>

<span data-ttu-id="3950f-145">추가 하 고 hello 노드를 시작 하면 toouse toorun 클러스터 작업 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-145">After you add and start hello nodes, they are ready for you toouse toorun cluster jobs.</span></span>

<span data-ttu-id="3950f-146">Azure 노드를 배포할 때 문제가 발생할 경우 [Microsoft HPC Pack을 사용하여 Azure 노드 배포 시 문제 해결](http://technet.microsoft.com/library/jj159097.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3950f-146">If you encounter problems when deploying Azure nodes, see [Troubleshoot Deployments of Azure Nodes with Microsoft HPC Pack](http://technet.microsoft.com/library/jj159097.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3950f-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3950f-147">Next steps</span></span>
* <span data-ttu-id="3950f-148">hello에 대 한 계산 집약적인 인스턴스 크기 toouse 버스트 노드의 hello 고려 사항을 참조 [VM 크기를 계산 하는 고성능](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-148">toouse a compute-intensive instance size for hello burst nodes, see hello considerations in [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="3950f-149">컴퓨팅 리소스 hello 클러스터 워크 로드에 따라 Azure hello, 참조를 자동으로 확대 하거나 축소 하려면 [자동으로 증가 하 고 HPC Pack 클러스터에서 Azure 계산 리소스를 축소](hpcpack-cluster-node-autogrowshrink.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3950f-149">If you want to automatically grow or shrink hello Azure computing resources according to hello cluster workload, see [Automatically grow and shrink Azure compute resources in an HPC Pack cluster](hpcpack-cluster-node-autogrowshrink.md).</span></span>

<!--Image references-->
[burst]: ./media/hpcpack-cluster-node-burst/burst.png
