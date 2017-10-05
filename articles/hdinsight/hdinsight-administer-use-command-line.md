---
title: "Azure CLI를 사용하여 Hadoop 클러스터 관리 - Azure HDInsight| Microsoft Docs"
description: "Azure 명령줄 인터페이스를 사용하여 Azure HDInsight의 Hadoop 클러스터를 관리하는 방법을 알아봅니다. Azure CLI는 Windows, Mac 및 Linux에서 작동합니다."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0ee9f2f28978b207dcaf8f77950bd82a897d3fd1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-the-azure-cli"></a><span data-ttu-id="0d135-104">Azure CLI를 사용하여 HDInsight의 Hadoop 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="0d135-104">Manage Hadoop clusters in HDInsight using the Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="0d135-105">[Azure 명령줄 인터페이스](../cli-install-nodejs.md)를 사용하여 Azure HDInsight의 Hadoop 클러스터를 관리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0d135-105">Learn how to use the [Azure Command-line Interface](../cli-install-nodejs.md) to manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="0d135-106">Azure CLI는 Node.js로 구현되며</span><span class="sxs-lookup"><span data-stu-id="0d135-106">The Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="0d135-107">Windows, Mac, Linux를 포함하여 Node.js를 지원하는 플랫폼에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d135-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="0d135-108">이 문서에서는 HDInsight을 통한 Azure CLI 사용에 대해서만 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0d135-108">This article covers only using the Azure CLI with HDInsight.</span></span> <span data-ttu-id="0d135-109">Azure CLI를 사용하는 방법에 대한 일반 가이드는 [Azure CLI 설치 및 구성][azure-command-line-tools]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d135-109">For a general guide on how to use Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="0d135-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0d135-110">Prerequisites</span></span>
<span data-ttu-id="0d135-111">이 문서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d135-111">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="0d135-112">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="0d135-112">**An Azure subscription**.</span></span> <span data-ttu-id="0d135-113">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d135-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="0d135-114">**Azure CLI** - 설치 및 구성 정보는 [Azure CLI 설치 및 구성](../cli-install-nodejs.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d135-114">**Azure CLI** - See [Install and configure the Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="0d135-115">**Azure에 연결**. 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0d135-115">**Connect to Azure**, using the following command:</span></span>
  
        azure login
  
    <span data-ttu-id="0d135-116">회사 또는 학교 계정을 사용하여 인증하는 방법에 대한 자세한 내용은 [Azure CLI에서 Azure 구독에 연결](../xplat-cli-connect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d135-116">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="0d135-117">**Azure Resource Manager 모드로 전환**은 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0d135-117">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="0d135-118">도움말을 보려면 **-h** 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0d135-118">To get help, use the **-h** switch.</span></span>  <span data-ttu-id="0d135-119">예:</span><span class="sxs-lookup"><span data-stu-id="0d135-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-the-cli"></a><span data-ttu-id="0d135-120">CLI를 사용하여 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="0d135-120">Create clusters with the CLI</span></span>
<span data-ttu-id="0d135-121">[Azure CLI를 사용하여 HDInsight의 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-azure-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d135-121">See [Create clusters in HDInsight using the Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="0d135-122">클러스터 세부 정보 나열 및 표시</span><span class="sxs-lookup"><span data-stu-id="0d135-122">List and show cluster details</span></span>
<span data-ttu-id="0d135-123">클러스터 세부 정보를 나열하고 표시하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0d135-123">Use the following commands to list and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="0d135-124">![클러스터 목록의 명령줄 보기][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="0d135-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="0d135-125">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="0d135-125">Delete clusters</span></span>
<span data-ttu-id="0d135-126">클러스터를 삭제하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0d135-126">Use the following command to delete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="0d135-127">또한 클러스터를 포함하는 리소스 그룹을 삭제하여 클러스터를 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d135-127">You can also delete a cluster by deleting the resource group that contains the cluster.</span></span> <span data-ttu-id="0d135-128">이렇게 하면 기본 저장소 계정을 포함한 그룹 내 모든 리소스가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d135-128">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="0d135-129">클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="0d135-129">Scale clusters</span></span>
<span data-ttu-id="0d135-130">Hadoop 클러스터 크기를 변경하려면</span><span class="sxs-lookup"><span data-stu-id="0d135-130">To change the Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="0d135-131">클러스터에 대한 HTTP 액세스 사용/사용 안 함</span><span class="sxs-lookup"><span data-stu-id="0d135-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="0d135-132">클러스터에 대한 RDP 액세스 사용/사용 안 함</span><span class="sxs-lookup"><span data-stu-id="0d135-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="0d135-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0d135-133">Next steps</span></span>
<span data-ttu-id="0d135-134">이 문서에서는 HDInsight 클러스터 관리 작업을 수행하는 여러 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="0d135-134">In this article, you have learned how to perform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="0d135-135">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d135-135">To learn more, see the following articles:</span></span>

* <span data-ttu-id="0d135-136">[Azure Portal을 사용하여 HDInsight 관리][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="0d135-136">[Administer HDInsight by using the Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="0d135-137">[Azure PowerShell을 사용하여 HDInsight 클러스터 관리][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="0d135-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="0d135-138">[Azure HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="0d135-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="0d135-139">[Azure CLI를 사용하는 방법][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="0d135-139">[How to use the Azure CLI][azure-command-line-tools]</span></span>

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "클러스터 나열 및 표시"
