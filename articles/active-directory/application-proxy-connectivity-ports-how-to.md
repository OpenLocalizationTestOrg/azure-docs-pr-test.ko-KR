---
title: "응용 프로그램 프록시 응용 프로그램에 필요한 aaaHow tooopen hello 방화벽 포트 | Microsoft Docs"
description: "Hello Azure AD 응용 프로그램 프록시 toowork 어떤 포트 tooopen 올바르게 확인"
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
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="cabe7-103">어떻게 tooopen hello 응용 프로그램 프록시 응용 프로그램에 필요한 방화벽 포트</span><span class="sxs-lookup"><span data-stu-id="cabe7-103">How tooopen hello firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="cabe7-104">hello의 hello 필수 구성 요소 섹션을 참조 하는 hello 필요한 포트 및 각 포트의 hello 함수의 전체 목록은 toosee [응용 프로그램 프록시 설명서](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable)합니다.</span><span class="sxs-lookup"><span data-stu-id="cabe7-104">toosee a full list of hello required ports and hello function of each port, see hello prerequisites section of hello [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="cabe7-105">응용 프로그램 프록시는 아웃바운드 포트만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cabe7-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="cabe7-106">열어 hello 여 모든 hello 필요한 포트가 열려 있는지를 확인할 수도 있습니다 [커넥터 포트 테스트 도구](https://aadap-portcheck.connectorporttest.msappproxy.net/) 온-프레미스 네트워크에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cabe7-106">You can also check whether you have all hello required ports open by opening hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="cabe7-107">녹색 확인 표시가 많을수록 복원력이 더 뛰어난 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cabe7-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="cabe7-108">앱 프록시 영역</span><span class="sxs-lookup"><span data-stu-id="cabe7-108">App Proxy regions</span></span>

<span data-ttu-id="cabe7-109">제작 하는 방식으로 이러한 영역의 알아야 toolet 요구에 toobe 녹색 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cabe7-109">We are working on a way toolet you know which of these regions needs toobe green for you.</span></span> <span data-ttu-id="cabe7-110">지금은 모두 녹색인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cabe7-110">For now, make sure they all are.</span></span> <span data-ttu-id="cabe7-111">미국 중부 지역은 현재 위치한 지역에 상관없이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cabe7-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="cabe7-112">toomake 있는지 hello 도구 제공 올바른 결과 hello 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cabe7-112">toomake sure hello tool gives you hello right results, be sure to:</span></span>

-   <span data-ttu-id="cabe7-113">Hello 커넥터를 설치한 hello 서버에서 브라우저에서 hello 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cabe7-113">Open hello tool on a browser from hello server where you have installed hello Connector.</span></span>

-   <span data-ttu-id="cabe7-114">커넥터는 모든 프록시 또는 방화벽 적용 가능한 tooyour toothis 페이지 적용 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cabe7-114">Ensure that any proxies or firewalls applicable tooyour Connector are also applied toothis page.</span></span> <span data-ttu-id="cabe7-115">이렇게 Internet Explorer에서 너무 이동 하 여**설정**  - &gt; **인터넷 옵션**  - &gt; **연결**  - &gt; **Lan 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="cabe7-115">This can be done in Internet Explorer by going too**Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="cabe7-116">이 페이지에서는 hello 필드 "a 프록시 서버에 대 한 사용자 LAN 사용"을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="cabe7-116">On this page, you see hello field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="cabe7-117">이 상자를 선택 하 고 hello 프록시 주소 hello "Address" 필드에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cabe7-117">Select this box, and put hello proxy address into hello “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cabe7-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cabe7-118">Next steps</span></span>
[<span data-ttu-id="cabe7-119">Azure AD 응용 프로그램 프록시 커넥터 이해</span><span class="sxs-lookup"><span data-stu-id="cabe7-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
