---
title: "edifact 디코딩할 앱 B2B aaaLogic 해결 UNH2.5-Azure 논리 앱 | Microsoft Docs"
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
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="74e2c-103">어떻게 toohandle EDIFACT 문서 UNH2.5 있는 세그먼트</span><span class="sxs-lookup"><span data-stu-id="74e2c-103">How toohandle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="74e2c-104">UNH2.5 hello EDIFACT 문서에 있는 경우에 스키마 조회에 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-104">When UNH2.5 is present in hello EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="74e2c-105">예: hello UNH 필드는 **EAN008** hello EDIFACT 메시지에</span><span class="sxs-lookup"><span data-stu-id="74e2c-105">Example: hello UNH field is **EAN008** in hello EDIFACT message</span></span>  
<span data-ttu-id="74e2c-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="74e2c-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="74e2c-107">단계 toofollow toohandle hello 메시지</span><span class="sxs-lookup"><span data-stu-id="74e2c-107">Steps toofollow toohandle hello message</span></span> 
1. <span data-ttu-id="74e2c-108">Hello 스키마 업데이트</span><span class="sxs-lookup"><span data-stu-id="74e2c-108">Update hello schema</span></span>
2. <span data-ttu-id="74e2c-109">Hello 규약 설정 확인</span><span class="sxs-lookup"><span data-stu-id="74e2c-109">Check hello agreement settings</span></span>  

## <a name="update-hello-schema"></a><span data-ttu-id="74e2c-110">Hello 스키마 업데이트</span><span class="sxs-lookup"><span data-stu-id="74e2c-110">Update hello schema</span></span>
<span data-ttu-id="74e2c-111">tooprocess hello 메시지 toodeploy 스키마 hello UNH2.5 루트 노드 이름 사용 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-111">tooprocess hello message, you need toodeploy a schema with hello UNH2.5 root node name.</span></span>  <span data-ttu-id="74e2c-112">예를 제공에 대 한 hello 스키마 루트 이름이 표시 됩니다 **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="74e2c-112">For given an example, hello schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="74e2c-113">다른 UNH2.5 세그먼트와 각 D03B_ORDERS에 대 한 해야 toodeploy 개별 스키마.</span><span class="sxs-lookup"><span data-stu-id="74e2c-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have toodeploy an individual schema.</span></span>  

## <a name="add-schema-toohello-edifact-agreement"></a><span data-ttu-id="74e2c-114">스키마 toohello EDIFACT 규약을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-114">Add schema toohello EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="74e2c-115">EDIFACT 디코딩</span><span class="sxs-lookup"><span data-stu-id="74e2c-115">EDIFACT Decode</span></span>
<span data-ttu-id="74e2c-116">tooDecode 들어오는 메시지를 hello, hello 스키마 구성 hello EDIFACT 규약 수신 설정</span><span class="sxs-lookup"><span data-stu-id="74e2c-116">tooDecode hello incoming message, configure hello schema in hello EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="74e2c-117">Hello 스키마 toohello 통합 계정 추가</span><span class="sxs-lookup"><span data-stu-id="74e2c-117">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="74e2c-118">Hello 스키마 구성 hello EDIFACT 규약 수신 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-118">Configure hello schema in hello EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="74e2c-119">EDIFACT 규약을 선택하고 **JSON으로 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="74e2c-120">Hello 수신 규약에에서 UNH2.5 값을 추가 **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="74e2c-120">Add UNH2.5 value in hello Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="74e2c-121">EDIFACT 인코딩</span><span class="sxs-lookup"><span data-stu-id="74e2c-121">EDIFACT Encode</span></span>
<span data-ttu-id="74e2c-122">tooEncode 들어오는 메시지를 hello hello EDIFACT 규약의 송신 설정에서 hello 스키마를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-122">tooEncode hello incoming message, configure hello schema in hello EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="74e2c-123">Hello 스키마 toohello 통합 계정 추가</span><span class="sxs-lookup"><span data-stu-id="74e2c-123">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="74e2c-124">Hello EDIFACT 규약의 송신 설정에서 hello 스키마를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-124">Configure hello schema in hello EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="74e2c-125">EDIFACT 규약을 선택하고 **JSON으로 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="74e2c-126">송신 계약 hello에 UNH2.5 값을 추가 **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="74e2c-126">Add UNH2.5 value in hello Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="74e2c-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74e2c-127">Next Steps</span></span>
* [<span data-ttu-id="74e2c-128">통합 계정 규약에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="74e2c-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "엔터프라이즈 통합 규약에 대해 알아보기")  