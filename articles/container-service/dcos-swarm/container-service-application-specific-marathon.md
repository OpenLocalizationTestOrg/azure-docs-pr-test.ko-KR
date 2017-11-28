---
title: "aaaApplication 또는 사용자 고유의 마라톤 서비스 | Microsoft Docs"
description: "응용 프로그램 또는 사용자 특정 Marathon 서비스 만들기"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "컨테이너, Marathon, 마이크로 서비스, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="7a87c-104">응용 프로그램 또는 사용자 특정 Marathon 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="7a87c-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="7a87c-105">Azure 컨테이너 서비스는 Apache Mesos 및 Marathon을 미리 구성하는 마스터 서버 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="7a87c-106">사용 되는 tooorchestrate 될 수 있습니다. hello 클러스터 있지만 응용 프로그램이 목적을 위해 하지 toouse hello 마스터 서버를 가장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-106">These can be used tooorchestrate your applications on hello cluster, but it's best not toouse hello master servers for this purpose.</span></span> <span data-ttu-id="7a87c-107">예를 들어 hello 마스터 서버 자체에 로그인 하 고 변경-이 필요 마라톤의 hello 구성을 조정 약간 표준 hello 및 기준은 필요 toobe과 다른 이며 관리 되는 고유 마스터 서버를 권장 합니다. 독립적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-107">For example, tweaking hello configuration of Marathon requires logging into hello master servers themselves and making changes--this encourages unique master servers that are a little different from hello standard and need toobe cared for and managed independently.</span></span> <span data-ttu-id="7a87c-108">또한 한 팀에 필요한 hello 구성의 다른 팀에 대 한 최적의 구성을 hello 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-108">Additionally, hello configuration required by one team might not be hello optimal configuration for another team.</span></span>

<span data-ttu-id="7a87c-109">이 문서에서는 설명 어떻게 tooadd는 응용 프로그램이 나 사용자 고유의 마라톤 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-109">In this article, we'll explain how tooadd an application or user-specific Marathon service.</span></span>

<span data-ttu-id="7a87c-110">무료 tooconfigure 되기 tooa 단일 사용자 또는 팀이이 서비스 속할 수 있습니다, 때문에 원하는 어떤 방식으로든 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-110">Because this service will belong tooa single user or team, they are free tooconfigure it in any way that they desire.</span></span> <span data-ttu-id="7a87c-111">또한 Azure 컨테이너 서비스는 hello 서비스 toorun 계속 되도록 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-111">Also, Azure Container Service will ensure that hello service continues toorun.</span></span> <span data-ttu-id="7a87c-112">Hello 서비스가 실패 하면 Azure 컨테이너 서비스는 다시 시작 드립니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-112">If hello service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="7a87c-113">대부분의 hello 없습니다도 알게 가동 중지 시간 이전의입니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-113">Most of hello time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a87c-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7a87c-114">Prerequisites</span></span>
<span data-ttu-id="7a87c-115">[Azure 컨테이너 서비스의 인스턴스가 배포](container-service-deployment.md) orchestrator와 DC/OS를 입력 하 고 [클라이언트 tooyour 클러스터를 연결할 수 있는지 확인](../container-service-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect tooyour cluster](../container-service-connect.md).</span></span> <span data-ttu-id="7a87c-116">또한 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-116">Also, do hello following steps.</span></span>

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="7a87c-117">응용 프로그램 또는 사용자 특정 Marathon 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="7a87c-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="7a87c-118">Toocreate 원하는 hello 응용 프로그램 서비스의 hello 이름을 정의 하는 JSON 구성 파일을 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-118">Begin by creating a JSON configuration file that defines hello name of hello application service that you want toocreate.</span></span> <span data-ttu-id="7a87c-119">사용 하 여 여기 `marathon-alice` hello 프레임 워크 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-119">Here we use `marathon-alice` as hello framework name.</span></span> <span data-ttu-id="7a87c-120">축 처럼 hello 파일을 저장 `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="7a87c-120">Save hello file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="7a87c-121">다음으로 hello DC/OS CLI tooinstall hello 마라톤 인스턴스 hello 설정 된 옵션을 구성 파일에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-121">Next, use hello DC/OS CLI tooinstall hello Marathon instance with hello options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="7a87c-122">이제 프로그램 `marathon-alice` DC/OS UI의 hello 서비스 탭에서 실행 되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-122">You should now see your `marathon-alice` service running in hello Services tab of your DC/OS UI.</span></span> <span data-ttu-id="7a87c-123">hello UI 됩니다 `http://<hostname>/service/marathon-alice/` tooaccess 하려는 경우 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-123">hello UI will be `http://<hostname>/service/marathon-alice/` if you want tooaccess it directly.</span></span>

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a><span data-ttu-id="7a87c-124">Hello DC/OS CLI tooaccess hello 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="7a87c-124">Set hello DC/OS CLI tooaccess hello service</span></span>
<span data-ttu-id="7a87c-125">필요에 따라 여 구성할 수 있습니다 DC/OS CLI tooaccess이 새로운 서비스 설정 hello `marathon.url` 속성 toopoint toohello `marathon-alice` 다음과 같이 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="7a87c-125">You can optionally configure your DC/OS CLI tooaccess this new service by setting hello `marathon.url` property toopoint toohello `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="7a87c-126">Hello로 여 CLI가 작동 하는 풀 마라톤의 인스턴스를 확인할 수 있습니다 `dcos config show` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-126">You can verify which instance of Marathon that your CLI is working against with hello `dcos config show` command.</span></span> <span data-ttu-id="7a87c-127">Hello 명령 사용 하 여 마스터 마라톤 서비스 toousing를 되돌릴 수 `dcos config unset marathon.url`합니다.</span><span class="sxs-lookup"><span data-stu-id="7a87c-127">You can revert toousing your master Marathon service with hello command `dcos config unset marathon.url`.</span></span>

