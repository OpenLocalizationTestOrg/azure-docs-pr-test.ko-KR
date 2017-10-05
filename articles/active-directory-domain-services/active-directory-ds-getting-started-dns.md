---
title: "Azure Active Directory Domain Services: Azure 가상 네트워크에 대한 DNS 설정 업데이트 | Microsoft Docs"
description: "Azure Active Directory Domain Services 시작"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: c704ee189072ce8ed196d1ef0a23edd528a10025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="6e424-103">Azure Active Directory Domain Services 활성화(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="6e424-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="6e424-104">작업 4: Azure 가상 네트워크에 대한 DNS 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="6e424-104">Task 4: update DNS settings for the Azure virtual network</span></span>
<span data-ttu-id="6e424-105">이전 구성 작업에서 디렉터리에 Azure Active Directory Domain Services를 사용하도록 성공적으로 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="6e424-106">다음 작업은 가상 네트워크 내의 컴퓨터가 이러한 서비스에 연결되고 해당 서비스를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span></span> <span data-ttu-id="6e424-107">이 문서에서는 가상 네트워크에서 Azure Active Directory Domain Services를 사용할 수 있는 두 개의 IP 주소를 가리키도록 가상 네트워크에 대한 DNS 서버 설정을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span></span>

<span data-ttu-id="6e424-108">Azure Active Directory Domain Services를 사용하도록 설정한 가상 네트워크에 대한 DNS 서버 설정을 업데이트하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-108">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, complete the following steps:</span></span>

1. <span data-ttu-id="6e424-109">**개요** 탭에는 관리되는 도메인을 완전히 프로비전한 후 수행할 일련의 **필수 구성 단계**가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-109">The **Overview** tab lists a set of **Required configuration steps** to be performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="6e424-110">첫 번째 구성 단계는 **가상 네트워크를 위한 DNS 서버 설정 업데이트**입니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-110">The first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Domain Services - 완전히 프로비전한 후 개요 탭](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="6e424-112">도메인이 완전히 프로비전되면 두 개의 IP 주소가 이 타일에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="6e424-113">이들 IP 주소 각각은 관리되는 도메인에 대한 도메인 컨트롤러를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="6e424-114">첫 번째 IP 주소를 클립보드에 복사하려면 옆에 있는 복사 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-114">To copy the first IP address to clipboard, click the copy button next to it.</span></span> <span data-ttu-id="6e424-115">그런 다음 **DNS 구성 서버** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-115">Then click the **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="6e424-116">첫 번째 IP 주소를 **DNS 서버** 블레이드에 있는 **DNS 서버 추가** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-116">Paste the first IP address into the **Add DNS server** textbox in the **DNS servers** blade.</span></span> <span data-ttu-id="6e424-117">왼쪽으로 스크롤 하여 두 번째 IP 주소를 복사하여 **DNS 서버 추가** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-117">Scroll horizontally to the left to copy the second IP address and paste it into the **Add DNS server** textbox.</span></span>

    ![Domain Services - DNS 업데이트](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="6e424-119">가상 네트워크에 대한 DNS 서버를 업데이트를 완료하면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-119">Click **Save** when you are done to update the DNS servers for the virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="6e424-120">다시 시작하고 나면 네트워크 상의 가상 컴퓨터만 새 DNS 설정을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-120">Virtual machines in the network only get the new DNS settings after a restart.</span></span> <span data-ttu-id="6e424-121">업데이트된 DNS 설정을 즉시 얻어야 하는 경우 포털, PowerShell 또는 CLI로 다시 시작을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="6e424-121">If you need them to get the updated DNS settings right away, trigger a restart either by the portal, PowerShell, or the CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="6e424-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6e424-122">Next step</span></span>
[<span data-ttu-id="6e424-123">작업 5: Azure Active Directory Domain Services에 대한 암호 동기화 활성화</span><span class="sxs-lookup"><span data-stu-id="6e424-123">Task 5: enable password synchronization to Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-password-sync.md)
