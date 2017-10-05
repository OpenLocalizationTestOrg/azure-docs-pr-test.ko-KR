---
title: "변환을 사용하여 XML 데이터 변환 - Azure Logic Apps | Microsoft Docs"
description: "엔터프라이즈 통합 SDK를 사용하여 Logic Apps에서 XML 데이터를 다른 형식으로 변환하기 위한 변환 또는 맵 만들기"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: fb6027769377b3527b11f7831dab3bb8d7061c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="b4f21-103">XML 변환과 엔터프라이즈 통합</span><span class="sxs-lookup"><span data-stu-id="b4f21-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="b4f21-104">개요</span><span class="sxs-lookup"><span data-stu-id="b4f21-104">Overview</span></span>
<span data-ttu-id="b4f21-105">엔터프라이즈 통합 변환 커넥터에서는 데이터의 형식을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-105">The Enterprise integration Transform connector converts data from one format to another format.</span></span> <span data-ttu-id="b4f21-106">예를 들어 YearMonthDay 형식의 현재 날짜가 포함된 들어오는 메시지가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-106">For example, you may have an incoming message that contains the current date in the YearMonthDay format.</span></span> <span data-ttu-id="b4f21-107">날짜를 MonthDayYear 형식으로 변경하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-107">You can use a transform to reformat the date to be in the MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="b4f21-108">변환의 기능은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="b4f21-108">What does a transform do?</span></span>
<span data-ttu-id="b4f21-109">맵으로 알려진 변환은 원본 XML 스키마(입력)와 대상 XML 스키마(출력)로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-109">A Transform, which is also known as a map, consists of a Source XML schema (the input) and a Target XML schema (the output).</span></span> <span data-ttu-id="b4f21-110">다양한 기본 제공 함수를 사용하여 문자열 조작, 조건부 할당, 산술 식, 날짜 시간 포맷터, 루핑 구문 등을 비롯한 데이터를 조작하거나 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-110">You can use different built-in functions to help manipulate or control the data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-to-create-a-transform"></a><span data-ttu-id="b4f21-111">변환 생성 방법</span><span class="sxs-lookup"><span data-stu-id="b4f21-111">How to create a transform?</span></span>
<span data-ttu-id="b4f21-112">Visual Studio [엔터프라이즈 통합 SDK](https://aka.ms/vsmapsandschemas)를 사용하여 변환/맵을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-112">You can create a transform/map by using the Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="b4f21-113">변환을 만들고 테스트하는 작업을 완료한 경우 통합 계정으로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-113">When you are finished creating and testing the transform, you upload the transform into your integration account.</span></span> 

## <a name="how-to-use-a-transform"></a><span data-ttu-id="b4f21-114">변환 사용 방법</span><span class="sxs-lookup"><span data-stu-id="b4f21-114">How to use a transform</span></span>
<span data-ttu-id="b4f21-115">변환/맵을 통합 계정에 업로드한 후에 논리 앱을 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-115">After you upload the transform/map into your integration account, you can use it to create a Logic app.</span></span> <span data-ttu-id="b4f21-116">논리 앱은 논리 앱이 트리거될 때마다 (그리고 변환해야 하는 입력 콘텐츠가 있는 경우) 변환을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-116">The Logic app runs your transformations whenever the Logic app is triggered (and there is input content that needs to be transformed).</span></span>

<span data-ttu-id="b4f21-117">**변환을 사용하는 단계는 다음과 같습니다**.</span><span class="sxs-lookup"><span data-stu-id="b4f21-117">**Here are the steps to use a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b4f21-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b4f21-118">Prerequisites</span></span>

* <span data-ttu-id="b4f21-119">통합 계정을 만든 후 맵 추가</span><span class="sxs-lookup"><span data-stu-id="b4f21-119">Create an integration account and add a map to it</span></span>  

<span data-ttu-id="b4f21-120">지금까지 필수 구성 요소를 살펴보았습니다. 이제 논리 앱을 만들 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-120">Now that you've taken care of the prerequisites, it's time to create your Logic app:</span></span>  

1. <span data-ttu-id="b4f21-121">논리 앱을 만들고 맵을 포함하는 [통합 계정에 연결](../logic-apps/logic-apps-enterprise-integration-accounts.md "논리 앱에 통합 계정을 연결하는 방법 알아보기")합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-121">Create a Logic app and [link it to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that contains the map.</span></span>
2. <span data-ttu-id="b4f21-122">논리 앱에 **요청** 트리거 추가</span><span class="sxs-lookup"><span data-stu-id="b4f21-122">Add a **Request** trigger to your Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="b4f21-123">먼저 **작업 추가** 를 선택하여 **변환 XML** 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-123">Add the **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="b4f21-124">사용하려는 작업에 대해 모든 작업을 필터링하기 위해 검색 상자에 *변환*이라는 단어를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-124">Enter the word *transform* in the search box to filter all the actions to the one that you want to use</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="b4f21-125">**변환 XML** 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-125">Select the **Transform XML** action</span></span>   
6. <span data-ttu-id="b4f21-126">변환할 XML **콘텐츠** 를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-126">Add the XML **CONTENT** that you transform.</span></span> <span data-ttu-id="b4f21-127">HTTP 요청에서 수신한 XML 데이터를 **콘텐츠**로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-127">You can use any XML data you receive in the HTTP request as the **CONTENT**.</span></span> <span data-ttu-id="b4f21-128">이 예제에서는 논리 앱을 트리거한 HTTP 요청의 본문을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-128">In this example, select the body of the HTTP request that triggered the Logic app.</span></span>
7. <span data-ttu-id="b4f21-129">변환을 수행하는 데 사용하려는 **맵** 의 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-129">Select the name of the **MAP** that you want to use to perform the transformation.</span></span> <span data-ttu-id="b4f21-130">맵이 이미 통합 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-130">The map must already be in your integration account.</span></span> <span data-ttu-id="b4f21-131">이전 단계에서 맵을 포함한 통합 계정에 논리 앱 액세스 권한을 이미 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-131">In an earlier step, you already gave your Logic app access to your integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="b4f21-132">작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="b4f21-133">이 시점에서 맵의 설정이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="b4f21-134">실제 응용 프로그램에서는 SalesForce와 같은 LOB 응용 프로그램에 변환한 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-134">In a real world application, you may want to store the transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="b4f21-135">Salesforce에 변환의 출력을 보내는 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-135">You can easily as an action to send the output of the transform to Salesforce.</span></span> 

<span data-ttu-id="b4f21-136">이제 HTTP 끝점에 요청하여 변환을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-136">You can now test your transform by making a request to the HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="b4f21-137">기능 및 사용 사례</span><span class="sxs-lookup"><span data-stu-id="b4f21-137">Features and use cases</span></span>
* <span data-ttu-id="b4f21-138">맵에서 만든 변환은 이름과 주소를 한 문서에서 다른 문서로 복사하는 것과 같이 단순할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-138">The transformation created in a map can be simple, such as copying a name and address from one document to another.</span></span> <span data-ttu-id="b4f21-139">또는 기본 맵 작업을 사용하여 더 복잡한 변환을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-139">Or, you can create more complex transformations using the out-of-the-box map operations.</span></span>  
* <span data-ttu-id="b4f21-140">문자열, 날짜 시간 함수 등 여러 맵 작업이나 함수를 바로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="b4f21-141">스키마 간에 직접 데이터 복사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-141">You can do a direct data copy between the schemas.</span></span> <span data-ttu-id="b4f21-142">SDK에 포함된 매퍼에서 원본 스키마의 요소를 대상 스키마의 대응 항목과 연결하는 선을 그리기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-142">In the Mapper included in the SDK, this is as simple as drawing a line that connects the elements in the source schema with their counterparts in the destination schema.</span></span>  
* <span data-ttu-id="b4f21-143">맵을 만들 때 만들어진 모든 관계와 링크를 보여 주는 맵의 그래픽 표현이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-143">When creating a map, you view a graphical representation of the map, which shows all the relationships and links you create.</span></span>
* <span data-ttu-id="b4f21-144">맵 테스트 기능을 사용하여 샘플 XML 메시지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-144">Use the Test Map feature to add a sample XML message.</span></span> <span data-ttu-id="b4f21-145">한 번만 클릭하면 만든 맵을 테스트하고 생성된 출력을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-145">With a simple click, you can test the map you created, and see the generated output.</span></span>  
* <span data-ttu-id="b4f21-146">기존 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="b4f21-146">Upload existing maps</span></span>  
* <span data-ttu-id="b4f21-147">XML 형식 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f21-147">Includes support for the XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="b4f21-148">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="b4f21-148">Learn more</span></span>
* [<span data-ttu-id="b4f21-149">엔터프라이즈 통합 팩에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="b4f21-149">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대해 알아보기")  
* [<span data-ttu-id="b4f21-150">맵에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="b4f21-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "엔터프라이즈 통합 맵에 대해 알아보기")  

