---
title: "Azure Cloud Shell(미리 보기) 제한 사항 | Microsoft Docs"
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
ms.openlocfilehash: e42841b126a9df9240bec3f489589d5ce4a6db80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="aab8b-103">Azure Cloud Shell의 제한 사항</span><span class="sxs-lookup"><span data-stu-id="aab8b-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="aab8b-104">Azure Cloud Shell에는 다음과 같이 알려진 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-104">Azure Cloud Shell has the following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="aab8b-105">시스템 상태 및 지속성</span><span class="sxs-lookup"><span data-stu-id="aab8b-105">System state and persistence</span></span>
<span data-ttu-id="aab8b-106">Cloud Shell 세션을 제공하는 컴퓨터는 일시적이며 세션이 20분 동안 비활성화된 후 재순환됩니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-106">The machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="aab8b-107">Cloud Shell에 파일 공유를 탑재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-107">Cloud Shell requires a file share to be mounted.</span></span> <span data-ttu-id="aab8b-108">따라서 Cloud Shell에 액세스하도록 구독에서 저장소 리소스를 설정할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-108">As a result, your subscription must be able to set up storage resources to access Cloud Shell.</span></span> <span data-ttu-id="aab8b-109">기타 고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-109">Other considerations include:</span></span>
* <span data-ttu-id="aab8b-110">탑재된 저장소에서 `$Home` 디렉터리 또는 `clouddrive` 디렉터리 내 수정 사항만 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="aab8b-111">파일 공유는 [할당된 지역](persisting-shell-storage.md#mount-a-new-clouddrive) 내에서만 탑재될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="aab8b-112">Azure 파일은 로컬 중복 저장소 및 지역 중복 저장소 계정만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="aab8b-113">사용자 권한</span><span class="sxs-lookup"><span data-stu-id="aab8b-113">User permissions</span></span>
<span data-ttu-id="aab8b-114">권한은 sudo 액세스 권한이 없는 일반 사용자로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="aab8b-115">사용자 `$Home` 디렉터리 외부에서의 설치는 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="aab8b-116">`git clone`와 같이 `clouddrive` 디렉터리 내 특정 명령에 적절한 권한이 없어도 사용자의 `$Home` 디렉터리에는 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-116">Although certain commands within the `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="aab8b-117">브라우저 지원</span><span class="sxs-lookup"><span data-stu-id="aab8b-117">Browser support</span></span>
<span data-ttu-id="aab8b-118">Cloud Shell은 Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox 및 Apple Safari의 최신 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-118">Cloud Shell supports the latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="aab8b-119">Safari는 개인 모드에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="aab8b-120">복사 및 붙여넣기</span><span class="sxs-lookup"><span data-stu-id="aab8b-120">Copy and paste</span></span>
<span data-ttu-id="aab8b-121">Ctrl+C 및 Ctrl+V가 Windows 컴퓨터에서 Cloud Shell의 복사/붙여넣기 바로 가기처럼 작동하지 않으므로 복사하여 붙여넣으려면 각각 Ctrl+Insert 및 Shift+Insert를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert to copy and paste respectively.</span></span>

<span data-ttu-id="aab8b-122">복사 및 붙여넣기 옵션을 마우스 오른쪽 단추로 클릭하여 사용할 수도 있지만 마우스 오른쪽 단추 클릭 기능은 브라우저 전용 클립보드 액세스의 적용을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-122">Right-click copy-and-paste options are also available, but right-click function is subject to browser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="aab8b-123">.bashrc 편집</span><span class="sxs-lookup"><span data-stu-id="aab8b-123">Editing .bashrc</span></span>
<span data-ttu-id="aab8b-124">.bashrc를 편집할 때는 Cloud Shell에 예기치 않은 오류가 발생할 수 있으니 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="aab8b-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="aab8b-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="aab8b-125">.bash_history</span></span>
<span data-ttu-id="aab8b-126">Cloud Shell 세션 중단 또는 동시 세션으로 인해 bash 명령의 기록이 일관되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="aab8b-127">사용 제한</span><span class="sxs-lookup"><span data-stu-id="aab8b-127">Usage limits</span></span>
<span data-ttu-id="aab8b-128">Cloud Shell은 대화형 사용 사례를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="aab8b-129">따라서 비대화형 세션을 오래 실행하면 경고 없이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="aab8b-130">네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="aab8b-130">Network connectivity</span></span>
<span data-ttu-id="aab8b-131">Cloud Shell의 대기 시간은 로컬 인터넷 연결의 영향을 받으며, Cloud Shell은 전송된 지침과 함께 작동을 계속 시도하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aab8b-131">Any latency in Cloud Shell is subject to local internet connectivity, Cloud Shell continues to attempt to carry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aab8b-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aab8b-132">Next steps</span></span>
[<span data-ttu-id="aab8b-133">Cloud Shell 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="aab8b-133">Cloud Shell Quickstart</span></span>](quickstart.md)
