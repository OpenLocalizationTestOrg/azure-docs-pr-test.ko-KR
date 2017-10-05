---
title: "Azure RemoteApp 클라이언트 모범 사례 | Microsoft Docs"
description: "RemoteApp 클라이언트를 사용하기 위한 모범 사례를 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 8c2e6068-8733-42f6-a05c-a2088634991b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 416cd37a907010176fe331ddb908a35b6fd6b253
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="best-practices-for-azure-remoteapp-clients"></a><span data-ttu-id="22b33-103">Azure RemoteApp 클라이언트 모범 사례</span><span class="sxs-lookup"><span data-stu-id="22b33-103">Best practices for Azure RemoteApp clients</span></span>
> [!IMPORTANT]
> <span data-ttu-id="22b33-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="22b33-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="22b33-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="22b33-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="22b33-106">다음 정보는 Azure RemoteApp 클라이언트를 사용하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22b33-106">The following information can help you use Azure RemoteApp clients:</span></span>

* <span data-ttu-id="22b33-107">항상 최신 클라이언트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22b33-107">Always use the latest client.</span></span> <span data-ttu-id="22b33-108">이렇게 하면 실행 중인 클라이언트 버전에 최신 버그 수정, 향상된 기능 및 특성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="22b33-108">This ensures that the client version you are running has the latest bug fixes, improvements and features.</span></span> <span data-ttu-id="22b33-109">해당 스토어에서 클라이언트 업데이트를 자동으로 받기 위해 등록해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22b33-109">You might need to sign up to automatically receive updates for the client in the appropriate Store.</span></span>
* <span data-ttu-id="22b33-110">일정 기간 동안 비활성 상태이면 RemoteApp에서 자동으로 로그오프됩니다.</span><span class="sxs-lookup"><span data-stu-id="22b33-110">RemoteApp will automatically log you off if you are inactive for a certain period of time.</span></span> <span data-ttu-id="22b33-111">데이터 손실을 방지하려면 서비스 사용을 마쳤을 때 응용 프로그램을 닫는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="22b33-111">In order to prevent data loss, we recommend closing your applications when you finish using the service.</span></span>

