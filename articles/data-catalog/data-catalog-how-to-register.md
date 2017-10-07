---
title: "Azure Data Catalog에서 데이터 원본을 aaaRegister | Microsoft Docs"
description: "이 문서는 hello 메타 데이터 필드를 비롯 한 Azure 데이터 카탈로그에서 tooregister 데이터 원본을 등록 하는 동안 추출 하는 방법을 강조 표시 합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: bab89906-186f-4d35-9ffd-61b1d903905d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: efc8a852ddc9fb4bbacc7b0280477bd47814936f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-sources-in-azure-data-catalog"></a><span data-ttu-id="799c1-103">Azure Data Catalog에서 데이터 원본 등록</span><span class="sxs-lookup"><span data-stu-id="799c1-103">Register data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="799c1-104">소개</span><span class="sxs-lookup"><span data-stu-id="799c1-104">Introduction</span></span>
<span data-ttu-id="799c1-105">Azure Data Catalog는 기업 데이터 원본의 등록 시스템 및 검색 역할을 하는 완전히 관리되는 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-105">Azure Data Catalog is a fully managed cloud service that serves as a system of registration and discovery for enterprise data sources.</span></span> <span data-ttu-id="799c1-106">다시 말해서 데이터 카탈로그는 사람들이 데이터 원본을 검색하고 이해하고 사용하도록 도우면서 조직의 기존 데이터로부터 더 많은 가치를 얻어내도록 돕는 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-106">In other words, Data Catalog helps people discover, understand, and use data sources, and it helps organizations get more value from their existing data.</span></span> <span data-ttu-id="799c1-107">첫 번째 단계 toomaking 데이터 소스를 hello 데이터 카탈로그를 통해 검색할 수는 tooregister 해당 데이터 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-107">hello first step toomaking a data source discoverable via Data Catalog is tooregister that data source.</span></span>

## <a name="register-data-sources"></a><span data-ttu-id="799c1-108">데이터 원본 등록</span><span class="sxs-lookup"><span data-stu-id="799c1-108">Register data sources</span></span>
<span data-ttu-id="799c1-109">등록은 hello 과정을 hello 데이터 원본에서 메타 데이터를 추출 하 고 해당 데이터 toohello 데이터 카탈로그 서비스를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-109">Registration is hello process of extracting metadata from hello data source and copying that data toohello Data Catalog service.</span></span> <span data-ttu-id="799c1-110">hello 데이터는 유지 여기서 현재 상주 하 고 hello 관리자의 hello 제어 및 정책의 hello 현재 시스템의 상태를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-110">hello data remains where it currently resides, and it remains under hello control of hello administrators and policies of hello current system.</span></span>

<span data-ttu-id="799c1-111">데이터 원본 tooregister 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-111">tooregister a data source, do hello following:</span></span>
1. <span data-ttu-id="799c1-112">Hello Azure Data Catalog 포털 hello 데이터 카탈로그 데이터 원본 등록 도구를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-112">In hello Azure Data Catalog portal, start hello Data Catalog data source registration tool.</span></span> 
2. <span data-ttu-id="799c1-113">동일한 hello로 회사 또는 학교 계정으로 로그인 toosign toohello 포털에서 사용 하는 Azure Active Directory 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-113">Sign in with your work or school account with hello same Azure Active Directory credentials that you use toosign in toohello portal.</span></span>
3. <span data-ttu-id="799c1-114">원하는 tooregister hello 데이터 원본을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-114">Select hello data source you want tooregister.</span></span>

<span data-ttu-id="799c1-115">자세한 단계별 세부 정보에 대 한 참조 hello [Azure Data Catalog 시작](data-catalog-get-started.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-115">For more step-by-step details, see hello [Get Started with Azure Data Catalog](data-catalog-get-started.md) tutorial.</span></span>

<span data-ttu-id="799c1-116">Hello 데이터 소스를 등록 한 후 hello 카탈로그의 위치를 추적 하 고 해당 메타 데이터를 인덱싱합니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-116">After you've registered hello data source, hello catalog tracks its location and indexes its metadata.</span></span> <span data-ttu-id="799c1-117">사용자 수 검색, 탐색 및 hello 데이터 원본 검색 및 다음 해당 위치 tooconnect tooit를 사용 하 여 hello 응용 프로그램이 나 선택한 도구를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-117">Users can search, browse, and discover hello data source, and then use its location tooconnect tooit by using hello application or tool of their choice.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="799c1-118">지원되는 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="799c1-118">Supported data sources</span></span>
<span data-ttu-id="799c1-119">현재 지원되는 데이터 원본 목록은 [데이터 카탈로그 DSR](data-catalog-dsr.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="799c1-119">For a list of currently supported data sources, see [Data Catalog DSR](data-catalog-dsr.md).</span></span>

## <a name="structural-metadata"></a><span data-ttu-id="799c1-120">구조적 메타데이터</span><span class="sxs-lookup"><span data-stu-id="799c1-120">Structural metadata</span></span>
<span data-ttu-id="799c1-121">데이터 소스를 등록할 때 hello 등록 도구 선택 하는 hello 개체의 hello 구조에 대 한 정보를 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-121">When you register a data source, hello registration tool extracts information about hello structure of hello objects you select.</span></span> <span data-ttu-id="799c1-122">이 정보는 참조 된 tooas 구조적 메타 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-122">This information is referred tooas structural metadata.</span></span>

<span data-ttu-id="799c1-123">모든 개체에 대 한 구조적 메타 데이터가이 hello 데이터를 검색 하는 사용자가 선택한 hello 클라이언트 도구에서 해당 정보 tooconnect toohello 개체를 사용할 수 있도록 hello 개체의 위치가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-123">For all objects, this structural metadata includes hello object’s location, so that users who discover hello data can use that information tooconnect toohello object in hello client tools of their choice.</span></span> <span data-ttu-id="799c1-124">다른 구조적 메타데이터는 개체 이름과 유형 및 특성/열 이름과 데이터 유형을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-124">Other structural metadata includes object name and type, and attribute/column name and data type.</span></span>

## <a name="descriptive-metadata"></a><span data-ttu-id="799c1-125">설명이 포함된 메타데이터</span><span class="sxs-lookup"><span data-stu-id="799c1-125">Descriptive metadata</span></span>
<span data-ttu-id="799c1-126">또한 toohello 핵심 hello 데이터 원본에서 추출 된 구조적 메타 데이터, hello 데이터 원본 등록 도구 설명이 포함 된 메타 데이터를 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-126">In addition toohello core structural metadata that's extracted from hello data source, hello data source registration tool extracts descriptive metadata.</span></span> <span data-ttu-id="799c1-127">SQL Server Analysis Services 및 SQL Server Reporting Services에 대 한 이러한 서비스에서 노출 하는 hello 설명 속성에서이 메타 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-127">For SQL Server Analysis Services and SQL Server Reporting Services, this metadata is taken from hello Description properties exposed by these services.</span></span> <span data-ttu-id="799c1-128">SQL Server, ms hello를 사용 하 여 제공 된 값에 대 한\_확장 속성 설명에서 추출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-128">For SQL Server, values provided using hello ms\_description extended property is extracted.</span></span> <span data-ttu-id="799c1-129">Oracle 데이터베이스에 대 한 hello 데이터 원본 등록 도구 추출 hello 주석 열에서 모든 hello\_탭\_주석 보기.</span><span class="sxs-lookup"><span data-stu-id="799c1-129">For Oracle Database, hello data-source registration tool extracts hello COMMENTS column from hello ALL\_TAB\_COMMENTS view.</span></span>

<span data-ttu-id="799c1-130">또한 toohello 설명이 포함 된 메타 데이터의 hello 데이터 원본에서 추출 된 hello 데이터 원본 등록 도구를 사용 하 여 설명 메타 데이터를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-130">In addition toohello descriptive metadata that's extracted from hello data source, users can enter descriptive metadata by using hello data source registration tool.</span></span> <span data-ttu-id="799c1-131">사용자가 태그를 추가 하 고 등록 되는 hello 개체에 대 한 전문가 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-131">Users can add tags, and they can identify experts for hello objects being registered.</span></span> <span data-ttu-id="799c1-132">이 설명이 포함 된 메타 데이터는 모두 hello 구조적 메타 데이터와 함께 toohello 데이터 카탈로그 서비스를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-132">All this descriptive metadata is copied toohello Data Catalog service along with hello structural metadata.</span></span>

## <a name="include-previews"></a><span data-ttu-id="799c1-133">미리 보기 포함</span><span class="sxs-lookup"><span data-stu-id="799c1-133">Include previews</span></span>
<span data-ttu-id="799c1-134">기본적으로 이해 데이터 원본을 더 자주 쉽게 포함 된 hello 데이터의 샘플을 볼 수 있을 때 데이터 원본 및 복사한 toohello 데이터 카탈로그 서비스 에서만 메타 데이터만 추출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-134">By default, only metadata is extracted from data sources and copied toohello Data Catalog service, but understanding a data source is often made easier when you can view a sample of hello data it contains.</span></span>

<span data-ttu-id="799c1-135">데이터 카탈로그 데이터 소스 hello 등록 도구를 사용 하 여 각 테이블 및 등록 된 보기에 hello 데이터의 스냅숏을 미리 보기를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-135">By using hello Data Catalog data-source registration tool, you can include a snapshot preview of hello data in each table and view that is registered.</span></span> <span data-ttu-id="799c1-136">등록 중 tooinclude 미리 보기를 선택 하면 hello 등록 도구에서 각 테이블 및 뷰의 too20 레코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-136">If you choose tooinclude previews during registration, hello registration tool includes up too20 records from each table and view.</span></span> <span data-ttu-id="799c1-137">이 스냅숏은 다음 복사 hello 구조적 및 설명이 포함 된 메타 데이터와 함께 toohello 카탈로그입니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-137">This snapshot is then copied toohello catalog along with hello structural and descriptive metadata.</span></span>

> [!NOTE]
> <span data-ttu-id="799c1-138">다수의 열을 포함하는 넓은 테이블은 미리 보기의 레코드가 20개 미만이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-138">Wide tables with a large number of columns might have fewer than 20 records included in their preview.</span></span>
>
>

## <a name="include-data-profiles"></a><span data-ttu-id="799c1-139">데이터 프로필 포함</span><span class="sxs-lookup"><span data-stu-id="799c1-139">Include data profiles</span></span>
<span data-ttu-id="799c1-140">포함 하 여 미리 보기 Data Catalog에서 데이터 원본을 검색 하는 사용자에 대 한 중요 한 컨텍스트를 제공와 마찬가지로 데이터 프로필을 포함 하 여 만들 수 쉽게 toounderstand 검색 데이터 원본.</span><span class="sxs-lookup"><span data-stu-id="799c1-140">Just as including previews can provide valuable context for users who search for data sources in Data Catalog, including a data profile can make it easier toounderstand discovered data sources.</span></span>

<span data-ttu-id="799c1-141">데이터 카탈로그 데이터 소스 hello 등록 도구를 사용 하 여 각 테이블 및 등록 된 보기에 대 한 데이터 프로필을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-141">By using hello Data Catalog data-source registration tool, you can include a data profile for each table and view that is registered.</span></span> <span data-ttu-id="799c1-142">Hello 등록 도구 hello 데이터에 대 한 집계 통계에 포함 되어 각 테이블 및 보기에 등록 하는 동안 데이터 프로필 tooinclude 선택 하면 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="799c1-142">If you choose tooinclude a data profile during registration, hello registration tool includes aggregate statistics about hello data in each table and view, including:</span></span>

* <span data-ttu-id="799c1-143">hello hello 개체에 hello 데이터 크기 및 행 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-143">hello number of rows and size of hello data in hello object.</span></span>
* <span data-ttu-id="799c1-144">hello 데이터와 hello 개체 스키마의 hello 가장 최근의 업데이트에 대 한 hello 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-144">hello date for hello most recent update of hello data and hello object schema.</span></span>
* <span data-ttu-id="799c1-145">hello null 레코드 및 열에 대 한 고유 값 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-145">hello number of null records and distinct values for columns.</span></span>
* <span data-ttu-id="799c1-146">열에 대 한 hello 최소값, 최대값, 평균 및 표준 편차 값입니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-146">hello minimum, maximum, average, and standard deviation values for columns.</span></span>

<span data-ttu-id="799c1-147">이러한 통계는 다음 복사 hello 구조적 및 설명이 포함 된 메타 데이터와 함께 toohello 카탈로그입니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-147">These statistics are then copied toohello catalog along with hello structural and descriptive metadata.</span></span>

> [!NOTE]
> <span data-ttu-id="799c1-148">텍스트 및 날짜 열은 해당 데이터 프로필의 평균 또는 표준 편차 통계에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-148">Text and date columns do not include average or standard deviation statistics in their data profile.</span></span>
>
>

## <a name="update-registrations"></a><span data-ttu-id="799c1-149">등록 업데이트</span><span class="sxs-lookup"><span data-stu-id="799c1-149">Update registrations</span></span>
<span data-ttu-id="799c1-150">데이터 원본 등록 하면 데이터 카탈로그에서 검색 가능한 hello 메타 데이터 및 등록 하는 동안 추출 하는 선택적 미리 보기를 사용 하는 경우 있습니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-150">Registering a data source makes it discoverable in Data Catalog when you use hello metadata and optional preview extracted during registration.</span></span> <span data-ttu-id="799c1-151">데이터 소스 hello toobe hello 카탈로그 (예를 들어 경우 개체의 hello 스키마가 변경 하 고, 원래 제외 테이블에 포함 되어야 할지 또는 hello 미리 보기에 포함 된 tooupdate hello 데이터)에서 업데이트 해야 하는 경우 hello 데이터 원본 등록 도구 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-151">If hello data source needs toobe updated in hello catalog (for example, if hello schema of an object has changed, tables originally excluded should be included, or you want tooupdate hello data that's included in hello previews), hello data source registration tool can be re-run.</span></span>

<span data-ttu-id="799c1-152">이미 등록된 데이터 원본의 재등록은 병합 “upsert” 작업을 수행합니다. 기존 개체는 업데이트되고 새 개체가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-152">Re-registering an already-registered data source performs a merge “upsert” operation: existing objects are updated, and new objects are created.</span></span> <span data-ttu-id="799c1-153">Hello Data Catalog 포털을 통해 사용자가 제공 된 모든 메타 데이터가 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-153">Any metadata provided by users through hello Data Catalog portal are retained.</span></span>

## <a name="summary"></a><span data-ttu-id="799c1-154">요약</span><span class="sxs-lookup"><span data-stu-id="799c1-154">Summary</span></span>
<span data-ttu-id="799c1-155">데이터 원본 toohello 카탈로그 서비스에서 구조적 및 설명이 포함 된 메타 데이터를 복사 하기 때문에 데이터 카탈로그에 hello 데이터 원본 등록 hello 데이터 보다 쉽게 toodiscover 만들고 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-155">Because it copies structural and descriptive metadata from a data source toohello catalog service, registering hello data source in Data Catalog makes hello data easier toodiscover and understand.</span></span> <span data-ttu-id="799c1-156">Hello 데이터 소스를 등록 한 후 주석을 달 수, 관리 및 hello Data Catalog 포털을 사용 하 여 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-156">After you have registered hello data source, you can annotate, manage, and discover it by using hello Data Catalog portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="799c1-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="799c1-157">Next steps</span></span>
<span data-ttu-id="799c1-158">데이터 원본 등록에 대 한 자세한 내용은 참조 hello [Azure Data Catalog 시작](data-catalog-get-started.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="799c1-158">For more information about registering data sources, see hello [Get Started with Azure Data Catalog](data-catalog-get-started.md) tutorial.</span></span>
