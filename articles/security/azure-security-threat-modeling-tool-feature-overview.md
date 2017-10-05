---
title: "Microsoft 위협 모델링 도구 - Azure | Microsoft Docs"
description: "위협 모델링 도구에서 사용할 수 있는 모든 기능에 대해 알아보기"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 621ff305d7e782f85eeaae6c3fb02031673549c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="9f10d-103">위협 모델링 도구 기능 개요</span><span class="sxs-lookup"><span data-stu-id="9f10d-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="9f10d-104">위협 모델링 필요에 맞도록 위협 모델링 도구를 사용하도록 선택해 주셔서 감사 드립니다!</span><span class="sxs-lookup"><span data-stu-id="9f10d-104">We are glad you chose to use the Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="9f10d-105">아직 선택하지 않았다면 **[위협 모델링 도구 시작](./azure-security-threat-modeling-tool-getting-started.md)**을 방문하여 기본 내용을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="9f10d-105">If you haven’t done so, visit **[Getting Started with the Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** to learn the basics.</span></span>

> <span data-ttu-id="9f10d-106">자사 도구는 자주 업데이트되므로 최신 기능 및 향상된 기능을 확인하도록 이 가이드를 자주 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="9f10d-106">Our tool is updated often, so check this guide often to see our latest features and improvements.</span></span>

<span data-ttu-id="9f10d-107">"새 모델 만들기" 단추를 클릭하면 아래 이미지와 유사하게 빈 시작 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-107">Clicking on the "Create a New Model" button opens a blank start page, similar to the image below:</span></span>

![빈 시작 페이지](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="9f10d-109">**[시작](./azure-security-threat-modeling-tool-getting-started.md)** 예제의 자사 팀에서 만든 위협 모델을 사용하여 현재 이 도구에서 사용할 수 있는 모든 기능을 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-109">Using the threat model created by our team in the **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all the features available in the tool today.</span></span>

![기본 위협 모델](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="9f10d-111">탐색</span><span class="sxs-lookup"><span data-stu-id="9f10d-111">Navigation</span></span>

<span data-ttu-id="9f10d-112">기본 제공 기능을 알아보기 전에 도구에 있는 주요 구성 요소를 검토해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-112">Before diving into the built-in features, let’s go over the main components found in the tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="9f10d-113">메뉴 항목</span><span class="sxs-lookup"><span data-stu-id="9f10d-113">Menu items</span></span>

<span data-ttu-id="9f10d-114">환경은 다른 Microsoft 제품과 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-114">The experience should be similar to other Microsoft products.</span></span> <span data-ttu-id="9f10d-115">최상위 메뉴 항목 간을 이동하여 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-115">Let’s begin by going through the top-level menu items:</span></span>

![메뉴 항목](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="9f10d-117">레이블</span><span class="sxs-lookup"><span data-stu-id="9f10d-117">Label</span></span>                               | <span data-ttu-id="9f10d-118">세부 정보</span><span class="sxs-lookup"><span data-stu-id="9f10d-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="9f10d-119">**파일**</span><span class="sxs-lookup"><span data-stu-id="9f10d-119">**File**</span></span> | <ul><li><span data-ttu-id="9f10d-120">파일 열기, 저장 및 닫기</span><span class="sxs-lookup"><span data-stu-id="9f10d-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="9f10d-121">OneDrive 계정의 로그인/로그아웃</span><span class="sxs-lookup"><span data-stu-id="9f10d-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="9f10d-122">공유 링크(보기 + 편집)</span><span class="sxs-lookup"><span data-stu-id="9f10d-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="9f10d-123">파일 정보 보기</span><span class="sxs-lookup"><span data-stu-id="9f10d-123">View File Information</span></span></li><li><span data-ttu-id="9f10d-124">기존 모델에 새 템플릿 적용</span><span class="sxs-lookup"><span data-stu-id="9f10d-124">Apply New Template to Existing Models</span></span></li></ul> |
| <span data-ttu-id="9f10d-125">**편집**</span><span class="sxs-lookup"><span data-stu-id="9f10d-125">**Edit**</span></span> | <span data-ttu-id="9f10d-126">작업 실행 취소/다시 실행, 복사, 붙여넣기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="9f10d-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="9f10d-127">**보기**</span><span class="sxs-lookup"><span data-stu-id="9f10d-127">**View**</span></span> | <ul><li><span data-ttu-id="9f10d-128">**분석** 및 **디자인** 보기 간 전환</span><span class="sxs-lookup"><span data-stu-id="9f10d-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="9f10d-129">닫힌 창 열기(예 스텐실, 요소 속성 및 메시지)</span><span class="sxs-lookup"><span data-stu-id="9f10d-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="9f10d-130">기본 설정으로 레이아웃 다시 설정</span><span class="sxs-lookup"><span data-stu-id="9f10d-130">Reset layout to default settings</span></span></li></ul> |
| <span data-ttu-id="9f10d-131">**다이어그램**</span><span class="sxs-lookup"><span data-stu-id="9f10d-131">**Diagram**</span></span> | <span data-ttu-id="9f10d-132">다이어그램 추가/삭제 및 다이어그램의 "탭"을 통해 이동</span><span class="sxs-lookup"><span data-stu-id="9f10d-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="9f10d-133">**보고서**</span><span class="sxs-lookup"><span data-stu-id="9f10d-133">**Reports**</span></span> | <span data-ttu-id="9f10d-134">다른 사용자와 공유하는 HTML 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="9f10d-134">Create HTML reports to share with others</span></span> |
| <span data-ttu-id="9f10d-135">**도움말**</span><span class="sxs-lookup"><span data-stu-id="9f10d-135">**Help**</span></span> | <span data-ttu-id="9f10d-136">도구를 사용하도록 돕는 가이드</span><span class="sxs-lookup"><span data-stu-id="9f10d-136">Guides to help you use the tool</span></span> |

<span data-ttu-id="9f10d-137">아이콘은 최상위 메뉴에 대한 바로 가기입니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-137">The icons are shortcuts for the top-level menus:</span></span>

| <span data-ttu-id="9f10d-138">아이콘</span><span class="sxs-lookup"><span data-stu-id="9f10d-138">Icon</span></span>                               | <span data-ttu-id="9f10d-139">세부 정보</span><span class="sxs-lookup"><span data-stu-id="9f10d-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="9f10d-140">**열기**</span><span class="sxs-lookup"><span data-stu-id="9f10d-140">**Open**</span></span> | <span data-ttu-id="9f10d-141">새 파일 열기</span><span class="sxs-lookup"><span data-stu-id="9f10d-141">Opens a new file</span></span> |
| <span data-ttu-id="9f10d-142">**저장**</span><span class="sxs-lookup"><span data-stu-id="9f10d-142">**Save**</span></span> | <span data-ttu-id="9f10d-143">현재 파일 저장</span><span class="sxs-lookup"><span data-stu-id="9f10d-143">Saves current file</span></span> |
| <span data-ttu-id="9f10d-144">**디자인**</span><span class="sxs-lookup"><span data-stu-id="9f10d-144">**Design**</span></span> | <span data-ttu-id="9f10d-145">모델을 만들 수 있는 디자인 보기로 이동</span><span class="sxs-lookup"><span data-stu-id="9f10d-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="9f10d-146">**분석**</span><span class="sxs-lookup"><span data-stu-id="9f10d-146">**Analyze**</span></span> | <span data-ttu-id="9f10d-147">생성된 위협 및 해당 속성 표시</span><span class="sxs-lookup"><span data-stu-id="9f10d-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="9f10d-148">**다이어그램 추가**</span><span class="sxs-lookup"><span data-stu-id="9f10d-148">**Add Diagram**</span></span> | <span data-ttu-id="9f10d-149">새 다이어그램 추가(Excel의 새 탭과 유사함)</span><span class="sxs-lookup"><span data-stu-id="9f10d-149">Adds new diagram (similar to new tabs in Excel)</span></span> |
| <span data-ttu-id="9f10d-150">**다이어그램 삭제**</span><span class="sxs-lookup"><span data-stu-id="9f10d-150">**Delete Diagram**</span></span> | <span data-ttu-id="9f10d-151">현재 다이어그램 삭제</span><span class="sxs-lookup"><span data-stu-id="9f10d-151">Deletes current diagram</span></span> |
| <span data-ttu-id="9f10d-152">**복사/잘라내기/붙여넣기**</span><span class="sxs-lookup"><span data-stu-id="9f10d-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="9f10d-153">요소 복사/잘라내기/붙여넣기</span><span class="sxs-lookup"><span data-stu-id="9f10d-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="9f10d-154">**실행 취소/다시 실행**</span><span class="sxs-lookup"><span data-stu-id="9f10d-154">**Undo/Redo**</span></span> | <span data-ttu-id="9f10d-155">작업 실행 취소/다시 실행</span><span class="sxs-lookup"><span data-stu-id="9f10d-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="9f10d-156">**확대/축소**</span><span class="sxs-lookup"><span data-stu-id="9f10d-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="9f10d-157">더 나은 보기를 위해 다이어그램 확대 및 축소</span><span class="sxs-lookup"><span data-stu-id="9f10d-157">Zooms in and out of the diagram for a better view</span></span> |
| <span data-ttu-id="9f10d-158">**사용자 의견**</span><span class="sxs-lookup"><span data-stu-id="9f10d-158">**Feedback**</span></span> | <span data-ttu-id="9f10d-159">MSDN 포럼 열기</span><span class="sxs-lookup"><span data-stu-id="9f10d-159">Opens the MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="9f10d-160">캔버스</span><span class="sxs-lookup"><span data-stu-id="9f10d-160">Canvas</span></span>

<span data-ttu-id="9f10d-161">요소를 끌어서 놓는 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-161">The space where you drag and drop elements into.</span></span> <span data-ttu-id="9f10d-162">끌어서 놓기는 모델을 작성하는 신속하고 가장 효율적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-162">Drag and drop is the quickest and most efficient way to build models.</span></span> <span data-ttu-id="9f10d-163">또한 마우스를 오른쪽 단추로 클릭하고 메뉴를 선택할 수도 있습니다. 이는 아래와 같이 사용 중인 요소의 일반 버전을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-163">You may also right click and select from the menu, which adds generic versions of the elements you’re using, as shown below.</span></span>

#### <a name="dropping-the-stencil-on-the-canvas"></a><span data-ttu-id="9f10d-164">캔버스에서 스텐실 삭제</span><span class="sxs-lookup"><span data-stu-id="9f10d-164">Dropping the stencil on the canvas</span></span>

![캔버스 삭제](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-the-stencil"></a><span data-ttu-id="9f10d-166">스텐실 클릭</span><span class="sxs-lookup"><span data-stu-id="9f10d-166">Clicking on the stencil</span></span>

![요소 속성](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="9f10d-168">스텐실</span><span class="sxs-lookup"><span data-stu-id="9f10d-168">Stencils</span></span>

<span data-ttu-id="9f10d-169">여기에서 선택한 템플릿에 따라 사용 가능한 모든 스텐실을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-169">Where you can find all stencils available to use based on the template selected.</span></span> <span data-ttu-id="9f10d-170">올바른 요소를 찾을 수 없는 경우 다른 템플릿을 사용하거나 필요에 맞게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-170">If you can’t find the right elements, try using another template, or modify one to fit your needs.</span></span> <span data-ttu-id="9f10d-171">일반적으로 아래와 같은 범주의 조합을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-171">Generally, you should be able to find a combination of categories like the ones below:</span></span>

| <span data-ttu-id="9f10d-172">스텐실 이름</span><span class="sxs-lookup"><span data-stu-id="9f10d-172">Stencil Name</span></span>                               | <span data-ttu-id="9f10d-173">세부 정보</span><span class="sxs-lookup"><span data-stu-id="9f10d-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="9f10d-174">**프로세스**</span><span class="sxs-lookup"><span data-stu-id="9f10d-174">**Process**</span></span> | <span data-ttu-id="9f10d-175">응용 프로그램, 브라우저 플러그 인, 스레드, 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9f10d-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="9f10d-176">**외부 인자**</span><span class="sxs-lookup"><span data-stu-id="9f10d-176">**External Interactor**</span></span> | <span data-ttu-id="9f10d-177">인증 공급자, 브라우저, 사용자, 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="9f10d-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="9f10d-178">**데이터 저장소**</span><span class="sxs-lookup"><span data-stu-id="9f10d-178">**Data Store**</span></span> | <span data-ttu-id="9f10d-179">캐시, 저장소, 구성 파일, 데이터베이스, 레지스트리</span><span class="sxs-lookup"><span data-stu-id="9f10d-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="9f10d-180">**데이터 흐름**</span><span class="sxs-lookup"><span data-stu-id="9f10d-180">**Data Flow**</span></span> | <span data-ttu-id="9f10d-181">이진, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, 명명된 파이프, RPC/DCOM, SMB, UDP</span><span class="sxs-lookup"><span data-stu-id="9f10d-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="9f10d-182">**신뢰 선/경계**</span><span class="sxs-lookup"><span data-stu-id="9f10d-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="9f10d-183">회사 네트워크, 인터넷, 컴퓨터, 샌드박스, 사용자/커널 모드</span><span class="sxs-lookup"><span data-stu-id="9f10d-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="9f10d-184">참고 사항/메시지</span><span class="sxs-lookup"><span data-stu-id="9f10d-184">Notes/Messages</span></span>

| <span data-ttu-id="9f10d-185">구성 요소</span><span class="sxs-lookup"><span data-stu-id="9f10d-185">Component</span></span>                               | <span data-ttu-id="9f10d-186">세부 정보</span><span class="sxs-lookup"><span data-stu-id="9f10d-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="9f10d-187">**메시지**</span><span class="sxs-lookup"><span data-stu-id="9f10d-187">**Messages**</span></span> | <span data-ttu-id="9f10d-188">요소 간 데이터 흐름 없음과 같은 오류가 발생할 때마다 사용자에게 경고하는 내부 도구 논리</span><span class="sxs-lookup"><span data-stu-id="9f10d-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="9f10d-189">**참고 사항**</span><span class="sxs-lookup"><span data-stu-id="9f10d-189">**Notes**</span></span> | <span data-ttu-id="9f10d-190">설계 및 검토 프로세스 전체에서 엔지니어링 팀에 의해 파일에 추가된 수동 참고 사항</span><span class="sxs-lookup"><span data-stu-id="9f10d-190">Manual notes added to the file by engineering teams throughout the design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="9f10d-191">요소 속성</span><span class="sxs-lookup"><span data-stu-id="9f10d-191">Element properties</span></span>

<span data-ttu-id="9f10d-192">이는 선택한 요소에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-192">These vary by the elements selected.</span></span> <span data-ttu-id="9f10d-193">신뢰 경계 외에도 다른 모든 요소에 일반적인 3가지 선택 항목이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="9f10d-194">요소 속성</span><span class="sxs-lookup"><span data-stu-id="9f10d-194">Element Property</span></span>                               | <span data-ttu-id="9f10d-195">세부 정보</span><span class="sxs-lookup"><span data-stu-id="9f10d-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="9f10d-196">**Name**</span><span class="sxs-lookup"><span data-stu-id="9f10d-196">**Name**</span></span> | <span data-ttu-id="9f10d-197">프로세스, 저장소, 인자 및 흐름을 쉽게 인식하도록 이름을 지정하는 데 유용</span><span class="sxs-lookup"><span data-stu-id="9f10d-197">Useful for naming your processes, stores, interactors and flows to be easily recognized</span></span> |
| <span data-ttu-id="9f10d-198">**범위 외**</span><span class="sxs-lookup"><span data-stu-id="9f10d-198">**Out of Scope**</span></span> | <span data-ttu-id="9f10d-199">선택한 경우 요소는 위협 생성 매트릭스에서 제거됩니다(권장하지 않음).</span><span class="sxs-lookup"><span data-stu-id="9f10d-199">If selected, the element is taken out of the threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="9f10d-200">**범위 외에 대한 이유**</span><span class="sxs-lookup"><span data-stu-id="9f10d-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="9f10d-201">범위 외가 선택된 이유를 사용자에게 알리는 이유 필드</span><span class="sxs-lookup"><span data-stu-id="9f10d-201">Justification field to let users know why out of scope was selected</span></span> |

<span data-ttu-id="9f10d-202">속성은 각 요소 범주 아래에서 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-202">Properties are changed under each element category.</span></span> <span data-ttu-id="9f10d-203">각 요소를 클릭하여 사용할 수 있는 옵션을 검사하거나 템플릿을 열어 자세한 내용을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-203">Click on each element to inspect the available options, or open the template to learn more.</span></span> <span data-ttu-id="9f10d-204">기능에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-204">Let’s get into the features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="9f10d-205">시작 화면</span><span class="sxs-lookup"><span data-stu-id="9f10d-205">Welcome screen</span></span>

<span data-ttu-id="9f10d-206">시작 화면은 앱을 열 때 보는 첫 번째 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-206">The welcome screen is the first thing you see when you open the app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="9f10d-207">모델 열기</span><span class="sxs-lookup"><span data-stu-id="9f10d-207">Open A model</span></span>

<span data-ttu-id="9f10d-208">"모델 열기" 단추를 가리키면 두 개의 숨겨진 옵션 "이 컴퓨터에서 열기" 및 "OneDrive에서 열기"가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="9f10d-209">첫 번째는 파일 열기 화면을 여는 반면 두 번째는 OneDrive에 대한 로그인 프로세스를 안내하여 성공적인 인증 후 파일 및 폴더를 선택할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-209">The first opens the File Open screen, while the second takes you through the sign in process for OneDrive, allowing you to pick folders and files after a successful authentication.</span></span>

![모델 열기](./media/azure-security-threat-modeling-tool/openmodel.png)

![컴퓨터 또는 OneDrive에서 열기](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="9f10d-212">피드백, 제안 및 문제</span><span class="sxs-lookup"><span data-stu-id="9f10d-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="9f10d-213">이 옵션을 선택하면 SDL 도구에 대한 MSDN 포럼으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-213">Selecting this option will take you to the MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="9f10d-214">해결 방법 및 새로운 아이디어를 포함한 도구에 대한 다른 사용자의 의견을 확인하는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-214">It’s a great way to check out what other people are saying about the tool, including workarounds and new ideas.</span></span>

![사용자 의견](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="9f10d-216">디자인 보기</span><span class="sxs-lookup"><span data-stu-id="9f10d-216">Design view</span></span>

<span data-ttu-id="9f10d-217">새 모델을 열거나 만들 때마다 디자인 보기로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-217">Whenever you open or create a new model, you’ll be taken to the design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="9f10d-218">요소 추가</span><span class="sxs-lookup"><span data-stu-id="9f10d-218">Adding elements</span></span>

<span data-ttu-id="9f10d-219">2가지 방법으로 그리드에서 요소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-219">There are 2 ways to add elements on the grid:</span></span>

- <span data-ttu-id="9f10d-220">**끌어서 놓기** – 원하는 요소를 그리드로 끌어온 다음 요소 속성을 사용하여 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-220">**Drag and Drop** – drag the desired element to the grid, then use the element properties to provide additional information.</span></span>
- <span data-ttu-id="9f10d-221">**마우스 오른쪽 단추로 클릭** – 마우스 오른쪽 단추로 그리드에서 아무 곳이나 클릭하고 드롭다운 메뉴에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-221">**Right Click** – right click anywhere on the grid and select from the dropdown menu.</span></span> <span data-ttu-id="9f10d-222">해당 요소에 대한 일반 표현이 화면에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-222">A generic representation of that element will appear on the screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="9f10d-223">요소 연결</span><span class="sxs-lookup"><span data-stu-id="9f10d-223">Connecting elements</span></span>

<span data-ttu-id="9f10d-224">2가지 방법으로 도구에서 요소를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-224">There are 2 ways to connect elements in the tool:</span></span>

- <span data-ttu-id="9f10d-225">**끌어서 놓기** – 원하는 데이터 흐름을 그리드로 끌어오고 양쪽 끝을 적절한 요소에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-225">**Drag and Drop** – drag the desired dataflow to the grid, and connect both ends to the appropriate elements.</span></span>
- <span data-ttu-id="9f10d-226">**클릭 + Shift** – 첫 번째 요소(데이터 전송)를 클릭하고, Shift 키를 누른 다음 두 번째 요소(데이터 수신)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-226">**Click + Shift** – click on the first element (sending data), press and hold the Shift key, then select the second element (receiving data).</span></span> <span data-ttu-id="9f10d-227">마우스 오른쪽 단추로 클릭하고 "연결"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="9f10d-228">양방향 데이터 흐름을 사용하는 경우 순서는 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-228">If you’re using a bi-directional dataflow, the order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="9f10d-229">properties</span><span class="sxs-lookup"><span data-stu-id="9f10d-229">Properties</span></span>

<span data-ttu-id="9f10d-230">다이어그램에 있는 스텐실에서 수정할 수 있는 모든 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-230">Shows all the properties that can be modified on the stencils placed in the diagram.</span></span> <span data-ttu-id="9f10d-231">속성을 보려면 스텐실을 클릭합니다. 정보가 그에 따라 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-231">To see the properties, just click on the stencil and the information will be populated accordingly.</span></span> <span data-ttu-id="9f10d-232">아래 예제에서는 "데이터베이스" 스텐실이 다이어그램으로 끌어진 이전 및 이후를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-232">The example below shows before and after a "Database" stencil is dragged onto the diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="9f10d-233">이전</span><span class="sxs-lookup"><span data-stu-id="9f10d-233">Before</span></span>

![이전](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="9f10d-235">이후</span><span class="sxs-lookup"><span data-stu-id="9f10d-235">After</span></span>

![이후](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="9f10d-237">메시지</span><span class="sxs-lookup"><span data-stu-id="9f10d-237">Messages</span></span>

<span data-ttu-id="9f10d-238">위협 모델을 만들고 데이터 흐름을 요소에 연결하는 것을 잊은 경우 메시지 창에서 해당 작업을 알립니다. 이를 무시하거나 지침을 따라 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-238">If you create a threat model and forget to connect data flows to elements, the message window notifies you to act. You can choose to ignore it or follow the instructions to fix the issue.</span></span> 

![메시지](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="9f10d-240">참고 사항</span><span class="sxs-lookup"><span data-stu-id="9f10d-240">Notes</span></span>

<span data-ttu-id="9f10d-241">메시지에서 참고 사항으로 탭을 전환하면 모든 아이디어를 캡처하도록 다이어그램에 메모를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-241">Switching tabs from Messages to Notes allows you to add notes to your diagram to capture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="9f10d-242">분석 보기</span><span class="sxs-lookup"><span data-stu-id="9f10d-242">Analysis view</span></span>

<span data-ttu-id="9f10d-243">다이어그램 작성을 완료하면 상단 메뉴 선택 항목으로 이동하고 페인트 팔레트 옆에 있는 돋보기를 선택하여 분석 보기로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-243">Once you're done building your diagram, switch over to analysis view by going to the top menu selections and choosing the magnifying glass next to the paint palette.</span></span>

![분석 보기](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="9f10d-245">생성된 위협 선택</span><span class="sxs-lookup"><span data-stu-id="9f10d-245">Generated threat selection</span></span>

<span data-ttu-id="9f10d-246">위협을 클릭하면 세 가지 고유한 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-246">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="9f10d-247">기능</span><span class="sxs-lookup"><span data-stu-id="9f10d-247">Feature</span></span>                               | <span data-ttu-id="9f10d-248">정보</span><span class="sxs-lookup"><span data-stu-id="9f10d-248">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="9f10d-249">**읽기 표시기**</span><span class="sxs-lookup"><span data-stu-id="9f10d-249">**Read Indicator**</span></span> | <p><span data-ttu-id="9f10d-250">위협은 이제 읽은 상태로 표시됩니다. 이를 통해 이미 지나간 항목의 추적을 쉽게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-250">Threat is now marked as read, which can easily help you keep track of the items you already went through</span></span></p><p>![읽기/읽지 않음 표시기](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="9f10d-252">**상호 작용 포커스**</span><span class="sxs-lookup"><span data-stu-id="9f10d-252">**Interaction Focus**</span></span> | <p><span data-ttu-id="9f10d-253">해당 위협에 속한 다이어그램의 상호 작용이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-253">Interaction in the diagram belonging to that threat is highlighted</span></span></p><p>![상호 작용 포커스](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="9f10d-255">**위협 속성**</span><span class="sxs-lookup"><span data-stu-id="9f10d-255">**Threat Properties**</span></span> | <p><span data-ttu-id="9f10d-256">위협에 대한 추가 정보가 위협 속성 창에 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-256">Additional information about the threat is populated in the threat properties window</span></span></p><p>![위협 속성](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="9f10d-258">우선 순위 변경</span><span class="sxs-lookup"><span data-stu-id="9f10d-258">Priority change</span></span>

<span data-ttu-id="9f10d-259">생성된 각 위협의 우선 순위 수준을 변경하면 높음, 중간 및 낮음 우선 순위 위협을 식별하기 쉽도록 해당 색도 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-259">Changing the priority level of each generated threat also changes their colors to make it easy to identify high, medium and low priority threats.</span></span>

![우선 순위 변경](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="9f10d-261">위협 속성 편집 가능한 필드</span><span class="sxs-lookup"><span data-stu-id="9f10d-261">Threat properties editable fields</span></span>

<span data-ttu-id="9f10d-262">위의 그림에서와 같이 사용자는 도구에서 생성되는 정보를 변경할 수 있으며 이유와 같은 특정 필드에 정보를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-262">As seen in the image above, users can change the information generated by the tool an also add information to certain fields, such as justification.</span></span> <span data-ttu-id="9f10d-263">이러한 필드는 템플릿에서 생성되므로 각 위협에 대한 자세한 정보가 필요한 경우 수정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-263">These fields are generated by the template, so if you need more information for each threat, you're encouraged to make modifications.</span></span>

![위협 속성](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="9f10d-265">보고서</span><span class="sxs-lookup"><span data-stu-id="9f10d-265">Reports</span></span>

<span data-ttu-id="9f10d-266">우선 순위 변경 및 생성된 각 위협의 상태 업데이트가 완료되면 파일을 저장하고/또는 "보고서", "전체 보고서 만들기"로 이동하여 보고서를 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-266">Once you're done changing priorities and updating the status of each generated threat, you can save the file and/or print out a report by going to "Report" and then "Create Full Report."</span></span> <span data-ttu-id="9f10d-267">보고서의 이름을 지정하라는 메시지가 나타나며 이름을 지정하면 아래 이미지와 비슷한 것이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-267">You'll be asked to name the report, and once you do, you should see something similar to the image below:</span></span>

![보고서](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="9f10d-269">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f10d-269">Next steps</span></span>

<span data-ttu-id="9f10d-270">커뮤니티에 템플릿을 제공하려면 **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** 페이지로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="9f10d-270">To contribute a template for the community, please go to our **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="9f10d-271">도구를 **[다운로드](https://aka.ms/tmtpreview)**하여 지금 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9f10d-271">**[Download](https://aka.ms/tmtpreview)** the tool to get started today.</span></span>
