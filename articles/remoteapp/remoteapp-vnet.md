---
title: "Azure RemoteApp과 함께 aaaValidate hello Azure VNET toouse | Microsoft Docs"
description: "어떻게 toomake Azure VNET가 확실 준비에 대해 알아봅니다 Azure RemoteApp과 함께 toouse"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a><span data-ttu-id="72083-103">Azure RemoteApp과 함께 hello Azure VNET toouse 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="72083-103">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="72083-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72083-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="72083-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="72083-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="72083-106">Azure RemoteApp과 함께 Azure VNET을 사용 하기 전에 toovalidate hello VNET을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72083-106">Before you use an Azure VNET with Azure RemoteApp, you might want toovalidate hello VNET.</span></span> <span data-ttu-id="72083-107">이렇게 하면 연결 문제를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72083-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="72083-108">toovalidate Azure VNET 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72083-108">toovalidate your Azure VNET, do hello following:</span></span>

1. <span data-ttu-id="72083-109">Hello Azure RemoteApp과 함께 toouse를 원하는 Azure VNET의 서브넷을 hello 내 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72083-109">Create an Azure virtual machine inside hello subnet of hello Azure VNET you want toouse with Azure RemoteApp.</span></span>
2. <span data-ttu-id="72083-110">Hello를 사용 하 여 VM toothat 연결 **연결** hello 관리 포털에서 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="72083-110">Connect toothat VM by using hello **Connect** option in hello management portal.</span></span>
3. <span data-ttu-id="72083-111">가상 컴퓨터 toohello hello 가입 toouse Azure RemoteApp과 함께 지정 하는 동일한 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="72083-111">Join hello virtual machine toohello same domain that you want toouse with Azure RemoteApp.</span></span> <span data-ttu-id="72083-112">Tooyour 온-프레미스 네트워크에 연결 하는 하이브리드 컬렉션을 만드는 경우 hello 가상 컴퓨터 tooyour 로컬 도메인에 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="72083-112">If you are creating a hybrid collection that connects tooyour on-premises network, join hello virtual machine tooyour local domain.</span></span>

<span data-ttu-id="72083-113">성공한 경우 hello Azure VNET은 준비 toouse RemoteApp과 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="72083-113">If this is successful, hello Azure VNET is ready toouse with RemoteApp.</span></span>

<span data-ttu-id="72083-114">종단 간 하이브리드 컬렉션 워크플로 hello에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="72083-114">For more information about hello end-to-end hybrid collection workflow, see hello following articles:</span></span>

* [<span data-ttu-id="72083-115">어떻게 tooplan Azure RemoteApp에 대 한 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="72083-115">How tooplan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="72083-116">하이브리드 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="72083-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="72083-117">ExpressRoute에 대 한 지원) (으로 Azure RemoteApp 컬렉션 tooyour Azure 가상 네트워크를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="72083-117">Deploy Azure RemoteApp collection tooyour Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

