---
title: "웹 응용 프로그램 리소스 tooanother aaaMove 리소스 그룹"
description: "하나의 리소스 그룹 tooanother에서 웹 앱 및 서비스 응용 프로그램을 이동할 수 있는 hello 시나리오를 설명 합니다."
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 931012fee656b7f8a4b2c225c38739a9171d3b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="a4ca0-103">지원되는 이동 구성</span><span class="sxs-lookup"><span data-stu-id="a4ca0-103">Supported Move Configurations</span></span>
<span data-ttu-id="a4ca0-104">Hello를 사용 하 여 Azure 웹 앱 리소스를 이동할 수 [리소스 관리자 리소스 이동 API](../azure-resource-manager/resource-group-move-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ca0-104">You can move Azure Web App resources using hello [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="a4ca0-105">현재 azure 웹 앱 hello 다음 이동 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ca0-105">Azure Web Apps currently supports hello following move scenarios:</span></span>

* <span data-ttu-id="a4ca0-106">Hello 전체 콘텐츠 (웹 앱, 앱 서비스 계획 및 인증서) 리소스 그룹의 이동 tooanother 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a4ca0-106">Move hello entire contents of a resource group (web apps, app service plans, and certificates) tooanother resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="a4ca0-107">hello 대상 리소스 그룹에는이 시나리오에서는 Microsoft.Web 리소스를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ca0-107">hello destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="a4ca0-108">여전히 자신의 현재 앱 서비스 계획 (hello 앱 서비스 계획에에서 유지 되며 hello 이전 리소스 그룹)에 호스트 하는 동안 개별 웹 응용 프로그램 tooa 다른 리소스 그룹을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ca0-108">Move individual web apps tooa different resource group, while still hosting them in their current app service plan (hello app service plan stays in hello old resource group).</span></span>


