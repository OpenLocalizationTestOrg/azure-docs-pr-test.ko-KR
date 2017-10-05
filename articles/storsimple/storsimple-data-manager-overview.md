---
title: "Microsoft Azure StorSimple 데이터 관리자 개요 | Microsoft Docs"
description: "StorSimple 데이터 관리자 서비스 개요 제공(비공개 미리 보기)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: aedb44610fe57055851538b9dbdb810e66e58d73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="989d8-103">StorSimple 데이터 관리자 개요(비공개 미리 보기)</span><span class="sxs-lookup"><span data-stu-id="989d8-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="989d8-104">개요</span><span class="sxs-lookup"><span data-stu-id="989d8-104">Overview</span></span>

<span data-ttu-id="989d8-105">Microsoft Azure StorSimple은 일반적으로 파일 공유와 연결된 구조화되지 않은 데이터의 복잡성을 해결하는 하이브리드 클라우드 저장소 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses the complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="989d8-106">StorSimple은 온-프레미스 솔루션의 확장으로 클라우드 저장소를 사용하여 자동으로 온-프레미스 솔루션 및 클라우드 저장소에서 데이터를 계층화합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-106">StorSimple uses cloud storage as an extension of the on-premises solution and automatically tiers data across the on-premises storage and cloud storage.</span></span> <span data-ttu-id="989d8-107">로컬 및 클라우드 스냅숏과 함께 통합 데이터 보호 기능은 제멋대로 늘어나는 저장소 인프라의 필요성을 없애줍니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-107">Integrated data protection, with local and cloud snapshots, eliminates the need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="989d8-108">보관 및 재해 복구는 오프 사이트 위치의 역할을 하는 클라우드와 원활하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-108">Archival and disaster recovery is also seamless with the cloud acting as an offsite location.</span></span>

<span data-ttu-id="989d8-109">이 문서에서 도입한 데이터 변환 서비스를 사용하면 클라우드에서 StorSimple 데이터에 원활하게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-109">The data transformation service that we are introducing in this document, allows you to seamlessly access the StorSimple data in the cloud.</span></span> <span data-ttu-id="989d8-110">이 서비스는 API를 제공하여 StorSimple에서 데이터를 추출하고 해당 데이터를 쉽게 사용할 수 없는 형식으로 다른 Azure 서비스에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-110">This service provides APIs to extract data from StorSimple and present it to other Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="989d8-111">이 미리 보기에서 지원되는 형식은 Azure Blob 및 Azure Media Services 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-111">The formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="989d8-112">이 변환을 사용하면 Azure Media Services, Azure HDInsight, Azure Machine Learning 및 Azure Search와 같은 서비스를 쉽게 연결하여 StorSimple 8000 시리즈 온-프레미스 장치에서 데이터를 운영할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-112">This transformation enables you to easily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search to operate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="989d8-113">이를 보여 주는 높은 수준의 블록 다이어그램은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-113">A high-level block diagram illustrating this is shown below.</span></span>

![높은 수준의 다이어그램](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="989d8-115">이 문서에서는 이 서비스의 비공개 미리 보기에 등록할 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="989d8-116">또한 이 서비스를 사용하여 클라우드에서 StorSimple 데이터 및 기타 Azure 서비스를 사용하는 응용 프로그램을 작성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-116">It also explains how you can use this service to write applications that use StorSimple data and other Azure services in the cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="989d8-117">데이터 관리자 미리 보기에 등록</span><span class="sxs-lookup"><span data-stu-id="989d8-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="989d8-118">데이터 관리자 서비스에 등록하기 전에 다음 필수 구성 요소를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-118">Before you sign up for the Data Manager service, review the following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="989d8-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="989d8-119">Prerequisites</span></span>

<span data-ttu-id="989d8-120">이 연습에서는 사용자에게 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="989d8-121">활성 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="989d8-121">an active Azure subscription.</span></span>
* <span data-ttu-id="989d8-122">등록된 StorSimple 8000 시리즈 장치에 대한 액세스</span><span class="sxs-lookup"><span data-stu-id="989d8-122">access to a registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="989d8-123">StorSimple 8000 시리즈 장치와 연결된 모든 키</span><span class="sxs-lookup"><span data-stu-id="989d8-123">all the keys associated with the StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="989d8-124">등록</span><span class="sxs-lookup"><span data-stu-id="989d8-124">Sign up</span></span>

<span data-ttu-id="989d8-125">StorSimple 데이터 관리자는 비공개 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-125">The StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="989d8-126">비공개 미리 보기인 이 서비스에 등록하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-126">Perform the following steps to sign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="989d8-127">[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)에서 StorSimple 데이터 관리자 확장을 사용하여 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-127">Log into the Azure portal with the StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="989d8-128">Azure 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-128">Use your Azure credentials to log in.</span></span>

2.  <span data-ttu-id="989d8-129">**+** 아이콘을 클릭하여 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-129">Click the **+** icon to create a service.</span></span> <span data-ttu-id="989d8-130">**저장소**를 클릭한 다음 열린 블레이드에서 **모두 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-130">Click **Storage** and then click **See All** in the blade that opens up.</span></span>

    ![StorSimple 데이터 관리자 아이콘 검색](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="989d8-132">StorSimple 데이터 관리자 아이콘이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-132">You see the StorSimple Data Manager icon.</span></span>

    ![StorSimple 데이터 관리자 아이콘 선택](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="989d8-134">StorSimple 데이터 관리자 아이콘을 클릭한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="989d8-135">비공개 미리 보기에 사용하려는 구독을 선택한 다음 **등록하기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-135">Pick the subscription that you want to enable for the private preview and then click **Sign me up!**</span></span>

    ![등록하기](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="989d8-137">요청을 보내서 사용자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-137">This sends a request to onboard you.</span></span> <span data-ttu-id="989d8-138">최대한 빨리 등록하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="989d8-139">구독을 사용하도록 설정한 후에 StorSimple 데이터 관리자 서비스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="989d8-140">StorSimple 데이터 관리자 서비스에 쉽게 액세스하려면 별표 아이콘을 클릭하여 즐겨찾기에 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="989d8-140">To easily access the StorSimple Data Manager service, click the star icon to pin it to your favorites.</span></span>

    ![StorSimple 데이터 관리자에 액세스](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="989d8-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="989d8-142">Next steps</span></span>

<span data-ttu-id="989d8-143">[StorSimple 데이터 관리자 UI를 사용하여 데이터를 변환합니다](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="989d8-143">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>