---
title: "aaaAn 응용 프로그램 프록시 응용 프로그램은 너무 긴 tooload | Microsoft Docs"
description: "Hello Azure AD 응용 프로그램 프록시를 통한 페이지 로드 성능 문제 해결"
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
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a><span data-ttu-id="e0896-103">응용 프로그램 프록시 응용 프로그램은 너무 긴 tooload</span><span class="sxs-lookup"><span data-stu-id="e0896-103">An Application Proxy application takes too long tooload</span></span>

<span data-ttu-id="e0896-104">이 문서가 도움이 Azure AD 응용 프로그램 프록시 응용 프로그램을 오랫동안 tooload 내용과 걸릴 수 있습니다 이유 toounderstand tooresolve이이 문제를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0896-104">This article help you toounderstand why an Azure AD Application Proxy application may take a long time tooload, and what you can do tooresolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="e0896-105">개요</span><span class="sxs-lookup"><span data-stu-id="e0896-105">Overview</span></span>
<span data-ttu-id="e0896-106">응용 프로그램을 작업 하는 중이지만 긴 대기 시간을 표시 하는 경우에 tooimprove hello 속도 고려할 수 있는 네트워크 토폴로지에 대해 몇 가지 사소한 변경 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0896-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider tooimprove hello speed.</span></span> <span data-ttu-id="e0896-107">여러 토폴로지를 평가 대 한 참조 hello [네트워크 고려 사항 문서](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0896-107">For an evaluation of different topologies, see hello [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="e0896-108">해당 고려 사항이 도움이 되지 않는 경우 안타깝게도 현재 성능을 조정하기 위한 추가 권장 사항이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0896-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="e0896-109">응용 프로그램 프록시 서비스 hello toomore 데이터 센터 자세히 tooyou 수 있는 확대 되 면 향상 toosee 대기 시간을 직접 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0896-109">As hello Application Proxy service expands toomore data centers that may be closer tooyou, you may start toosee improved latency directly.</span></span> <span data-ttu-id="e0896-110">toosee hello 전체 목록은 Azure 데이터 센터, hello 나타나면 [테스트 페이지 대기 시간](http://www.azurespeed.com/Azure/Latency)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0896-110">toosee hello full list of Azure data centers, you can see hello [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="e0896-111">hello hello 응용 프로그램 프록시 서비스와 데이터 센터 있습니다 hello로 [커넥터 포트 테스트 도구](https://aadap-portcheck.connectorporttest.msappproxy.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0896-111">hello data centers with hello Application Proxy service can be found with hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="e0896-112">응용 프로그램 프록시 데이터 센터 위치에 대한 피드백</span><span class="sxs-lookup"><span data-stu-id="e0896-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="e0896-113">Azure 데이터 센터에 응용 프로그램 프록시를 아직 포함 되지 않습니다 되지만 드립니다 tooa 훌륭한 대기 시간이 개선 해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0896-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead tooa great latency improvement for you.</span></span> <span data-ttu-id="e0896-114">hello 데이터 센터 위치에서 < aadapfeedback@microsoft.com > 피드백 tooplan 확장으로 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0896-114">hello data center location at <aadapfeedback@microsoft.com> so we can use your feedback tooplan as we expand.</span></span>

<span data-ttu-id="e0896-115">긴 대기 시간, 현재 참조 하는 테 넌 트에 대 한 hello 대기 시간을 개선 하는 데 도움이 되는 몇 가지 추가 기능에서 작업 하는 하 고 문서일 있는지 tooshare 후 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0896-115">We are working on some additional capabilities that help improve hello latency for tenants that currently see long latencies, and be sure tooshare documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0896-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0896-116">Next steps</span></span>
[<span data-ttu-id="e0896-117">기존 온-프레미스 프록시 서버 작업</span><span class="sxs-lookup"><span data-stu-id="e0896-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
