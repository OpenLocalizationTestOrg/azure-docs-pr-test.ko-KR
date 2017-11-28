---
title: "Microsoft Power BI embedded 시작 aaaGet"
description: "Power BI Embedded, 대화형 Power BI 보고서를 비즈니스 인텔리전스 응용 프로그램에 추가"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="44ede-103">Microsoft Power BI Embedded 시작</span><span class="sxs-lookup"><span data-stu-id="44ede-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="44ede-104">**Power BI 포함** 자신의 응용 프로그램에 대화형 Power BI 보고서를 사용 하면 응용 프로그램 개발자 tooadd Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-104">**Power BI Embedded** is an Azure service that enables application developers tooadd interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="44ede-105">**Power BI Embedded** 작동 하는 재설계 필요 하거나 hello 방식으로 사용자가 변경 하지 않고 기존 응용 프로그램에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-105">**Power BI Embedded** works with existing applications without needing redesign or changing hello way users sign in.</span></span>

<span data-ttu-id="44ede-106">에 대 한 리소스 **Microsoft Power BI Embedded** hello를 통해 프로 비전 되 [Azure ARM Api](https://msdn.microsoft.com/library/mt712306.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-106">Resources for **Microsoft Power BI Embedded** are provisioned through hello [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="44ede-107">이 경우에 hello 리소스 프로 비전 하는 **Power BI 작업 영역 컬렉션**합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-107">In this case, hello resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="44ede-108">작업 영역 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="44ede-108">Create a workspace collection</span></span>

<span data-ttu-id="44ede-109">A **작업 영역 컬렉션** hello 최상위 Azure 리소스와 응용 프로그램에 포함 되는 hello 콘텐츠에 대 한 컨테이너가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-109">A **Workspace Collection** is hello top-level Azure resource and a container for hello content that will be embedded in your application.</span></span> <span data-ttu-id="44ede-110">**작업 영역 컬렉션** 은 두 가지 방법으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="44ede-111">Hello Azure 포털을 사용 하 여 수동으로</span><span class="sxs-lookup"><span data-stu-id="44ede-111">Manually using hello Azure Portal</span></span>
* <span data-ttu-id="44ede-112">프로그래밍 방식으로 hello Azure 리소스 Manager(ARM) Api를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="44ede-112">Programmatically using hello Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="44ede-113">Hello 단계 toobuild 살펴보겠습니다는 **작업 영역 컬렉션** Azure 포털 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-113">Let's walk through hello steps toobuild a **Workspace Collection** using hello Azure Portal.</span></span>

1. <span data-ttu-id="44ede-114">**Azure 포털**( [http://portal.azure.com](http://portal.azure.com))을 열고 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="44ede-115">클릭 **+ 새로 만들기** hello 위쪽 패널에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-115">Click **+ New** on hello top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="44ede-116">**데이터 + 분석**에서 **Power BI Embedded**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="44ede-117">Hello에 **작업 영역 컬렉션 블레이드**, hello 필요한 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-117">On hello **Workspace Collection Blade**, enter hello required information.</span></span> <span data-ttu-id="44ede-118">**가격 책정**이 경우 [Power BI Embedded 가격](http://go.microsoft.com/fwlink/?LinkID=760527)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44ede-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="44ede-119">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-119">Click **Create**.</span></span>

<span data-ttu-id="44ede-120">hello **작업 영역 컬렉션** 몇 분 정도의 tooprovision 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-120">hello **Workspace Collection** will take a few moments tooprovision.</span></span> <span data-ttu-id="44ede-121">완료 되 면 이동 됩니다 toohello **작업 영역 컬렉션 블레이드**합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-121">When completed, you'll be taken toohello **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="44ede-122">hello **생성 블레이드** toocall hello 작업 영역을 만들고 toothem 콘텐츠를 배포 하는 Api 필요한 hello 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-122">hello **Creation Blade** contains hello information you need toocall hello APIs that create workspaces and deploy content toothem.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="44ede-123">Power BI API 액세스 키 보기</span><span class="sxs-lookup"><span data-stu-id="44ede-123">View Power BI API access keys</span></span>

<span data-ttu-id="44ede-124">Hello 가장 중요 한 필요한 정보 toocall 가지 hello Power BI REST Api 중 하나는 hello **선택 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-124">One of hello most important pieces of information needed toocall hello Power BI REST APIs are hello **Access Keys**.</span></span> <span data-ttu-id="44ede-125">사용 되는 toogenerate hello 이들은 **앱 토큰** tooauthenticate 사용된 중인 API 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-125">These are used toogenerate hello **app tokens** that are used tooauthenticate your API requests.</span></span> <span data-ttu-id="44ede-126">tooview 프로그램 **선택 키**, 클릭 **선택 키** hello에 **설정 블레이드에서**합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-126">tooview your **Access Keys**, click **Access Keys** on hello **Settings Blade**.</span></span> <span data-ttu-id="44ede-127">**앱 토큰**에 대한 자세한 내용은 [Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44ede-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="44ede-128">두 개의 키가 있는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="44ede-129">이러한 키를 복사하고 응용 프로그램에 안전하게 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="44ede-130">tooall hello 콘텐츠에 액세스를 제공 합니다 하기 때문에 암호와 마찬가지로 이러한 키를 처리 하는 반드시 프로그램 **작업 영역 컬렉션**합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-130">It's very important that you treat these keys as you would a password, because they'll provide access tooall hello content in your **Workspace Collection**.</span></span>

<span data-ttu-id="44ede-131">두 키가 나열되지만 한 번에 하나의 키만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="44ede-132">두 번째 키 hello 액세스 toohello 서비스를 중단 하지 않고 키를 다시 생성 주기적으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-132">hello second key is provided so you can periodically regenerate keys without interrupting access toohello service.</span></span>

<span data-ttu-id="44ede-133">이제 응용 프로그램에 대한 Power BI의 인스턴스, **선택키**가 있으며 보고서를 사용자 자신의 앱에 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="44ede-134">전에는 보고서, 다음 섹션 hello tooimport 응용 프로그램에 만드는 Power BI 데이터 집합 및 보고서 tooembed를 설명 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-134">Before you learn how tooimport a report, hello next section describes creating Power BI datasets and reports tooembed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="44ede-135">작업 영역에서 작업</span><span class="sxs-lookup"><span data-stu-id="44ede-135">Working with workspaces</span></span>

<span data-ttu-id="44ede-136">작업 영역 컬렉션을 만든 후 보고서 및 데이터 집합을 보관 하는 작업 영역 toocreate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-136">After you have created your workspace collection, you will need toocreate a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="44ede-137">작업 영역 toocreate 해야 toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-137">toocreate a workspace, you will need toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="44ede-138">Power BI Desktop을 사용 하 여 앱에 Power BI 데이터 집합 및 보고서 tooembed 만들기</span><span class="sxs-lookup"><span data-stu-id="44ede-138">Create Power BI datasets and reports tooembed into an app using Power BI Desktop</span></span>

<span data-ttu-id="44ede-139">응용 프로그램에 대 한 Power BI의 인스턴스를 만든 하 고 있는 **선택 키**, toocreate hello Power BI 데이터 집합 및 보고서 tooembed 되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need toocreate hello Power BI datasets and reports that you want tooembed.</span></span> <span data-ttu-id="44ede-140">데이터 집합 및 보고서는 **Power BI 데스크톱**을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="44ede-141">[Power BI 데스크톱은 무료로](https://go.microsoft.com/fwlink/?LinkId=521662)다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="44ede-142">또는 tooquickly 시작, hello를 다운로드할 수 있습니다 [소매 분석 샘플 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-142">Or, tooquickly get started, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="44ede-143">방법에 대 한 자세한 toolearn toouse **Power BI Desktop**, 참조 [Power BI Desktop 시작](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop)합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-143">toolearn more about how toouse **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="44ede-144">와 **Power BI Desktop**, hello 데이터의 복사본을 가져와서 tooyour 데이터 소스를 연결 **Power BI Desktop** toohello 데이터 직접 연결 하는 또는 사용 하 여 원본 **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="44ede-144">With **Power BI Desktop**, you connect tooyour data source by importing a copy of hello data into **Power BI Desktop** or connecting directly toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="44ede-145">다음은 hello를 사용 하 여 차이점 **가져오기** 및 **DirectQuery**합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-145">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="44ede-146">가져오기</span><span class="sxs-lookup"><span data-stu-id="44ede-146">Import</span></span> | <span data-ttu-id="44ede-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="44ede-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="44ede-148">테이블, 열 *및 데이터* 를 **Power BI 데스크톱**으로 가져오거나 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="44ede-149">시각화를 작업할 때와 같이 **Power BI Desktop** hello 데이터의 복사본을 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-149">As you work with visualizations, **Power BI Desktop** queries a copy of hello data.</span></span> <span data-ttu-id="44ede-150">toosee 모든 변경 내용이 해당 오류가 발생 했습니다 toohello 기본 데이터를 새로 고침을 하거나, 완전 하 고 현재 데이터 집합 가져오기 다시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-150">toosee any changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="44ede-151">*테이블 및 열* 만 **Power BI 데스크톱**으로 가져오거나 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="44ede-152">시각화를 작업할 때와 같이 **Power BI Desktop** 쿼리 hello 항상 현재 데이터를 보는 것을 의미 하는 기본 데이터 원본에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-152">As you work with visualizations, **Power BI Desktop** queries hello underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="44ede-153">연결 tooa 데이터 원본에 대 한 자세한 내용은 [tooa 데이터 원본 연결](power-bi-embedded-connect-datasource.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-153">For more about connecting tooa data source, see [Connect tooa data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="44ede-154">**Power BI 데스크톱**에 작업을 저장하면 PBIX 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="44ede-155">이 파일에는 보고서가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-155">This file contains your report.</span></span> <span data-ttu-id="44ede-156">또한 PBIX 포함 데이터 hello를 가져오면 hello 전체 데이터 집합을 사용 하는 경우 또는 **DirectQuery**, hello PBIX 데이터 집합 스키마만 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-156">In addition, if you import data hello PBIX contains hello complete dataset, or if you use **DirectQuery**, hello PBIX contains just a dataset schema.</span></span> <span data-ttu-id="44ede-157">Hello를 사용 하 여 작업 영역으로 hello PBIX를 프로그래밍 방식으로 배포 [Power BI 가져오기 API](https://msdn.microsoft.com/library/mt711504.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-157">You programmatically deploy hello PBIX into your workspace using hello [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="44ede-158">**Power BI 포함** 추가 Api toochange hello 서버 개이고 하는 데이터베이스는 데이터 집합은 tooand 집합 hello 데이터 집합 서비스 계정 자격 증명 tooconnect tooyour 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-158">**Power BI Embedded** has additional APIs toochange hello server and database that your dataset is pointing tooand set a service account credential that hello dataset will use tooconnect tooyour database.</span></span> <span data-ttu-id="44ede-159">[SetAllConnections 게시](https://msdn.microsoft.com/library/mt711505.aspx) 및 [게이트웨이 데이터 원본 패치](https://msdn.microsoft.com/library/mt711498.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44ede-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="44ede-160">API를 사용하여 Power BI 데이터 집합 및 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="44ede-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="44ede-161">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="44ede-161">Datsets</span></span>

<span data-ttu-id="44ede-162">내 Power BI 포함 hello REST API를 사용 하 여 데이터 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-162">You can create datasets within Power BI Embedded using hello REST API.</span></span> <span data-ttu-id="44ede-163">그런 다음 데이터를 데이터 집합에 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-163">You can then push data into your dataset.</span></span> <span data-ttu-id="44ede-164">이렇게 하면 Power BI Desktop의 hello 필요 없이 데이터와 toowork 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-164">This allows you toowork with data without hello need of Power BI Desktop.</span></span> <span data-ttu-id="44ede-165">자세한 내용은 [데이터 집합 게시](https://msdn.microsoft.com/library/azure/mt778875.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44ede-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="44ede-166">보고서</span><span class="sxs-lookup"><span data-stu-id="44ede-166">Reports</span></span>

<span data-ttu-id="44ede-167">Hello JavaScript API를 사용 하 여 응용 프로그램에 직접 데이터 집합에서 보고서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44ede-167">You can create a report from a dataset directly in your application using hello JavaScript API.</span></span> <span data-ttu-id="44ede-168">자세한 내용은 [Power BI Embedded의 데이터 집합에서 새 보고서 만들기](power-bi-embedded-create-report-from-dataset.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44ede-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="44ede-169">참고 항목</span><span class="sxs-lookup"><span data-stu-id="44ede-169">See Also</span></span>

[<span data-ttu-id="44ede-170">샘플 시작</span><span class="sxs-lookup"><span data-stu-id="44ede-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="44ede-171">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="44ede-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="44ede-172">보고서 포함</span><span class="sxs-lookup"><span data-stu-id="44ede-172">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
<span data-ttu-id="44ede-173">[Power BI Embedded의 데이터 집합에서 새 보고서 만들기](power-bi-embedded-create-report-from-dataset.md)
[보고서 저장](power-bi-embedded-save-reports.md)</span><span class="sxs-lookup"><span data-stu-id="44ede-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="44ede-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="44ede-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="44ede-175">JavaScript Embed 샘플</span><span class="sxs-lookup"><span data-stu-id="44ede-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="44ede-176">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="44ede-176">More questions?</span></span> [<span data-ttu-id="44ede-177">Power BI 커뮤니티 hello를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="44ede-177">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

