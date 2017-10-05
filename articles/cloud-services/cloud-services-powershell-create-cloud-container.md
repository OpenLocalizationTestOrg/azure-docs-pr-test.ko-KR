---
title: "PowerShell을 사용하여 클라우드 서비스 컨테이너 만들기 | Microsoft Docs"
description: "이 문서에서는 PowerShell을 사용하여 클라우드 서비스 컨테이너를 만드는 방법을 설명합니다. 컨테이너는 웹 및 작업자 역할을 호스트합니다."
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: 
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 2023fa7b318f9f76ce1e1ea0a46110297be9a001
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-an-azure-powershell-command-to-create-an-empty-cloud-service-container"></a><span data-ttu-id="82771-104">Azure PowerShell 명령을 사용하여 빈 클라우드 서비스 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="82771-104">Use an Azure PowerShell command to create an empty cloud service container</span></span>
<span data-ttu-id="82771-105">이 문서에서는 Azure PowerShell cmdlet을 사용하여 신속하게 클라우드 서비스 컨테이너를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="82771-105">This article explains how to quickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="82771-106">다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="82771-106">Please follow the steps below:</span></span>

1. <span data-ttu-id="82771-107">[Azure PowerShell 다운로드](http://aka.ms/webpi-azps) 페이지에서 Microsoft Azure PowerShell cmdlet을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="82771-107">Install the Microsoft Azure PowerShell cmdlet from the [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="82771-108">PowerShell 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="82771-108">Open the PowerShell command prompt.</span></span>
3. <span data-ttu-id="82771-109">[Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) 를 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="82771-109">Use the [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) to sign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="82771-110">Azure PowerShell cmdlet을 설치하고 Azure 구독에 연결하는 방법에 대한 자세한 지침은 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82771-110">For further instruction on installing the Azure PowerShell cmdlet and connecting to your Azure subscription, refer to [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="82771-111">**New-AzureService** cmdlet을 사용하여 빈 Azure 클라우드 서비스 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82771-111">Use the **New-AzureService** cmdlet to create an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="82771-112">이 예제를 따라 cmdlet을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="82771-112">Follow this example to invoke the cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="82771-113">Azure 클라우드 서비스 만들기에 대한 자세한 내용을 보려면 다음을 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="82771-113">For more information about creating the Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="82771-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="82771-114">Next steps</span></span>
* <span data-ttu-id="82771-115">클라우드 서비스 배포를 관리하려면 [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx) 및 [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) 명령을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82771-115">To manage the cloud service deployment, refer to the [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="82771-116">더욱 자세한 내용을 보려면 [클라우드 서비스를 구성하는 방법](cloud-services-how-to-configure.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82771-116">You may also refer to [How to configure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="82771-117">클라우드 서비스 프로젝트를 Azure에 게시하려면, **PublishCloudService.ps1** 코드 예제를 [Azure에서 클라우드 서비스에 대한 지속적인 전송](cloud-services-dotnet-continuous-delivery.md)에서 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82771-117">To publish your cloud service project to Azure, refer to the  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
