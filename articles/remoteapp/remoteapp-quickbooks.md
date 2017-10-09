---
title: "Azure RemoteApp에서 QuickBooks aaaDeploy | Microsoft Docs"
description: "자세한 내용은 방법 tooshare QuickBooks Azure RemoteApp과 함께 합니다."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="dace9-103">Azure RemoteApp에서 QuickBooks를 배포하려면 어떻게 해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="dace9-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dace9-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dace9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="dace9-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="dace9-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="dace9-106">Azure RemoteApp에서 응용 프로그램으로 정보 tooshare QuickBooks 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dace9-106">Use hello following information tooshare QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="dace9-107">하이브리드 또는 클라우드 컬렉션에 QuickBooks 2015 Enterprise를 Azure remoteapp과 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dace9-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="dace9-108">hello 회사 파일 hello Azure RemoteApp 서버와에서 별개인 QuickBooks 데이터베이스 서버를 실행 하는 VM에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dace9-108">hello company file must reside on a VM that is running QuickBooks database server that is separate from hello Azure RemoteApp servers.</span></span> <span data-ttu-id="dace9-109">Azure RemoteApp 이미지에 hello 회사 파일을 저장 하지 않으며-이 작업을 수행 하는 경우 데이터 손실이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dace9-109">Never store hello company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="dace9-110">QuickBooks 엔터프라이즈만 표준 Windows 네트워킹을 통해 액세스할 수 있는 QuickBooks 데이터베이스 서버와 외부 공유에 호스팅 hello QuickBooks 파일을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dace9-110">Only QuickBooks Enterprise supports hosting hello QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="dace9-111">hello hello 회사 파일을 호스팅하는 QuickBooks 데이터베이스 서버에 있어야 hello 내에서 별도 VM 동일한 VNET hello Azure RemoteApp 컬렉션으로.</span><span class="sxs-lookup"><span data-stu-id="dace9-111">hello QuickBooks database server that is hosting hello company file must reside on a separate VM within hello same VNET as hello Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a><span data-ttu-id="dace9-112">단계 toodeploy QuickBooks</span><span class="sxs-lookup"><span data-stu-id="dace9-112">Steps toodeploy QuickBooks</span></span>
1. <span data-ttu-id="dace9-113">Azure VM 만들기 QuickBooks, QuickBooks 데이터베이스 서버와 Azure VM에 hello 회사 파일을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dace9-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place hello company file on a Azure VM.</span></span>  <span data-ttu-id="dace9-114">방화벽 규칙을 구성 하는지 tooproperly를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dace9-114">Make sure tooproperly configure firewall rules.</span></span>
2. <span data-ttu-id="dace9-115">에 QuickBooks 설치는 [사용자 지정 이미지](remoteapp-imageoptions.md) 만듭니다는 [Azure RemoteApp 컬렉션](remoteapp-collections.md), 클라우드 또는 하이브리드 hello 내에서 정확히 동일한 VNET 위치와 데이터베이스 서버를 QuickBooks hello hello VM 호스팅 회사 파일에 상주 합니다.</span><span class="sxs-lookup"><span data-stu-id="dace9-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within hello exact same VNET where hello VM hosting hello QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="dace9-116">[게시](remoteapp-publish.md) QuickBooks 앱 toousers</span><span class="sxs-lookup"><span data-stu-id="dace9-116">[Publish](remoteapp-publish.md) QuickBooks app toousers</span></span>
4. <span data-ttu-id="dace9-117">Hello Azure RemoteApp 호스팅되지 QuickBooks 클라이언트를 시작 하 고 표준 Windows 네트워킹 toohello VM 호스팅 hello QuickBooks 데이터베이스 서버를 사용 하 여 탐색 hello 회사 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dace9-117">Launch hello Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking toohello VM hosting hello QuickBooks database server and open hello company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="dace9-118">설명서 참조</span><span class="sxs-lookup"><span data-stu-id="dace9-118">Documentation references</span></span>
* <span data-ttu-id="dace9-119">QuickBooks [지원되는 구성](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="dace9-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="dace9-120">QuickBooks [배포 옵션](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="dace9-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="dace9-121">Ignite 프레젠테이션을 확인할 수 있습니다 [Microsoft Azure RemoteApp 관리 기본 사항 및 관리](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -too1:02:45 tooget toohello QuickBooks 부분 빨리 감기 합니다.</span><span class="sxs-lookup"><span data-stu-id="dace9-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward too1:02:45 tooget toohello QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="dace9-122">배포 아키텍처</span><span class="sxs-lookup"><span data-stu-id="dace9-122">Deployment architecture</span></span>
![QuickBooks + Azure RemoteApp 배포](./media/remoteapp-quickbooks/ra-quickbooks.png)

