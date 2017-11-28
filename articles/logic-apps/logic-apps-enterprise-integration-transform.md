---
title: "Azure 논리 앱-변환 사용 하 여 XML 데이터 aaaConvert | Microsoft Docs"
description: "변환 또는 mapps hello 엔터프라이즈 통합 SDK를 사용 하 여 논리 앱에 대 한 형식 간에 tooconvert XML 데이터 만들기"
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
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="fad71-103">XML 변환과 엔터프라이즈 통합</span><span class="sxs-lookup"><span data-stu-id="fad71-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="fad71-104">개요</span><span class="sxs-lookup"><span data-stu-id="fad71-104">Overview</span></span>
<span data-ttu-id="fad71-105">hello 엔터프라이즈 통합 변환 커넥터 형식 tooanother 형식 으로부터 데이터를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-105">hello Enterprise integration Transform connector converts data from one format tooanother format.</span></span> <span data-ttu-id="fad71-106">예를 들어 hello hello YearMonthDay 형식의 현재 날짜를 포함 하는 들어오는 메시지를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-106">For example, you may have an incoming message that contains hello current date in hello YearMonthDay format.</span></span> <span data-ttu-id="fad71-107">변환 tooreformat hello 날짜 toobe hello MonthDayYear 형식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-107">You can use a transform tooreformat hello date toobe in hello MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="fad71-108">변환의 기능은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="fad71-108">What does a transform do?</span></span>
<span data-ttu-id="fad71-109">지도 라고도 변환을 소스 XML 스키마 (입력 hello)와 대상 XML 스키마 (hello 출력)으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-109">A Transform, which is also known as a map, consists of a Source XML schema (hello input) and a Target XML schema (hello output).</span></span> <span data-ttu-id="fad71-110">도 루프 구문 및 문자열 조작, 조건부 할당, 산술 식, 날짜 시간 포맷터를 포함 하 여 서로 다른 기본 제공 함수 toohelp 조작 하거나 컨트롤 hello 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-110">You can use different built-in functions toohelp manipulate or control hello data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-toocreate-a-transform"></a><span data-ttu-id="fad71-111">어떻게 toocreate 변환?</span><span class="sxs-lookup"><span data-stu-id="fad71-111">How toocreate a transform?</span></span>
<span data-ttu-id="fad71-112">변환/매핑 hello Visual Studio를 사용 하 여 만들 수 있습니다 [엔터프라이즈 통합 SDK](https://aka.ms/vsmapsandschemas)합니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-112">You can create a transform/map by using hello Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="fad71-113">완료를 만들고 테스트 hello 변환 되 면 통합 계정에 hello 변환을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-113">When you are finished creating and testing hello transform, you upload hello transform into your integration account.</span></span> 

## <a name="how-toouse-a-transform"></a><span data-ttu-id="fad71-114">어떻게 toouse 변환</span><span class="sxs-lookup"><span data-stu-id="fad71-114">How toouse a transform</span></span>
<span data-ttu-id="fad71-115">Hello 변환/매핑을 통합 계정에 업로드 한 후 논리 앱 toocreate를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-115">After you upload hello transform/map into your integration account, you can use it toocreate a Logic app.</span></span> <span data-ttu-id="fad71-116">hello 논리 앱 hello 논리 앱 (트리거되고 toobe 변환 해야 하는 입력 콘텐츠가) 될 때마다 변환을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-116">hello Logic app runs your transformations whenever hello Logic app is triggered (and there is input content that needs toobe transformed).</span></span>

<span data-ttu-id="fad71-117">**같습니다. hello 단계 toouse 변환을**:</span><span class="sxs-lookup"><span data-stu-id="fad71-117">**Here are hello steps toouse a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fad71-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fad71-118">Prerequisites</span></span>

* <span data-ttu-id="fad71-119">통합 계정을 만들고 지도 tooit 추가</span><span class="sxs-lookup"><span data-stu-id="fad71-119">Create an integration account and add a map tooit</span></span>  

<span data-ttu-id="fad71-120">이제 hello 필수 구성 요소 처리 한 있습니다,입니다 시간 toocreate 논리 앱:</span><span class="sxs-lookup"><span data-stu-id="fad71-120">Now that you've taken care of hello prerequisites, it's time toocreate your Logic app:</span></span>  

1. <span data-ttu-id="fad71-121">논리 앱 만들기 및 [tooyour 통합 계정 연결](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink 통합 계정 tooa 논리 앱에 알아봅니다") hello 맵을 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-121">Create a Logic app and [link it tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that contains hello map.</span></span>
2. <span data-ttu-id="fad71-122">추가 **요청** 트리거 tooyour 논리 앱</span><span class="sxs-lookup"><span data-stu-id="fad71-122">Add a **Request** trigger tooyour Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="fad71-123">추가 hello **XML 변환** 먼저 선택 하 여 작업 **동작 추가** </span><span class="sxs-lookup"><span data-stu-id="fad71-123">Add hello **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="fad71-124">Hello 단어를 입력 *변환* toouse 되도록 하나 작업 toohello를 모든 hello hello 검색 상자 toofilter</span><span class="sxs-lookup"><span data-stu-id="fad71-124">Enter hello word *transform* in hello search box toofilter all hello actions toohello one that you want toouse</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="fad71-125">선택 hello **XML 변환** 동작</span><span class="sxs-lookup"><span data-stu-id="fad71-125">Select hello **Transform XML** action</span></span>   
6. <span data-ttu-id="fad71-126">Hello XML 추가 **콘텐츠** 변환입니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-126">Add hello XML **CONTENT** that you transform.</span></span> <span data-ttu-id="fad71-127">Hello hello HTTP 요청에 수신 하는 XML 데이터를 사용할 수 있습니다 **콘텐츠**합니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-127">You can use any XML data you receive in hello HTTP request as hello **CONTENT**.</span></span> <span data-ttu-id="fad71-128">이 예에서는 hello hello 논리 앱을 트리거한 hello HTTP 요청 본문을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-128">In this example, select hello body of hello HTTP request that triggered hello Logic app.</span></span>
7. <span data-ttu-id="fad71-129">Hello의 선택 hello 이름을 **지도** toouse tooperform hello 변환 한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-129">Select hello name of hello **MAP** that you want toouse tooperform hello transformation.</span></span> <span data-ttu-id="fad71-130">hello 지도 통합 계정에 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-130">hello map must already be in your integration account.</span></span> <span data-ttu-id="fad71-131">이전 단계에서 이미 제공한 맵이 포함 된 논리 앱 액세스 tooyour 통합 계정.</span><span class="sxs-lookup"><span data-stu-id="fad71-131">In an earlier step, you already gave your Logic app access tooyour integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="fad71-132">작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="fad71-133">이 시점에서 맵의 설정이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="fad71-134">실제 응용 프로그램에서 SalesForce와 같은 LOB 응용 프로그램의 toostore 변환 hello 데이터 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-134">In a real world application, you may want toostore hello transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="fad71-135">TooSalesforce hello의 동작 toosend hello 출력으로 쉽게 변형할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-135">You can easily as an action toosend hello output of hello transform tooSalesforce.</span></span> 

<span data-ttu-id="fad71-136">이제 요청 toohello HTTP 끝점을 만들어서 변환을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-136">You can now test your transform by making a request toohello HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="fad71-137">기능 및 사용 사례</span><span class="sxs-lookup"><span data-stu-id="fad71-137">Features and use cases</span></span>
* <span data-ttu-id="fad71-138">지도에서 만든 hello 변환에서 하나의 문서 tooanother 이름 및 주소를 복사 하는 등의 간단한 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-138">hello transformation created in a map can be simple, such as copying a name and address from one document tooanother.</span></span> <span data-ttu-id="fad71-139">또는 hello의 기본 매핑 작업을 사용 하 여 보다 복잡 한 변환을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-139">Or, you can create more complex transformations using hello out-of-the-box map operations.</span></span>  
* <span data-ttu-id="fad71-140">문자열, 날짜 시간 함수 등 여러 맵 작업이나 함수를 바로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="fad71-141">Hello 스키마 간에 직접 데이터 복사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-141">You can do a direct data copy between hello schemas.</span></span> <span data-ttu-id="fad71-142">Hello hello SDK에에서 포함 된 맵 편집기, hello 소스 스키마의 hello 요소 hello 대상 스키마의 해당 항목을 연결 하는 선을 그리기 단순하게입니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-142">In hello Mapper included in hello SDK, this is as simple as drawing a line that connects hello elements in hello source schema with their counterparts in hello destination schema.</span></span>  
* <span data-ttu-id="fad71-143">지도 만들 때 모든 hello 관계를 보여 주는 hello 맵 및 생성 하는 링크의 그래픽 표현을 보려면 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-143">When creating a map, you view a graphical representation of hello map, which shows all hello relationships and links you create.</span></span>
* <span data-ttu-id="fad71-144">Hello 맵 테스트 기능 tooadd 샘플 XML 메시지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-144">Use hello Test Map feature tooadd a sample XML message.</span></span> <span data-ttu-id="fad71-145">간단한 클릭으로 hello 맵 생성 및 hello 생성 된 출력을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-145">With a simple click, you can test hello map you created, and see hello generated output.</span></span>  
* <span data-ttu-id="fad71-146">기존 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="fad71-146">Upload existing maps</span></span>  
* <span data-ttu-id="fad71-147">Hello XML 형식에 대 한 지원이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad71-147">Includes support for hello XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="fad71-148">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="fad71-148">Learn more</span></span>
* [<span data-ttu-id="fad71-149">엔터프라이즈 통합 팩 hello에 대 한 자세한</span><span class="sxs-lookup"><span data-stu-id="fad71-149">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보")  
* [<span data-ttu-id="fad71-150">맵에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="fad71-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "엔터프라이즈 통합 맵에 대해 알아보기")  

