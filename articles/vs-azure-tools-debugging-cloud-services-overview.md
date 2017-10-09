---
title: "Azure 디버깅을 위해 aaaOptions 클라우드 서비스 | Microsoft Docs"
description: "Azure Cloud Services 디버깅"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/18/2017
ms.author: kraigb
ms.openlocfilehash: 8b7779ca33cfd82fd5fbccf229ea822c311bdea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-hello-various-ways-toodebug-an-azure-cloud-service"></a><span data-ttu-id="29978-103">Hello 다양 한 방법에 알아봅니다 toodebug Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="29978-103">Learn hello various ways toodebug an Azure cloud service</span></span>
<span data-ttu-id="29978-104">이 문서에서는 링크 toohello 다양 한 방법으로 toodebug Azure 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="29978-104">This article provides links toohello various ways toodebug an Azure cloud service.</span></span> 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a><span data-ttu-id="29978-105">Visual Studio에서 Azure 클라우드 서비스 디버깅</span><span class="sxs-lookup"><span data-stu-id="29978-105">Debugging an Azure cloud service in Visual Studio</span></span>
<span data-ttu-id="29978-106">저장할 수 있습니다 시간과 비용 hello Azure 계산 에뮬레이터 toodebug를 사용 하 여 클라우드 서비스는 로컬 컴퓨터에서.</span><span class="sxs-lookup"><span data-stu-id="29978-106">You can save time and money by using hello Azure compute emulator toodebug your cloud service on a local machine.</span></span> <span data-ttu-id="29978-107">배포하기 전에 로컬로 서비스를 디버깅하면, 계산 시간이 소요되지 않고 안정성과 성능을 향상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29978-107">By debugging a service locally before you deploy it, you can improve reliability and performance without paying for compute time.</span></span> <span data-ttu-id="29978-108">그러나, Azure에서 클라우드 서비스를 실행하는 경우, 일부 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29978-108">However, some errors might occur only when you run a cloud service in Azure.</span></span> <span data-ttu-id="29978-109">사용자가 서비스를 게시할 때 원격 디버깅을 hello 디버거 tooa 역할 인스턴스를 한 다음 연결을 사용 하 여 Azure에서 클라우드 서비스를 실행 하는 경우에 발생 하는 오류를 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29978-109">Errors that occur only when you run a cloud service in Azure can be debugged by enabling remote debugging when you publish your service, and then attaching hello debugger tooa role instance.</span></span> <span data-ttu-id="29978-110">자세한 내용은 [로컬 컴퓨터에서 클라우드 서비스 디버그](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29978-110">For more information, see [Debug your cloud service on your local computer](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer).</span></span>

## <a name="using-azure-diagnostics"></a><span data-ttu-id="29978-111">Azure 진단 사용</span><span class="sxs-lookup"><span data-stu-id="29978-111">Using Azure Diagnostics</span></span> 
<span data-ttu-id="29978-112">Azure 진단을 사용 하 여 hello 역할이 hello 개발 환경에서 또는 Azure에서 실행 되는 여부 toolog 자세한 역할 내에서 코드 실행 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="29978-112">You can use Azure Diagnostics toolog detailed information from code running within roles, whether hello roles are running in hello development environment or in Azure.</span></span> <span data-ttu-id="29978-113">자세한 내용은 [Azure 클라우드 서비스에서 Azure 진단 사용](http://go.microsoft.com/fwlink/p/?LinkId=400450)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29978-113">For more information, see [Enabling Azure Diagnostics in Azure Cloud Services](http://go.microsoft.com/fwlink/p/?LinkId=400450).</span></span>

## <a name="using-intellitrace"></a><span data-ttu-id="29978-114">IntelliTrace 사용</span><span class="sxs-lookup"><span data-stu-id="29978-114">Using IntelliTrace</span></span> 
<span data-ttu-id="29978-115">사용 중인 경우 Visual Studio Enterprise toowrite 역할 대상이.NET Framework 4.5, Visual Studio에서 Azure 클라우드 서비스를 배포 하는 hello 시간에 IntelliTrace를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29978-115">If you are using Visual Studio Enterprise toowrite roles targeted .NET Framework 4.5, you can enable IntelliTrace at hello time that you deploy an Azure cloud service from Visual Studio.</span></span> <span data-ttu-id="29978-116">IntelliTrace에 대 한 로그 제공는 경우 사용할 수 있습니다 Visual Studio toodebug와 응용 프로그램으로 Azure에서 실행 중인 것입니다.</span><span class="sxs-lookup"><span data-stu-id="29978-116">IntelliTrace provides a log that you can use with Visual Studio toodebug your application as if it were running in Azure.</span></span> <span data-ttu-id="29978-117">자세한 내용은 [IntelliTrace 및 Visual Studio를 사용하여 게시된 클라우드 서비스 디버깅](http://go.microsoft.com/fwlink/p/?LinkId=623016)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="29978-117">For more information, see [Debugging a published cloud service with IntelliTrace and Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623016).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="29978-118">원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="29978-118">Remote debugging</span></span> 
<span data-ttu-id="29978-119">Visual Studio에서 hello 클라우드 서비스를 배포 하는 경우 hello 시간에 클라우드 서비스에서 원격 디버깅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29978-119">You can enable remote debugging on your cloud services at hello time when you deploy hello cloud service from Visual Studio.</span></span> <span data-ttu-id="29978-120">원격 배포에 대 한 디버깅 tooenable을 선택 하면 원격 디버깅 서비스가 각 역할 인스턴스를 실행 하는 hello 가상 컴퓨터에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29978-120">If you choose tooenable remote debugging for a deployment, remote debugging services are installed on hello virtual machines that run each role instance.</span></span> <span data-ttu-id="29978-121">`msvsmon.exe` 같은 서비스는 성능에 영향을 주지 않거나 추가 비용이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29978-121">These services - such as `msvsmon.exe` - do not affect performance or result in extra costs.</span></span> <span data-ttu-id="29978-122">자세한 내용은 [Azure에서 클라우드 서비스 디버그](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29978-122">For more information, see [Debug a cloud service in Azure](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure).</span></span>

## <a name="next-steps"></a><span data-ttu-id="29978-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29978-123">Next steps</span></span>
- <span data-ttu-id="29978-124">[Azure 클라우드 서비스 또는 VM Visual Studio에서 디버깅](./vs-azure-tools-debug-cloud-services-virtual-machines.md) -어떻게 toodebug Azure 클라우드 서비스의 hello 세부 정보에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="29978-124">[Debugging an Azure cloud service or VM in Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md) - Learn hello details of how toodebug Azure cloud services.</span></span>
