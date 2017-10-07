---
title: "Azure RemoteApp 클라이언트에 대 한 aaaBest 사례 | Microsoft Docs"
description: "Hello RemoteApp 클라이언트를 사용 하기 위한 모범 사례에 알아보기"
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
ms.openlocfilehash: aa0ccb2f51d381462b78d60e966b87a67d8c247e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-remoteapp-clients"></a><span data-ttu-id="8d6a7-103">Azure RemoteApp 클라이언트 모범 사례</span><span class="sxs-lookup"><span data-stu-id="8d6a7-103">Best practices for Azure RemoteApp clients</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8d6a7-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8d6a7-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8d6a7-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d6a7-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8d6a7-106">다음 정보는 hello Azure RemoteApp 클라이언트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d6a7-106">hello following information can help you use Azure RemoteApp clients:</span></span>

* <span data-ttu-id="8d6a7-107">항상 최신 클라이언트 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d6a7-107">Always use hello latest client.</span></span> <span data-ttu-id="8d6a7-108">이렇게 하면 해당 hello를 사용 중인 클라이언트 버전에는 hello 최신 버그 수정, 개선 사항 및 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="8d6a7-108">This ensures that hello client version you are running has hello latest bug fixes, improvements and features.</span></span> <span data-ttu-id="8d6a7-109">해야 tooautomatically toosign hello 적절 한 저장소에 클라이언트 hello에 대 한 업데이트를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d6a7-109">You might need toosign up tooautomatically receive updates for hello client in hello appropriate Store.</span></span>
* <span data-ttu-id="8d6a7-110">일정 기간 동안 비활성 상태이면 RemoteApp에서 자동으로 로그오프됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d6a7-110">RemoteApp will automatically log you off if you are inactive for a certain period of time.</span></span> <span data-ttu-id="8d6a7-111">순서 tooprevent 데이터 손실, hello 서비스 사용을 마칠 때 응용 프로그램을 닫는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8d6a7-111">In order tooprevent data loss, we recommend closing your applications when you finish using hello service.</span></span>

