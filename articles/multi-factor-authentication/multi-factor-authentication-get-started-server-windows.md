---
title: "Windows 인증 및 Azure MFA 서버 | Microsoft Docs"
description: "Windows 인증 및 Azure Multi-Factor Authentication을 배포하는 데 도움이 되는 Azure Multi-Factor Authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 7e6384ea8fea686b5cad1a3bc3007252b9cfcd65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="52641-103">Windows 인증 및 Azure Multi-Factor Authentication 서버</span><span class="sxs-lookup"><span data-stu-id="52641-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="52641-104">Azure Multi-Factor Authentication 서버의 Windows 인증 섹션을 사용하여 응용 프로그램에 대한 Windows 인증을 사용하도록 설정하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52641-104">Use the Windows Authentication section of the Azure Multi-Factor Authentication Server to enable and configure Windows authentication for applications.</span></span> <span data-ttu-id="52641-105">Windows 인증을 설정하기 전에 다음 목록을 유념하세요.</span><span class="sxs-lookup"><span data-stu-id="52641-105">Before you set up Windows Authentication, keep the following list in mind:</span></span>

* <span data-ttu-id="52641-106">설정한 후에는 터미널 서비스에 대한 Azure Multi-Factor Authentication을 다시 부팅하여 적용되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="52641-106">After setup, reboot the Azure Multi-Factor Authentication for Terminal Services to take effect.</span></span>
* <span data-ttu-id="52641-107">'Azure Multi-Factor Authentication 사용자 일치'를 선택하고 사용자 목록에 없는 경우, 다시 부팅하면 컴퓨터에 로그인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="52641-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in the user list, you will not be able to log into the machine after reboot.</span></span>
* <span data-ttu-id="52641-108">신뢰할 수 있는 IP는 응용 프로그램이 클라이언트 IP에 인증을 제공할 수 있는지 여부에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="52641-108">Trusted IPs is dependent on whether the application can provide the client IP with the authentication.</span></span> <span data-ttu-id="52641-109">현재는 터미널 서비스만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="52641-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="52641-110">이 기능은 Windows Server 2012 R2에서 보안 터미널 서비스를 보안하는 데 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="52641-110">This feature is not supported to secure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="to-secure-an-application-with-windows-authentication-use-the-following-procedure"></a><span data-ttu-id="52641-111">Windows 인증을 사용하는 응용 프로그램을 보호하려면 다음 절차를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="52641-111">To secure an application with Windows Authentication, use the following procedure.</span></span>
1. <span data-ttu-id="52641-112">Azure Multi-Factor Authentication 서버에서 Windows 인증 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="52641-112">In the Azure Multi-Factor Authentication Server click the Windows Authentication icon.</span></span>
   <span data-ttu-id="52641-113">![Windows 인증](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="52641-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="52641-114">**Windows 인증 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52641-114">Check the **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="52641-115">이 상자는 기본적으로 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="52641-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="52641-116">응용 프로그램 탭에서 관리자는 Windows 인증을 위해 하나 이상의 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52641-116">The Applications tab allows the administrator to configure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="52641-117">서버 또는 응용 프로그램을 선택합니다. 서버/응용 프로그램이 사용되는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="52641-117">Select a server or application – specify whether the server/application is enabled.</span></span> <span data-ttu-id="52641-118">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="52641-118">Click **OK**.</span></span>
5. <span data-ttu-id="52641-119">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="52641-119">Click **Add…**</span></span>
6. <span data-ttu-id="52641-120">신뢰할 수 있는 IP 탭에서 특정 IP에서 오는 Windows용 Azure Multi-Factor Authentication 세션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52641-120">The Trusted IPs tab allows you to skip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="52641-121">예를 들어, 직원이 사무실과 집에서 응용 프로그램을 사용하는 경우 사무실에 있는 동안 Azure Multi-Factor Authentication 확인용 전화를 원하지 않음을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52641-121">For example, if employees use the application from the office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at the office.</span></span> <span data-ttu-id="52641-122">이를 위해 사무실 서브넷을 신뢰할 수 있는 IP 항목으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52641-122">For this, you would specify the office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="52641-123">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="52641-123">Click **Add…**</span></span>
8. <span data-ttu-id="52641-124">단일 IP 주소를 건너뛰려면 **단일 IP**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52641-124">Select **Single IP** if you would like to skip a single IP address.</span></span>
9. <span data-ttu-id="52641-125">전체 IP 범위를 건너뛰려면 **IP 범위**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52641-125">Select **IP Range** if you would like to skip an entire IP range.</span></span> <span data-ttu-id="52641-126">예 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="52641-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="52641-127">서브넷 표기법을 사용하여 IP 범위를 지정하려면 **서브넷**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52641-127">Select **Subnet** if you would like to specify a range of IPs using subnet notation.</span></span> <span data-ttu-id="52641-128">시작 IP 서브넷을 입력하고 드롭다운 목록에서 적절한 네트워크 마스크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52641-128">Enter the subnet's starting IP and pick the appropriate netmask from the drop-down list.</span></span>
11. <span data-ttu-id="52641-129">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="52641-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52641-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="52641-130">Next steps</span></span>

- [<span data-ttu-id="52641-131">Azure MFA 서버에 대한 타사 VPN 어플라이언스 구성</span><span class="sxs-lookup"><span data-stu-id="52641-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="52641-132">Azure MFA에 대한 NPS 확장으로 기존 인증 인프라 보강</span><span class="sxs-lookup"><span data-stu-id="52641-132">Augment your existing authentication infrastructure with the NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)
