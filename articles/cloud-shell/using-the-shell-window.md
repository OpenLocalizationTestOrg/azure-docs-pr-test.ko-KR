---
title: "aaaUsing hello Azure 클라우드 셸 (미리 보기) 창 | Microsoft Docs"
description: "연습 hello Azure 클라우드 셸 창입니다."
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
ms.openlocfilehash: 571db3c8e177799a9e05f38a7cf8d2a4d5f8c8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cloud-shell-window"></a><span data-ttu-id="a2bd6-103">Hello Azure 클라우드 셸 창을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a2bd6-103">Using hello Azure Cloud Shell window</span></span>

<span data-ttu-id="a2bd6-104">이 문서에서는 toouse 클라우드 셸 창을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-104">This document explains how toouse hello Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="a2bd6-105">동시 세션</span><span class="sxs-lookup"><span data-stu-id="a2bd6-105">Concurrent sessions</span></span>
<span data-ttu-id="a2bd6-106">클라우드 셸 각 세션 tooexist을 별도 Bash 프로세스를 허용 하 여 브라우저 탭에서 여러 동시 세션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session tooexist as a separate Bash process.</span></span>
<span data-ttu-id="a2bd6-107">세션을 종료 해야 tooexit 각 세션 창에서 각 프로세스 독립적으로 실행에서 실행 되지만 대로 hello 같은 경우 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-107">If exiting a session, be sure tooexit from each session window as each process runs independently although they run on hello same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="a2bd6-108">Cloud Shell 다시 시작</span><span class="sxs-lookup"><span data-stu-id="a2bd6-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="a2bd6-109">Cloud Shell을 다시 시작하면 컴퓨터 상태가 다시 설정되고 파일 공유에서 유지하지 않는 파일은 모두 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="a2bd6-110">Hello 도구 모음 tooreceive 새 클라우드 셸 환경에서 hello를 다시 시작 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-110">Click hello restart icon on hello toolbar tooreceive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="a2bd6-111">Cloud Shell 창 최소화 및 최대화</span><span class="sxs-lookup"><span data-stu-id="a2bd6-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="a2bd6-112">Hello 클릭 hello에 아이콘을 최소화 hello 창 toohide의 오른쪽 위에 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-112">Click hello minimize icon on hello top right of hello window toohide it.</span></span> <span data-ttu-id="a2bd6-113">Toounhide 다시 hello 클라우드 셸 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-113">Click hello Cloud Shell icon again toounhide.</span></span>
* <span data-ttu-id="a2bd6-114">Hello 클릭 아이콘 tooset 창 toomax 높이 최대화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-114">Click hello maximize icon tooset window toomax height.</span></span> <span data-ttu-id="a2bd6-115">toorestore 창 tooprevious 크기 복원을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-115">toorestore window tooprevious size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="a2bd6-116">복사 및 붙여넣기</span><span class="sxs-lookup"><span data-stu-id="a2bd6-116">Copy and paste</span></span>
* <span data-ttu-id="a2bd6-117">Windows: `Ctrl-insert` toocopy 및 `Shift-insert` toopaste 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-117">Windows: `Ctrl-insert` toocopy and `Shift-insert` toopaste.</span></span> <span data-ttu-id="a2bd6-118">마우스 오른쪽 단추로 드롭다운을 클릭하여 복사/붙여넣기를 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="a2bd6-119">FireFox/IE에서 클립보드 사용 권한을 제대로 지원하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="a2bd6-120">Mac OS: `Cmd-c` toocopy 및 `Cmd-v` toopaste 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-120">Mac OS: `Cmd-c` toocopy and `Cmd-v` toopaste.</span></span> <span data-ttu-id="a2bd6-121">마우스 오른쪽 단추로 드롭다운을 클릭하여 복사/붙여넣기를 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="a2bd6-122">Cloud Shell 창 크기 조정</span><span class="sxs-lookup"><span data-stu-id="a2bd6-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="a2bd6-123">클릭 하 고 위로 또는 아래로 tooresize hello 클라우드 셸 창을 hello hello 도구 모음의 위쪽 가장자리를 끌어 옵니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-123">Click and drag hello top edge of hello toolbar up or down tooresize hello Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="a2bd6-124">텍스트 표시 스크롤</span><span class="sxs-lookup"><span data-stu-id="a2bd6-124">Scrolling text display</span></span>
* <span data-ttu-id="a2bd6-125">마우스 또는 터치 toomove 터미널 텍스트와 함께 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-125">Scroll with your mouse or touchpad toomove terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="a2bd6-126">종료 명령</span><span class="sxs-lookup"><span data-stu-id="a2bd6-126">Exit command</span></span>
<span data-ttu-id="a2bd6-127">실행 `exit` hello 활성 세션을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-127">Running `exit` terminates hello active session.</span></span> <span data-ttu-id="a2bd6-128">이 동작은 기본적으로 상호 작용 없이 20분 후에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bd6-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2bd6-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a2bd6-129">Next steps</span></span>
[<span data-ttu-id="a2bd6-130">Cloud Shell 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="a2bd6-130">Cloud Shell Quickstart</span></span>](quickstart.md)
