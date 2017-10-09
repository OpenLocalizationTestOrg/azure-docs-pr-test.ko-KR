---
title: "Azure 논리 앱 aaaValidate XML-| Microsoft Docs"
description: "엔터프라이즈 통합 팩 hello를 사용 하 여 Azure 논리 앱 및 B2B 시나리오에 대 한 스키마와 XML 유효성 검사"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="5103c-103">엔터프라이즈 통합에 대한 XML 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="5103c-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="5103c-104">종종 B2B 시나리오에서 hello 파트너 규약에서 hello 메시지를 교환 하는 유효한 데이터 처리를 시작할 수 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5103c-104">Often in B2B scenarios, hello partners in an agreement must make sure that hello messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="5103c-105">Hello 엔터프라이즈 통합 팩의에서 커넥터 hello 사용 hello XML 유효성 검사를 사용 하 여 미리 정의 된 스키마에 대 한 문서를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5103c-105">You can validate documents against a predefined schema by using hello use hello XML Validation connector in hello Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-hello-xml-validation-connector"></a><span data-ttu-id="5103c-106">Hello XML 유효성 검사 커넥터와 함께 문서 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="5103c-106">Validate a document with hello XML Validation connector</span></span>

1. <span data-ttu-id="5103c-107">논리 앱 만들기 및 [hello 앱 toohello 통합 계정 연결](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink 통합 계정 tooa 논리 앱에 알아봅니다") hello 스키마 toouse XML 데이터 유효성 검사에 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5103c-107">Create a logic app, and [link hello app toohello integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that has hello schema you want toouse for validating XML data.</span></span>

2. <span data-ttu-id="5103c-108">추가 **요청-때 HTTP 요청을 받으면** 트리거 tooyour 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="5103c-108">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="5103c-109">tooadd hello **XML 유효성 검사** 동작을 선택 **동작 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5103c-109">tooadd hello **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="5103c-110">원하는 하나 작업 toohello hello 모든 toofilter 입력 *xml* hello 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5103c-110">toofilter all hello actions toohello one that you want, enter *xml* in hello search box.</span></span> <span data-ttu-id="5103c-111">**XML 유효성 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5103c-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="5103c-112">toospecify hello toovalidate, 원하는 XML 콘텐츠 선택 **콘텐츠**합니다.</span><span class="sxs-lookup"><span data-stu-id="5103c-112">toospecify hello XML content that you want toovalidate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="5103c-113">Hello toovalidate 원하는 내용으로 hello body 태그를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5103c-113">Select hello body tag as hello content that you want toovalidate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="5103c-114">toouse hello 이전 유효성 검사에 대 한 원하는 toospecify hello 스키마 *콘텐츠* 입력, 선택 **스키마 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="5103c-114">toospecify hello schema you want toouse for validating hello previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="5103c-115">작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5103c-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="5103c-116">이제 유효성 검사 커넥터 설정이 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="5103c-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="5103c-117">실제 응용 프로그램에서 SalesForce와 같은 기간 업무 (LOB) 응용 프로그램에서 유효성을 검사 하는 hello 데이터 toostore 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5103c-117">In a real world application, you might want toostore hello validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="5103c-118">toosend는 유효성이 검사 된 출력 tooSalesforce hello, 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5103c-118">toosend hello validated output tooSalesforce, add an action.</span></span>

<span data-ttu-id="5103c-119">tootest 유효성 검사 동작을 요청 toohello HTTP 끝점을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5103c-119">tootest your validation action, make a request toohello HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5103c-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5103c-120">Next steps</span></span>
[<span data-ttu-id="5103c-121">엔터프라이즈 통합 팩 hello에 대 한 자세한</span><span class="sxs-lookup"><span data-stu-id="5103c-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보")   

