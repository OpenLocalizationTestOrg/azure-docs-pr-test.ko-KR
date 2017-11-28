---
title: "Azure 시간 시계열 Insights의 aaaData 액세스 정책 | Microsoft Docs"
description: "이 자습서에서는 시간 시계열 Insights의 데이터 액세스 정책을 toomanage를 설명"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="b4428-103">Azure 포털을 사용 하 여 권한 부여 데이터 액세스 tooa 시간 계열 Insights 환경</span><span class="sxs-lookup"><span data-stu-id="b4428-103">Grant data access tooa Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="b4428-104">Time Series Insights 환경에는 다음과 같은 두 가지 독립적인 액세스 정책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="b4428-105">관리 액세스 정책</span><span class="sxs-lookup"><span data-stu-id="b4428-105">Management access policies</span></span>
* <span data-ttu-id="b4428-106">데이터 액세스 정책</span><span class="sxs-lookup"><span data-stu-id="b4428-106">Data access policies</span></span>

<span data-ttu-id="b4428-107">두 정책 모두 Azure Active Directory 주체(사용자 및 앱)에게 특정 환경에 대한 다양한 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="b4428-108">hello 이름 (사용자 및 응용 프로그램)의 구성원 이어야 toohello active hello 환경을 포함 하는 hello 구독과 연결 된 디렉터리 (또는 "Azure 테 넌 트").</span><span class="sxs-lookup"><span data-stu-id="b4428-108">hello principals (users and apps) must belong toohello active directory (or “Azure tenant”) associated with hello subscription containing hello environment.</span></span>

<span data-ttu-id="b4428-109">와 같은 권한을 부여 사용 권한 관련된 toohello 구성 hello 환경의 관리 액세스 정책</span><span class="sxs-lookup"><span data-stu-id="b4428-109">Management access policies grant permissions related toohello configuration of hello environment, such as</span></span>
*   <span data-ttu-id="b4428-110">이벤트 소스 hello 환경의 생성 및 삭제 참조 데이터 집합 및</span><span class="sxs-lookup"><span data-stu-id="b4428-110">Creation and deletion of hello environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="b4428-111">Hello 데이터 액세스 정책 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-111">Management of hello data access policies.</span></span>

<span data-ttu-id="b4428-112">데이터 액세스 정책을 tooissue 데이터 쿼리, 사용 권한을 부여 hello 환경에서 참조 데이터를 조작 하 고 hello 환경에 연결 된 큐브 뷰 및 저장 된 쿼리를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-112">Data access policies grant permissions tooissue data queries, manipulate reference data in hello environment, and share saved queries and perspectives associated with hello environment.</span></span>

<span data-ttu-id="b4428-113">hello 두 가지 정책 명확히 구분 hello 환경의 액세스 toohello 관리 및 hello 환경 내 toohello 데이터 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-113">hello two kinds of policies allow clear separation between access toohello management of hello environment and access toohello data inside hello environment.</span></span> <span data-ttu-id="b4428-114">예를 들어, hello 소유자/hello 환경의 작성자 hello 데이터 액세스에서 제거 되는 가능한 toosetup 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-114">For example, it is possible toosetup an environment such that hello owner/creator of hello environment is removed from hello data access.</span></span> <span data-ttu-id="b4428-115">사용자 및 서비스 허용 되는 hello 환경에서 tooread 데이터 뿐 아니라 부여할 수 있습니다 hello 환경의 액세스 toohello 구성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-115">As well as users and services that are allowed tooread data from hello environment may be granted no access toohello configuration of hello environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="b4428-116">데이터 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="b4428-116">Grant data access</span></span>
<span data-ttu-id="b4428-117">hello 다음 단계 표시 toogrant 데이터는 사용자 계정에 대 한 액세스 하는 방법을:</span><span class="sxs-lookup"><span data-stu-id="b4428-117">hello following steps show how toogrant data access for a user principal:</span></span>

1.  <span data-ttu-id="b4428-118">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="b4428-119">Hello hello Azure 포털의 왼쪽에 hello 메뉴에서 "모든 리소스"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-119">Click “All resources” in hello menu on hello left side of hello Azure portal.</span></span>
3.  <span data-ttu-id="b4428-120">Time Series Insights 환경을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-120">Select your Time Series Insights environment.</span></span>

  ![Hello 시간 계열 Insights 원본 관리-환경](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="b4428-122">“데이터 평면 액세스”를 선택하고 “추가”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Hello 시간 계열 Insights 원본 관리-추가](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="b4428-124">“사용자 선택”을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="b4428-125">검색 하 고 hello 전자 메일을 통해 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-125">Search and select user by hello email.</span></span>
7.  <span data-ttu-id="b4428-126">“사용자 선택” 블레이드에서 “선택”을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-126">Click “Select” in “Select User” blade.</span></span>

  ![Hello 시간 계열 Insights 원본 관리-사용자 선택](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="b4428-128">“역할 선택”을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="b4428-129">큐브 뷰 및 저장 된 쿼리를 다른 사용자와 공유할 hello 환경의 tooallow 사용자 toochange 참조 데이터를 원할 경우 "기여자"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-129">Select “Contributor” if you want tooallow user toochange reference data and share saved queries and perspectives with other users of hello environment.</span></span> <span data-ttu-id="b4428-130">그렇지 않으면 hello 환경에서 "Reader" tooallow 사용자 쿼리 데이터를 선택 하 고 hello 환경에서 개인 (공유) 쿼리를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-130">Otherwise select “Reader” tooallow user query data in hello environment and save personal (not shared) queries in hello environment.</span></span>
10. <span data-ttu-id="b4428-131">Hello "선택 역할" 블레이드에서 "확인"을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-131">Click “Ok” in hello “Select Role” blade.</span></span>

  ![Hello 시간 계열 Insights 원본 관리-역할 선택](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="b4428-133">Hello "사용자 역할 선택" 블레이드에서 "확인"을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-133">Click “Ok” in hello “Select User Role” blade.</span></span>
12. <span data-ttu-id="b4428-134">다음과 같은 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4428-134">You should see:</span></span>

  ![Hello 시간 계열 Insights 원본 관리-결과](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="b4428-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4428-136">Next steps</span></span>

* [<span data-ttu-id="b4428-137">이벤트 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="b4428-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="b4428-138">[이벤트를 보내는](time-series-insights-send-events.md) toohello 이벤트 소스</span><span class="sxs-lookup"><span data-stu-id="b4428-138">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="b4428-139">[Time Series Insights 포털](https://insights.timeseries.azure.com)에서 환경 보기</span><span class="sxs-lookup"><span data-stu-id="b4428-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
