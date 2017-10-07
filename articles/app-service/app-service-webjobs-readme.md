---
title: "Azure 앱 서비스의 aaaWebJobs"
description: "WebJobs toorun 배경 toobuild 테스트 하는 방법에 대해 알아봅니다, 그리고 저장소 및 서비스 버스와 같은 서비스와 상호 작용 및 예약 된 작업을 만듭니다."
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="77be6-103">Azure 앱 서비스에서 WebJobs 사용</span><span class="sxs-lookup"><span data-stu-id="77be6-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="77be6-104">이 문서 연결 방법에 대 한 리소스 toodocumentation toouse Azure WebJobs Azure WebJobs SDK hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="77be6-104">This article links toodocumentation resources about how toouse Azure WebJobs and hello Azure WebJobs SDK.</span></span> <span data-ttu-id="77be6-105">Azure WebJobs 쉽게 toorun 스크립트를 제공 하거나으로 프로그램에서 프로세스를 백그라운드 [앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.</span><span class="sxs-lookup"><span data-stu-id="77be6-105">Azure WebJobs provide an easy way toorun scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="77be6-106">cmd, bat, exe(.NET), ps1, sh, php, py, js 및 jar와 같은 실행 파일을 업로드하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77be6-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="77be6-107">이러한 프로그램은 일정에 따라(cron) 또는 지속적으로 WebJob으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="77be6-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="77be6-108">WebJobs SDK hello Azure 저장소 보다 쉽게 toouse가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77be6-108">hello WebJobs SDK makes it easier toouse Azure Storage.</span></span> <span data-ttu-id="77be6-109">hello WebJobs SDK는 한 바인딩 및 서비스 버스 큐 뿐만 아니라 Microsoft Azure 저장소 Blob, 큐 및 테이블을 사용 하는 트리거 시스템에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77be6-109">hello WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="77be6-110">Visual Studio의 통합 도구를 사용하면 WebJob을 원활하게 만들고, 배포하고, 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77be6-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="77be6-111">템플릿에서 WebJob을 만들고, 게시하고 관리(실행/중지/모니터링/디버깅)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77be6-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="77be6-112">hello Azure 포털에서에서 WebJobs 대시보드 hello hello hello 기능 tooinvoke WebJobs 내에서 개별 기능을 포함 하 여 WebJobs 실행에 대 한 모든 권한을 제공 하는 강력한 관리 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="77be6-112">hello WebJobs dashboard in hello Azure portal provides powerful management capabilities that give you full control over hello execution of WebJobs, including hello ability tooinvoke individual functions within WebJobs.</span></span> <span data-ttu-id="77be6-113">hello 대시보드 함수 런타임 및 로깅 출력에도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77be6-113">hello dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

