---
title: "응용 프로그램 프록시 응용 프로그램을 로드하는 데 시간이 너무 오래 걸림 | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시의 로드 성능 문제 해결 페이지"
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
ms.openlocfilehash: ce462c90746e6af0dc201686557121665b82b93d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="an-application-proxy-application-takes-too-long-to-load"></a><span data-ttu-id="3ce71-103">응용 프로그램 프록시 응용 프로그램을 로드하는 데 시간이 너무 오래 걸림</span><span class="sxs-lookup"><span data-stu-id="3ce71-103">An Application Proxy application takes too long to load</span></span>

<span data-ttu-id="3ce71-104">이 문서를 통해 Azure AD 응용 프로그램 프록시 응용 프로그램을 로드하는 데 시간이 오래 걸리고 이 문제를 해결하기 위해 수행할 수 있는 작업을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ce71-104">This article help you to understand why an Azure AD Application Proxy application may take a long time to load, and what you can do to resolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="3ce71-105">개요</span><span class="sxs-lookup"><span data-stu-id="3ce71-105">Overview</span></span>
<span data-ttu-id="3ce71-106">응용 프로그램이 작동 중이지만 대기 시간이 길게 표시되는 경우 네트워크 토폴로지에서 속도를 개선하기 위해 고려할 수 있는 몇 가지 사소한 변경 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ce71-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider to improve the speed.</span></span> <span data-ttu-id="3ce71-107">여러 토폴로지에 대한 평가는 [네트워크 고려 사항 문서](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ce71-107">For an evaluation of different topologies, see the [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="3ce71-108">해당 고려 사항이 도움이 되지 않는 경우 안타깝게도 현재 성능을 조정하기 위한 추가 권장 사항이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ce71-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="3ce71-109">응용 프로그램 프록시 서비스가 사용자에게 인접한 추가 데이터 센터로 확장되어 향상된 대기 시간을 직접 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ce71-109">As the Application Proxy service expands to more data centers that may be closer to you, you may start to see improved latency directly.</span></span> <span data-ttu-id="3ce71-110">Azure 데이터 센터의 전체 목록을 보려면 [대기 시간 테스트 페이지](http://www.azurespeed.com/Azure/Latency)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ce71-110">To see the full list of Azure data centers, you can see the [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="3ce71-111">응용 프로그램 프록시 서비스를 포함하는 데이터 센터는 [커넥터 포트 테스트 도구](https://aadap-portcheck.connectorporttest.msappproxy.net/)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ce71-111">The data centers with the Application Proxy service can be found with the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="3ce71-112">응용 프로그램 프록시 데이터 센터 위치에 대한 피드백</span><span class="sxs-lookup"><span data-stu-id="3ce71-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="3ce71-113">응용 프로그램 프록시를 아직 포함하지 않지만 사용자의 대기 시간을 개선할 수 있는 Azure 데이터 센터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ce71-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead to a great latency improvement for you.</span></span> <span data-ttu-id="3ce71-114">데이터 센터가 <aadapfeedback@microsoft.com>에 위치하므로 확장한 대로 계획하는 데 피드백을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ce71-114">The data center location at <aadapfeedback@microsoft.com> so we can use your feedback to plan as we expand.</span></span>

<span data-ttu-id="3ce71-115">현재 긴 대기 시간을 표시하는 테넌트의 대기 시간을 개선할 수 있는 몇 가지 추가 기능으로 작업하고 있으므로 사용할 수 있는 문서를 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ce71-115">We are working on some additional capabilities that help improve the latency for tenants that currently see long latencies, and be sure to share documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ce71-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3ce71-116">Next steps</span></span>
[<span data-ttu-id="3ce71-117">기존 온-프레미스 프록시 서버 작업</span><span class="sxs-lookup"><span data-stu-id="3ce71-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
