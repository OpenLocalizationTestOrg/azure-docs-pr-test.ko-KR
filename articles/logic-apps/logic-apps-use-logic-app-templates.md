---
title: "템플릿으로 워크플로 만들기 - Azure Logic Apps | Microsoft Docs"
description: "시작 - Azure 논리 앱 템플릿을 사용하여 앱을 연결하고 데이터를 통합하는 워크플로를 신속하게 만듭니다."
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
ms.openlocfilehash: 89272869f7dfaa34cbd2ad32d67dca0955e6158b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-to-get-started-quickly"></a><span data-ttu-id="3b435-103">미리 작성된 템플릿 또는 패턴을 사용하여 워크플로를 구성하고 빠르게 시작</span><span class="sxs-lookup"><span data-stu-id="3b435-103">Configure a workflow using a pre-built template or pattern to get started quickly</span></span>

## <a name="what-are-logic-app-templates"></a><span data-ttu-id="3b435-104">논리 앱 템플릿이란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="3b435-104">What are logic app templates</span></span>
<span data-ttu-id="3b435-105">논리 앱 템플릿은 미리 만들어진 논리 앱으로서 사용자 고유의 워크플로를 빠르게 만들기 시작하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-105">A logic app template is a pre-built logic app that you can use to quickly get started creating your own workflow.</span></span> 

<span data-ttu-id="3b435-106">이러한 템플릿을 통해 논리 앱을 사용하여 빌드할 수 있는 다양한 패턴을 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-106">These templates are a good way to discover various patterns that can be built using logic apps.</span></span> <span data-ttu-id="3b435-107">템플릿을 그대로 사용하거나 시나리오에 맞도록 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-107">You can either use these templates as-is or modify them to fit your scenario.</span></span>

## <a name="overview-of-available-templates"></a><span data-ttu-id="3b435-108">사용 가능한 템플릿 개요</span><span class="sxs-lookup"><span data-stu-id="3b435-108">Overview of available templates</span></span>
<span data-ttu-id="3b435-109">현재 사용 가능한 여러 템플릿이 논리 앱 플랫폼에 게시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-109">There are many available templates currently published in the logic app platform.</span></span> <span data-ttu-id="3b435-110">일부 예제 범주 및 이에 사용되는 커넥터 유형은 아래에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-110">Some example categories, as well as the type of connectors used in them, are listed below.</span></span>

### <a name="enterprise-cloud-templates"></a><span data-ttu-id="3b435-111">엔터프라이즈 클라우드 템플릿</span><span class="sxs-lookup"><span data-stu-id="3b435-111">Enterprise cloud templates</span></span>
<span data-ttu-id="3b435-112">Dynamics CRM, Salesforce, Box, Azure Blob 및 엔터프라이즈 클라우드 요구 사항에 대한 다른 커넥터를 통합하는 템플릿</span><span class="sxs-lookup"><span data-stu-id="3b435-112">Templates that integrate Dynamics CRM, Salesforce, Box, Azure Blob, and other connectors for your enterprise cloud needs.</span></span> <span data-ttu-id="3b435-113">이러한 템플릿을 사용하여 수행할 수 있는 몇 가지 예에는 잠재 고객을 구성하고 회사 파일 데이터를 백업하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-113">Some examples of what can be done with these templates include organizing your leads and backing up your corporate file data.</span></span>

### <a name="enterprise-integration-pack-templates"></a><span data-ttu-id="3b435-114">엔터프라이즈 통합 팩 템플릿</span><span class="sxs-lookup"><span data-stu-id="3b435-114">Enterprise integration pack templates</span></span>
<span data-ttu-id="3b435-115">VETER(유효성 검사, 추출, 변환, 보강, 라우팅) 파이프라인의 구성, AS2를 통한 X12 EDI 문서 수신과 XML로 변환 및 X12와 AS2 메시지 처리가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-115">Configurations of VETER (validate, extract, transform, enrich, route) pipelines, receiving an X12 EDI document over AS2 and transforming it to XML, as well as X12 and AS2 message handling.</span></span>

### <a name="protocol-pattern-templates"></a><span data-ttu-id="3b435-116">프로토콜 패턴 템플릿</span><span class="sxs-lookup"><span data-stu-id="3b435-116">Protocol pattern templates</span></span>
<span data-ttu-id="3b435-117">이러한 템플릿은 FTP 및 SFTP에 걸친 통합뿐만 아니라 HTTP를 통해 요청-응답과 같은 프로토콜 패턴을 포함하는 논리 앱으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-117">These templates consist of logic apps that contain protocol patterns such as request-response over HTTP as well as integrations across FTP and SFTP.</span></span> <span data-ttu-id="3b435-118">존재하는 대로 또는 더 복잡한 프로토콜 패턴을 만드는 기준으로 이러한 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-118">Use these as they exist, or as a basis for creating more complex protocol patterns.</span></span>  

### <a name="personal-productivity-templates"></a><span data-ttu-id="3b435-119">개인 생산성 템플릿</span><span class="sxs-lookup"><span data-stu-id="3b435-119">Personal productivity templates</span></span>
<span data-ttu-id="3b435-120">개인 생산성을 향상시킬 수 있는 패턴에는 매일 미리 알림을 설정하고 할 일 목록에 중요한 작업 항목을 설정하고 단일 사용자 승인 단계까지 시간이 걸리는 작업을 자동화하는 템플릿이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-120">Patterns to help improve personal productivity include templates that set daily reminders, turn important work items into to-do lists, and automate lengthy tasks down to a single user approval step.</span></span>

### <a name="consumer-cloud-templates"></a><span data-ttu-id="3b435-121">소비자 클라우드 템플릿</span><span class="sxs-lookup"><span data-stu-id="3b435-121">Consumer cloud templates</span></span>
<span data-ttu-id="3b435-122">Twitter, Slack 및 전자 메일과 같은 소셜 미디어 서비스와 통합하는 간단한 템플릿은 궁극적으로 소셜 마케팅 미디어 이니셔티브를 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-122">Simple templates that integrate with social media services such as Twitter, Slack, and email, ultimately capable of strengthening social media marketing initiatives.</span></span> <span data-ttu-id="3b435-123">알림에는 흐린 복사 등의 템플릿을 포함하며 일반적으로 반복 작업에 소요된 시간을 저장하여 생산성을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-123">These also include templates such as cloudy copying, which can help increase productivity by saving time spent on traditionally repetitive tasks.</span></span> 

## <a name="how-to-create-a-logic-app-using-a-template"></a><span data-ttu-id="3b435-124">템플릿을 사용하여 논리 앱을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="3b435-124">How to create a logic app using a template</span></span>
<span data-ttu-id="3b435-125">논리 앱 템플릿을 사용하여 시작하려면 논리 앱 디자이너로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-125">To get started using a logic app template, go into the logic app designer.</span></span> <span data-ttu-id="3b435-126">기존 논리 앱을 열어 디자이너를 입력하는 경우 논리 앱은 디자이너 보기로 자동으로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-126">If you're entering the designer by opening an existing logic app, the logic app automatically loads in your designer view.</span></span> <span data-ttu-id="3b435-127">그러나 새 논리 앱을 만드는 경우 아래의 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-127">However, if you're creating a new logic app, you see the screen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

<span data-ttu-id="3b435-128">이 화면에서 빈 논리 앱 또는 미리 작성된 템플릿을 시작하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-128">From this screen, you can either choose to start with a blank logic app or a pre-built template.</span></span> <span data-ttu-id="3b435-129">템플릿 중 하나를 선택하는 경우 추가 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-129">If you select one of the templates, you are provided with additional information.</span></span> <span data-ttu-id="3b435-130">이 예제에서는 *새 파일이 Dropbox에서 만들어지면 OneDrive에 복사합니다.* 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-130">In this example, we use the *When a new file is created in Dropbox, copy it to OneDrive* template.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

<span data-ttu-id="3b435-131">템플릿을 사용하려면 *이 템플릿 사용* 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-131">If you choose to use the template, just select the *use this template* button.</span></span> <span data-ttu-id="3b435-132">템플릿이 사용하는 커넥터에 따라 계정에 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-132">You'll be asked to sign in to your accounts based on which connectors the template utilizes.</span></span> <span data-ttu-id="3b435-133">또는 이러한 커넥터와 연결을 이전에 설정한 경우 아래와 같이 계속하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-133">Or, if you've previously established a connection with these connectors, you can select continue as seen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

<span data-ttu-id="3b435-134">연결을 설정하고 *계속*하도록 선택한 후에 논리 앱은 디자이너 보기로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-134">After establishing the connection and selecting *continue*, the logic app opens in designer view.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

<span data-ttu-id="3b435-135">위의 예제에서 많은 템플릿의 경우와 마찬가지로 일부 필수 속성 필드는 커넥터 내에서 채워질 수 있습니다. 그러나 어떤 경우에는 논리 앱을 제대로 배포하기 전에 값이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-135">In the example above, as is the case with many templates, some of the mandatory property fields may be filled out within the connectors; however, some might still require a value before being able to properly deploy the logic app.</span></span> <span data-ttu-id="3b435-136">누락된 필드 중 일부를 입력하지 않고 배포하려는 경우 오류 메시지와 함께 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-136">If you try to deploy without entering some of the missing fields, you'll be notified with an error message.</span></span>

<span data-ttu-id="3b435-137">템플릿 뷰어로 돌아가려는 경우 위쪽 탐색 모음에서 *템플릿* 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-137">If you wish to return to the template viewer, select the *Templates* button in the top navigation bar.</span></span> <span data-ttu-id="3b435-138">템플릿 뷰어로 다시 전환하면 저장하지 않은 진행 상황이 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-138">By switching back to the template viewer, you lose any unsaved progress.</span></span> <span data-ttu-id="3b435-139">템플릿 뷰어로 다시 전환하기 전에 이를 알리는 경고 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-139">Prior to switching back into template viewer, you'll see a warning message notifying you of this.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-to-deploy-a-logic-app-created-from-a-template"></a><span data-ttu-id="3b435-140">템플릿에서 만든 논리 앱을 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="3b435-140">How to deploy a logic app created from a template</span></span>
<span data-ttu-id="3b435-141">템플릿을 로드하고 원하는 대로 변경하면 왼쪽 위 모퉁이에서 저장 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-141">Once you have loaded your template and made any desired changes, select the save button in the upper left corner.</span></span> <span data-ttu-id="3b435-142">이렇게 하면 논리 앱을 저장하고 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="3b435-142">This saves and publishes your logic app.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

<span data-ttu-id="3b435-143">기존 논리 앱 템플릿에 다른 단계를 추가하거나 전체적으로 편집하는 방법에 대한 자세한 내용을 찾고 있다면 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)에서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="3b435-143">If you would like more information on how to add more steps into an existing logic app template, or make edits in general, read more at [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

