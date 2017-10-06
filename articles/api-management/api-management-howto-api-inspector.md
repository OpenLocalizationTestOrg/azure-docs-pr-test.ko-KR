---
title: "API 관리자-Azure API 관리를 사용 하 여 aaaTrace 호출 | Microsoft Docs"
description: "방법을 사용 하 여 tootrace 호출 hello Azure API 관리에서 API 검사자에 알아봅니다."
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
ms.openlocfilehash: b0c401caa8da1b789f6cfe5edf97a5f118d78f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a><span data-ttu-id="412f1-103">Azure API 관리에서 toouse hello API 검사기 tootrace 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="412f1-103">How toouse hello API Inspector tootrace calls in Azure API Management</span></span>
<span data-ttu-id="412f1-104">API 관리에서는 API 검사기 도구 toohelp Api 문제 해결 및 디버깅 있습니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-104">API Management provides an API Inspector tool toohelp you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="412f1-105">hello API 검사기 프로그래밍 방식으로 사용할 수 있습니다 및 hello 개발자 포털에서 직접 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-105">hello API Inspector can be used programmatically and can also be used directly from hello developer portal.</span></span> 

<span data-ttu-id="412f1-106">또한 tootracing 작업 API 관리자도 추적 [정책 식을](https://msdn.microsoft.com/library/azure/dn910913.aspx) 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-106">In addition tootracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="412f1-107">데모를 보려면 참조 [클라우드 포괄 에피소드 177: 더욱 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too21:00 빨리 감기 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too21:00.</span></span>

<span data-ttu-id="412f1-108">이 안내서는 API 검사기 사용을 단계적으로 안내해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="412f1-109">관리자 API 추적만 생성 및 toohello 속하는 구독 키가 포함 된 요청에 사용할 수 있도록 [관리자](api-management-howto-create-groups.md) 계정.</span><span class="sxs-lookup"><span data-stu-id="412f1-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong toohello [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="412f1-110"><a name="trace-call"></a> API 관리자를 사용 하 여 tootrace 호출</span><span class="sxs-lookup"><span data-stu-id="412f1-110"><a name="trace-call"> </a> Use API Inspector tootrace a call</span></span>
<span data-ttu-id="412f1-111">API 검사기 toouse 추가 **ocp apim 추적: true** 요청 헤더 tooyour 작업 호출을 다운로드 하 여 hello로 표시 하는 hello URL을 사용 하 여 hello 추적 검사 **apim 추적 위치 ocp** 응답 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-111">toouse API Inspector, add an **ocp-apim-trace: true** request header tooyour operation call, and then download and inspect hello trace using hello URL indicated by hello **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="412f1-112">이 프로그래밍을 수행할 수 있습니다 및 hello 개발자 포털에서 직접 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-112">This can be done programatically, and can also be done directly from hello developer portal.</span></span>

<span data-ttu-id="412f1-113">이 자습서에서는 방법을 사용 하 여 toouse hello API 검사기 tootrace 작업 hello hello에 구성 된 기본 계산기 API [첫 번째 API 관리](api-management-get-started.md) 자습서를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-113">This tutorial shows how toouse hello API Inspector tootrace operations using hello Basic Calculator API that is configured in hello [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="412f1-114">해당 자습서를 완료 하지 않은 경우 단 몇 분 정도의 tooimport hello 기본 계산기 API 또는 선택 hello 에코 API 등의 다른 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-114">If you haven't completed that tutorial it only takes a few moments tooimport hello Basic Calculator API, or you can use another API of your choosing such as hello Echo API.</span></span> <span data-ttu-id="412f1-115">각 API 관리 서비스 인스턴스를 사용 하는 tooexperiment 및 API 관리에 대 한 자세한 내용은 수 있는 에코 API로 미리 구성 되어 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-115">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="412f1-116">hello 에코 API는 모든 입력이 tooit 전송 다시 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-116">hello Echo API returns back whatever input is sent tooit.</span></span> <span data-ttu-id="412f1-117">toouse, 모든 HTTP 동사를 호출할 수 있으며 hello 반환 값은 단순히 보낸 있습니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-117">toouse it, you can invoke any HTTP verb, and hello return value will simply be what you sent.</span></span> 

<span data-ttu-id="412f1-118">시작 tooget 클릭 **개발자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="412f1-118">tooget started, click **Developer portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="412f1-119">작업 편리 tooview 제공 하는 hello 개발자 포털에서 직접 호출할 수 있습니다 및 API의 hello 작동을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-119">Operations can be called directly from hello developer portal which provides a convenient way tooview and test hello operations of an API.</span></span>

> <span data-ttu-id="412f1-120">API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![API 관리 개발자 포털][api-management-developer-portal-menu]

<span data-ttu-id="412f1-122">클릭 **Api** hello 상단 메뉴에서 **기본 계산기**합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-122">Click **APIs** from hello top menu, and then click **Basic Calculator**.</span></span>

![Echo API][api-management-api]

<span data-ttu-id="412f1-124">클릭 **실습** tootry hello **정수 두 개를 추가** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-124">Click **Try it** tootry hello **Add two integers** operation.</span></span>

![시도][api-management-open-console]

<span data-ttu-id="412f1-126">Hello에서 hello 기본 매개 변수 값 및 원하는 hello 제품에 대 한 등록 키를 선택 hello toouse 유지 **구독 키** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-126">Keep hello default parameter values, and select hello subscription key for hello product you want toouse from hello **subscription-key** drop-down.</span></span>

<span data-ttu-id="412f1-127">Hello 개발자 포털 hello에 기본적으로 **Ocp Apim 추적** 헤더가 너무 이미 설정 되어**true**합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-127">By default in hello developer portal hello **Ocp-Apim-Trace** header is already set too**true**.</span></span> <span data-ttu-id="412f1-128">이 헤더는 추적 생성 여부를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-128">This header configures whether or not a trace is generated.</span></span>

![보내기][api-management-http-get]

<span data-ttu-id="412f1-130">클릭 **보낼** tooinvoke hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-130">Click **Send** tooinvoke hello operation.</span></span>

![보내기][api-management-send-results]

<span data-ttu-id="412f1-132">Hello 응답에서 헤더 수는 **apim 추적 위치 ocp** 다음 예제에서는 값 비슷한 toohello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-132">In hello response headers will be an **ocp-apim-trace-location** with a value similar toohello following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="412f1-133">hello 추적에서 다운로드할 수 있습니다 hello 위치를 지정 하 고 hello 다음 단계에서와 같이 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-133">hello trace can be downloaded from hello specified location and reviewed as demonstrated in hello next step.</span></span> <span data-ttu-id="412f1-134">Note만 hello 마지막 100 로그 항목 저장 되 고 로그 위치는 회전에서 재사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-134">Note that only hello last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="412f1-135">따라서 100 개 이상의 호출을 수행 하는 경우 추적을 사용 하면서 결국 먼저 위치에서 첫 번째 추적 hello를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting hello first traces in place.</span></span>

## <span data-ttu-id="412f1-136"><a name="inspect-trace"></a>Hello 추적을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-136"><a name="inspect-trace"> </a>Inspect hello trace</span></span>
<span data-ttu-id="412f1-137">hello에서 hello 추적 파일을 다운로드 하는 hello 추적에서 tooreview hello 값 **apim 추적 위치 ocp** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-137">tooreview hello values in hello trace, download hello trace file from hello **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="412f1-138">JSON 형식의 텍스트 파일로 이며 항목 비슷한 toohello 다음 예제를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-138">It is a text file in JSON format, and contains entries similar toohello following example.</span></span>

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
                    "message": "Request is being forwarded toohello backend service.",
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
                    "message": "Response headers have been sent toohello caller. Starting toostream hello response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming toohello caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="412f1-139"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="412f1-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="412f1-140">[Cloud Cover 에피소드 177: 추가 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)에서 추적 정책 식의 데모를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="412f1-141">빠른 정방향 too21:00 toosee hello 데모입니다.</span><span class="sxs-lookup"><span data-stu-id="412f1-141">Fast-forward too21:00 toosee hello demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector tootrace a call]: #trace-call
[Inspect hello trace]: #inspect-trace
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




