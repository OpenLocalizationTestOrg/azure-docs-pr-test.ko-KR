---
title: "Excel을 사용하여 Azure Analysis Services에 연결 | Microsoft Docs"
description: "Excel을 사용하여 Azure Analysis Services 서버에 연결하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: d51b6980120f1cf9bc8d053d463a73ac600b915f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="eddcf-103">Excel로 연결</span><span class="sxs-lookup"><span data-stu-id="eddcf-103">Connect with Excel</span></span>

<span data-ttu-id="eddcf-104">Azure에서 서버를 만들고 테이블 형식 모델을 배포하면 데이터를 연결하고 탐색할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eddcf-104">Once you've created a server in Azure, and deployed a tabular model to it, you're ready to connect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="eddcf-105">Excel에서 연결</span><span class="sxs-lookup"><span data-stu-id="eddcf-105">Connect in Excel</span></span>

<span data-ttu-id="eddcf-106">Excel 2016에서 Get Data를 사용하여 Excel에서 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="eddcf-106">Connecting to a server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="eddcf-107">파워 피벗에서 테이블 가져오기 마법사를 사용하여 연결하는 작업은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eddcf-107">Connecting by using the Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="eddcf-108">**Excel 2016에서 연결하려면**</span><span class="sxs-lookup"><span data-stu-id="eddcf-108">**To connect in Excel 2016**</span></span>

1. <span data-ttu-id="eddcf-109">Excel 2016의 **데이터** 리본 메뉴에서 **외부 데이터 가져오기** > **다른 원본에서** > **Analysis Services에서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eddcf-109">In Excel 2016, on the **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="eddcf-110">데이터 연결 마법사에서 **서버 이름**에 프로토콜 및 URI를 포함하여 서버 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eddcf-110">In the Data Connection Wizard, in **Server name**, enter the server name including protocol and URI.</span></span> <span data-ttu-id="eddcf-111">그런 다음 **로그온 자격 증명**에서 **다음 사용자 이름 및 암호 사용**을 선택하고 조직 사용자 이름(예: nancy@adventureworks.com 및 암호)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eddcf-111">Then, in **Logon credentials**, select **Use the following User Name and Password**, and then type the organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Excel 로그온에서 연결](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="eddcf-113">**데이터베이스 및 테이블 선택**에서 데이터베이스, 모델 또는 큐브 뷰를 선택한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eddcf-113">In **Select Database and Table**, select the database and model or perspective, and then click **Finish**.</span></span>
   
    ![Excel 선택 모델에서 연결](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="eddcf-115">참고 항목</span><span class="sxs-lookup"><span data-stu-id="eddcf-115">See also</span></span>
<span data-ttu-id="eddcf-116">[클라이언트 라이브러리](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="eddcf-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="eddcf-117">서버 관리</span><span class="sxs-lookup"><span data-stu-id="eddcf-117">Manage your server</span></span>](analysis-services-manage.md)     


