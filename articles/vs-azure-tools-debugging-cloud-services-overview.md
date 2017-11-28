---
title: "Azure Cloud Services 디버깅 옵션 | Microsoft Docs"
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
ms.openlocfilehash: cdcd4ca1fbc7e0a2f24122b32148cbda3d6951a0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="learn-the-various-ways-to-debug-an-azure-cloud-service"></a><span data-ttu-id="4396f-103">Azure 클라우드 서비스를 디버그하는 다양한 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4396f-103">Learn the various ways to debug an Azure cloud service</span></span>
<span data-ttu-id="4396f-104">이 문서에서는 Azure 클라우드 서비스를 디버그하는 다양한 방법에 대한 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4396f-104">This article provides links to the various ways to debug an Azure cloud service.</span></span> 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a><span data-ttu-id="4396f-105">Visual Studio에서 Azure 클라우드 서비스 디버깅</span><span class="sxs-lookup"><span data-stu-id="4396f-105">Debugging an Azure cloud service in Visual Studio</span></span>
<span data-ttu-id="4396f-106">Azure 계산 에뮬레이터를 사용하여 로컬 컴퓨터에서 클라우드 서비스 디버그하면 시간과 돈을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4396f-106">You can save time and money by using the Azure compute emulator to debug your cloud service on a local machine.</span></span> <span data-ttu-id="4396f-107">배포하기 전에 로컬로 서비스를 디버깅하면, 계산 시간이 소요되지 않고 안정성과 성능을 향상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4396f-107">By debugging a service locally before you deploy it, you can improve reliability and performance without paying for compute time.</span></span> <span data-ttu-id="4396f-108">그러나, Azure에서 클라우드 서비스를 실행하는 경우, 일부 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4396f-108">However, some errors might occur only when you run a cloud service in Azure.</span></span> <span data-ttu-id="4396f-109">Azure에서 클라우드 서비스를 실행할 때만 발생하는 오류는 서비스를 게시할 때 원격 디버깅을 사용하도록 설정한 다음 역할 인스턴스에 디버거를 연결하여 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4396f-109">Errors that occur only when you run a cloud service in Azure can be debugged by enabling remote debugging when you publish your service, and then attaching the debugger to a role instance.</span></span> <span data-ttu-id="4396f-110">자세한 내용은 [로컬 컴퓨터에서 클라우드 서비스 디버그](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4396f-110">For more information, see [Debug your cloud service on your local computer](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer).</span></span>

## <a name="using-azure-diagnostics"></a><span data-ttu-id="4396f-111">Azure 진단 사용</span><span class="sxs-lookup"><span data-stu-id="4396f-111">Using Azure Diagnostics</span></span> 
<span data-ttu-id="4396f-112">개발 환경 또는 Azure에서 실행되는 역할 내에서 실행되는 코드의 자세한 정보를 기록하는 Azure 진단을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4396f-112">You can use Azure Diagnostics to log detailed information from code running within roles, whether the roles are running in the development environment or in Azure.</span></span> <span data-ttu-id="4396f-113">자세한 내용은 [Azure 클라우드 서비스에서 Azure 진단 사용](http://go.microsoft.com/fwlink/p/?LinkId=400450)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4396f-113">For more information, see [Enabling Azure Diagnostics in Azure Cloud Services](http://go.microsoft.com/fwlink/p/?LinkId=400450).</span></span>

## <a name="using-intellitrace"></a><span data-ttu-id="4396f-114">IntelliTrace 사용</span><span class="sxs-lookup"><span data-stu-id="4396f-114">Using IntelliTrace</span></span> 
<span data-ttu-id="4396f-115">Visual Studio를 사용하여 .NET Framework 4.5를 대상으로 하는 역할을 작성하는 경우, Visual Studio에서 Azure 클라우드 서비스를 배포할 때 IntelliTrace를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4396f-115">If you are using Visual Studio Enterprise to write roles targeted .NET Framework 4.5, you can enable IntelliTrace at the time that you deploy an Azure cloud service from Visual Studio.</span></span> <span data-ttu-id="4396f-116">IntelliTrace는 Azure에서 실행할 때처럼 응용 프로그램을 디버그하는 Visual Studio와 사용 가능한 로그를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4396f-116">IntelliTrace provides a log that you can use with Visual Studio to debug your application as if it were running in Azure.</span></span> <span data-ttu-id="4396f-117">자세한 내용은 [IntelliTrace 및 Visual Studio를 사용하여 게시된 클라우드 서비스 디버깅](http://go.microsoft.com/fwlink/p/?LinkId=623016)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="4396f-117">For more information, see [Debugging a published cloud service with IntelliTrace and Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623016).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="4396f-118">원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="4396f-118">Remote debugging</span></span> 
<span data-ttu-id="4396f-119">Visual Studio에서 클라우드 서비스를 배포할 때 클라우드 서비스를 원격 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4396f-119">You can enable remote debugging on your cloud services at the time when you deploy the cloud service from Visual Studio.</span></span> <span data-ttu-id="4396f-120">배포에 원격 디버깅 사용을 선택하면 원격 디버깅 서비스는 각 역할 인스턴스에 실행되는 가상 컴퓨터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="4396f-120">If you choose to enable remote debugging for a deployment, remote debugging services are installed on the virtual machines that run each role instance.</span></span> <span data-ttu-id="4396f-121">`msvsmon.exe` 같은 서비스는 성능에 영향을 주지 않거나 추가 비용이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4396f-121">These services - such as `msvsmon.exe` - do not affect performance or result in extra costs.</span></span> <span data-ttu-id="4396f-122">자세한 내용은 [Azure에서 클라우드 서비스 디버그](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4396f-122">For more information, see [Debug a cloud service in Azure](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4396f-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4396f-123">Next steps</span></span>
- <span data-ttu-id="4396f-124">[Visual Studio에서 Azure 클라우드 서비스 또는 VM 디버깅](./vs-azure-tools-debug-cloud-services-virtual-machines.md) - Azure Cloud Services를 디버그하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4396f-124">[Debugging an Azure cloud service or VM in Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md) - Learn the details of how to debug Azure cloud services.</span></span>