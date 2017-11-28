---
title: "Azure 응용 프로그램 게이트웨이 위한 aaaRedirect 개요 | Microsoft Docs"
description: "Azure 응용 프로그램 게이트웨이에 hello 리디렉션 기능에 대 한 자세한 내용은"
services: application-gateway
documentationcenter: na
author: amsriva
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: amsriva
ms.openlocfilehash: 7149e3bd000d336c51995fb0e90f971b4d9ba2be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-redirect-overview"></a><span data-ttu-id="99b65-103">Application Gateway 리디렉션 개요</span><span class="sxs-lookup"><span data-stu-id="99b65-103">Application Gateway redirect overview</span></span>

<span data-ttu-id="99b65-104">많은 웹 응용 프로그램에 대 한 일반적인 시나리오는 toosupport 자동 HTTP tooHTTPS 리디렉션 tooensure 응용 프로그램과 사용자 간의 모든 통신이 암호화 된 경로 통해 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-104">A common scenario for many web applications is toosupport automatic HTTP tooHTTPS redirection tooensure all communication between application and its users occurs over an encrypted path.</span></span> <span data-ttu-id="99b65-105">지난 hello, 고객 tooredirect 요청 받은 HTTP tooHTTPS에는 해당 목적으로 제공 하는 전용된 백 엔드 풀 만들기와 같은 기술을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-105">In hello past, customers have used techniques such as creating a dedicated backend pool whose sole purpose is tooredirect requests it receives on HTTP tooHTTPS.</span></span>  <span data-ttu-id="99b65-106">응용 프로그램 게이트웨이 이제 응용 프로그램 게이트웨이 hello에 tooredirect 트래픽 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-106">Application gateway now supports ability tooredirect traffic on hello Application Gateway.</span></span> <span data-ttu-id="99b65-107">이 간단한 응용 프로그램 구성, hello 리소스 사용을 최적화 하며 전역 및 경로 기반 리디렉션을 비롯 한 새로운 리디렉션 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-107">This simplifies application configuration, optimizes hello resource usage, and supports new redirection scenarios including global and path-based redirection.</span></span> <span data-ttu-id="99b65-108">응용 프로그램 게이트웨이 리디렉션 지원은 제한 되어 tooHTTP HTTPS 리디렉션만-> 합니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-108">Application Gateway redirection support is not limited tooHTTP -> HTTPS redirection alone.</span></span> <span data-ttu-id="99b65-109">응용 프로그램 게이트웨이에 대 한 수신기 tooanother 수신기에서 수신 하는 트래픽의 리디렉션을 허용 하는 제네릭 리디렉션 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-109">This is a generic redirection mechanism, which allows for redirection of traffic received at one listener tooanother listener on Application Gateway.</span></span> <span data-ttu-id="99b65-110">또한 리디렉션 tooan 외부 사이트도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-110">It also supports redirection tooan external site as well.</span></span> <span data-ttu-id="99b65-111">응용 프로그램 게이트웨이 리디렉션 지원 hello 다음 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-111">Application Gateway redirection support offers hello following capabilities:</span></span>

1. <span data-ttu-id="99b65-112">게이트웨이 hello에 하나의 수신기 tooanother 수신기에서 전역 리디렉션.</span><span class="sxs-lookup"><span data-stu-id="99b65-112">Global redirection from one listener tooanother listener on hello Gateway.</span></span> <span data-ttu-id="99b65-113">따라서 사이트에 HTTP tooHTTPS 리디렉션을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-113">This enables HTTP tooHTTPS redirection on a site.</span></span>
2. <span data-ttu-id="99b65-114">경로 기반 리디렉션.</span><span class="sxs-lookup"><span data-stu-id="99b65-114">Path-based redirection.</span></span> <span data-ttu-id="99b65-115">이 형식의 리디렉션 사용 하 여 특정 사이트 영역에만 HTTP tooHTTPS 리디렉션/카트/으로 쇼핑 카트 영역을 표시 하는 예를 들어 * 합니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-115">This type of redirection enables HTTP tooHTTPS redirection only on a specific site area, for example a shopping cart area denoted by /cart/*.</span></span>
3. <span data-ttu-id="99b65-116">리디렉션 tooexternal 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-116">Redirect tooexternal site.</span></span>

![리디렉션](./media/application-gateway-redirect-overview/redirect.png)

<span data-ttu-id="99b65-118">이러한 변경으로 인해 고객 toocreate hello 대상 수신기를 지정 하는 새 리디렉션 구성 개체를 해야 합니다. 또는 외부 사이트 toowhich 리디렉션이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-118">With this change, customers would need toocreate a new redirect configuration object, which specifies hello target listener or external site toowhich redirection is desired.</span></span> <span data-ttu-id="99b65-119">hello 구성 요소는 hello URI 경로 조회가 문자열 toohello 리디렉션 URL을 추가 하는 옵션 tooenable도 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-119">hello configuration element also supports options tooenable appending hello URI path and query string toohello redirected URL.</span></span> <span data-ttu-id="99b65-120">고객은 리디렉션이 임시 리디렉션(HTTP 상태 코드 302)인지 영구 리디렉션(HTTP 상태 코드 301)인지도 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-120">Customers could also choose whether redirection is a temporary (HTTP status code 302) or a permanent redirect (HTTP status code 301).</span></span> <span data-ttu-id="99b65-121">이 리디렉션 구성을 만든 후 새 규칙을 통해 연결 된 toohello 소스 수신기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-121">Once created this redirect configuration is attached toohello source listener via a new rule.</span></span> <span data-ttu-id="99b65-122">기본 규칙을 사용 하는 경우 hello 리디렉션 구성 소스 수신기와 연결 된 이며 글로벌 리디렉션.</span><span class="sxs-lookup"><span data-stu-id="99b65-122">When using a basic rule, hello redirect configuration is associated with a source listener and is a global redirect.</span></span> <span data-ttu-id="99b65-123">경로 기반 규칙을 사용할 경우 hello 리디렉션 구성 hello URL 경로 지도에 정의 되 고 따라서 사이트의 toohello 특정 경로 영역에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99b65-123">When a path-based rule is used, hello redirect configuration is defined on hello URL path map and hence only applies toohello specific path area of a site.</span></span>

### <a name="next-steps"></a><span data-ttu-id="99b65-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="99b65-124">Next steps</span></span>

[<span data-ttu-id="99b65-125">응용 프로그램 게이트웨이에서 URL 리디렉션 구성</span><span class="sxs-lookup"><span data-stu-id="99b65-125">Configure URL redirection on an application gateway</span></span>](application-gateway-configure-redirect-powershell.md)
