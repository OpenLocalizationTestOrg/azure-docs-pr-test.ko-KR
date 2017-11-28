---
title: "aaaEncode Azure 논리 앱에 있는 플랫 파일 디코딩 또는 | Microsoft Docs"
description: "파일 파일 인코더 또는 디코더가 논리 앱에 엔터프라이즈 통합 팩 hello에 toouse hello 하는 방법"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 82152dab-c7ad-43df-b721-596559703be8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 2c295586625fd84366ec7cbafdcebf0489ba234d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a><span data-ttu-id="84b26-103">플랫 파일을 사용한 엔터프라이즈 통합 개요</span><span class="sxs-lookup"><span data-stu-id="84b26-103">Overview of enterprise integration with flat files</span></span>

<span data-ttu-id="84b26-104">기업 (B2B) 시나리오에서 tooa 비즈니스 파트너를 보내기 전에 XML tooencode를 콘텐츠 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-104">You may want tooencode XML content before you send it tooa business partner in a business-to-business (B2B) scenario.</span></span> <span data-ttu-id="84b26-105">논리 앱에서는이 커넥터 toodo 인코딩 hello 플랫 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-105">In a logic app, you can use hello flat file encoding connector toodo this.</span></span> <span data-ttu-id="84b26-106">hello 만드는 논리 앱 콘텐츠를 볼 수는 XML에서 다양 한 소스를 포함 하 여 HTTP 요청 트리거, 다른 응용 프로그램 또는 hello 중 하나 에서도 많은 [커넥터](../connectors/apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-106">hello logic app that you create can get its XML content from a variety of sources, including from an HTTP request trigger, from another application, or even from one of hello many [connectors](../connectors/apis-list.md).</span></span> <span data-ttu-id="84b26-107">논리 앱에 대 한 자세한 내용은 참조 hello [논리 앱 설명서](logic-apps-what-are-logic-apps.md "논리 앱에 대 한 자세한")합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-107">For more information about logic apps, see hello [logic apps documentation](logic-apps-what-are-logic-apps.md "Learn more about Logic apps").</span></span>  

## <a name="create-hello-flat-file-encoding-connector"></a><span data-ttu-id="84b26-108">Hello 플랫 파일 인코딩 커넥터 만들기</span><span class="sxs-lookup"><span data-stu-id="84b26-108">Create hello flat file encoding connector</span></span>
<span data-ttu-id="84b26-109">이러한 단계 tooadd를 플랫 파일 인코딩 커넥터 tooyour 논리 앱을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-109">Follow these steps tooadd a flat file encoding connector tooyour logic app.</span></span>

1. <span data-ttu-id="84b26-110">논리 앱 만들기 및 [tooyour 통합 계정 연결](logic-apps-enterprise-integration-accounts.md "toolink 통합 계정 tooa 논리 앱에 알아봅니다")합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-110">Create a logic app and [link it tooyour integration account](logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app").</span></span> <span data-ttu-id="84b26-111">이 계정은 tooencode hello XML 데이터를 사용 하 여 hello 스키마를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-111">This account contains hello schema you will use tooencode hello XML data.</span></span>  
2. <span data-ttu-id="84b26-112">추가 **요청-때 HTTP 요청을 받으면** 트리거 tooyour 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="84b26-112">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>  
   <span data-ttu-id="84b26-113">![트리거 tooselect의 스크린샷](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span><span class="sxs-lookup"><span data-stu-id="84b26-113">![Screenshot of trigger tooselect](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span></span>    
3. <span data-ttu-id="84b26-114">작업을 다음과 같이 인코딩 hello 플랫 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-114">Add hello flat file encoding action, as follows:</span></span>
   
    <span data-ttu-id="84b26-115">a.</span><span class="sxs-lookup"><span data-stu-id="84b26-115">a.</span></span> <span data-ttu-id="84b26-116">선택 hello **플러스** 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-116">Select hello **plus** sign.</span></span>
   
    <span data-ttu-id="84b26-117">b.</span><span class="sxs-lookup"><span data-stu-id="84b26-117">b.</span></span> <span data-ttu-id="84b26-118">선택 hello **동작 추가** 링크 (hello 더하기 기호를 선택한 후 표시 됨).</span><span class="sxs-lookup"><span data-stu-id="84b26-118">Select hello **Add an action** link (appears after you have selected hello plus sign).</span></span>
   
    <span data-ttu-id="84b26-119">c.</span><span class="sxs-lookup"><span data-stu-id="84b26-119">c.</span></span> <span data-ttu-id="84b26-120">Hello 검색 상자에 입력 *플랫* toofilter toouse 되도록 하나 작업 toohello hello 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-120">In hello search box, enter *Flat* toofilter all hello actions toohello one that you want toouse.</span></span>
   
    <span data-ttu-id="84b26-121">d.</span><span class="sxs-lookup"><span data-stu-id="84b26-121">d.</span></span> <span data-ttu-id="84b26-122">선택 hello **플랫 파일 인코딩** hello 목록에서 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-122">Select hello **Flat File Encoding** option from hello list.</span></span>   
   <span data-ttu-id="84b26-123">![플랫 파일 인코딩 옵션의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span><span class="sxs-lookup"><span data-stu-id="84b26-123">![Screenshot of Flat File Encoding option](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span></span>   
4. <span data-ttu-id="84b26-124">Hello에 **플랫 파일 인코딩** 대화 상자, 선택 hello **콘텐츠** 입력란.</span><span class="sxs-lookup"><span data-stu-id="84b26-124">On hello **Flat File Encoding** dialog box, select hello **Content** text box.</span></span>  
   <span data-ttu-id="84b26-125">![텍스트 상자 콘텐츠의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)</span><span class="sxs-lookup"><span data-stu-id="84b26-125">![Screenshot of Content text box](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)</span></span>  
5. <span data-ttu-id="84b26-126">Hello tooencode 원하는 내용으로 hello body 태그를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-126">Select hello body tag as hello content that you want tooencode.</span></span> <span data-ttu-id="84b26-127">hello body 태그는 hello 콘텐츠 필드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-127">hello body tag will populate hello content field.</span></span>     
   ![본문 태그의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. <span data-ttu-id="84b26-129">선택 hello **스키마 이름** 목록 상자 및 toouse tooencode hello hello 스키마 입력 콘텐츠를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-129">Select hello **Schema Name** list box, and choose hello schema you want toouse tooencode hello input content.</span></span>    
   <span data-ttu-id="84b26-130">![스키마 이름 목록 상자의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)</span><span class="sxs-lookup"><span data-stu-id="84b26-130">![Screenshot of Schema Name list box](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)</span></span>  
7. <span data-ttu-id="84b26-131">작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-131">Save your work.</span></span>   
   ![저장 아이콘의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

<span data-ttu-id="84b26-133">이 시점에서 플랫 파일 인코딩 커넥터의 설정이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-133">At this point, you are finished setting up your flat file encoding connector.</span></span> <span data-ttu-id="84b26-134">실제 응용 프로그램에서 Salesforce와 같은 기간 업무 응용 프로그램에서는 hello로 인코딩된 데이터 toostore 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-134">In a real world application, you may want toostore hello encoded data in a line-of-business application, such as Salesforce.</span></span> <span data-ttu-id="84b26-135">또는 해당 인코딩된 데이터 tooa 거래 업체를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-135">Or you can send that encoded data tooa trading partner.</span></span> <span data-ttu-id="84b26-136">쉽게 제공 하는 다른 커넥터 hello hello 중 하나를 사용 하 여 인코딩 작업 tooSalesforce 또는 tooyour 거래 업체의 작업 toosend hello 결과 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-136">You can easily add an action toosend hello output of hello encoding action tooSalesforce, or tooyour trading partner, by using any one of hello other connectors provided.</span></span>

<span data-ttu-id="84b26-137">이제 요청 toohello HTTP 끝점을 만들고이 hello hello 요청 본문에 hello XML 콘텐츠를 포함 하 여 커넥터를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-137">You can now test your connector by making a request toohello HTTP endpoint, and including hello XML content in hello body of hello request.</span></span>  

## <a name="create-hello-flat-file-decoding-connector"></a><span data-ttu-id="84b26-138">Hello 플랫 파일 디코딩 커넥터 만들기</span><span class="sxs-lookup"><span data-stu-id="84b26-138">Create hello flat file decoding connector</span></span>

> [!NOTE]
> <span data-ttu-id="84b26-139">이 단계는 toocomplete, toohave 스키마 파일을 이미 통합 계정에 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-139">toocomplete these steps, you need toohave a schema file already uploaded into you integration account.</span></span>

1. <span data-ttu-id="84b26-140">추가 **요청-때 HTTP 요청을 받으면** 트리거 tooyour 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="84b26-140">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>  
   <span data-ttu-id="84b26-141">![트리거 tooselect의 스크린샷](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span><span class="sxs-lookup"><span data-stu-id="84b26-141">![Screenshot of trigger tooselect](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span></span>    
2. <span data-ttu-id="84b26-142">다음과 같이 작업을 디코딩 hello 플랫 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-142">Add hello flat file decoding action, as follows:</span></span>
   
    <span data-ttu-id="84b26-143">a.</span><span class="sxs-lookup"><span data-stu-id="84b26-143">a.</span></span> <span data-ttu-id="84b26-144">선택 hello **플러스** 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-144">Select hello **plus** sign.</span></span>
   
    <span data-ttu-id="84b26-145">b.</span><span class="sxs-lookup"><span data-stu-id="84b26-145">b.</span></span> <span data-ttu-id="84b26-146">선택 hello **동작 추가** 링크 (hello 더하기 기호를 선택한 후 표시 됨).</span><span class="sxs-lookup"><span data-stu-id="84b26-146">Select hello **Add an action** link (appears after you have selected hello plus sign).</span></span>
   
    <span data-ttu-id="84b26-147">c.</span><span class="sxs-lookup"><span data-stu-id="84b26-147">c.</span></span> <span data-ttu-id="84b26-148">Hello 검색 상자에 입력 *플랫* toofilter toouse 되도록 하나 작업 toohello hello 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-148">In hello search box, enter *Flat* toofilter all hello actions toohello one that you want toouse.</span></span>
   
    <span data-ttu-id="84b26-149">d.</span><span class="sxs-lookup"><span data-stu-id="84b26-149">d.</span></span> <span data-ttu-id="84b26-150">선택 hello **플랫 파일 디코딩** hello 목록에서 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-150">Select hello **Flat File Decoding** option from hello list.</span></span>   
   <span data-ttu-id="84b26-151">![플랫 파일 디코딩 옵션의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span><span class="sxs-lookup"><span data-stu-id="84b26-151">![Screenshot of Flat File Decoding option](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span></span>   
3. <span data-ttu-id="84b26-152">선택 hello **콘텐츠** 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-152">Select hello **Content** control.</span></span> <span data-ttu-id="84b26-153">Hello 콘텐츠의 콘텐츠 toodecode hello로 사용할 수 있는 이전 단계에서 목록이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-153">This produces a list of hello content from earlier steps that you can use as hello content toodecode.</span></span> <span data-ttu-id="84b26-154">해당 hello 확인 *본문* hello에서 들어오는 HTTP 요청은 사용할 수 있는 toobe 콘텐츠 toodecode hello로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-154">Notice that hello *Body* from hello incoming HTTP request is available toobe used as hello content toodecode.</span></span> <span data-ttu-id="84b26-155">Hello 콘텐츠 toodecode hello에 직접 입력할 수도 있습니다 **콘텐츠** 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-155">You can also enter hello content toodecode directly into hello **Content** control.</span></span>     
4. <span data-ttu-id="84b26-156">선택 hello *본문* 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-156">Select hello *Body* tag.</span></span> <span data-ttu-id="84b26-157">이제 알림 hello body 태그는 hello에 **콘텐츠** 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-157">Notice hello body tag is now in hello **Content** control.</span></span>
5. <span data-ttu-id="84b26-158">Toouse toodecode hello 콘텐츠 hello 스키마의 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-158">Select hello name of hello schema that you want toouse toodecode hello content.</span></span> <span data-ttu-id="84b26-159">hello 다음 스크린샷에서 *OrderFile* hello 선택한 스키마 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-159">hello following screenshot shows that *OrderFile* is hello selected schema name.</span></span> <span data-ttu-id="84b26-160">이 스키마 이름은 hello 통합 계정에 이전에 업로드 했습니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-160">This schema name had been uploaded into hello integration account previously.</span></span>
   
   ![플랫 파일 디코딩 대화 상자의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. <span data-ttu-id="84b26-162">작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-162">Save your work.</span></span>  
   ![저장 아이콘의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

<span data-ttu-id="84b26-164">이 시점에서 플랫 파일 디코딩 커넥터의 설정이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-164">At this point, you are finished setting up your flat file decoding connector.</span></span> <span data-ttu-id="84b26-165">실제 응용 프로그램에서 Salesforce와 같은 기간 업무 응용 프로그램에서 toostore hello 디코딩할 데이터 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-165">In a real world application, you may want toostore hello decoded data in a line-of-business application such as Salesforce.</span></span> <span data-ttu-id="84b26-166">hello 동작 tooSalesforce 디코딩 작업 toosend hello 결과 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-166">You can easily add an action toosend hello output of hello decoding action tooSalesforce.</span></span>

<span data-ttu-id="84b26-167">이제 요청 toohello HTTP 끝점을 하 여 커넥터를 테스트할 수 있습니다 및 hello XML 내용을 포함 하 여 hello hello 요청 본문에 toodecode 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-167">You can now test your connector by making a request toohello HTTP endpoint and including hello XML content you want toodecode in hello body of hello request.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="84b26-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="84b26-168">Next steps</span></span>
* <span data-ttu-id="84b26-169">[엔터프라이즈 통합 팩 hello에 대 한 자세한](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보")합니다.</span><span class="sxs-lookup"><span data-stu-id="84b26-169">[Learn more about hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack").</span></span>  

