---
title: "Azure Machine Learning 웹 서비스의 동시성을 향상하는 방법 | Microsoft Docs"
description: "끝점을 추가하여 Azure Machine Learning 웹 서비스의 동시성을 향상하는 방법을 알아봅니다."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "azure 기계 학습, 웹 서비스, 조작화, 확장, 끝점, 동시성"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: 013354515d841003c912ac0338690dd975a79ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="a4438-104">끝점을 추가하여 Azure Machine Learning 웹 서비스 확장</span><span class="sxs-lookup"><span data-stu-id="a4438-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="a4438-105">이 항목에서는 **기존** Machine Learning 웹 서비스에 적용되는 기술을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a4438-105">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="a4438-106">기본적으로 게시된 각각의 웹 서비스는 20개의 동시 요청을 지원하고 최대 200개의 동시 요청을 지원할 수 있도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4438-106">By default, each published Web service is configured to support 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="a4438-107">Azure 클래식 포털은 이 값을 설정하는 방법을 제공하지만 Azure Machine Learning은 웹 서비스에 대한 최상의 성능을 제공하기 위해 설정을 자동으로 최적화하고 포털 값은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4438-107">While the Azure classic portal provides a way to set this value, Azure Machine Learning automatically optimizes the setting to provide the best performance for your web service and the portal value is ignored.</span></span> 

<span data-ttu-id="a4438-108">최대 동시 호출 값인 200에서 지원하는 것보다 많은 부하를 가진 API를 호출하려는 경우 동일한 웹 서비스에서 여러 끝점을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4438-108">If you plan to call the API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on the same Web service.</span></span> <span data-ttu-id="a4438-109">그런 다음 모든 끝점에 부하를 무작위로 분산해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4438-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="a4438-110">웹 서비스의 크기를 조정하는 것은 일반적인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a4438-110">The scaling of a Web service is a common task.</span></span> <span data-ttu-id="a4438-111">크기를 조정하는 몇 가지 이유는 200개 이상의 동시 요청을 지원하거나, 여러 끝점을 통해 가용성을 높이거나, 웹 서비스에 대한 별도의 끝점을 제공하기 위해서 입니다.</span><span class="sxs-lookup"><span data-stu-id="a4438-111">Some reasons to scale are to support more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for the web service.</span></span> <span data-ttu-id="a4438-112">[Azure 클래식 포털](https://manage.windowsazure.com/) 또는 [Azure Machine Learning 웹 서비스](https://services.azureml.net/) 포털을 통해 동일한 웹 서비스에 대한 추가 끝점을 추가하여 규모를 증가시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4438-112">You can increase the scale by adding additional endpoints for the same Web service through [Azure classic portal](https://manage.windowsazure.com/) or the [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="a4438-113">새로운 끝점 추가에 대한 자세한 내용은 [끝점 만들기](machine-learning-create-endpoint.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4438-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="a4438-114">해당하는 높은 속도로 API를 호출하지 않을 경우 매우 높은 동시성 개수를 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4438-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling the API with a correspondingly high rate.</span></span> <span data-ttu-id="a4438-115">높은 부하로 구성된 API에 상대적으로 낮은 부하를 배치할 경우 가끔 시간 초과 및/또는 대기 시간 급증이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4438-115">You might see sporadic timeouts and/or spikes in the latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="a4438-116">동기 API는 일반적으로 낮은 대기 시간을 원하는 경우에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4438-116">The synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="a4438-117">여기서 대기 시간은 API가 하나의 요청을 완료하는 데 걸리는 시간을 의미하며 네트워크 지연을 고려하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4438-117">Latency here implies the time it takes for the API to complete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="a4438-118">대기 시간이 50ms인 API가 있다고 가정합시다.</span><span class="sxs-lookup"><span data-stu-id="a4438-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="a4438-119">높음 제한 수준 및 최대 동시 호출 = 20으로 사용 가능한 용량을 완전히 사용하려면 이 API를 초당 20 * 1000 / 50 = 400회 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4438-119">To fully consume the available capacity with throttle level High and Max Concurrent Calls = 20, you need to call this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="a4438-120">더욱 확장하여 최대 동시 호출 수를 200으로 설정하면 대기 시간이 50ms일 경우 API를 초당 4000회 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4438-120">Extending this further, a Max Concurrent Calls of 200 allows you to call the API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
