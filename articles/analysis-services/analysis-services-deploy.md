---
title: "SSDT를 사용 하 여 Analysis Services aaaDeploy tooAzure | Microsoft Docs"
description: "Azure Analysis Services 하는 테이블 형식 모델 tooan toodeploy 방법에 대해 알아봅니다 SSDT를 사용 하 여 서버입니다."
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
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="e444b-103">SSDT에서 모델 배포</span><span class="sxs-lookup"><span data-stu-id="e444b-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="e444b-104">Azure 구독에는 서버를 만들면 준비 toodeploy 테이블 형식 모델 데이터베이스 tooit 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-104">Once you've created a server in your Azure subscription, you're ready toodeploy a tabular model database tooit.</span></span> <span data-ttu-id="e444b-105">SQL Server Data Tools (SSDT) toobuild를 사용할 수 있으며에서 작업 하는 테이블 형식 모델 프로젝트를 배포.</span><span class="sxs-lookup"><span data-stu-id="e444b-105">You can use SQL Server Data Tools (SSDT) toobuild and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e444b-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e444b-106">Prerequisites</span></span>
<span data-ttu-id="e444b-107">시작 tooget를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-107">tooget started, you need:</span></span>

* <span data-ttu-id="e444b-108">Azure의 **Analysis Services 서버** -</span><span class="sxs-lookup"><span data-stu-id="e444b-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="e444b-109">toolearn 더 참조 [Azure Analysis Services 서버를 만들](analysis-services-create-server.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-109">toolearn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="e444b-110">**테이블 형식 모델 프로젝트** SSDT 또는 1200 hello 또는 더 높은 호환성 수준에서 기존 테이블 형식 모델에서.</span><span class="sxs-lookup"><span data-stu-id="e444b-110">**Tabular model project** in SSDT or an existing tabular model at hello 1200 or higher compatibility level.</span></span> <span data-ttu-id="e444b-111">만들어 본 적이 없나요?</span><span class="sxs-lookup"><span data-stu-id="e444b-111">Never created one?</span></span> <span data-ttu-id="e444b-112">Hello 시도 [Adventure Works 인터넷 판매 테이블 형식 모델링 자습서](https://msdn.microsoft.com/library/hh231691.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-112">Try hello [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="e444b-113">**온-프레미스 게이트웨이** -tooinstall 하나 이상의 데이터 원본을 온-프레미스 조직 네트워크의 경우 해야는 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="e444b-114">hello 게이트웨이 hello 클라우드에서 서버 tooyour 온-프레미스 데이터 원본 tooprocess 및 새로 고침 데이터 hello 모델에서 연결을 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-114">hello gateway is necessary for your server in hello cloud connect tooyour on-premises data sources tooprocess and refresh data in hello model.</span></span>

> [!TIP]
> <span data-ttu-id="e444b-115">를 배포 하기 전에 테이블의 hello 데이터를 처리할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-115">Before you deploy, make sure you can process hello data in your tables.</span></span> <span data-ttu-id="e444b-116">SSDT에서 **모델** > **처리** > **모두 처리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="e444b-117">처리가 실패하는 경우 성공적으로 배포할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="e444b-118">toodeploy SSDT에서 테이블 형식 모델</span><span class="sxs-lookup"><span data-stu-id="e444b-118">toodeploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="e444b-119">를 배포 하기 전에 tooget hello 서버 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-119">Before you deploy, you need tooget hello server name.</span></span> <span data-ttu-id="e444b-120">**Azure 포털** > 서버 > **개요** > **서버 이름**, hello 서버 이름 복사.</span><span class="sxs-lookup"><span data-stu-id="e444b-120">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Azure에서 서버 이름 가져오기](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="e444b-122">SSDT에서 > **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello 프로젝트 > **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-122">In SSDT > **Solution Explorer**, right-click hello project > **Properties**.</span></span> <span data-ttu-id="e444b-123">그런 다음 **배포** > **서버** hello 서버 이름을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-123">Then in **Deployment** > **Server** paste hello server name.</span></span>   
   
    ![배포 서버 속성에 서버 이름을 붙여 넣습니다](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="e444b-125">**솔루션 탐색기**에서 **속성**을 마우스 오른쪽 단추로 클릭한 후 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="e444b-126">TooAzure에서 증명된 toosign 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-126">You may be prompted toosign in tooAzure.</span></span>
   
    ![Tooserver 배포](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="e444b-128">배포 상태는 배포 및 두 hello 출력 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-128">Deployment status appears in both hello Output window and in Deploy.</span></span>
   
    ![배포 상태](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="e444b-130">그 tooit 있습니다!</span><span class="sxs-lookup"><span data-stu-id="e444b-130">That's all there is tooit!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="e444b-131">문제 해결</span><span class="sxs-lookup"><span data-stu-id="e444b-131">Troubleshooting</span></span>
<span data-ttu-id="e444b-132">메타 데이터를 배포할 때 배포에 실패 될 SSDT tooyour 서버를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect tooyour server.</span></span> <span data-ttu-id="e444b-133">SSMS를 사용 하 여 tooyour 서버를 연결할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-133">Make sure you can connect tooyour server using SSMS.</span></span> <span data-ttu-id="e444b-134">Hello hello 프로젝트에 대 한 배포 서버 속성이 올바른지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-134">Then make sure hello Deployment Server property for hello project is correct.</span></span>

<span data-ttu-id="e444b-135">배포에 실패 한 테이블에 되므로 가능성이 서버 tooa 데이터 원본에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-135">If deployment fails on a table, it's likely because your server couldn't connect tooa data source.</span></span> <span data-ttu-id="e444b-136">데이터 원본이 온-프레미스 조직 네트워크의 경우 수 있는지 tooinstall는 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-136">If your data source is on-premises in your organization's network, be sure tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e444b-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e444b-137">Next steps</span></span>
<span data-ttu-id="e444b-138">테이블 형식 모델 배포 tooyour 서버를가지고 준비 tooconnect tooit 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-138">Now that you have your tabular model deployed tooyour server, you're ready tooconnect tooit.</span></span> <span data-ttu-id="e444b-139">있습니다 수 [tooit SSMS를 사용 하 여 연결](analysis-services-manage.md) toomanage 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-139">You can [connect tooit with SSMS](analysis-services-manage.md) toomanage it.</span></span> <span data-ttu-id="e444b-140">할 수 있습니다 및 [tooit 클라이언트 도구를 사용 하 여 연결](analysis-services-connect.md) 같은 Power BI, Power BI Desktop 또는 Excel 및 보고서를 만들기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e444b-140">And, you can [connect tooit using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

