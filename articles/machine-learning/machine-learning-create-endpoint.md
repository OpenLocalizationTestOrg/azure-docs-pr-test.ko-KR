---
title: "기계 학습에서 웹 서비스 끝점 aaaCreating | Microsoft Docs"
description: "Azure Machine Learning에서 웹 서비스 끝점 만들기"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="83a5a-103">끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="83a5a-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="83a5a-104">이 항목에서는 기술을 적용 가능한 tooa 설명 **클래식** 컴퓨터 학습 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-104">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="83a5a-105">정방향 tooyour 고객을 판매 하는 웹 서비스를 만들 서비스를 만들 때 어떤 hello 웹에서에서 여전히 연결 된 toohello 실험은 tooprovide 학습 된 모델 tooeach 고객이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-105">When you create Web services that you sell forward tooyour customers, you need tooprovide trained models tooeach customer that are still linked toohello experiment from which hello Web service was created.</span></span> <span data-ttu-id="83a5a-106">또한 toohello 실험 해야 업데이트 선택적 적용 tooan 끝점 hello 사용자 지정 항목을 덮어쓰지 않고 합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-106">In addition, any updates toohello experiment should be applied selectively tooan endpoint without overwriting hello customizations.</span></span>

<span data-ttu-id="83a5a-107">tooaccomplish이를 Azure 기계 학습 toocreate을 사용 하면 배포 된 웹 서비스에 대 한 여러 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-107">tooaccomplish this, Azure Machine Learning allows you toocreate multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="83a5a-108">각 끝점 hello 웹 서비스에에서 독립적으로 주소가 지정 된 제한 하 여 있고, 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-108">Each endpoint in hello Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="83a5a-109">각 끝점은 고유한 URL 및 권한 부여 키 tooyour 고객을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-109">Each endpoint is a unique URL and authorization key that you can distribute tooyour customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a><span data-ttu-id="83a5a-110">끝점 tooa 웹 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="83a5a-110">Adding endpoints tooa Web service</span></span>
<span data-ttu-id="83a5a-111">끝점 tooa 웹 서비스는 세 가지 방법으로 tooadd 합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-111">There are three ways tooadd an endpoint tooa Web service.</span></span>

* <span data-ttu-id="83a5a-112">프로그래밍 방식</span><span class="sxs-lookup"><span data-stu-id="83a5a-112">Programmatically</span></span>
* <span data-ttu-id="83a5a-113">Hello Azure 컴퓨터 학습 웹 서비스 포털을 통해</span><span class="sxs-lookup"><span data-stu-id="83a5a-113">Through hello Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="83a5a-114">그러나 Azure 클래식 포털을 hello</span><span class="sxs-lookup"><span data-stu-id="83a5a-114">Though hello Azure classic portal</span></span>

<span data-ttu-id="83a5a-115">Hello 끝점을 만든 후에 동기 Api 일괄 처리, Api 통해 사용할 수 있으며 excel 워크시트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-115">Once hello endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="83a5a-116">또한이 UI 통해 tooadding 끝점을 사용할 수도 있습니다 hello 끝점 관리 Api tooprogrammatically 끝점을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-116">In addition tooadding endpoints through this UI, you can also use hello Endpoint Management APIs tooprogrammatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="83a5a-117">추가 끝점 toohello 웹 서비스를 추가한 경우 hello 기본 끝점을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-117">If you have added additional endpoints toohello Web service, you cannot delete hello default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="83a5a-118">프로그래밍 방식으로 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="83a5a-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="83a5a-119">프로그래밍 방식으로 hello를 사용 하는 끝점 tooyour 웹 서비스를 추가할 수 있습니다 [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-119">You can add an endpoint tooyour Web service programmatically using hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="83a5a-120">Hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="83a5a-120">Adding an endpoint using hello Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="83a5a-121">기계 학습 스튜디오에서는 hello 왼쪽된 탐색 열 웹 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-121">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="83a5a-122">Hello 웹 서비스 대시보드 hello 아래쪽 클릭 **끝점을 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-122">At hello bottom of hello Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="83a5a-123">hello Azure 컴퓨터 학습 웹 서비스 포털 hello 웹 서비스에 대 한 toohello 끝점 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-123">hello Azure Machine Learning Web Services portal opens toohello endpoints page for hello Web service.</span></span>
3. <span data-ttu-id="83a5a-124">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-124">Click **New**.</span></span>
4. <span data-ttu-id="83a5a-125">이름 및 hello 새 끝점에 대 한 설명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-125">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="83a5a-126">끝점 이름은 길이가 24자 이하이고 알파벳 소문자 또는 숫자로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="83a5a-127">Hello 로깅 수준 및 예제 데이터가 활성화 되어 있는지 여부를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-127">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="83a5a-128">로깅에 대한 자세한 내용은 [Machine Learning 웹 서비스에 대한 로깅 사용](machine-learning-web-services-logging.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83a5a-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a><span data-ttu-id="83a5a-129">Hello Azure 클래식 포털을 사용 하 여 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="83a5a-129">Adding an endpoint using hello Azure classic portal</span></span>
1. <span data-ttu-id="83a5a-130">Toohello 로그인 [Azure 클래식 포털](http://manage.windowsazure.com), 클릭 **기계 학습** hello 왼쪽된 열에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-130">Sign in toohello [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in hello left column.</span></span> <span data-ttu-id="83a5a-131">관심이 있는 hello 웹 서비스를 포함 하는 hello 작업 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-131">Click hello workspace which contains hello Web service in which you are interested.</span></span>
   
    ![Tooworkspace 이동](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="83a5a-133">**웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-133">Click **Web Services**.</span></span>
   
    ![TooWeb 서비스 탐색](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="83a5a-135">사용 가능한 끝점의 toosee hello 목록에 관심이 hello 웹 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-135">Click hello Web service you're interested in toosee hello list of available endpoints.</span></span>
   
    ![Tooendpoint 이동](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="83a5a-137">Hello hello 페이지의 아래쪽에 있는 클릭 **끝점 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-137">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="83a5a-138">이름 및 설명을 입력 하을이 웹 서비스의 이름과 같은 이름을 hello로 다른 끝점이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-138">Type a name and description, ensure there are no other endpoints with hello same name in this Web service.</span></span> <span data-ttu-id="83a5a-139">특별 한 요구 사항이 없다면 hello 제한 수준을 값이 기본값으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-139">Leave hello throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="83a5a-140">제한에 대해 자세히 toolearn 참조 [API 끝점 확장](machine-learning-scaling-webservice.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-140">toolearn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![끝점 만들기](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="83a5a-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="83a5a-142">Next Steps</span></span>
<span data-ttu-id="83a5a-143">[어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83a5a-143">[How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

