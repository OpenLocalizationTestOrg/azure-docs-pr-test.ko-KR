---
title: "응용 프로그램 프록시 응용 프로그램에 대 한 aaaNo 작업 커넥터 그룹을 찾을 | Microsoft Docs"
description: "커넥터 응용 프로그램에 hello Azure AD 응용 프로그램 프록시 커넥터 그룹에 없는 작업 없을 때 발생 하는 문제 해결"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="8f3c4-103">응용 프로그램 프록시 응용 프로그램에 대해 작동하는 커넥터 그룹 없음</span><span class="sxs-lookup"><span data-stu-id="8f3c4-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="8f3c4-104">Azure Active Directory와 통합 tooresolve hello 일반적인 문제 1 응용 프로그램 프록시 응용 프로그램에 대 한 커넥터 없을 때 직면 하는이 문서 도움말입니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-104">This article help you tooresolve hello common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="8f3c4-105">단계 개요</span><span class="sxs-lookup"><span data-stu-id="8f3c4-105">Overview of steps</span></span>
<span data-ttu-id="8f3c4-106">커넥터 응용 프로그램에 대 한 커넥터 그룹에 없는 작업 인 경우 몇 가지 방법으로 tooresolve hello 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-106">If there is no working Connector in a Connector Group for your application, there are a few ways tooresolve hello problem:</span></span>

-   <span data-ttu-id="8f3c4-107">Hello 그룹에서 커넥터가 없는 경우에 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-107">If you have no connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="8f3c4-108">Hello 오른쪽 온-프레미스 서버에 새 커넥터를 다운로드 하 고 toothis 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="8f3c4-108">Download a new Connector on hello right on-prem server, and assign it toothis group</span></span>

    -   <span data-ttu-id="8f3c4-109">현재 커넥터 hello 그룹으로 이동</span><span class="sxs-lookup"><span data-stu-id="8f3c4-109">Move an active Connector into hello group</span></span>

-   <span data-ttu-id="8f3c4-110">Hello 그룹에 활성 커넥터가 없는 경우에 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-110">If you have no active connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="8f3c4-111">커넥터 아니기 때문에 hello 이유를 식별 및 해결</span><span class="sxs-lookup"><span data-stu-id="8f3c4-111">Identify hello reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="8f3c4-112">현재 커넥터 hello 그룹으로 이동</span><span class="sxs-lookup"><span data-stu-id="8f3c4-112">Move an active Connector into hello group</span></span>

<span data-ttu-id="8f3c4-113">tooknow hello 문제가 중 어느 응용 프로그램에서 hello "Application Proxy" 메뉴를 열고 hello 커넥터 그룹 경고 메시지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-113">tooknow which of these is hello issue, open hello “Application Proxy” menu in your Application, and look at hello Connector Group warning message.</span></span> <span data-ttu-id="8f3c4-114">Hello 그룹 중 하나 (있어야 hello 그룹에서 없음) 커넥터가 하나 이상 필요 하거나 (비활성 커넥터 있을 가능성이 높습니다) 되지만 활성 커넥터가 없는 있는지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-114">It specify either that hello group needs at least one Connector (you have none in hello group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Azure Portal에서 커넥터 그룹 선택](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="8f3c4-116">이러한 각 옵션에 대 한 세부 정보를 아래 hello 해당 섹션을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-116">For details on each of these options, see hello corresponding section below.</span></span> <span data-ttu-id="8f3c4-117">이러한 각 hello 커넥터 관리 페이지에서 시작 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-117">Each of these assumes that you are starting from hello Connector management page.</span></span> <span data-ttu-id="8f3c4-118">위의 hello 오류 메시지에서 찾으려는 경우 hello 경고 메시지를 클릭 하 여 toothis 페이지를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-118">If you are looking at hello error message above, you can go toothis page by clicking on hello warning message.</span></span> <span data-ttu-id="8f3c4-119">그렇지 않으면 너무 이동 하 여 찾을 수 있습니다**Azure Active Directory**에, **엔터프라이즈 응용 프로그램**, 다음 **응용 프로그램 프록시입니다.**</span><span class="sxs-lookup"><span data-stu-id="8f3c4-119">Otherwise this can be found by going too**Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Azure Portal에서 커넥터 그룹 관리](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="8f3c4-121">새 커넥터 다운로드</span><span class="sxs-lookup"><span data-stu-id="8f3c4-121">Download a new Connector</span></span>

<span data-ttu-id="8f3c4-122">새 커넥터 toodownload hello hello 페이지 위쪽에 hello "커넥터 다운로드" 단추를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-122">toodownload a new Connector, use hello “Download Connector” button at hello top of hello page.</span></span>

<span data-ttu-id="8f3c4-123">hello 응용 프로그램으로 동일한 서버를 hello 하는 참고 hello 커넥터 요구 toobe 직접적인 toohello 백 엔드 응용 프로그램을 사용 하는 컴퓨터에 설치 하 고에 일반적으로 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-123">note hello Connector needs toobe installed on a machine with direct line of sight toohello backend application, and is typically placed on hello same server as hello application.</span></span> <span data-ttu-id="8f3c4-124">다운로드 한 후 커넥터 hello이이 메뉴에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-124">After downloading, hello Connector should appear in this menu.</span></span> <span data-ttu-id="8f3c4-125">hello 커넥터를 클릭 하 고 hello "커넥터 그룹" 드롭 다운 toomake toohello 권한 그룹에 속해 있는지를 사용 하 여 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-125">click hello Connector, and use hello “Connector Group” drop-down toomake sure it belongs toohello right group.</span></span> <span data-ttu-id="8f3c4-126">Hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-126">Save hello change.</span></span>

   ![Hello Azure 포털에서에서 hello 커넥터를 다운로드 합니다.](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="8f3c4-128">활성 커넥터 이동</span><span class="sxs-lookup"><span data-stu-id="8f3c4-128">Move an Active Connector</span></span>

<span data-ttu-id="8f3c4-129">Toohello 그룹에 속해야 하며 시야 toohello 대상 백 엔드 응용 프로그램을 포함 하는 활성 커넥터를 설정한 경우 커넥터 hello hello 할당 된 그룹으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-129">If you have an active Connector that should belong toohello group and has line of sight toohello target backend application, you can move hello Connector into hello assigned group.</span></span> <span data-ttu-id="8f3c4-130">따라서 toodo hello 커넥터를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-130">toodo so, click hello Connector.</span></span> <span data-ttu-id="8f3c4-131">Hello "커넥터 그룹" 필드에 hello 드롭 다운 tooselect hello 올바른 그룹을 사용 하 고 저장을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-131">In hello “Connector Group” field, use hello drop-down tooselect hello correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="8f3c4-132">비활성 커넥터 해결</span><span class="sxs-lookup"><span data-stu-id="8f3c4-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="8f3c4-133">있더라도 hello hello 그룹의 커넥터 비활성 상태인 경우에 하지 않는 컴퓨터에 있을 가능성이 있는 모든 hello 필요한 포트의 차단을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-133">If hello only Connectors in hello group are inactive, they are likely on a machine that does not have all hello necessary ports unblocked.</span></span>

<span data-ttu-id="8f3c4-134">hello 포트를 참조 하십시오.이 문제를 조사 하는 중에 대 한 내용은 문서 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3c4-134">see hello ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f3c4-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f3c4-135">Next steps</span></span>
[<span data-ttu-id="8f3c4-136">Azure AD 응용 프로그램 프록시 커넥터 이해</span><span class="sxs-lookup"><span data-stu-id="8f3c4-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


