---
title: "통합 계정 아티팩트 메타데이터 관리 - Azure Logic Apps | Microsoft Docs"
description: "Azure Logic Apps에 대한 통합 계정에서 아티팩트 메타데이터 추가 또는 검색"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 28bb8296ddd820ec5aa9793dc0928b4b1e67bf6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="fa923-103">Logic Apps에 대한 통합 계정에서 아티팩트 메타데이터 관리</span><span class="sxs-lookup"><span data-stu-id="fa923-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="fa923-104">통합 계정에서 아티팩트에 대한 사용자 지정 메타데이터를 정의하고 논리 앱에 대한 런타임 동안 해당 메타데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="fa923-105">예를 들어 파트너, 규약, 스키마 및 맵 등의 아티팩트에 대해 메타데이터를 지정할 수 있습니다. 모두 키-값 쌍을 사용해서 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="fa923-106">현재 아티팩트는 UI를 통해 메타데이터를 만들 수 없고 REST API를 사용하여 메타데이터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs to create metadata.</span></span> <span data-ttu-id="fa923-107">Azure Portal에서 파트너, 규약, 또는 스키마를 만들거나 선택할 때 메타데이터를 추가하려면 **JSON으로 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-107">To add metadata when you create or select a partner, agreement, or schema in the Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="fa923-108">Logic Apps에서 아티팩트 메타데이터를 검색하려면 통합 계정 아티팩트 조회 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-108">To retrieve artifact metadata in logic apps, you can use the Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-to-artifacts-in-integration-accounts"></a><span data-ttu-id="fa923-109">통합 계정에서 아티팩트에 메타데이터 추가</span><span class="sxs-lookup"><span data-stu-id="fa923-109">Add metadata to artifacts in integration accounts</span></span>

1. <span data-ttu-id="fa923-110">[통합 계정](logic-apps-enterprise-integration-create-integration-account.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="fa923-111">예를 들어 통합 계정에 [파트너](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [계약](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements) 또는 [스키마](logic-apps-enterprise-integration-schemas.md)와 같은 아티팩트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-111">Add an artifact to your integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="fa923-112">아티팩트를 선택하고 **JSON으로 편집**을 선택한 후 메타데이터 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-112">Select the artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![메타데이터 입력](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="fa923-114">Logic Apps에 대한 아티팩트에서 메타데이터 검색</span><span class="sxs-lookup"><span data-stu-id="fa923-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="fa923-115">[논리 앱](logic-apps-create-a-logic-app.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="fa923-116">[논리 앱에서 통합 계정으로의 연결](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-116">Create a [link from your logic app to your integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="fa923-117">논리 앱 디자이너에서 *요청* 또는 *HTTP*와 같은 트리거를 논리 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-117">In Logic App Designer, add a trigger like *Request* or *HTTP* to your logic app.</span></span>

4.  <span data-ttu-id="fa923-118">**다음 단계** > **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="fa923-119">*통합*을 검색합니다. 그러면 **통합 계정 - 통합 계정 아티팩트 조회**를 찾아서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![통합 계정 아티팩트 조회 선택](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="fa923-121">**아티팩트 유형**을 선택하고 **아티팩트 이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-121">Select the **Artifact Type**, and provide the **Artifact Name**.</span></span>

    ![아티팩트 유형 선택 및 아티팩트 이름 제공](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="fa923-123">예제: 파트너 메타데이터 검색</span><span class="sxs-lookup"><span data-stu-id="fa923-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="fa923-124">파트너 메타데이터는 다음과 같은 세 가지 `routingUrl` 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-124">Partner metadata has these `routingUrl` details:</span></span>

![파트너 "routingURL" 메타데이터 찾기](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="fa923-126">논리 앱에서 트리거, 파트너에 대한 **통합 계정 - 통합계정 아티팩트 조회** 작업 및 **HTTP**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![논리 앱에 트리거, 아티팩트 조회 및 "HTTP" 추가](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="fa923-128">URI를 검색하려면 논리 앱에 대한 코드 보기로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-128">To retrieve the URI, go to Code View for your logic app.</span></span> <span data-ttu-id="fa923-129">논리 앱 정의가 다음 예제와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa923-129">Your logic app definition should look like this example:</span></span>

    ![검색 조회](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="fa923-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fa923-131">Next steps</span></span>
* [<span data-ttu-id="fa923-132">규약에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="fa923-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "엔터프라이즈 통합 규약에 대해 알아보기")  
