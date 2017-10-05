---
title: "응용 프로그램 프록시 응용 프로그램에 대해 작동하는 커넥터 그룹 없음 | Microsoft 문서"
description: "Azure AD 응용 프로그램 프록시를 사용하는 응용 프로그램에 대한 커넥터 그룹에 작동 중인 커넥터가 없을 때 발생할 수 있는 주소 문제"
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
ms.openlocfilehash: 4945958deedc8a1d9989ff901192c03a5363b4dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="09149-103">응용 프로그램 프록시 응용 프로그램에 대해 작동하는 커넥터 그룹 없음</span><span class="sxs-lookup"><span data-stu-id="09149-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="09149-104">이 문서는 Azure Active Directory와 통합된 응용 프로그램 프록시 응용 프로그램에 대해 감지된 커넥터가 없을 때 자주 발생하는 문제를 해결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="09149-104">This article help you to resolve the common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="09149-105">단계 개요</span><span class="sxs-lookup"><span data-stu-id="09149-105">Overview of steps</span></span>
<span data-ttu-id="09149-106">응용 프로그램의 커넥터 그룹에 작동 중인 커넥터가 없는 경우 몇 가지 방법을 사용하여 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09149-106">If there is no working Connector in a Connector Group for your application, there are a few ways to resolve the problem:</span></span>

-   <span data-ttu-id="09149-107">그룹에 커넥터가 없는 경우 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09149-107">If you have no connectors in the group, you can:</span></span>

    -   <span data-ttu-id="09149-108">오른쪽 온-프레미스 서버에 새로운 커넥터를 다운로드하여 이 그룹에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="09149-108">Download a new Connector on the right on-prem server, and assign it to this group</span></span>

    -   <span data-ttu-id="09149-109">활성 커넥터를 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="09149-109">Move an active Connector into the group</span></span>

-   <span data-ttu-id="09149-110">그룹에 활성 커넥터가 없는 경우 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09149-110">If you have no active connectors in the group, you can:</span></span>

    -   <span data-ttu-id="09149-111">커넥터가 비활성 상태인 이유를 식별하고 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="09149-111">Identify the reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="09149-112">활성 커넥터를 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="09149-112">Move an active Connector into the group</span></span>

<span data-ttu-id="09149-113">문제를 파악하려면 응용 프로그램에서 "응용 프로그램 프록시" 메뉴를 열고 커넥터 그룹 경고 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="09149-113">To know which of these is the issue, open the “Application Proxy” menu in your Application, and look at the Connector Group warning message.</span></span> <span data-ttu-id="09149-114">여기에는 그룹에 적어도 하나의 커넥터가 필요하거나(그룹에 없음) 활성 커넥터가 없다(비활성 커넥터는 있을 수 있음)고 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09149-114">It specify either that the group needs at least one Connector (you have none in the group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Azure Portal에서 커넥터 그룹 선택](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="09149-116">이러한 각 옵션에 대한 자세한 내용은 아래 해당 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09149-116">For details on each of these options, see the corresponding section below.</span></span> <span data-ttu-id="09149-117">각 섹션에서는 커넥터 관리 페이지에서 시작한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="09149-117">Each of these assumes that you are starting from the Connector management page.</span></span> <span data-ttu-id="09149-118">위의 오류 메시지가 표시되면 경고 메시지를 클릭하여 이 페이지로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09149-118">If you are looking at the error message above, you can go to this page by clicking on the warning message.</span></span> <span data-ttu-id="09149-119">그렇지 않으면 **Azure Active Directory**로 이동하여 **엔터프라이즈 응용 프로그램**을 클릭한 다음 **응용 프로그램 프록시**를 클릭하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09149-119">Otherwise this can be found by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Azure Portal에서 커넥터 그룹 관리](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="09149-121">새 커넥터 다운로드</span><span class="sxs-lookup"><span data-stu-id="09149-121">Download a new Connector</span></span>

<span data-ttu-id="09149-122">새 커넥터를 다운로드하려면 페이지 맨 위에 있는 "커넥터 다운로드" 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="09149-122">To download a new Connector, use the “Download Connector” button at the top of the page.</span></span>

<span data-ttu-id="09149-123">커넥터는 백 엔드 응용 프로그램에 직접 연결된 컴퓨터에 설치해야 하며 일반적으로 응용 프로그램과 동일한 서버에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09149-123">note the Connector needs to be installed on a machine with direct line of sight to the backend application, and is typically placed on the same server as the application.</span></span> <span data-ttu-id="09149-124">다운로드 후 커넥터가 이 메뉴에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="09149-124">After downloading, the Connector should appear in this menu.</span></span> <span data-ttu-id="09149-125">커넥터를 클릭하고 "커넥터 그룹" 드롭다운을 사용하여 해당 그룹에 속하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="09149-125">click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group.</span></span> <span data-ttu-id="09149-126">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="09149-126">Save the change.</span></span>

   ![Azure Portal에서 커넥터 다운로드](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="09149-128">활성 커넥터 이동</span><span class="sxs-lookup"><span data-stu-id="09149-128">Move an Active Connector</span></span>

<span data-ttu-id="09149-129">그룹에 속해야 하며 대상 백 엔드 응용 프로그램에 직접 연결된 활성 커넥터가 있는 경우 지정된 그룹으로 커넥터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09149-129">If you have an active Connector that should belong to the group and has line of sight to the target backend application, you can move the Connector into the assigned group.</span></span> <span data-ttu-id="09149-130">이렇게 하려면 커넥터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09149-130">To do so, click the Connector.</span></span> <span data-ttu-id="09149-131">"커넥터 그룹" 필드에서 드롭다운을 사용하여 올바른 그룹을 선택하고 저장을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09149-131">In the “Connector Group” field, use the drop-down to select the correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="09149-132">비활성 커넥터 해결</span><span class="sxs-lookup"><span data-stu-id="09149-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="09149-133">그룹의 커넥터만 비활성 상태인 경우 필요한 모든 포트가 차단되지 않은 컴퓨터에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09149-133">If the only Connectors in the group are inactive, they are likely on a machine that does not have all the necessary ports unblocked.</span></span>

<span data-ttu-id="09149-134">이 문제를 조사하는 방법에 대한 자세한 내용은 포트 문제 해결 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09149-134">see the ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09149-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="09149-135">Next steps</span></span>
[<span data-ttu-id="09149-136">Azure AD 응용 프로그램 프록시 커넥터 이해</span><span class="sxs-lookup"><span data-stu-id="09149-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


