---
title: "응용 프로그램 프록시 응용 프로그램에 필요한 방화벽 포트를 여는 방법 | Microsoft 문서"
description: "Azure AD 응용 프로그램 프록시가 올바르게 작동하기 위해 열어야 하는 포트 찾기"
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
ms.openlocfilehash: 8ecd6d7e666d362194126a4abba7a65f2c7b8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-open-the-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="13095-103">응용 프로그램 프록시 응용 프로그램에 필요한 방화벽 포트를 여는 방법</span><span class="sxs-lookup"><span data-stu-id="13095-103">How to open the firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="13095-104">각 포트의 기능 및 필요한 포트의 전체 목록을 보려면 [응용 프로그램 프록시 설명서](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable)의 필수 조건 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13095-104">To see a full list of the required ports and the function of each port, see the prerequisites section of the [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="13095-105">응용 프로그램 프록시는 아웃바운드 포트만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13095-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="13095-106">또한 온-프레미스 네트워크에서 [커넥터 포트 테스트 도구](https://aadap-portcheck.connectorporttest.msappproxy.net/)를 열어 필요한 모든 포트가 열려 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13095-106">You can also check whether you have all the required ports open by opening the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="13095-107">녹색 확인 표시가 많을수록 복원력이 더 뛰어난 것입니다.</span><span class="sxs-lookup"><span data-stu-id="13095-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="13095-108">앱 프록시 영역</span><span class="sxs-lookup"><span data-stu-id="13095-108">App Proxy regions</span></span>

<span data-ttu-id="13095-109">다음 중 반드시 녹색이어야 하는 영역을 알려주는 방법에 대해 연구하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13095-109">We are working on a way to let you know which of these regions needs to be green for you.</span></span> <span data-ttu-id="13095-110">지금은 모두 녹색인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="13095-110">For now, make sure they all are.</span></span> <span data-ttu-id="13095-111">미국 중부 지역은 현재 위치한 지역에 상관없이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="13095-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="13095-112">이 도구로 올바른 결과를 얻을 수 있는지 확인하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="13095-112">To make sure the tool gives you the right results, be sure to:</span></span>

-   <span data-ttu-id="13095-113">커넥터를 설치한 서버의 브라우저에서 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="13095-113">Open the tool on a browser from the server where you have installed the Connector.</span></span>

-   <span data-ttu-id="13095-114">커넥터에 적용할 수 있는 프록시 또는 방화벽이 이 페이지에도 적용되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="13095-114">Ensure that any proxies or firewalls applicable to your Connector are also applied to this page.</span></span> <span data-ttu-id="13095-115">이 작업은 Internet Explorer의 **설정** -&gt; **인터넷 옵션** -&gt; **연결** -&gt; **LAN 설정**으로 이동하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13095-115">This can be done in Internet Explorer by going to **Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="13095-116">이 페이지에 "사용자 LAN에 프록시 서버 사용" 필드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="13095-116">On this page, you see the field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="13095-117">이 확인란을 선택하고 "주소" 필드에 프록시 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="13095-117">Select this box, and put the proxy address into the “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13095-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="13095-118">Next steps</span></span>
[<span data-ttu-id="13095-119">Azure AD 응용 프로그램 프록시 커넥터 이해</span><span class="sxs-lookup"><span data-stu-id="13095-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
