---
title: "Azure Cloud Shell(미리 보기) 창 사용 | Microsoft Docs"
description: "Azure Cloud Shell 창을 둘러봅니다."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: juluk
ms.openlocfilehash: a47961dfdaf178a6b793bd68105d9792a9275bb3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-azure-cloud-shell-window"></a><span data-ttu-id="cbbfb-103">Azure Cloud Shell 창 사용</span><span class="sxs-lookup"><span data-stu-id="cbbfb-103">Using the Azure Cloud Shell window</span></span>

<span data-ttu-id="cbbfb-104">이 문서에는 Cloud Shell 창을 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-104">This document explains how to use the Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="cbbfb-105">동시 세션</span><span class="sxs-lookup"><span data-stu-id="cbbfb-105">Concurrent sessions</span></span>
<span data-ttu-id="cbbfb-106">Cloud Shell을 사용하면 각 세션이 별도의 Bash 프로세스로 존재할 수 있게 하여 브라우저 탭에서 여러 개의 세션을 동시에 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session to exist as a separate Bash process.</span></span>
<span data-ttu-id="cbbfb-107">세션을 종료하는 경우 동일한 컴퓨터에서 실행하더라도 각 프로세스가 독립적으로 실행되므로 각 세션 창을 개별적으로 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-107">If exiting a session, be sure to exit from each session window as each process runs independently although they run on the same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="cbbfb-108">Cloud Shell 다시 시작</span><span class="sxs-lookup"><span data-stu-id="cbbfb-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="cbbfb-109">Cloud Shell을 다시 시작하면 컴퓨터 상태가 다시 설정되고 파일 공유에서 유지하지 않는 파일은 모두 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="cbbfb-110">새 Cloud Shell 환경을 수신하려면 도구 모음에서 다시 시작 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-110">Click the restart icon on the toolbar to receive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="cbbfb-111">Cloud Shell 창 최소화 및 최대화</span><span class="sxs-lookup"><span data-stu-id="cbbfb-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="cbbfb-112">창을 숨기려면 창의 오른쪽 위에 있는 최소화 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-112">Click the minimize icon on the top right of the window to hide it.</span></span> <span data-ttu-id="cbbfb-113">숨기기를 취소하려면 Cloud Shell 아이콘을 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-113">Click the Cloud Shell icon again to unhide.</span></span>
* <span data-ttu-id="cbbfb-114">창을 최대 높이로 설정하려면 최대화 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-114">Click the maximize icon to set window to max height.</span></span> <span data-ttu-id="cbbfb-115">창을 이전 크기로 복원하려면 복원 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-115">To restore window to previous size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="cbbfb-116">복사 및 붙여넣기</span><span class="sxs-lookup"><span data-stu-id="cbbfb-116">Copy and paste</span></span>
* <span data-ttu-id="cbbfb-117">Windows: `Ctrl-insert`: 복사, `Shift-insert`: 붙여넣기</span><span class="sxs-lookup"><span data-stu-id="cbbfb-117">Windows: `Ctrl-insert` to copy and `Shift-insert` to paste.</span></span> <span data-ttu-id="cbbfb-118">마우스 오른쪽 단추로 드롭다운을 클릭하여 복사/붙여넣기를 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="cbbfb-119">FireFox/IE에서 클립보드 사용 권한을 제대로 지원하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="cbbfb-120">Mac OS: `Cmd-c`: 복사, `Cmd-v`: 붙여넣기</span><span class="sxs-lookup"><span data-stu-id="cbbfb-120">Mac OS: `Cmd-c` to copy and `Cmd-v` to paste.</span></span> <span data-ttu-id="cbbfb-121">마우스 오른쪽 단추로 드롭다운을 클릭하여 복사/붙여넣기를 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="cbbfb-122">Cloud Shell 창 크기 조정</span><span class="sxs-lookup"><span data-stu-id="cbbfb-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="cbbfb-123">도구 모음의 위쪽 가장자리를 클릭한 채 위/아래로 끌어 Cloud Shell 창의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-123">Click and drag the top edge of the toolbar up or down to resize the Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="cbbfb-124">텍스트 표시 스크롤</span><span class="sxs-lookup"><span data-stu-id="cbbfb-124">Scrolling text display</span></span>
* <span data-ttu-id="cbbfb-125">마우스 또는 터치 패드로 터미널 텍스트까지 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-125">Scroll with your mouse or touchpad to move terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="cbbfb-126">종료 명령</span><span class="sxs-lookup"><span data-stu-id="cbbfb-126">Exit command</span></span>
<span data-ttu-id="cbbfb-127">`exit`를 실행하면 활성 세션이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-127">Running `exit` terminates the active session.</span></span> <span data-ttu-id="cbbfb-128">이 동작은 기본적으로 상호 작용 없이 20분 후에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="cbbfb-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbbfb-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cbbfb-129">Next steps</span></span>
[<span data-ttu-id="cbbfb-130">Cloud Shell 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="cbbfb-130">Cloud Shell Quickstart</span></span>](quickstart.md)
