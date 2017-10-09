---
title: "템플릿-Azure 논리 앱에서에서 aaaCreate 워크플로 | Microsoft Docs"
description: "시작-Azure 논리 앱 템플릿은 tooconnect 앱을 사용 하 여 워크플로 신속 하 게 생성 하 고 데이터를 통합 합니다."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0127523662a12076772b52968f1e2f9cbad72a1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-tooget-started-quickly"></a><span data-ttu-id="69300-103">미리 작성 된 템플릿 또는 패턴 tooget 신속 하 게 시작을 사용 하는 워크플로 구성</span><span class="sxs-lookup"><span data-stu-id="69300-103">Configure a workflow using a pre-built template or pattern tooget started quickly</span></span>

## <a name="what-are-logic-app-templates"></a><span data-ttu-id="69300-104">논리 앱 템플릿이란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="69300-104">What are logic app templates</span></span>
<span data-ttu-id="69300-105">논리 앱 템플릿은 tooquickly를 사용할 수 있는 미리 빌드된 논리 앱 직접 워크플로 만들기 전에입니다.</span><span class="sxs-lookup"><span data-stu-id="69300-105">A logic app template is a pre-built logic app that you can use tooquickly get started creating your own workflow.</span></span> 

<span data-ttu-id="69300-106">이러한 서식 파일은 좋은 방법 toodiscover 논리 앱을 사용 하 여 빌드할 수 있는 다양 한 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="69300-106">These templates are a good way toodiscover various patterns that can be built using logic apps.</span></span> <span data-ttu-id="69300-107">이러한 템플릿을으로 사용할 수 있습니다-되었거나 toofit 수정 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="69300-107">You can either use these templates as-is or modify them toofit your scenario.</span></span>

## <a name="overview-of-available-templates"></a><span data-ttu-id="69300-108">사용 가능한 템플릿 개요</span><span class="sxs-lookup"><span data-stu-id="69300-108">Overview of available templates</span></span>
<span data-ttu-id="69300-109">Hello 논리 앱 플랫폼에 현재 게시 된 많은 사용 가능한 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69300-109">There are many available templates currently published in hello logic app platform.</span></span> <span data-ttu-id="69300-110">에 사용 되는 커넥터 hello 형식 뿐만 아니라 일부 예제에서는 범주는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="69300-110">Some example categories, as well as hello type of connectors used in them, are listed below.</span></span>

### <a name="enterprise-cloud-templates"></a><span data-ttu-id="69300-111">엔터프라이즈 클라우드 템플릿</span><span class="sxs-lookup"><span data-stu-id="69300-111">Enterprise cloud templates</span></span>
<span data-ttu-id="69300-112">Dynamics CRM, Salesforce, Box, Azure Blob 및 엔터프라이즈 클라우드 요구 사항에 대한 다른 커넥터를 통합하는 템플릿</span><span class="sxs-lookup"><span data-stu-id="69300-112">Templates that integrate Dynamics CRM, Salesforce, Box, Azure Blob, and other connectors for your enterprise cloud needs.</span></span> <span data-ttu-id="69300-113">이러한 템플릿을 사용하여 수행할 수 있는 몇 가지 예에는 잠재 고객을 구성하고 회사 파일 데이터를 백업하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69300-113">Some examples of what can be done with these templates include organizing your leads and backing up your corporate file data.</span></span>

### <a name="enterprise-integration-pack-templates"></a><span data-ttu-id="69300-114">엔터프라이즈 통합 팩 템플릿</span><span class="sxs-lookup"><span data-stu-id="69300-114">Enterprise integration pack templates</span></span>
<span data-ttu-id="69300-115">VETER의 구성 (유효성 검사, 추출, 변환, 보강, 라우팅할) s 2를 통해 문서화 하 고 tooXML, 변형 변경과 X12 및 AS2 메시지로 처리 하는 EDI X12 수신 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="69300-115">Configurations of VETER (validate, extract, transform, enrich, route) pipelines, receiving an X12 EDI document over AS2 and transforming it tooXML, as well as X12 and AS2 message handling.</span></span>

### <a name="protocol-pattern-templates"></a><span data-ttu-id="69300-116">프로토콜 패턴 템플릿</span><span class="sxs-lookup"><span data-stu-id="69300-116">Protocol pattern templates</span></span>
<span data-ttu-id="69300-117">이러한 템플릿은 FTP 및 SFTP에 걸친 통합뿐만 아니라 HTTP를 통해 요청-응답과 같은 프로토콜 패턴을 포함하는 논리 앱으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="69300-117">These templates consist of logic apps that contain protocol patterns such as request-response over HTTP as well as integrations across FTP and SFTP.</span></span> <span data-ttu-id="69300-118">존재하는 대로 또는 더 복잡한 프로토콜 패턴을 만드는 기준으로 이러한 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69300-118">Use these as they exist, or as a basis for creating more complex protocol patterns.</span></span>  

### <a name="personal-productivity-templates"></a><span data-ttu-id="69300-119">개인 생산성 템플릿</span><span class="sxs-lookup"><span data-stu-id="69300-119">Personal productivity templates</span></span>
<span data-ttu-id="69300-120">패턴 toohelp 개인 생산성 향상 매일 미리 알림을 설정할 고 할 일 목록으로 중요 한 작업 항목을 설정 하 고 tooa 단일 사용자 승인 단계 다운 시간이 오래 걸리는 작업을 자동화 하는 템플릿을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="69300-120">Patterns toohelp improve personal productivity include templates that set daily reminders, turn important work items into to-do lists, and automate lengthy tasks down tooa single user approval step.</span></span>

### <a name="consumer-cloud-templates"></a><span data-ttu-id="69300-121">소비자 클라우드 템플릿</span><span class="sxs-lookup"><span data-stu-id="69300-121">Consumer cloud templates</span></span>
<span data-ttu-id="69300-122">Twitter, Slack 및 전자 메일과 같은 소셜 미디어 서비스와 통합하는 간단한 템플릿은 궁극적으로 소셜 마케팅 미디어 이니셔티브를 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69300-122">Simple templates that integrate with social media services such as Twitter, Slack, and email, ultimately capable of strengthening social media marketing initiatives.</span></span> <span data-ttu-id="69300-123">알림에는 흐린 복사 등의 템플릿을 포함하며 일반적으로 반복 작업에 소요된 시간을 저장하여 생산성을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69300-123">These also include templates such as cloudy copying, which can help increase productivity by saving time spent on traditionally repetitive tasks.</span></span> 

## <a name="how-toocreate-a-logic-app-using-a-template"></a><span data-ttu-id="69300-124">어떻게 toocreate 서식 파일을 사용 하 여 논리 앱</span><span class="sxs-lookup"><span data-stu-id="69300-124">How toocreate a logic app using a template</span></span>
<span data-ttu-id="69300-125">논리 앱 템플릿을 사용 하 여 시작 tooget hello 논리가 응용 프로그램 디자이너도 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69300-125">tooget started using a logic app template, go into hello logic app designer.</span></span> <span data-ttu-id="69300-126">기존 논리 앱을 열어 hello 디자이너를 입력 하는 경우 hello 논리 앱 디자이너 보기에 자동으로 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="69300-126">If you're entering hello designer by opening an existing logic app, hello logic app automatically loads in your designer view.</span></span> <span data-ttu-id="69300-127">그러나 새 논리 앱을 만드는 경우에 아래의 hello 화면을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="69300-127">However, if you're creating a new logic app, you see hello screen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

<span data-ttu-id="69300-128">이 화면에서 toostart 빈 논리 앱 또는 미리 작성된 된 템플릿을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69300-128">From this screen, you can either choose toostart with a blank logic app or a pre-built template.</span></span> <span data-ttu-id="69300-129">Hello 템플릿 중 하나를 선택 하는 경우에 추가 정보와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69300-129">If you select one of hello templates, you are provided with additional information.</span></span> <span data-ttu-id="69300-130">이 예제에서는 사용 하 여 hello *드롭 상자에서는 새 파일을 만들 때 복사 tooOneDrive* 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="69300-130">In this example, we use hello *When a new file is created in Dropbox, copy it tooOneDrive* template.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

<span data-ttu-id="69300-131">Hello toouse hello 서식 파일을 선택 하면 선택 *이 서식 파일을 사용 하 여* 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="69300-131">If you choose toouse hello template, just select hello *use this template* button.</span></span> <span data-ttu-id="69300-132">만들라는 메시지가 toosign tooyour 계정에서 사용 되는 커넥터 hello 서식 파일에 따라 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69300-132">You'll be asked toosign in tooyour accounts based on which connectors hello template utilizes.</span></span> <span data-ttu-id="69300-133">또는 이러한 커넥터와 연결을 이전에 설정한 경우 아래와 같이 계속하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69300-133">Or, if you've previously established a connection with these connectors, you can select continue as seen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

<span data-ttu-id="69300-134">Hello 연결을 선택한 후 *계속*, 디자이너 뷰에서 hello 논리 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="69300-134">After establishing hello connection and selecting *continue*, hello logic app opens in designer view.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

<span data-ttu-id="69300-135">위의 hello 예제에서 많은 템플릿 hello 경우 처럼 hello 필수 속성 필드 중 일부를 수 있습니다 채워야 hello 커넥터; 내에서 그러나 일부 여전히 필요한 값 수 있을 때까지 tooproperly hello 논리 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="69300-135">In hello example above, as is hello case with many templates, some of hello mandatory property fields may be filled out within hello connectors; however, some might still require a value before being able tooproperly deploy hello logic app.</span></span> <span data-ttu-id="69300-136">Hello 누락 된 필드 중 일부를 입력 하지 않고 toodeploy를 시도 하면 오류 메시지와 함께 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69300-136">If you try toodeploy without entering some of hello missing fields, you'll be notified with an error message.</span></span>

<span data-ttu-id="69300-137">Tooreturn toohello 서식 파일 뷰어를 선택 하 hello *템플릿* hello 위쪽 탐색 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="69300-137">If you wish tooreturn toohello template viewer, select hello *Templates* button in hello top navigation bar.</span></span> <span data-ttu-id="69300-138">뒤로 toohello 서식 파일 뷰어를 전환 하 여 저장 되지 않은 진행 상황을 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69300-138">By switching back toohello template viewer, you lose any unsaved progress.</span></span> <span data-ttu-id="69300-139">서식 파일 뷰어로 다시 이전 tooswitching이 알리는 경고 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69300-139">Prior tooswitching back into template viewer, you'll see a warning message notifying you of this.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-toodeploy-a-logic-app-created-from-a-template"></a><span data-ttu-id="69300-140">Toodeploy 논리 앱을 만드는 방법 서식 파일에서</span><span class="sxs-lookup"><span data-stu-id="69300-140">How toodeploy a logic app created from a template</span></span>
<span data-ttu-id="69300-141">서식 파일을 로드 하 고 원하는 변경 내용이 hello 왼쪽된 위 모서리에서 hello 저장 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="69300-141">Once you have loaded your template and made any desired changes, select hello save button in hello upper left corner.</span></span> <span data-ttu-id="69300-142">이렇게 하면 논리 앱을 저장하고 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="69300-142">This saves and publishes your logic app.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

<span data-ttu-id="69300-143">기존 논리 앱 템플릿은 단계씩 tooadd 더 실행 방법에 대 한 자세한 내용은 하거나 일반적 편집할 하는 경우에서 자세한 내용을 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="69300-143">If you would like more information on how tooadd more steps into an existing logic app template, or make edits in general, read more at [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

