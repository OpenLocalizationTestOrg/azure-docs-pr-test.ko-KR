---
title: "Azure HDInsight 클러스터-aaaHow toodelete | Microsoft Docs"
description: "HDInsight 클러스터를 삭제할 수 있는 다양 한 방법으로 hello에 대 한 정보입니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a><span data-ttu-id="24a2f-103">브라우저, PowerShell 또는 Azure CLI hello를 사용 하 여 HDInsight 클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="24a2f-103">Delete an HDInsight cluster using your browser, PowerShell, or hello Azure CLI</span></span>

<span data-ttu-id="24a2f-104">HDInsight 클러스터 결제 클러스터 만들어지고 hello 클러스터를 삭제할 때 중지 되 면 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="24a2f-104">HDInsight cluster billing starts once a cluster is created and stops when hello cluster is deleted.</span></span> <span data-ttu-id="24a2f-105">분 단위로 청구되므로 더 이상 사용하지 않으면 항상 클러스터를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24a2f-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="24a2f-106">이 문서에서는 Azure 포털, Azure PowerShell 및 Azure CLI 1.0 hello 사용 하 여 클러스터 toodelete hello 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="24a2f-106">In this document, you learn how toodelete a cluster using hello Azure portal, Azure PowerShell, and hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24a2f-107">HDInsight 클러스터를 삭제 해도 hello Azure 저장소 계정 또는 hello 클러스터와 연결 된 데이터 레이크 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="24a2f-107">Deleting an HDInsight cluster does not delete hello Azure Storage accounts or Data Lake Store associated with hello cluster.</span></span> <span data-ttu-id="24a2f-108">Hello 나중에 해당 서비스에 저장 된 데이터를 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a2f-108">You can reuse data stored in those services in hello future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="24a2f-109">Azure portal</span><span class="sxs-lookup"><span data-stu-id="24a2f-109">Azure portal</span></span>

1. <span data-ttu-id="24a2f-110">Toohello 로그인 [Azure 포털](https://portal.azure.com) 고 HDInsight 클러스터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="24a2f-110">Log in toohello [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="24a2f-111">HDInsight 클러스터에 고정 된 toohello 대시보드 없으면 hello 검색 필드를 사용 하 여 이름별으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a2f-111">If your HDInsight cluster is not pinned toohello dashboard, you can search for it by name using hello search field.</span></span>
   
    ![포털 검색](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="24a2f-113">Hello 블레이드 hello 클러스터에 대 한가 되 면 선택 hello **삭제** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="24a2f-113">Once hello blade opens for hello cluster, select hello **Delete** icon.</span></span> <span data-ttu-id="24a2f-114">메시지가 나타나면 선택 **예** toodelete hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="24a2f-114">When prompted, select **Yes** toodelete hello cluster.</span></span>
   
    ![삭제 아이콘](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="24a2f-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="24a2f-116">Azure PowerShell</span></span>

<span data-ttu-id="24a2f-117">PowerShell 프롬프트에서 다음 명령을 toodelete hello 클러스터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24a2f-117">From a PowerShell prompt, use hello following command toodelete hello cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="24a2f-118">대체 **CLUSTERNAME** HDInsight 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="24a2f-118">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="24a2f-119">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="24a2f-119">Azure CLI 1.0</span></span>

<span data-ttu-id="24a2f-120">프롬프트에서 다음 toodelete hello 클러스터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24a2f-120">From a prompt, use hello following toodelete hello cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="24a2f-121">대체 **CLUSTERNAME** HDInsight 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="24a2f-121">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="24a2f-122">Azure CLI 2.0은 현재(2017년 7월 31일) HDInsight 클러스터를 삭제하도록 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24a2f-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>