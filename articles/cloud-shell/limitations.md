---
title: "aaaAzure 클라우드 셸 (미리 보기) 제한 사항 | Microsoft Docs"
description: "Azure Cloud Shell의 제한 사항 개요"
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
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="dfcb1-103">Azure Cloud Shell의 제한 사항</span><span class="sxs-lookup"><span data-stu-id="dfcb1-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="dfcb1-104">Azure 클라우드 셸에 hello 다음과 같은 알려진 제한 사항:</span><span class="sxs-lookup"><span data-stu-id="dfcb1-104">Azure Cloud Shell has hello following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="dfcb1-105">시스템 상태 및 지속성</span><span class="sxs-lookup"><span data-stu-id="dfcb1-105">System state and persistence</span></span>
<span data-ttu-id="dfcb1-106">클라우드 셸 세션을 제공 하는 hello 컴퓨터는 일시적 이며 재활용 되는 세션이 비활성화 된 후 20 분 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-106">hello machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="dfcb1-107">클라우드 셸 탑재 하는 파일 공유 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-107">Cloud Shell requires a file share toobe mounted.</span></span> <span data-ttu-id="dfcb1-108">결과적으로, 구독을 저장소 리소스 tooaccess 클라우드 셸 수 tooset 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-108">As a result, your subscription must be able tooset up storage resources tooaccess Cloud Shell.</span></span> <span data-ttu-id="dfcb1-109">기타 고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-109">Other considerations include:</span></span>
* <span data-ttu-id="dfcb1-110">탑재된 저장소에서 `$Home` 디렉터리 또는 `clouddrive` 디렉터리 내 수정 사항만 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="dfcb1-111">파일 공유는 [할당된 지역](persisting-shell-storage.md#mount-a-new-clouddrive) 내에서만 탑재될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="dfcb1-112">Azure 파일은 로컬 중복 저장소 및 지역 중복 저장소 계정만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="dfcb1-113">사용자 권한</span><span class="sxs-lookup"><span data-stu-id="dfcb1-113">User permissions</span></span>
<span data-ttu-id="dfcb1-114">권한은 sudo 액세스 권한이 없는 일반 사용자로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="dfcb1-115">사용자 `$Home` 디렉터리 외부에서의 설치는 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="dfcb1-116">내에서 특정 명령을 hello 있지만 `clouddrive` 디렉터리와 같은 `git clone`, 적절 한 권한 없는 사용자 `$Home` 디렉터리에 권한이 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-116">Although certain commands within hello `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="dfcb1-117">브라우저 지원</span><span class="sxs-lookup"><span data-stu-id="dfcb1-117">Browser support</span></span>
<span data-ttu-id="dfcb1-118">클라우드 셸 hello Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox 및 Apple Safari의 최신 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-118">Cloud Shell supports hello latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="dfcb1-119">Safari는 개인 모드에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="dfcb1-120">복사 및 붙여넣기</span><span class="sxs-lookup"><span data-stu-id="dfcb1-120">Copy and paste</span></span>
<span data-ttu-id="dfcb1-121">Ctrl + C 및 Ctrl + V 복사/붙여넣기 바로 가기 클라우드 셸에서 Windows 컴퓨터에서 Ctrl + Insert 및 Shift + Insert toocopy를 사용 하 고 각각 붙여 대로 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert toocopy and paste respectively.</span></span>

<span data-ttu-id="dfcb1-122">오른쪽 클릭 복사-붙여넣기 옵션도 사용할 수 있지만 마우스 오른쪽 단추 클릭 함수는 주체 toobrowser 특정 클립보드 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-122">Right-click copy-and-paste options are also available, but right-click function is subject toobrowser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="dfcb1-123">.bashrc 편집</span><span class="sxs-lookup"><span data-stu-id="dfcb1-123">Editing .bashrc</span></span>
<span data-ttu-id="dfcb1-124">.bashrc를 편집할 때는 Cloud Shell에 예기치 않은 오류가 발생할 수 있으니 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="dfcb1-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="dfcb1-125">.bash_history</span></span>
<span data-ttu-id="dfcb1-126">Cloud Shell 세션 중단 또는 동시 세션으로 인해 bash 명령의 기록이 일관되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="dfcb1-127">사용 제한</span><span class="sxs-lookup"><span data-stu-id="dfcb1-127">Usage limits</span></span>
<span data-ttu-id="dfcb1-128">Cloud Shell은 대화형 사용 사례를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="dfcb1-129">따라서 비대화형 세션을 오래 실행하면 경고 없이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="dfcb1-130">네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="dfcb1-130">Network connectivity</span></span>
<span data-ttu-id="dfcb1-131">클라우드 셸에서 대기 시간 주체 toolocal 인터넷에 연결을 클라우드 셸은 모든 명령 전송 tooattempt toocarry 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfcb1-131">Any latency in Cloud Shell is subject toolocal internet connectivity, Cloud Shell continues tooattempt toocarry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfcb1-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dfcb1-132">Next steps</span></span>
[<span data-ttu-id="dfcb1-133">Cloud Shell 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="dfcb1-133">Cloud Shell Quickstart</span></span>](quickstart.md)
