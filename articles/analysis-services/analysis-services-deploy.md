---
title: "SSDT를 사용하여 Azure Analysis Services에 배포 | Microsoft Docs"
description: "SSDT를 사용하여 Azure Analysis Services 서버에 테이블 형식 모델을 배포하는 방법에 대해 알아봅니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e9a3aedfb6e55696e1525e226fada1062fd5eda8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="ee896-103">SSDT에서 모델 배포</span><span class="sxs-lookup"><span data-stu-id="ee896-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="ee896-104">Azure 구독에서 서버를 만들면 여기에 테이블 형식 모델 데이터베이스를 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-104">Once you've created a server in your Azure subscription, you're ready to deploy a tabular model database to it.</span></span> <span data-ttu-id="ee896-105">SSDT(SQL Server 데이터 도구)를 사용하여 작업하는 테이블 형식 모델 프로젝트를 빌드하고 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-105">You can use SQL Server Data Tools (SSDT) to build and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ee896-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ee896-106">Prerequisites</span></span>
<span data-ttu-id="ee896-107">시작하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-107">To get started, you need:</span></span>

* <span data-ttu-id="ee896-108">Azure의 **Analysis Services 서버** -</span><span class="sxs-lookup"><span data-stu-id="ee896-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="ee896-109">자세한 내용은 [Azure Analysis Services 서버 만들기](analysis-services-create-server.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ee896-109">To learn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="ee896-110">SSDT의 **테이블 형식 모델 프로젝트** 또는 1200 이상 호환성 수준의 기존 테이블 형식 모델</span><span class="sxs-lookup"><span data-stu-id="ee896-110">**Tabular model project** in SSDT or an existing tabular model at the 1200 or higher compatibility level.</span></span> <span data-ttu-id="ee896-111">만들어 본 적이 없나요?</span><span class="sxs-lookup"><span data-stu-id="ee896-111">Never created one?</span></span> <span data-ttu-id="ee896-112">[Adventure Works Internet Sales Tabular Modeling 자습서](https://msdn.microsoft.com/library/hh231691.aspx)를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="ee896-112">Try the [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="ee896-113">**온-프레미스 게이트웨이** - 하나 이상의 데이터 원본이 조직 네트워크의 온-프레미스에 있는 경우 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need to install an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="ee896-114">온-프레미스 데이터 원본에 대한 클라우드 연결에 있는 서버가 모델에서 데이터를 처리하고 새로 고치는 데 게이트웨이가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-114">The gateway is necessary for your server in the cloud connect to your on-premises data sources to process and refresh data in the model.</span></span>

> [!TIP]
> <span data-ttu-id="ee896-115">배포하기 전에 테이블에서 데이터를 처리할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-115">Before you deploy, make sure you can process the data in your tables.</span></span> <span data-ttu-id="ee896-116">SSDT에서 **모델** > **처리** > **모두 처리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="ee896-117">처리가 실패하는 경우 성공적으로 배포할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="to-deploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="ee896-118">SSDT에서 테이블 형식 모델을 배포하려면</span><span class="sxs-lookup"><span data-stu-id="ee896-118">To deploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="ee896-119">배포하기 전에 서버 이름을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-119">Before you deploy, you need to get the server name.</span></span> <span data-ttu-id="ee896-120">**Azure Portal** > 서버 > **개요** > **서버 이름**에서 서버 이름을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-120">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Azure에서 서버 이름 가져오기](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="ee896-122">SSDT > **솔루션 탐색기**에서 프로젝트 > **속성**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-122">In SSDT > **Solution Explorer**, right-click the project > **Properties**.</span></span> <span data-ttu-id="ee896-123">그런 다음 **배포** > **서버**에서 서버 이름을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-123">Then in **Deployment** > **Server** paste the server name.</span></span>   
   
    ![배포 서버 속성에 서버 이름을 붙여 넣습니다](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="ee896-125">**솔루션 탐색기**에서 **속성**을 마우스 오른쪽 단추로 클릭한 후 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="ee896-126">Azure에 로그인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-126">You may be prompted to sign in to Azure.</span></span>
   
    ![서버에 배포](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="ee896-128">배포 상태는 출력 창 및 배포 모두에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-128">Deployment status appears in both the Output window and in Deploy.</span></span>
   
    ![배포 상태](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="ee896-130">이제 모든 작업을 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-130">That's all there is to it!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="ee896-131">문제 해결</span><span class="sxs-lookup"><span data-stu-id="ee896-131">Troubleshooting</span></span>
<span data-ttu-id="ee896-132">메타데이터를 배포하는 데 실패한 경우 SSDT가 서버에 연결할 수 없기 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect to your server.</span></span> <span data-ttu-id="ee896-133">SSMS를 사용하여 서버에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-133">Make sure you can connect to your server using SSMS.</span></span> <span data-ttu-id="ee896-134">프로젝트에 대한 배포 서버 속성이 정확한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-134">Then make sure the Deployment Server property for the project is correct.</span></span>

<span data-ttu-id="ee896-135">테이블에서 배포에 실패한 경우 서버가 데이터 원본에 연결할 수 없기 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-135">If deployment fails on a table, it's likely because your server couldn't connect to a data source.</span></span> <span data-ttu-id="ee896-136">데이터 원본이 조직의 온-프레미스에 있는 경우 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-136">If your data source is on-premises in your organization's network, be sure to install an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee896-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ee896-137">Next steps</span></span>
<span data-ttu-id="ee896-138">테이블 형식 모델을 서버에 배포했으므로 연결할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-138">Now that you have your tabular model deployed to your server, you're ready to connect to it.</span></span> <span data-ttu-id="ee896-139">[SSMS과 연결](analysis-services-manage.md)하여 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-139">You can [connect to it with SSMS](analysis-services-manage.md) to manage it.</span></span> <span data-ttu-id="ee896-140">그리고 Power BI, Power BI Desktop 또는 Excel과 같은 [클라이언트 도구를 사용하여 연결](analysis-services-connect.md)하고 보고서를 만들기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee896-140">And, you can [connect to it using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

