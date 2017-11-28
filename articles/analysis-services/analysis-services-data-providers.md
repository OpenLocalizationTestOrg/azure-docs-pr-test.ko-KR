---
title: "tooAzure Analysis Services에 연결 하는 데 필요한 aaaClient 라이브러리 | Microsoft Docs"
description: "클라이언트 응용 프로그램 및 도구 tooconnect Azure Analysis Services에 필요한 클라이언트 라이브러리를 설명 합니다."
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
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a><span data-ttu-id="44e58-103">TooAzure Analysis Services에 연결 하기 위한 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="44e58-103">Client libraries for connecting tooAzure Analysis Services</span></span>

<span data-ttu-id="44e58-104">클라이언트 라이브러리는 클라이언트 응용 프로그램 및 도구 tooconnect tooAnalysis 서비스 서버에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-104">Client libraries are necessary for client applications and tools tooconnect tooAnalysis Services servers.</span></span> 

<span data-ttu-id="44e58-105">Analysis Services는 세 가지 클라이언트 라이브러리를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="44e58-106">ADOMD.NET 및 AMO(Analysis Services Management Objects)는 관리되는 클라이언트 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="44e58-107">hello Analysis Services OLE DB 공급자 (MSOLAP DLL)는 네이티브 클라이언트 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-107">hello Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="44e58-108">hello에 3을 모두 설치 하는 일반적으로 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-108">Typically, all three are installed at hello same time.</span></span> <span data-ttu-id="44e58-109">Azure Analysis Services hello 최신 버전이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-109">Azure Analysis Services requires hello latest versions.</span></span> 

<span data-ttu-id="44e58-110">Power BI Desktop 및 Excel과 같은 Microsoft 클라이언트 응용 프로그램은 세 가지 클라이언트 라이브러리를 모두 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="44e58-111">그러나 hello 버전 또는 업데이트 빈도 따라 클라이언트 라이브러리 아닐 Azure Analysis Services에서 필요한 hello 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-111">However, depending on hello version or frequency of updates, client libraries may not be hello latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="44e58-112">hello 마찬가지 toocustom 응용 프로그램이 나 AsCmd, TOM, ADOMD.NET 같은 다른 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-112">hello same applies toocustom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="44e58-113">이러한 응용 프로그램 hello 라이브러리를 수동으로 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-113">These applications require manually installing hello libraries.</span></span> <span data-ttu-id="44e58-114">수동 설치를 위한 hello 클라이언트 라이브러리는 배포 가능한 패키지와 SQL Server 기능 팩에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-114">hello client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="44e58-115">그러나 이러한 클라이언트 라이브러리 동률된 toohello SQL Server 버전 이며 hello를 최신 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-115">However, these client libraries are tied toohello SQL Server version and may not be hello latest.</span></span>  

<span data-ttu-id="44e58-116">클라이언트 연결에 대 한 클라이언트 라이브러리는 Azure Analysis Services 서버 tooa 데이터 원본에서 데이터 공급자 필요한 tooconnect 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-116">Client libraries for client connections are different from data providers required tooconnect from an Azure Analysis Services server tooa data source.</span></span> <span data-ttu-id="44e58-117">데이터 원본 연결에 대해 자세히 toolearn 참조 [데이터 원본 연결](analysis-services-datasource.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-117">toolearn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-hello-latest-client-libraries"></a><span data-ttu-id="44e58-118">Hello 최신 클라이언트 라이브러리 다운로드</span><span class="sxs-lookup"><span data-stu-id="44e58-118">Download hello latest client libraries</span></span>  
<span data-ttu-id="44e58-119">프로덕션 환경에 있으며 완전히 해제 한 후 지원 되는 버전을 필요로 하는 경우 클라이언트 라이브러리를 따라 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44e58-119">Use hello following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="44e58-120">MSOLAP(amd64)</span><span class="sxs-lookup"><span data-stu-id="44e58-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="44e58-121">
[MSOLAP(x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="44e58-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="44e58-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="44e58-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="44e58-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="44e58-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="44e58-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="44e58-124">Next steps</span></span>
<span data-ttu-id="44e58-125">[Excel로 연결](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="44e58-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="44e58-126">Power BI와 연결</span><span class="sxs-lookup"><span data-stu-id="44e58-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
