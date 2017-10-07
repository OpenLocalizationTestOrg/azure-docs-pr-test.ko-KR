---
title: "응용 프로그램 tooAzure aaaDeploying 앱 서비스"
description: "응용 프로그램 tooApp tooDeploy 서비스 작동 방식에 대해 알아봅니다"
keywords: "앱 서비스, azure 앱 서비스, 배포, 배포"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: 
ms.assetid: de12cd6e-e124-4e48-90bc-c3a3801305da
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 925341e12daf3cb05b25199f5c5218e82f062f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="df76f-104">Azure 앱 서비스 배포 개요</span><span class="sxs-lookup"><span data-stu-id="df76f-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="df76f-105">통합된 기능 집합 toosupport 강력 하 고 유연한 배포 워크플로 만들기 및 azure 앱 서비스는 다양 한 기능의 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="df76f-105">Azure App Service provides a rich and integrated feature set toosupport creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="df76f-106">앱 배포에서 지속적인 통합 또는 로컬 소스 제어 게시, WebDeploy 및 FTP를 포함하는 옵션을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df76f-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="df76f-107">hello는 프로덕션 응용 프로그램 배포 방법은 배포 슬롯 교환 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="df76f-107">hello recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="df76f-108">배포 슬롯은 프로덕션 앱과 연결된 준비 및 통합 환경을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="df76f-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="df76f-109">배포 슬롯 구성 하 고 대상으로 지정 된 유효성 검사에 대 한 웹 트래픽을 수 및 트래픽 요구에 대 한 중단 시간 없이 배포 tooproduction 교환할 수 있습니다 및 준비를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="df76f-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment tooproduction with no down time and automated warm-up.</span></span> <span data-ttu-id="df76f-110">Visual Studio Release Management와 같은 관리 제품 릴리스를 통해 배포 워크플로의 hello 단계를 쉽게 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df76f-110">hello steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="df76f-111">이는 배포의 여러 단위에서 다른 솔루션 리소스(예: 데이터 저장소)와 조정, 되풀이 및 복제에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="df76f-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

