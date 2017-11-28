---
title: "SQL Data Warehouse용 Visual Studio 및 SSDT 설치 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스용 Visual Studio 및 SSDT(SQL Server 개발 도구) 설치"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: f7023b78c241a7bc8014276cd0bfa455165b42cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="9dcd1-103">SQL Data Warehouse용 Visual Studio 및 SSDT 설치</span><span class="sxs-lookup"><span data-stu-id="9dcd1-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="9dcd1-104">SQL 데이터 웨어하우스용 응용 프로그램을 개발하려면 최신 버전의 SSDT(SQL Server 데이터 도구)와 함께 최신 버전의 Visual Studio를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-104">To develop applications for SQL Data Warehouse, we recommend using the most recent version of Visual Studio with the most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="9dcd1-105">이전 버전과의 호환성을 위해 SSDT와 함께 Visual Studio 2013 업데이트 5도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="9dcd1-106">SSDT로 Visual Studio를 사용하면 시각적 탐색 테이블, 뷰, 저장된 프로시저 및 SQL 데이터 웨어하우스의 더 많은 개체 뿐만 아니라 쿼리 실행에 SQL Server 개체 탐색기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-106">Using Visual Studio with SSDT will allow you to use the SQL Server Object Explorer to visually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="9dcd1-107">SQL 데이터 웨어하우스는 아직 Visual Studio 데이터베이스 프로젝트를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="9dcd1-108">이 기능은 이후 버전에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="9dcd1-109">1단계: Visual Studio 설치</span><span class="sxs-lookup"><span data-stu-id="9dcd1-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="9dcd1-110">이 링크를 따라 Visual Studio를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-110">Follow these links to download and install Visual Studio.</span></span> <span data-ttu-id="9dcd1-111">Visual Studio 2013 이상이 설치되어 있는 경우 2단계로 건너뛰어 SSDT를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-111">If you already have Visual Studio 2013 or later installed, you can skip to Step 2, install SSDT.</span></span>

1. <span data-ttu-id="9dcd1-112">[Visual Studio를 다운로드][]합니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="9dcd1-113">MSDN의 [Visual Studio 설치][Installing Visual Studio] 지침을 따르고 기본 구성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-113">Follow the [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose the default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="9dcd1-114">2단계: SSDT 설치</span><span class="sxs-lookup"><span data-stu-id="9dcd1-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="9dcd1-115">Visual Studio 용 SSDT를 설치하려면 다음 이 단계를 수행하여 Visual Studio 내에서 SSDT 업데이트를 확인하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-115">To install SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="9dcd1-116">Visual Studio에서 **도구** / **확장 및 업데이트...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="9dcd1-117"> / **업데이트**</span><span class="sxs-lookup"><span data-stu-id="9dcd1-117"> / **Updates**</span></span>
2. <span data-ttu-id="9dcd1-118">**제품 업데이트**를 선택한 후 **데이터베이스 도구용 Microsoft SQL Server 업데이트**를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="9dcd1-119">업데이트가 없는 경우 최신 버전을 설치했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-119">If an update is not found, then you should have the latest version installed.</span></span>  <span data-ttu-id="9dcd1-120">SSDT가 설치되었는지 확인하려면 **도움말** / **Microsoft Visual Studio 정보**를 클릭하여 목록에서 SQL Server 데이터 도구를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-120">To confirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in the list.</span></span>  <span data-ttu-id="9dcd1-121">최신 버전의 SSDT는 14.0.60525.0입니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-121">The latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="9dcd1-122">설치 옵션을 Visual Studio에서 사용할 수 없는 경우 [SSDT 다운로드][SSDT Download] 페이지를 방문하여 SSDT를 수동으로 다운로드하고 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-122">If the option to install is not available from Visual Studio, alternatively you can visit the [SSDT Download][SSDT Download] page to download and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9dcd1-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9dcd1-123">Next steps</span></span>
<span data-ttu-id="9dcd1-124">이제 최신 버전의 SSDT가 설치되었으므로 SQL Data Warehouse에 [연결][connect]할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-124">Now that you have the latest version of SSDT, you are ready to [connect][connect] to your SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
<span data-ttu-id="9dcd1-125">[Visual Studio를 다운로드]: https://www.visualstudio.com/downloads/합니다.</span><span class="sxs-lookup"><span data-stu-id="9dcd1-125">[Download Visual Studio]: https://www.visualstudio.com/downloads/</span></span>
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
