---
title: "Azure Time Series Insights의 데이터 액세스 정책 | Microsoft Docs"
description: "이 자습서에서는 Time Series Insights의 데이터 액세스 정책을 관리하는 방법을 배웁니다."
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
ms.openlocfilehash: e975c6d8f217bc73948c0c046204b16b1a742bc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="grant-data-access-to-a-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="0ca26-103">Azure Portal을 사용하여 Time Series Insights 환경에 대한 데이터 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="0ca26-103">Grant data access to a Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="0ca26-104">Time Series Insights 환경에는 다음과 같은 두 가지 독립적인 액세스 정책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="0ca26-105">관리 액세스 정책</span><span class="sxs-lookup"><span data-stu-id="0ca26-105">Management access policies</span></span>
* <span data-ttu-id="0ca26-106">데이터 액세스 정책</span><span class="sxs-lookup"><span data-stu-id="0ca26-106">Data access policies</span></span>

<span data-ttu-id="0ca26-107">두 정책 모두 Azure Active Directory 주체(사용자 및 앱)에게 특정 환경에 대한 다양한 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="0ca26-108">주체(사용자 및 앱)는 환경을 포함하고 있는 구독과 연결된 활성 디렉터리(또는 “Azure 테넌트”)에 속해 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-108">The principals (users and apps) must belong to the active directory (or “Azure tenant”) associated with the subscription containing the environment.</span></span>

<span data-ttu-id="0ca26-109">관리 액세스 정책은</span><span class="sxs-lookup"><span data-stu-id="0ca26-109">Management access policies grant permissions related to the configuration of the environment, such as</span></span>
*   <span data-ttu-id="0ca26-110">환경 생성 및 삭제, 이벤트 원본, 참조 데이터 집합 및</span><span class="sxs-lookup"><span data-stu-id="0ca26-110">Creation and deletion of the environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="0ca26-111">데이터 액세스 정책 관리 등 환경의 구성과 관련된 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-111">Management of the data access policies.</span></span>

<span data-ttu-id="0ca26-112">데이터 액세스 정책은 데이터 쿼리를 실행하고 환경에서 참조 데이터를 조작하며 환경과 관련된 저장된 쿼리 및 관심 사항을 공유 할 수 있는 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-112">Data access policies grant permissions to issue data queries, manipulate reference data in the environment, and share saved queries and perspectives associated with the environment.</span></span>

<span data-ttu-id="0ca26-113">두 종류의 정책은 환경 관리에 대한 액세스와 환경 내 데이터에 대한 액세스를 명확하게 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-113">The two kinds of policies allow clear separation between access to the management of the environment and access to the data inside the environment.</span></span> <span data-ttu-id="0ca26-114">예를 들어 환경의 소유자/생성자가 데이터 액세스에서 제거되도록 환경을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-114">For example, it is possible to setup an environment such that the owner/creator of the environment is removed from the data access.</span></span> <span data-ttu-id="0ca26-115">환경에서 데이터를 읽을 수 있는 사용자 및 서비스에도 환경의 구성에 대한 액세스 권한을 부여하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-115">As well as users and services that are allowed to read data from the environment may be granted no access to the configuration of the environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="0ca26-116">데이터 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="0ca26-116">Grant data access</span></span>
<span data-ttu-id="0ca26-117">다음 단계는 사용자 주체에 대한 데이터 액세스를 부여하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-117">The following steps show how to grant data access for a user principal:</span></span>

1.  <span data-ttu-id="0ca26-118">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="0ca26-119">Azure Portal의 왼쪽에 있는 메뉴에서 “모든 리소스”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-119">Click “All resources” in the menu on the left side of the Azure portal.</span></span>
3.  <span data-ttu-id="0ca26-120">Time Series Insights 환경을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-120">Select your Time Series Insights environment.</span></span>

  ![Time Series Insights 소스 관리 - 환경](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="0ca26-122">“데이터 평면 액세스”를 선택하고 “추가”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Time Series Insights 소스 관리 - 추가](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="0ca26-124">“사용자 선택”을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="0ca26-125">전자 메일로 사용자를 검색하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-125">Search and select user by the email.</span></span>
7.  <span data-ttu-id="0ca26-126">“사용자 선택” 블레이드에서 “선택”을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-126">Click “Select” in “Select User” blade.</span></span>

  ![Time Series Insights 소스 관리 - 사용자 선택](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="0ca26-128">“역할 선택”을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="0ca26-129">사용자가 참조 데이터를 변경하고 저장된 쿼리 및 큐브 뷰를 환경의 다른 사용자와 공유할 수 있게 허용하려면 “참가자”를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-129">Select “Contributor” if you want to allow user to change reference data and share saved queries and perspectives with other users of the environment.</span></span> <span data-ttu-id="0ca26-130">또는 사용자가 환경의 데이터를 쿼리하고 개인(공유되지 않는) 쿼리를 환경에 저장할 수 있게 허용하려면 “읽기 권한자”를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-130">Otherwise select “Reader” to allow user query data in the environment and save personal (not shared) queries in the environment.</span></span>
10. <span data-ttu-id="0ca26-131">“역할 선택” 블레이드에서 “확인”을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-131">Click “Ok” in the “Select Role” blade.</span></span>

  ![Time Series Insights 소스 관리 - 역할 선택](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="0ca26-133">“사용자 역할 선택” 블레이드에서 “확인”을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-133">Click “Ok” in the “Select User Role” blade.</span></span>
12. <span data-ttu-id="0ca26-134">다음과 같은 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ca26-134">You should see:</span></span>

  ![Time Series Insights 소스 관리 - 결과](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="0ca26-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0ca26-136">Next steps</span></span>

* [<span data-ttu-id="0ca26-137">이벤트 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="0ca26-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="0ca26-138">이벤트 원본으로 [이벤트 보내기](time-series-insights-send-events.md)</span><span class="sxs-lookup"><span data-stu-id="0ca26-138">[Send events](time-series-insights-send-events.md) to the event source</span></span>
* <span data-ttu-id="0ca26-139">[Time Series Insights 포털](https://insights.timeseries.azure.com)에서 환경 보기</span><span class="sxs-lookup"><span data-stu-id="0ca26-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
