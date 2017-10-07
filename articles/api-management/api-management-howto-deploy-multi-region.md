---
title: "aaaDeploy Azure API 관리 서비스 toomultiple Azure 지역 | Microsoft Docs"
description: "Toodeploy Azure API 관리 인스턴스 toomultiple Azure를 서비스 하는 방법에 대해 알아봅니다 영역입니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a><span data-ttu-id="57677-103">어떻게 toodeploy Azure API 관리 서비스 인스턴스 toomultiple Azure 지역</span><span class="sxs-lookup"><span data-stu-id="57677-103">How toodeploy an Azure API Management service instance toomultiple Azure regions</span></span>
<span data-ttu-id="57677-104">API 관리 개수에 관계 없이 원하는 Azure 지역에서 게시자 toodistribute 단일 API 관리 서비스 API를 매핑함으로써 다중 지역 배포를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="57677-104">API Management supports multi-region deployment which enables API publishers toodistribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="57677-105">이를 통해 지역적으로 배포된 API 소비자가 느끼는 요청 대기 시간을 줄일 수 있으며 한 지역이 오프라인인 경우 가능한 서비스를 개선할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57677-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="57677-106">API 관리 서비스를 만들면 처음에 하나만 가질 [단위] [ unit] hello 기본 지역으로 지정 하는 단일 Azure 지역에 상주 합니다.</span><span class="sxs-lookup"><span data-stu-id="57677-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as hello Primary Region.</span></span> <span data-ttu-id="57677-107">추가 영역 hello Azure 포털을 통해 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57677-107">Additional regions can be easily added through hello Azure Portal.</span></span> <span data-ttu-id="57677-108">API 관리 게이트웨이 서버 배포 tooeach 지역 이며 호출 트래픽을 가장 가까운 게이트웨이 라우팅된 toohello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57677-108">An API Management gateway server is deployed tooeach region and call traffic will be routed toohello closest gateway.</span></span> <span data-ttu-id="57677-109">영역 오프 라인인 경우 hello 트래픽이 자동으로 리디렉션됩니다 toohello 다음 가장 가까운 게이트웨이로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57677-109">If a region goes offline, hello traffic is automatically re-directed toohello next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="57677-110">다중 지역 배포는 hello에서 사용할 수만  **[프리미엄] [ Premium]**  계층입니다.</span><span class="sxs-lookup"><span data-stu-id="57677-110">Multi-region deployment is only available in hello **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="57677-111"><a name="add-region"></a>는 API 관리 서비스 인스턴스 tooa 새 지역 배포</span><span class="sxs-lookup"><span data-stu-id="57677-111"><a name="add-region"> </a>Deploy an API Management service instance tooa new region</span></span>
> [!NOTE]
> <span data-ttu-id="57677-112">API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="57677-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="57677-113">Hello Azure 포털에서에서 탐색 toohello **배율과 가격** API 관리 서비스 인스턴스에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="57677-113">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![크기 조정 탭][api-management-scale-service]

<span data-ttu-id="57677-115">toodeploy tooa 새 영역을 클릭할 **+ 추가 영역** hello 도구 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="57677-115">toodeploy tooa new region, click on **+ Add region** from hello toolbar.</span></span>

![지역 추가][api-management-add-region]

<span data-ttu-id="57677-117">Hello 드롭 다운 목록에서 hello 위치를 선택 하 고 hello와 hello 슬라이더에 대 한 단위 수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="57677-117">Select hello location from hello drop-down list and set hello number of units for with hello slider.</span></span>

![단위 지정][api-management-select-location-units]

<span data-ttu-id="57677-119">클릭 **추가** tooplace hello 위치 테이블에서 선택 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="57677-119">Click **Add** tooplace your selection in hello Locations table.</span></span> 

<span data-ttu-id="57677-120">구성 된 모든 위치 구성할 때까지이 과정을 반복 하 고 클릭 **저장** hello 도구 모음 toostart hello 배포 프로세스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="57677-120">Repeat this process until you have all locations configured and click **Save** from hello toolbar toostart hello deployment process.</span></span>

## <span data-ttu-id="57677-121"><a name="remove-region"> </a>위치에 API 관리 서비스 인스턴스 삭제</span><span class="sxs-lookup"><span data-stu-id="57677-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="57677-122">Hello Azure 포털에서에서 탐색 toohello **배율과 가격** API 관리 서비스 인스턴스에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="57677-122">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![크기 조정 탭][api-management-scale-service]

<span data-ttu-id="57677-124">원하는 hello 위치에 대 한 tooremove hello를 사용 하 여 hello 상황에 맞는 메뉴를 열고 **...**  hello 테이블의 hello 오른쪽 끝 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="57677-124">For hello location you would like tooremove open hello context menu using hello **...** button at hello right end of hello table.</span></span> <span data-ttu-id="57677-125">선택 hello **삭제** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="57677-125">Select hello **Delete** option.</span></span>

![지역 제거][api-management-remove-region]

<span data-ttu-id="57677-127">Hello 삭제를 확인 하 고 클릭 **저장** tooapply hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="57677-127">Confirm hello deletion and click **Save** tooapply hello changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

