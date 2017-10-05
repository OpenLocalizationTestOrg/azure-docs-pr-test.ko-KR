---
title: "Logic Apps B2B EDIFACT 디코딩 확인 UNH2.5 - Azure Logic Apps | Microsoft Docs"
description: "Azure Logic Apps B2B EDIFACT 디코딩 확인 UNH2.5"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 62ad8183cc6e9f56255b2729a04ee7710d00a21a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-handle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="05ff7-103">UNH2.5 세그먼트를 포함하는 EDIFACT 문서를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="05ff7-103">How to handle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="05ff7-104">EDIFACT 문서에 UNH2.5가 표시되면 스키마 조회에 사용되고 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-104">When UNH2.5 is present in the EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="05ff7-105">예제: UNH 필드는 EDIFACT 메시지에서 **EAN008**입니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-105">Example: The UNH field is **EAN008** in the EDIFACT message</span></span>  
<span data-ttu-id="05ff7-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="05ff7-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="05ff7-107">메시지를 처리하기 위해 수행하는 단계</span><span class="sxs-lookup"><span data-stu-id="05ff7-107">Steps to follow to handle the message</span></span> 
1. <span data-ttu-id="05ff7-108">스키마 업데이트</span><span class="sxs-lookup"><span data-stu-id="05ff7-108">Update the schema</span></span>
2. <span data-ttu-id="05ff7-109">규약 설정 확인</span><span class="sxs-lookup"><span data-stu-id="05ff7-109">Check the agreement settings</span></span>  

## <a name="update-the-schema"></a><span data-ttu-id="05ff7-110">스키마 업데이트</span><span class="sxs-lookup"><span data-stu-id="05ff7-110">Update the schema</span></span>
<span data-ttu-id="05ff7-111">메시지를 처리하려면 UNH2.5 루트 노드 이름을 갖는 스키마를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-111">To process the message, you need to deploy a schema with the UNH2.5 root node name.</span></span>  <span data-ttu-id="05ff7-112">예제에서 스키마 루트 이름은 **EFACT_D03B_ORDERS_EAN008**입니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-112">For given an example, the schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="05ff7-113">다른 UNH2.5 세그먼트를 갖는 각 D03B_ORDERS에 대해 개별 스키마를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have to deploy an individual schema.</span></span>  

## <a name="add-schema-to-the-edifact-agreement"></a><span data-ttu-id="05ff7-114">EDIFACT 규약에 스키마 추가</span><span class="sxs-lookup"><span data-stu-id="05ff7-114">Add schema to the EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="05ff7-115">EDIFACT 디코딩</span><span class="sxs-lookup"><span data-stu-id="05ff7-115">EDIFACT Decode</span></span>
<span data-ttu-id="05ff7-116">들어오는 메시지를 디코딩하려면 EDIFACT 규약 수신 설정에서 스키마를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-116">To Decode the incoming message, configure the schema in the EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="05ff7-117">통합 계정에 스키마를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-117">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="05ff7-118">EDIFACT 규약 수신 설정에서 스키마를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-118">Configure the schema in the EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="05ff7-119">EDIFACT 규약을 선택하고 **JSON으로 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="05ff7-120">수신 규약 **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)에 UNH2.5 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-120">Add UNH2.5 value in the Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="05ff7-121">EDIFACT 인코딩</span><span class="sxs-lookup"><span data-stu-id="05ff7-121">EDIFACT Encode</span></span>
<span data-ttu-id="05ff7-122">들어오는 메시지를 인코딩하려면 EDIFACT 규약 송신 설정에서 스키마를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-122">To Encode the incoming message, configure the schema in the EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="05ff7-123">통합 계정에 스키마를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-123">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="05ff7-124">EDIFACT 규약 송신 설정에서 스키마를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-124">Configure the schema in the EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="05ff7-125">EDIFACT 규약을 선택하고 **JSON으로 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="05ff7-126">송신 규약 **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)에 UNH2.5 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05ff7-126">Add UNH2.5 value in the Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="05ff7-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="05ff7-127">Next Steps</span></span>
* [<span data-ttu-id="05ff7-128">통합 계정 규약에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="05ff7-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "엔터프라이즈 통합 규약에 대해 알아보기")  