---
title: "Power BI를 사용하여 Azure Analysis Services에 연결 | Microsoft Docs"
description: "Power BI를 사용하여 Azure Analysis Services 서버에 연결하는 방법에 대해 알아봅니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3a2af043feddb4a1d6d63f50e838c8a39035449f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="d325a-103">Power BI로 연결</span><span class="sxs-lookup"><span data-stu-id="d325a-103">Connect with Power BI</span></span>

<span data-ttu-id="d325a-104">Azure에서 서버를 만들고 테이블 형식 모델을 배포하면 조직의 사용자는 데이터를 연결하고 탐색할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-104">Once you've created a server in Azure, and deployed a tabular model to it, users in your organization are ready to connect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="d325a-105">최신 버전의 [Power BI Desktop](https://powerbi.microsoft.com/desktop/)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-105">Be sure to use the latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="d325a-106">Power BI Desktop에서 연결</span><span class="sxs-lookup"><span data-stu-id="d325a-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="d325a-107">Power BI Desktop에서 **데이터 가져오기** > **Azure** > **Azure Analysis Services 데이터베이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="d325a-108">**서버**에 서버 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-108">In **Server**, enter the server name.</span></span> 
    
    <span data-ttu-id="d325a-109">전체 URL을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-109">Be sure to include the full URL.</span></span> <span data-ttu-id="d325a-110">예를 들어 asazure://westcentralus.asazure.windows.net/advworks 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="d325a-111">**데이터베이스**에서 연결하려는 테이블 형식 모델 데이터베이스 및 큐브 뷰의 이름을 알고 있는 경우 여기에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-111">In **Database**, if you know the name of the tabular model database or perspective you want to connect to, paste it here.</span></span> <span data-ttu-id="d325a-112">그러지 않으면 이 필드를 비워 두고 나중에 데이터베이스 또는 큐브 뷰를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="d325a-113">기본 **라이브 연결** 옵션을 그대로 두고 **연결**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-113">Leave the default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="d325a-114">메시지가 표시되면 로그인 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="d325a-115">**탐색기**에서 서버를 확장한 다음 연결하려는 모델 또는 큐브 뷰를 선택하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-115">In **Navigator**, expand the server, then select the model or perspective you want to connect to, then click **Connect**.</span></span> <span data-ttu-id="d325a-116">모델 또는 큐브 뷰를 클릭하여 해당 보기에 대한 모든 개체를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-116">Click  a model or perspective to show all the objects for that view.</span></span>

    <span data-ttu-id="d325a-117">모델은 보고서 보기의 빈 보고서와 함께 Power BI Desktop에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-117">The model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="d325a-118">필드 목록에는 숨겨지지 않은 모든 모델 개체가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-118">The Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="d325a-119">연결 상태는 오른쪽 아래 모서리에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-119">Connection status is displayed in the lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="d325a-120">Power BI(서비스)에서 연결</span><span class="sxs-lookup"><span data-stu-id="d325a-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="d325a-121">서버의 모델에 대한 라이브 연결을 포함하는 Power BI Desktop 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-121">Create a Power BI Desktop file that has a live connection to your model on your server.</span></span>
2. <span data-ttu-id="d325a-122">[Power BI](https://powerbi.microsoft.com)에서 **데이터 가져오기** > **파일**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="d325a-123">파일을 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d325a-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="d325a-124">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d325a-124">See also</span></span>
<span data-ttu-id="d325a-125">[Azure Analysis Services에 연결](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="d325a-125">[Connect to Azure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="d325a-126">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="d325a-126">Client libraries</span></span>](analysis-services-data-providers.md)

