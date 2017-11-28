---
title: "aaaMicrosoft Azure StorSimple 데이터 관리자 개요 | Microsoft Docs"
description: "Hello 데이터 StorSimple Manager 서비스 (비공개 미리 보기)에 대 한 개요를 제공합니다."
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
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="bc8eb-103">StorSimple 데이터 관리자 개요(비공개 미리 보기)</span><span class="sxs-lookup"><span data-stu-id="bc8eb-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="bc8eb-104">개요</span><span class="sxs-lookup"><span data-stu-id="bc8eb-104">Overview</span></span>

<span data-ttu-id="bc8eb-105">Microsoft Azure StorSimple 주소 hello 일반적으로 파일 공유와 관련 된 구조화 되지 않은 데이터의 복잡성을 하는 하이브리드 클라우드 저장소 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses hello complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="bc8eb-106">StorSimple의 hello 확장 온-프레미스 솔루션 및 hello 온-프레미스 저장소와 클라우드 저장소에서 데이터를 자동으로 눈금으로 클라우드 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-106">StorSimple uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="bc8eb-107">데이터 보호와 통합 된 로컬 및 클라우드 스냅숏, 대 한 저장소 인프라에 대 한 hello 필요성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-107">Integrated data protection, with local and cloud snapshots, eliminates hello need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="bc8eb-108">보관 및 재해 복구 역할을 오프 사이트 위치 hello 클라우드로 원활 하 게 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-108">Archival and disaster recovery is also seamless with hello cloud acting as an offsite location.</span></span>

<span data-ttu-id="bc8eb-109">이 문서에 도입 하는 hello 데이터 변환 서비스 있습니다 tooseamlessly 액세스 hello를 StorSimple 클라우드의 데이터를 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-109">hello data transformation service that we are introducing in this document, allows you tooseamlessly access hello StorSimple data in hello cloud.</span></span> <span data-ttu-id="bc8eb-110">이 서비스는 StorSimple에서 Api tooextract 데이터를 제공 하 고 Azure tooother 제공할 서비스를 쉽게 사용할 수 있는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-110">This service provides APIs tooextract data from StorSimple and present it tooother Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="bc8eb-111">이 미리 보기에서 지 원하는 hello 형식은 Azure blob 및 Azure 미디어 서비스 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-111">hello formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="bc8eb-112">이 변환에는 StorSimple 8000 시리즈 온-프레미스 장치에서 Azure 미디어 서비스, Azure HDInsight, Azure 기계 학습 및 Azure 검색 toooperate 데이터 등의 서비스를 있습니다 tooeasily 연결할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-112">This transformation enables you tooeasily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search toooperate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="bc8eb-113">이를 보여 주는 높은 수준의 블록 다이어그램은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-113">A high-level block diagram illustrating this is shown below.</span></span>

![높은 수준의 다이어그램](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="bc8eb-115">이 문서에서는 이 서비스의 비공개 미리 보기에 등록할 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="bc8eb-116">또한 hello 클라우드에서 StorSimple 데이터 및 기타 Azure 서비스를 사용 하는이 서비스 toowrite 응용 프로그램을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-116">It also explains how you can use this service toowrite applications that use StorSimple data and other Azure services in hello cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="bc8eb-117">데이터 관리자 미리 보기에 등록</span><span class="sxs-lookup"><span data-stu-id="bc8eb-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="bc8eb-118">Hello 데이터 관리자 서비스에 등록 하기 전에 hello 다음 필수 구성 요소를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-118">Before you sign up for hello Data Manager service, review hello following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="bc8eb-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="bc8eb-119">Prerequisites</span></span>

<span data-ttu-id="bc8eb-120">이 연습에서는 사용자에게 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="bc8eb-121">활성 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="bc8eb-121">an active Azure subscription.</span></span>
* <span data-ttu-id="bc8eb-122">액세스 tooa StorSimple 8000 시리즈 장치 등록</span><span class="sxs-lookup"><span data-stu-id="bc8eb-122">access tooa registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="bc8eb-123">모든 hello hello StorSimple 8000 시리즈 장치에 연관 된 키입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-123">all hello keys associated with hello StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="bc8eb-124">등록</span><span class="sxs-lookup"><span data-stu-id="bc8eb-124">Sign up</span></span>

<span data-ttu-id="bc8eb-125">StorSimple 데이터 관리자 hello 비공개 미리 보기 버전에서입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-125">hello StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="bc8eb-126">Hello 단계 toosign이이 서비스의 비공개 미리 보기에 대해 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-126">Perform hello following steps toosign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="bc8eb-127">에 로그인 hello Azure 포털에서 StorSimple Data Manager 확장 hello: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-127">Log into hello Azure portal with hello StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="bc8eb-128">Azure 자격 증명 toolog 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-128">Use your Azure credentials toolog in.</span></span>

2.  <span data-ttu-id="bc8eb-129">Hello 클릭  **+**  아이콘 toocreate 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-129">Click hello **+** icon toocreate a service.</span></span> <span data-ttu-id="bc8eb-130">클릭 **저장소** 클릭 하 고 **모든 참조** 가 열리면 hello 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-130">Click **Storage** and then click **See All** in hello blade that opens up.</span></span>

    ![StorSimple 데이터 관리자 아이콘 검색](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="bc8eb-132">Hello StorSimple 데이터 관리자 아이콘을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-132">You see hello StorSimple Data Manager icon.</span></span>

    ![StorSimple 데이터 관리자 아이콘 선택](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="bc8eb-134">StorSimple 데이터 관리자 아이콘을 클릭한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="bc8eb-135">Hello 구독 tooenable hello 비공개 미리 보기를 선택 하 고 클릭 선택 **보기 등록 합니다!**</span><span class="sxs-lookup"><span data-stu-id="bc8eb-135">Pick hello subscription that you want tooenable for hello private preview and then click **Sign me up!**</span></span>

    ![등록하기](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="bc8eb-137">이 전송 요청 tooonboard 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-137">This sends a request tooonboard you.</span></span> <span data-ttu-id="bc8eb-138">최대한 빨리 등록하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="bc8eb-139">구독을 사용하도록 설정한 후에 StorSimple 데이터 관리자 서비스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="bc8eb-140">tooeasily hello 데이터 StorSimple Manager 서비스에 액세스, 별 모양 아이콘 toopin hello 클릭 것 tooyour 즐겨찾기 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-140">tooeasily access hello StorSimple Data Manager service, click hello star icon toopin it tooyour favorites.</span></span>

    ![StorSimple 데이터 관리자에 액세스](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="bc8eb-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bc8eb-142">Next steps</span></span>

<span data-ttu-id="bc8eb-143">[데이터 tootransform StorSimple 데이터 관리자 UI를 사용 하 여](storsimple-data-manager-ui.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8eb-143">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
