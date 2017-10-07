---
title: "aaaMicrosoft 위협 모델링 도구-Azure | Microsoft Docs"
description: "Hello 위협 모델링 도구에서에서 사용할 수 있는 모든 hello 기능에 알아보기"
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
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="82c36-103">위협 모델링 도구 기능 개요</span><span class="sxs-lookup"><span data-stu-id="82c36-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="82c36-104">우리는 위협 모델링 요구 사항에 대해 toouse hello 위협 모델링 도구를 선택한 주셔서 감사 드립니다!</span><span class="sxs-lookup"><span data-stu-id="82c36-104">We are glad you chose toouse hello Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="82c36-105">그렇게 하지 않은 경우 방문  **[hello 위협 모델링 도구 시작](./azure-security-threat-modeling-tool-getting-started.md)**  toolearn hello 기본 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-105">If you haven’t done so, visit **[Getting Started with hello Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** toolearn hello basics.</span></span>

> <span data-ttu-id="82c36-106">이 도구는 자주 업데이트 되므로이 확인 하세요 우리의 최신 기능 및 향상 된 종종 toosee를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-106">Our tool is updated often, so check this guide often toosee our latest features and improvements.</span></span>

<span data-ttu-id="82c36-107">Hello "새 모델 만들기" 단추 클릭 하면 빈 시작 페이지, 아래와 유사한 toohello 이미지 열립니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-107">Clicking on hello "Create a New Model" button opens a blank start page, similar toohello image below:</span></span>

![빈 시작 페이지](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="82c36-109">Hello에 팀에서 만든 hello 위협 모델을 사용 하 여  **[시작](./azure-security-threat-modeling-tool-getting-started.md)**  예제에서는 현재 hello 도구에서 사용할 수 있는 모든 hello 기능을 사용해 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-109">Using hello threat model created by our team in hello **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all hello features available in hello tool today.</span></span>

![기본 위협 모델](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="82c36-111">탐색</span><span class="sxs-lookup"><span data-stu-id="82c36-111">Navigation</span></span>

<span data-ttu-id="82c36-112">Hello 기본 제공 기능을 알아보기 전에 검토해 hello 도구에 있는 hello 주 구성 요소</span><span class="sxs-lookup"><span data-stu-id="82c36-112">Before diving into hello built-in features, let’s go over hello main components found in hello tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="82c36-113">메뉴 항목</span><span class="sxs-lookup"><span data-stu-id="82c36-113">Menu items</span></span>

<span data-ttu-id="82c36-114">hello 경험 유사한 tooother Microsoft 제품 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-114">hello experience should be similar tooother Microsoft products.</span></span> <span data-ttu-id="82c36-115">Hello 최상위 메뉴 항목 간을 이동 하 여 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-115">Let’s begin by going through hello top-level menu items:</span></span>

![메뉴 항목](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="82c36-117">레이블</span><span class="sxs-lookup"><span data-stu-id="82c36-117">Label</span></span>                               | <span data-ttu-id="82c36-118">세부 정보</span><span class="sxs-lookup"><span data-stu-id="82c36-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="82c36-119">**파일**</span><span class="sxs-lookup"><span data-stu-id="82c36-119">**File**</span></span> | <ul><li><span data-ttu-id="82c36-120">파일 열기, 저장 및 닫기</span><span class="sxs-lookup"><span data-stu-id="82c36-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="82c36-121">OneDrive 계정의 로그인/로그아웃</span><span class="sxs-lookup"><span data-stu-id="82c36-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="82c36-122">공유 링크(보기 + 편집)</span><span class="sxs-lookup"><span data-stu-id="82c36-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="82c36-123">파일 정보 보기</span><span class="sxs-lookup"><span data-stu-id="82c36-123">View File Information</span></span></li><li><span data-ttu-id="82c36-124">새 템플릿 tooExisting 모델을 적용</span><span class="sxs-lookup"><span data-stu-id="82c36-124">Apply New Template tooExisting Models</span></span></li></ul> |
| <span data-ttu-id="82c36-125">**편집**</span><span class="sxs-lookup"><span data-stu-id="82c36-125">**Edit**</span></span> | <span data-ttu-id="82c36-126">작업 실행 취소/다시 실행, 복사, 붙여넣기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="82c36-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="82c36-127">**보기**</span><span class="sxs-lookup"><span data-stu-id="82c36-127">**View**</span></span> | <ul><li><span data-ttu-id="82c36-128">**분석** 및 **디자인** 보기 간 전환</span><span class="sxs-lookup"><span data-stu-id="82c36-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="82c36-129">닫힌 창 열기(예 스텐실, 요소 속성 및 메시지)</span><span class="sxs-lookup"><span data-stu-id="82c36-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="82c36-130">레이아웃 toodefault 설정을 다시 설정</span><span class="sxs-lookup"><span data-stu-id="82c36-130">Reset layout toodefault settings</span></span></li></ul> |
| <span data-ttu-id="82c36-131">**다이어그램**</span><span class="sxs-lookup"><span data-stu-id="82c36-131">**Diagram**</span></span> | <span data-ttu-id="82c36-132">다이어그램 추가/삭제 및 다이어그램의 "탭"을 통해 이동</span><span class="sxs-lookup"><span data-stu-id="82c36-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="82c36-133">**보고서**</span><span class="sxs-lookup"><span data-stu-id="82c36-133">**Reports**</span></span> | <span data-ttu-id="82c36-134">다른 사용자를 사용 하 여 HTML 보고서 tooshare 만들기</span><span class="sxs-lookup"><span data-stu-id="82c36-134">Create HTML reports tooshare with others</span></span> |
| <span data-ttu-id="82c36-135">**도움말**</span><span class="sxs-lookup"><span data-stu-id="82c36-135">**Help**</span></span> | <span data-ttu-id="82c36-136">안내선 toohelp hello 도구를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="82c36-136">Guides toohelp you use hello tool</span></span> |

<span data-ttu-id="82c36-137">hello 아이콘은 hello 최상위 메뉴에 대 한 바로 가기 키:</span><span class="sxs-lookup"><span data-stu-id="82c36-137">hello icons are shortcuts for hello top-level menus:</span></span>

| <span data-ttu-id="82c36-138">아이콘</span><span class="sxs-lookup"><span data-stu-id="82c36-138">Icon</span></span>                               | <span data-ttu-id="82c36-139">세부 정보</span><span class="sxs-lookup"><span data-stu-id="82c36-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="82c36-140">**열기**</span><span class="sxs-lookup"><span data-stu-id="82c36-140">**Open**</span></span> | <span data-ttu-id="82c36-141">새 파일 열기</span><span class="sxs-lookup"><span data-stu-id="82c36-141">Opens a new file</span></span> |
| <span data-ttu-id="82c36-142">**저장**</span><span class="sxs-lookup"><span data-stu-id="82c36-142">**Save**</span></span> | <span data-ttu-id="82c36-143">현재 파일 저장</span><span class="sxs-lookup"><span data-stu-id="82c36-143">Saves current file</span></span> |
| <span data-ttu-id="82c36-144">**디자인**</span><span class="sxs-lookup"><span data-stu-id="82c36-144">**Design**</span></span> | <span data-ttu-id="82c36-145">모델을 만들 수 있는 디자인 보기로 이동</span><span class="sxs-lookup"><span data-stu-id="82c36-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="82c36-146">**분석**</span><span class="sxs-lookup"><span data-stu-id="82c36-146">**Analyze**</span></span> | <span data-ttu-id="82c36-147">생성된 위협 및 해당 속성 표시</span><span class="sxs-lookup"><span data-stu-id="82c36-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="82c36-148">**다이어그램 추가**</span><span class="sxs-lookup"><span data-stu-id="82c36-148">**Add Diagram**</span></span> | <span data-ttu-id="82c36-149">새 다이어그램 (Excel에서 유사한 toonew 탭)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-149">Adds new diagram (similar toonew tabs in Excel)</span></span> |
| <span data-ttu-id="82c36-150">**다이어그램 삭제**</span><span class="sxs-lookup"><span data-stu-id="82c36-150">**Delete Diagram**</span></span> | <span data-ttu-id="82c36-151">현재 다이어그램 삭제</span><span class="sxs-lookup"><span data-stu-id="82c36-151">Deletes current diagram</span></span> |
| <span data-ttu-id="82c36-152">**복사/잘라내기/붙여넣기**</span><span class="sxs-lookup"><span data-stu-id="82c36-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="82c36-153">요소 복사/잘라내기/붙여넣기</span><span class="sxs-lookup"><span data-stu-id="82c36-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="82c36-154">**실행 취소/다시 실행**</span><span class="sxs-lookup"><span data-stu-id="82c36-154">**Undo/Redo**</span></span> | <span data-ttu-id="82c36-155">작업 실행 취소/다시 실행</span><span class="sxs-lookup"><span data-stu-id="82c36-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="82c36-156">**확대/축소**</span><span class="sxs-lookup"><span data-stu-id="82c36-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="82c36-157">아웃 보다 잘 표시에 대 한 hello 다이어그램을 확대합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-157">Zooms in and out of hello diagram for a better view</span></span> |
| <span data-ttu-id="82c36-158">**사용자 의견**</span><span class="sxs-lookup"><span data-stu-id="82c36-158">**Feedback**</span></span> | <span data-ttu-id="82c36-159">MSDN 포럼 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-159">Opens hello MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="82c36-160">캔버스</span><span class="sxs-lookup"><span data-stu-id="82c36-160">Canvas</span></span>

<span data-ttu-id="82c36-161">hello 공간을 끌어서 놓으면 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-161">hello space where you drag and drop elements into.</span></span> <span data-ttu-id="82c36-162">끌어서 놓기는 가장 빠른 hello와 가장 효율적인 방식으로 toobuild 모델.</span><span class="sxs-lookup"><span data-stu-id="82c36-162">Drag and drop is hello quickest and most efficient way toobuild models.</span></span> <span data-ttu-id="82c36-163">또한 마우스 오른쪽 단추로 클릭 하 고 아래와 같이 hello 요소를 사용 하는 제네릭 버전을 추가 하는 hello 메뉴에서 선택 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-163">You may also right click and select from hello menu, which adds generic versions of hello elements you’re using, as shown below.</span></span>

#### <a name="dropping-hello-stencil-on-hello-canvas"></a><span data-ttu-id="82c36-164">Hello 캔버스에 hello 스텐실을 삭제 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-164">Dropping hello stencil on hello canvas</span></span>

![캔버스 삭제](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a><span data-ttu-id="82c36-166">Hello 스텐실 클릭 하면</span><span class="sxs-lookup"><span data-stu-id="82c36-166">Clicking on hello stencil</span></span>

![요소 속성](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="82c36-168">스텐실</span><span class="sxs-lookup"><span data-stu-id="82c36-168">Stencils</span></span>

<span data-ttu-id="82c36-169">찾을 수 있는 모든 스텐실이 선택한 hello 템플릿을 기반으로 사용할 수 있는 toouse를 열립니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-169">Where you can find all stencils available toouse based on hello template selected.</span></span> <span data-ttu-id="82c36-170">Hello 오른쪽 요소를 찾을 수 없으면 다른 서식 파일을 사용 하 여 시도 하거나 하나의 toofit 요구에 맞게 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-170">If you can’t find hello right elements, try using another template, or modify one toofit your needs.</span></span> <span data-ttu-id="82c36-171">일반적으로 아래 hello 것과 같은 범주의 조합 수 toofind 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-171">Generally, you should be able toofind a combination of categories like hello ones below:</span></span>

| <span data-ttu-id="82c36-172">스텐실 이름</span><span class="sxs-lookup"><span data-stu-id="82c36-172">Stencil Name</span></span>                               | <span data-ttu-id="82c36-173">세부 정보</span><span class="sxs-lookup"><span data-stu-id="82c36-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="82c36-174">**프로세스**</span><span class="sxs-lookup"><span data-stu-id="82c36-174">**Process**</span></span> | <span data-ttu-id="82c36-175">응용 프로그램, 브라우저 플러그 인, 스레드, 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="82c36-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="82c36-176">**외부 인자**</span><span class="sxs-lookup"><span data-stu-id="82c36-176">**External Interactor**</span></span> | <span data-ttu-id="82c36-177">인증 공급자, 브라우저, 사용자, 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="82c36-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="82c36-178">**데이터 저장소**</span><span class="sxs-lookup"><span data-stu-id="82c36-178">**Data Store**</span></span> | <span data-ttu-id="82c36-179">캐시, 저장소, 구성 파일, 데이터베이스, 레지스트리</span><span class="sxs-lookup"><span data-stu-id="82c36-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="82c36-180">**데이터 흐름**</span><span class="sxs-lookup"><span data-stu-id="82c36-180">**Data Flow**</span></span> | <span data-ttu-id="82c36-181">이진, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, 명명된 파이프, RPC/DCOM, SMB, UDP</span><span class="sxs-lookup"><span data-stu-id="82c36-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="82c36-182">**신뢰 선/경계**</span><span class="sxs-lookup"><span data-stu-id="82c36-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="82c36-183">회사 네트워크, 인터넷, 컴퓨터, 샌드박스, 사용자/커널 모드</span><span class="sxs-lookup"><span data-stu-id="82c36-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="82c36-184">참고 사항/메시지</span><span class="sxs-lookup"><span data-stu-id="82c36-184">Notes/Messages</span></span>

| <span data-ttu-id="82c36-185">구성 요소</span><span class="sxs-lookup"><span data-stu-id="82c36-185">Component</span></span>                               | <span data-ttu-id="82c36-186">세부 정보</span><span class="sxs-lookup"><span data-stu-id="82c36-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="82c36-187">**메시지**</span><span class="sxs-lookup"><span data-stu-id="82c36-187">**Messages**</span></span> | <span data-ttu-id="82c36-188">요소 간 데이터 흐름 없음과 같은 오류가 발생할 때마다 사용자에게 경고하는 내부 도구 논리</span><span class="sxs-lookup"><span data-stu-id="82c36-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="82c36-189">**참고 사항**</span><span class="sxs-lookup"><span data-stu-id="82c36-189">**Notes**</span></span> | <span data-ttu-id="82c36-190">엔지니어링 팀에서 수동 메모 추가 toohello 파일 전반적 디자인 hello 및 검토 프로세스</span><span class="sxs-lookup"><span data-stu-id="82c36-190">Manual notes added toohello file by engineering teams throughout hello design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="82c36-191">요소 속성</span><span class="sxs-lookup"><span data-stu-id="82c36-191">Element properties</span></span>

<span data-ttu-id="82c36-192">이러한 선택한 hello 요소에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-192">These vary by hello elements selected.</span></span> <span data-ttu-id="82c36-193">신뢰 경계 외에도 다른 모든 요소에 일반적인 3가지 선택 항목이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="82c36-194">요소 속성</span><span class="sxs-lookup"><span data-stu-id="82c36-194">Element Property</span></span>                               | <span data-ttu-id="82c36-195">세부 정보</span><span class="sxs-lookup"><span data-stu-id="82c36-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="82c36-196">**Name**</span><span class="sxs-lookup"><span data-stu-id="82c36-196">**Name**</span></span> | <span data-ttu-id="82c36-197">프로세스, 저장소, 인자 및 흐름 toobe 쉽게 인식 이름을 지정 하는 데 유용</span><span class="sxs-lookup"><span data-stu-id="82c36-197">Useful for naming your processes, stores, interactors and flows toobe easily recognized</span></span> |
| <span data-ttu-id="82c36-198">**범위 외**</span><span class="sxs-lookup"><span data-stu-id="82c36-198">**Out of Scope**</span></span> | <span data-ttu-id="82c36-199">Hello 요소 (권장 하지 않음) hello 위협 생성 매트릭스에서 제거 됩니다. 선택한 경우</span><span class="sxs-lookup"><span data-stu-id="82c36-199">If selected, hello element is taken out of hello threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="82c36-200">**범위 외에 대한 이유**</span><span class="sxs-lookup"><span data-stu-id="82c36-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="82c36-201">양쪽 맞춤 필드 toolet 사용자가 알고 이유 때문에 선택 된 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-201">Justification field toolet users know why out of scope was selected</span></span> |

<span data-ttu-id="82c36-202">속성은 각 요소 범주 아래에서 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-202">Properties are changed under each element category.</span></span> <span data-ttu-id="82c36-203">Hello 템플릿 toolearn 더 많은 열 또는 각 요소 tooinspect hello 사용할 수 있는 옵션을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-203">Click on each element tooinspect hello available options, or open hello template toolearn more.</span></span> <span data-ttu-id="82c36-204">Hello 기능으로 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-204">Let’s get into hello features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="82c36-205">시작 화면</span><span class="sxs-lookup"><span data-stu-id="82c36-205">Welcome screen</span></span>

<span data-ttu-id="82c36-206">시작 화면 hello는 hello 앱을 열 때 hello 첫 번째 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-206">hello welcome screen is hello first thing you see when you open hello app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="82c36-207">모델 열기</span><span class="sxs-lookup"><span data-stu-id="82c36-207">Open A model</span></span>

<span data-ttu-id="82c36-208">"모델 열기" 단추를 가리키면 두 개의 숨겨진 옵션 "이 컴퓨터에서 열기" 및 "OneDrive에서 열기"가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="82c36-209">먼저 hello hello 두 번째 과정을 안내해 hello 로그인 프로세스 OneDrive에 대 한 인증을 거친 후 toopick 폴더와 파일 수 하는 동안 hello 파일 열기 화면을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-209">hello first opens hello File Open screen, while hello second takes you through hello sign in process for OneDrive, allowing you toopick folders and files after a successful authentication.</span></span>

![모델 열기](./media/azure-security-threat-modeling-tool/openmodel.png)

![컴퓨터 또는 OneDrive에서 열기](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="82c36-212">피드백, 제안 및 문제</span><span class="sxs-lookup"><span data-stu-id="82c36-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="82c36-213">이 옵션을 선택 하면 이동 됩니다 toohello MSDN 포럼 SDL 도구에 대 한.</span><span class="sxs-lookup"><span data-stu-id="82c36-213">Selecting this option will take you toohello MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="82c36-214">해결 방법 및 새로운 아이디어를 포함 하는 hello 도구에 대 한 다른 사용자는 말 아웃 위한 훌륭한 방법 toocheck 이며</span><span class="sxs-lookup"><span data-stu-id="82c36-214">It’s a great way toocheck out what other people are saying about hello tool, including workarounds and new ideas.</span></span>

![사용자 의견](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="82c36-216">디자인 보기</span><span class="sxs-lookup"><span data-stu-id="82c36-216">Design view</span></span>

<span data-ttu-id="82c36-217">열거나 새 모델을 만들 때마다 toohello 디자인 보기로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-217">Whenever you open or create a new model, you’ll be taken toohello design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="82c36-218">요소 추가</span><span class="sxs-lookup"><span data-stu-id="82c36-218">Adding elements</span></span>

<span data-ttu-id="82c36-219">두 가지 방법이 있습니다 tooadd 요소 hello 그리드에서:</span><span class="sxs-lookup"><span data-stu-id="82c36-219">There are 2 ways tooadd elements on hello grid:</span></span>

- <span data-ttu-id="82c36-220">**끌어서 놓기** – hello 원하는 요소 toohello 그리드를 끌어 온 다음 hello 요소 속성 tooprovide 추가 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-220">**Drag and Drop** – drag hello desired element toohello grid, then use hello element properties tooprovide additional information.</span></span>
- <span data-ttu-id="82c36-221">**마우스 오른쪽 단추로 클릭** – 마우스 오른쪽 단추로 hello 그리드에서 아무 곳 이나 클릭 하 고 hello 드롭다운 메뉴에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-221">**Right Click** – right click anywhere on hello grid and select from hello dropdown menu.</span></span> <span data-ttu-id="82c36-222">해당 요소에 대 한 일반 표현을 hello 화면에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-222">A generic representation of that element will appear on hello screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="82c36-223">요소 연결</span><span class="sxs-lookup"><span data-stu-id="82c36-223">Connecting elements</span></span>

<span data-ttu-id="82c36-224">두 가지 방법이 있습니다 tooconnect 요소 hello 도구에서:</span><span class="sxs-lookup"><span data-stu-id="82c36-224">There are 2 ways tooconnect elements in hello tool:</span></span>

- <span data-ttu-id="82c36-225">**끌어서 놓기** – hello 원하는 데이터 흐름 toohello 눈금 끌어서 두 ends toohello 적절 한 요소를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-225">**Drag and Drop** – drag hello desired dataflow toohello grid, and connect both ends toohello appropriate elements.</span></span>
- <span data-ttu-id="82c36-226">**Shift + 클릭** – hello 첫 번째 요소 (데이터 전송)를 클릭, 키를 누른 hello Shift 키를 그 선택 hello 두 번째 요소 (데이터 수신) 합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-226">**Click + Shift** – click on hello first element (sending data), press and hold hello Shift key, then select hello second element (receiving data).</span></span> <span data-ttu-id="82c36-227">마우스 오른쪽 단추로 클릭하고 "연결"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="82c36-228">양방향 데이터 흐름을 사용 하는 hello 순서가 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-228">If you’re using a bi-directional dataflow, hello order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="82c36-229">properties</span><span class="sxs-lookup"><span data-stu-id="82c36-229">Properties</span></span>

<span data-ttu-id="82c36-230">Hello 다이어그램에 배치 하는 hello 스텐실에 수정할 수 있는 모든 hello 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-230">Shows all hello properties that can be modified on hello stencils placed in hello diagram.</span></span> <span data-ttu-id="82c36-231">hello 스텐실 toosee hello 속성을 클릭 하 고 hello 정보를 그에 따라 정보가 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-231">toosee hello properties, just click on hello stencil and hello information will be populated accordingly.</span></span> <span data-ttu-id="82c36-232">다음 예제에서는 hello 스텐실 hello 다이어그램으로 끌 "Database" 전후 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-232">hello example below shows before and after a "Database" stencil is dragged onto hello diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="82c36-233">이전</span><span class="sxs-lookup"><span data-stu-id="82c36-233">Before</span></span>

![이전](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="82c36-235">이후</span><span class="sxs-lookup"><span data-stu-id="82c36-235">After</span></span>

![이후](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="82c36-237">메시지</span><span class="sxs-lookup"><span data-stu-id="82c36-237">Messages</span></span>

<span data-ttu-id="82c36-238">위협 모델을 만들고 tooconnect 데이터 흐름 tooelements 잊은 경우 hello 메시지 창 tooact을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-238">If you create a threat model and forget tooconnect data flows tooelements, hello message window notifies you tooact.</span></span> <span data-ttu-id="82c36-239">또는 다음 tooignore를 선택할 수 있습니다 hello 지침 toofix hello 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-239">You can choose tooignore it or follow hello instructions toofix hello issue.</span></span> 

![메시지](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="82c36-241">참고 사항</span><span class="sxs-lookup"><span data-stu-id="82c36-241">Notes</span></span>

<span data-ttu-id="82c36-242">메시지 tooNotes에서 탭 간을 전환할 수 있습니다 있습니다 tooadd 노트 tooyour 다이어그램 toocapture 모든 의견을</span><span class="sxs-lookup"><span data-stu-id="82c36-242">Switching tabs from Messages tooNotes allows you tooadd notes tooyour diagram toocapture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="82c36-243">분석 보기</span><span class="sxs-lookup"><span data-stu-id="82c36-243">Analysis view</span></span>

<span data-ttu-id="82c36-244">완료 하 고 나면 toohello 상단 메뉴 선택 항목을 이동 하 고 hello 돋보기 다음 toohello 페인트 색상표를 선택 하 여 tooanalysis 보기 전환 다이어그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-244">Once you're done building your diagram, switch over tooanalysis view by going toohello top menu selections and choosing hello magnifying glass next toohello paint palette.</span></span>

![분석 보기](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="82c36-246">생성된 위협 선택</span><span class="sxs-lookup"><span data-stu-id="82c36-246">Generated threat selection</span></span>

<span data-ttu-id="82c36-247">위협을 클릭하면 세 가지 고유한 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-247">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="82c36-248">기능</span><span class="sxs-lookup"><span data-stu-id="82c36-248">Feature</span></span>                               | <span data-ttu-id="82c36-249">정보</span><span class="sxs-lookup"><span data-stu-id="82c36-249">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="82c36-250">**읽기 표시기**</span><span class="sxs-lookup"><span data-stu-id="82c36-250">**Read Indicator**</span></span> | <p><span data-ttu-id="82c36-251">위협은 hello 항목 이미 진행을 추적할 수를 쉽게 얻을 수 있는 읽은 상태로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-251">Threat is now marked as read, which can easily help you keep track of hello items you already went through</span></span></p><p>![읽기/읽지 않음 표시기](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="82c36-253">**상호 작용 포커스**</span><span class="sxs-lookup"><span data-stu-id="82c36-253">**Interaction Focus**</span></span> | <p><span data-ttu-id="82c36-254">상호 작용 toothat 위협 속하는 hello 다이어그램에 강조 표시</span><span class="sxs-lookup"><span data-stu-id="82c36-254">Interaction in hello diagram belonging toothat threat is highlighted</span></span></p><p>![상호 작용 포커스](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="82c36-256">**위협 속성**</span><span class="sxs-lookup"><span data-stu-id="82c36-256">**Threat Properties**</span></span> | <p><span data-ttu-id="82c36-257">Hello 위협에 대 한 자세한 내용은 hello 위협 속성 창에 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-257">Additional information about hello threat is populated in hello threat properties window</span></span></p><p>![위협 속성](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="82c36-259">우선 순위 변경</span><span class="sxs-lookup"><span data-stu-id="82c36-259">Priority change</span></span>

<span data-ttu-id="82c36-260">생성 된 각 위협의 hello 우선 순위 수준 변경의 색 toomake 설치 경로도 변경 하기 쉬운 tooidentify 높음, 중간 및 낮음 우선 순위 위협입니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-260">Changing hello priority level of each generated threat also changes their colors toomake it easy tooidentify high, medium and low priority threats.</span></span>

![우선 순위 변경](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="82c36-262">위협 속성 편집 가능한 필드</span><span class="sxs-lookup"><span data-stu-id="82c36-262">Threat properties editable fields</span></span>

<span data-ttu-id="82c36-263">위의 hello 이미지와 같이 사용자 hello 도구에 의해 생성 된 hello 정보를 변경할 수 있습니다를 근거 등의 정보 toocertain 필드를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-263">As seen in hello image above, users can change hello information generated by hello tool an also add information toocertain fields, such as justification.</span></span> <span data-ttu-id="82c36-264">이러한 필드는 hello 템플릿에 의해 생성 되는 것이 좋습니다 toomake 수정 하는 각 위협에 대 한 자세한 정보를 필요 하므로.</span><span class="sxs-lookup"><span data-stu-id="82c36-264">These fields are generated by hello template, so if you need more information for each threat, you're encouraged toomake modifications.</span></span>

![위협 속성](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="82c36-266">보고서</span><span class="sxs-lookup"><span data-stu-id="82c36-266">Reports</span></span>

<span data-ttu-id="82c36-267">우선 순위 변경 완료 되 고 각 업데이트 hello 상태 위협 생성 되 면에 hello 파일을 저장 하거나 이동 하 여 너무 "보고서" 다음 "전체 보고서 만들기." 보고서를 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-267">Once you're done changing priorities and updating hello status of each generated threat, you can save hello file and/or print out a report by going too"Report" and then "Create Full Report."</span></span> <span data-ttu-id="82c36-268">만들라는 메시지가 tooname hello 보고서 및 이렇게 할 경우, 다음과 유사한 toohello 이미지 아래 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-268">You'll be asked tooname hello report, and once you do, you should see something similar toohello image below:</span></span>

![보고서](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="82c36-270">다음 단계</span><span class="sxs-lookup"><span data-stu-id="82c36-270">Next steps</span></span>

<span data-ttu-id="82c36-271">toocontribute hello 커뮤니티에 대 한 템플릿을 참조 하십시오. tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  페이지.</span><span class="sxs-lookup"><span data-stu-id="82c36-271">toocontribute a template for hello community, please go tooour **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="82c36-272">**[다운로드](https://aka.ms/tmtpreview)**  hello 도구 tooget 오늘 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="82c36-272">**[Download](https://aka.ms/tmtpreview)** hello tool tooget started today.</span></span>
