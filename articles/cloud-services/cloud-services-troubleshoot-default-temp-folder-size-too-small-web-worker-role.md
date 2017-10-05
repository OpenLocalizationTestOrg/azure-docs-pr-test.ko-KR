---
title: "역할에 대한 기본 TEMP 폴더 크기가 너무 작음 | Microsoft Docs"
description: "클라우드 서비스 역할에는 TEMP 폴더에 대한 공간이 제한되어 있습니다. 이 문서에서는 공간 부족을 방지하는 방법을 몇 가지 제안합니다."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f2af8dd-2012-4b36-9dd5-19bf6a67e47d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 577d090a009eb2331b401273257c7cc7c1eea772
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="d708e-104">클라우드 서비스 웹/작업자 역할에서 기본 TEMP 폴더 크기가 너무 작습니다.</span><span class="sxs-lookup"><span data-stu-id="d708e-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="d708e-105">클라우드 서비스 작업자 또는 웹 역할의 기본 임시 디렉터리에는 최대 100MB 크기의 공간이 있으며 특정 시점에 꽉 찰 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d708e-105">The default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="d708e-106">이 문서는 임시 디렉터리에 대한 공간 부족을 방지하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d708e-106">This article describes how to avoid running out of space for the temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="d708e-107">공간이 부족한 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="d708e-107">Why do I run out of space?</span></span>
<span data-ttu-id="d708e-108">표준 Windows 환경 변수 TEMP 및 TMP는 응용 프로그램에서 실행되는 코드에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d708e-108">The standard Windows environment variables TEMP and TMP are available to code that is running in your application.</span></span> <span data-ttu-id="d708e-109">TEMP와 TMP는 모두 최대 크기가 100MB인 단일 디렉터리를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="d708e-109">Both TEMP and TMP point to a single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="d708e-110">이 디렉터리에 저장된 모든 데이터는 클라우드 서비스의 수명 주기 전체에 지속되지 않습니다. 클라우드 서비스의 역할 인스턴스가 재활용되면 디렉터리가 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="d708e-110">Any data that is stored in this directory is not persisted across the lifecycle of the cloud service; if the role instances in a cloud service are recycled, the directory is cleaned.</span></span>

## <a name="suggestion-to-fix-the-problem"></a><span data-ttu-id="d708e-111">문제를 해결하려는 제안</span><span class="sxs-lookup"><span data-stu-id="d708e-111">Suggestion to fix the problem</span></span>
<span data-ttu-id="d708e-112">다음 대안 중 하나를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="d708e-112">Implement one of the following alternatives:</span></span>

* <span data-ttu-id="d708e-113">로컬 저장소 리소스를 구성하고 TEMP 또는 TMP를 사용하는 대신 직접 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="d708e-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="d708e-114">응용 프로그램 내에서 실행되는 코드에서 로컬 저장소 리소스에 액세스하려면 [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d708e-114">To access a local storage resource from code that is running within your application, call the [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="d708e-115">로컬 저장소 리소스를 구성하고 TEMP 및 TMP 디렉터리를 카리켜서 로컬 저장소 리소스의 경로를 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d708e-115">Configure a local storage resource, and point the TEMP and TMP directories to point to the path of the local storage resource.</span></span> <span data-ttu-id="d708e-116">이 수정 작업은 [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) 메서드 내에서 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d708e-116">This modification should be performed within the [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="d708e-117">다음 코드 예제에서는 OnStart 메서드 내에서 TEMP 및 TMP에 대한 대상 디렉터리를 수정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d708e-117">The following code example shows how to modify the target directories for TEMP and TMP from within the OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // The local resource declaration must have been added to the
            // service definition file for the role named WorkerRole1:
            //
            // <LocalResources>
            //    <LocalStorage name="CustomTempLocalStore"
            //                  cleanOnRoleRecycle="false"
            //                  sizeInMB="1024" />
            // </LocalResources>

            string customTempLocalResourcePath =
            RoleEnvironment.GetLocalResource("CustomTempLocalStore").RootPath;
            Environment.SetEnvironmentVariable("TMP", customTempLocalResourcePath);
            Environment.SetEnvironmentVariable("TEMP", customTempLocalResourcePath);

            // The rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="d708e-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d708e-118">Next steps</span></span>
<span data-ttu-id="d708e-119">[Azure 웹 역할 ASP.NET 임시 폴더의 크기를 늘리는 방법](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx)을 설명하는 블로그를 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="d708e-119">Read a blog that describes [How to increase the size of the Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="d708e-120">클라우드 서비스에 대한 [문제해결 문서](/?tag=top-support-issue&product=cloud-services) 를 더 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d708e-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="d708e-121">Azure PaaS 컴퓨터 진단 데이터를 사용하여 클라우드 서비스 역할 문제를 해결하는 방법을 알아보려면 [Kevin Williamson의 블로그 시리즈](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d708e-121">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
