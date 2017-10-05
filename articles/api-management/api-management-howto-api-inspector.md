---
title: "API 검사기를 사용하여 호출 추적 - Azure API Management | Microsoft Docs"
description: "API 검사기를 사용하여 Azure API 관리에서 호출을 추적하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 4b222327-c8a4-4f33-9a06-adff2a9834d9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a9d4d3be7f046af975f6dc25670070204848588c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-api-inspector-to-trace-calls-in-azure-api-management"></a><span data-ttu-id="6b2c2-103">API 검사기를 사용하여 Azure API 관리에서 호출을 추적하는 방법</span><span class="sxs-lookup"><span data-stu-id="6b2c2-103">How to use the API Inspector to trace calls in Azure API Management</span></span>
<span data-ttu-id="6b2c2-104">API 관리는 API 디버깅 및 문제 해결로 사용자를 돕는 API 검사기 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-104">API Management provides an API Inspector tool to help you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="6b2c2-105">API 검사기를 프로그래밍 방식으로 사용할 수 있으며 개발자 포털에서 직접 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-105">The API Inspector can be used programmatically and can also be used directly from the developer portal.</span></span> 

<span data-ttu-id="6b2c2-106">API 검사기는 작업 추적 외에 [정책 식](https://msdn.microsoft.com/library/azure/dn910913.aspx) 평가도 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-106">In addition to tracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="6b2c2-107">데모를 보려면 [Cloud Cover 에피소드 177: 추가 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) 에서 21:00 지점을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 21:00.</span></span>

<span data-ttu-id="6b2c2-108">이 안내서는 API 검사기 사용을 단계적으로 안내해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="6b2c2-109">API 검사기 추적은 [관리자](api-management-howto-create-groups.md) 계정에 속하는 구독 키가 포함된 요청에 대해서만 생성되고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong to the [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="6b2c2-110"><a name="trace-call"> </a> API 검사기를 사용하여 호출 추적</span><span class="sxs-lookup"><span data-stu-id="6b2c2-110"><a name="trace-call"> </a> Use API Inspector to trace a call</span></span>
<span data-ttu-id="6b2c2-111">API 검사기를 사용하려면 **ocp-apim-trace: true** 요청 헤더를 작업 호출에 추가한 다음 **ocp-apim-trace-location** 응답 헤더로 표시된 URL을 사용하여 추적을 다운로드하고 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-111">To use API Inspector, add an **ocp-apim-trace: true** request header to your operation call, and then download and inspect the trace using the URL indicated by the **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="6b2c2-112">이 작업은 프로그래밍 방식으로 수행할 수도 있고, 개발자 포털에서 직접 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-112">This can be done programatically, and can also be done directly from the developer portal.</span></span>

<span data-ttu-id="6b2c2-113">이 자습서에서는 [첫 번째 API 관리](api-management-get-started.md) 시작 자습서에서 구성한 기본 계산기 API를 사용하여 작업을 추적하기 위해 API 검사기를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-113">This tutorial shows how to use the API Inspector to trace operations using the Basic Calculator API that is configured in the [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="6b2c2-114">해당 자습서를 완료하지 않은 경우에는 기본 계산기 API를 가져오는 데 잠깐의 시간이 걸리며 Echo API와 같은 다른 API를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-114">If you haven't completed that tutorial it only takes a few moments to import the Basic Calculator API, or you can use another API of your choosing such as the Echo API.</span></span> <span data-ttu-id="6b2c2-115">각 API 관리 서비스 인스턴스는 실험해 보고 API 관리에 대해 알아보는 데 사용할 수 있는 Echo API가 미리 구성되어 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-115">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="6b2c2-116">Echo API는 전송된 입력을 다시 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-116">The Echo API returns back whatever input is sent to it.</span></span> <span data-ttu-id="6b2c2-117">이를 사용하려면 HTTP 동사를 호출하세요. 반환 값은 단순히 사용자가 보낸 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-117">To use it, you can invoke any HTTP verb, and the return value will simply be what you sent.</span></span> 

<span data-ttu-id="6b2c2-118">시작하려면 Azure Portal에서 API 관리 서비스에 대한 **개발자 포털**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-118">To get started, click **Developer portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="6b2c2-119">개발자 포털에서 직접 작업을 호출할 수 있으며, 이 포털을 사용하면 편리한 방법으로 API의 작업을 보고 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-119">Operations can be called directly from the developer portal which provides a convenient way to view and test the operations of an API.</span></span>

> <span data-ttu-id="6b2c2-120">아직 API Management 서비스 인스턴스를 만들지 않은 경우 [Azure API Management 시작][Get started with Azure API Management] 자습서의 [API Management 서비스 인스턴스 만들기][Create an API Management service instance]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![API 관리 개발자 포털][api-management-developer-portal-menu]

<span data-ttu-id="6b2c2-122">상단 메뉴에서 **API**를 클릭한 다음 **기본 계산기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-122">Click **APIs** from the top menu, and then click **Basic Calculator**.</span></span>

![Echo API][api-management-api]

<span data-ttu-id="6b2c2-124">**두 정수 추가** 작업을 하려면 **시도**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-124">Click **Try it** to try the **Add two integers** operation.</span></span>

![시도][api-management-open-console]

<span data-ttu-id="6b2c2-126">기본 매개 변수 값을 유지하고 **구독 키** 드롭다운에서 사용할 제품의 구독 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-126">Keep the default parameter values, and select the subscription key for the product you want to use from the **subscription-key** drop-down.</span></span>

<span data-ttu-id="6b2c2-127">기본적으로 개발자 포털에서 **Ocp-Apim-Trace** 헤더는 이미 **true**로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-127">By default in the developer portal the **Ocp-Apim-Trace** header is already set to **true**.</span></span> <span data-ttu-id="6b2c2-128">이 헤더는 추적 생성 여부를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-128">This header configures whether or not a trace is generated.</span></span>

![보내기][api-management-http-get]

<span data-ttu-id="6b2c2-130">**보내기** 를 클릭하여 작업을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-130">Click **Send** to invoke the operation.</span></span>

![보내기][api-management-send-results]

<span data-ttu-id="6b2c2-132">응답 헤더에서는 다음 예제와 유사한 값이 포함된 **ocp-apim-trace-location** 이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-132">In the response headers will be an **ocp-apim-trace-location** with a value similar to the following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="6b2c2-133">다음 단계에 설명된 대로 지정된 위치에서 추적을 다운로드하고 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-133">The trace can be downloaded from the specified location and reviewed as demonstrated in the next step.</span></span> <span data-ttu-id="6b2c2-134">마지막100개의 로그 항목만 저장되며 로그 위치는 교대로 재사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-134">Note that only the last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="6b2c2-135">따라서 추적 기능이 활성화된 상태로 100개 이상의 호출을 할 경우 결국에는 첫 번째 추적을 덮어쓰기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting the first traces in place.</span></span>

## <span data-ttu-id="6b2c2-136"><a name="inspect-trace"> </a>추적 검사</span><span class="sxs-lookup"><span data-stu-id="6b2c2-136"><a name="inspect-trace"> </a>Inspect the trace</span></span>
<span data-ttu-id="6b2c2-137">추적에서 값을 검토하려면 **ocp-apim-trace-location** URL에서 추적 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-137">To review the values in the trace, download the trace file from the **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="6b2c2-138">이 파일은 JSON 형식의 텍스트 파일이며 다음 예제와 유사한 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-138">It is a text file in JSON format, and contains entries similar to the following example.</span></span>

```json
{
    "traceId": "abcd8ea63d134c1fabe6371566c7cbea",
    "traceEntries": {
        "inbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0725926",
                "data": {
                    "request": {
                        "method": "GET",
                        "url": "https://contoso5.azure-api.net/calc/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "Connection",
                                "value": "Keep-Alive"
                            },
                            {
                                "name": "Host",
                                "value": "contoso5.azure-api.net"
                            }
                        ]
                    }
                }
            },
            {
                "source": "mapper",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0726213",
                "data": {
                    "configuration": {
                        "api": {
                            "from": "/calc",
                            "to": {
                                "scheme": "http",
                                "host": "calcapi.cloudapp.net",
                                "port": 80,
                                "path": "/api",
                                "queryString": "",
                                "query": {},
                                "isDefaultPort": true
                            }
                        },
                        "operation": {
                            "method": "GET",
                            "uriTemplate": "/add?a={a}&b={b}"
                        },
                        "user": {
                            "id": 1,
                            "groups": [
                                "Administrators",
                                "Developers"
                            ]
                        },
                        "product": {
                            "id": 1
                        }
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0727522",
                "data": {
                    "message": "Request is being forwarded to the backend service.",
                    "request": {
                        "method": "GET",
                        "url": "http://calcapi.cloudapp.net/api/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "X-Forwarded-For",
                                "value": "33.52.215.35"
                            }
                        ]
                    }
                }
            }
        ],
        "outbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1960601",
                "data": {
                    "response": {
                        "status": {
                            "code": 200,
                            "reason": "OK"
                        },
                        "headers": [
                            {
                                "name": "Pragma",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Length",
                                "value": "124"
                            },
                            {
                                "name": "Cache-Control",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Type",
                                "value": "application/xml; charset=utf-8"
                            },
                            {
                                "name": "Date",
                                "value": "Tue, 23 Jun 2015 19:51:35 GMT"
                            },
                            {
                                "name": "Expires",
                                "value": "-1"
                            },
                            {
                                "name": "Server",
                                "value": "Microsoft-IIS/8.5"
                            },
                            {
                                "name": "X-AspNet-Version",
                                "value": "4.0.30319"
                            },
                            {
                                "name": "X-Powered-By",
                                "value": "ASP.NET"
                            }
                        ]
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1961112",
                "data": {
                    "message": "Response headers have been sent to the caller. Starting to stream the response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming to the caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="6b2c2-139"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b2c2-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="6b2c2-140">[Cloud Cover 에피소드 177: 추가 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)에서 추적 정책 식의 데모를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="6b2c2-141">데모를 보려면 21:00 지점으로 빨리 감기 하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-141">Fast-forward to 21:00 to see the demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector to trace a call]: #trace-call
[Inspect the trace]: #inspect-trace
[Next steps]: #next-steps

[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Azure Classic Portal]: https://manage.windowsazure.com/


[api-management-developer-portal-menu]: ./media/api-management-howto-api-inspector/api-management-developer-portal-menu.png
[api-management-api]: ./media/api-management-howto-api-inspector/api-management-api.png
[api-management-echo-api-get]: ./media/api-management-howto-api-inspector/api-management-echo-api-get.png
[api-management-developer-key]: ./media/api-management-howto-api-inspector/api-management-developer-key.png
[api-management-open-console]: ./media/api-management-howto-api-inspector/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-api-inspector/api-management-http-get.png
[api-management-send-results]: ./media/api-management-howto-api-inspector/api-management-send-results.png




