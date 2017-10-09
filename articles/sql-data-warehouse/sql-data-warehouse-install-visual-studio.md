---
title: "aaaInstall Visual Studio 및 SQL 데이터 웨어하우스 용 SSDT | Microsoft Docs"
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
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="ed521-103">SQL Data Warehouse용 Visual Studio 및 SSDT 설치</span><span class="sxs-lookup"><span data-stu-id="ed521-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="ed521-104">SQL 데이터 웨어하우스에 대 한 응용 프로그램 toodevelop hello 가장 최신 버전의 Visual Studio를 사용 하 여 hello 가장 최근 버전 SQL Server Data Tools (SSDT)의 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-104">toodevelop applications for SQL Data Warehouse, we recommend using hello most recent version of Visual Studio with hello most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="ed521-105">이전 버전과의 호환성을 위해 SSDT와 함께 Visual Studio 2013 업데이트 5도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="ed521-106">SSDT Visual Studio를 사용 하면 toouse hello SQL Server 개체 탐색기 toovisually 테이블, 뷰, 저장된 프로시저 및 SQL 데이터 웨어하우스에 더 많은 개체를 탐색할 수 있을 뿐만 아니라 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-106">Using Visual Studio with SSDT will allow you toouse hello SQL Server Object Explorer toovisually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="ed521-107">SQL 데이터 웨어하우스는 아직 Visual Studio 데이터베이스 프로젝트를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="ed521-108">이 기능은 이후 버전에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="ed521-109">1단계: Visual Studio 설치</span><span class="sxs-lookup"><span data-stu-id="ed521-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="ed521-110">이러한 링크 toodownload 따르고 Visual Studio를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-110">Follow these links toodownload and install Visual Studio.</span></span> <span data-ttu-id="ed521-111">이미 Visual Studio 2013 또는 이상이 설치 되어 tooStep 2를 건너뛸 수, 하는 경우 SSDT를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-111">If you already have Visual Studio 2013 or later installed, you can skip tooStep 2, install SSDT.</span></span>

1. <span data-ttu-id="ed521-112">[Visual Studio를 다운로드][]합니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="ed521-113">Hello에 따라 [Visual Studio 설치] [ Installing Visual Studio] MSDN에서 안내 하 고 hello 기본 구성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-113">Follow hello [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose hello default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="ed521-114">2단계: SSDT 설치</span><span class="sxs-lookup"><span data-stu-id="ed521-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="ed521-115">Visual Studio 용 SSDT tooinstall 다음이 단계를 수행 하 여 Visual Studio 내에서 SSDT 업데이트에 대 한 단순히 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-115">tooinstall SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="ed521-116">Visual Studio에서 **도구** / **확장 및 업데이트...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="ed521-117"> / **업데이트**</span><span class="sxs-lookup"><span data-stu-id="ed521-117"> / **Updates**</span></span>
2. <span data-ttu-id="ed521-118">**제품 업데이트**를 선택한 후 **데이터베이스 도구용 Microsoft SQL Server 업데이트**를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="ed521-119">업데이트가 발견 되지 않으면 경우에 hello 최신 버전이 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-119">If an update is not found, then you should have hello latest version installed.</span></span>  <span data-ttu-id="ed521-120">tooconfirm SSDT가 설치 되어 클릭 **도움말** / **에 대 한 Microsoft Visual Studio** hello 목록에서 SQL Server Data Tools을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-120">tooconfirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in hello list.</span></span>  <span data-ttu-id="ed521-121">최신 버전의 SSDT hello 14.0.60525.0입니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-121">hello latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="ed521-122">Hello 옵션 tooinstall Visual Studio에서 사용할 수 없는 경우 또는 방문할 수 있습니다 hello [SSDT 다운로드] [ SSDT Download] toodownload 페이지 SSDT를 수동으로 설치 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ed521-122">If hello option tooinstall is not available from Visual Studio, alternatively you can visit hello [SSDT Download][SSDT Download] page toodownload and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed521-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ed521-123">Next steps</span></span>
<span data-ttu-id="ed521-124">Hello 최신 버전의 SSDT가지고 준비가 너무[연결] [ connect] tooyour SQL 데이터 웨어하우스 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed521-124">Now that you have hello latest version of SSDT, you are ready too[connect][connect] tooyour SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Visual Studio를 다운로드]: https://www.visualstudio.com/downloads/합니다.
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
