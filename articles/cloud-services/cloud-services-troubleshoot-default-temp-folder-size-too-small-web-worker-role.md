---
title: "역할에 대 한 aaaDefault TEMP 폴더 크기가 너무 작습니다. | Microsoft Docs"
description: "클라우드 서비스 역할에는 제한 된 양의 hello TEMP 폴더에 대 한 공간에 있습니다. 이 문서는 방법에 몇 가지 제안 사항 제공 tooavoid 공간이 부족 합니다."
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
ms.openlocfilehash: 307dc20f3264e29d122a6616be0028d2ec1282c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="7aac7-104">클라우드 서비스 웹/작업자 역할에서 기본 TEMP 폴더 크기가 너무 작습니다.</span><span class="sxs-lookup"><span data-stu-id="7aac7-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="7aac7-105">hello 기본 클라우드 서비스 작업자 또는 웹 역할의 임시 디렉터리에 최대 크기인 100MB를 특정 시점에 전체 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aac7-105">hello default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="7aac7-106">이 문서에서는 설명 방법을 tooavoid hello 임시 디렉터리에 대 한 공간이 부족 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aac7-106">This article describes how tooavoid running out of space for hello temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="7aac7-107">공간이 부족한 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="7aac7-107">Why do I run out of space?</span></span>
<span data-ttu-id="7aac7-108">hello 표준 Windows 환경 변수 TEMP 및 TMP는 응용 프로그램에서 실행 되는 사용 가능한 toocode 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aac7-108">hello standard Windows environment variables TEMP and TMP are available toocode that is running in your application.</span></span> <span data-ttu-id="7aac7-109">TEMP와 TMP 모두 최대 크기가 100mb tooa 단일 디렉터리를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="7aac7-109">Both TEMP and TMP point tooa single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="7aac7-110">Hello 클라우드 서비스의 hello 수명 주기에 걸쳐이 디렉터리에 저장 된 모든 데이터가 유지 되지 않습니다. 클라우드 서비스의 hello 역할 인스턴스 재활용 인 hello 디렉터리가 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="7aac7-110">Any data that is stored in this directory is not persisted across hello lifecycle of hello cloud service; if hello role instances in a cloud service are recycled, hello directory is cleaned.</span></span>

## <a name="suggestion-toofix-hello-problem"></a><span data-ttu-id="7aac7-111">제안 toofix hello 문제</span><span class="sxs-lookup"><span data-stu-id="7aac7-111">Suggestion toofix hello problem</span></span>
<span data-ttu-id="7aac7-112">Hello 다음 대체 방법 중 하나를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aac7-112">Implement one of hello following alternatives:</span></span>

* <span data-ttu-id="7aac7-113">로컬 저장소 리소스를 구성하고 TEMP 또는 TMP를 사용하는 대신 직접 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7aac7-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="7aac7-114">호출 hello 응용 프로그램 내에서 실행 되는 코드에서 로컬 저장소 리소스 tooaccess [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="7aac7-114">tooaccess a local storage resource from code that is running within your application, call hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="7aac7-115">로컬 저장소 리소스를 구성 하 고 hello TEMP 및 TMP 디렉터리 toopoint toohello hello 로컬 저장소 리소스의 경로 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="7aac7-115">Configure a local storage resource, and point hello TEMP and TMP directories toopoint toohello path of hello local storage resource.</span></span> <span data-ttu-id="7aac7-116">Hello 내에서이 수정 작업을 수행 해야 [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="7aac7-116">This modification should be performed within hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="7aac7-117">hello 다음 코드 예제에서는 어떻게 toomodify hello 대상 디렉터리에서 TEMP 및 TMP에 대 한 hello OnStart 메서드 내에서:</span><span class="sxs-lookup"><span data-stu-id="7aac7-117">hello following code example shows how toomodify hello target directories for TEMP and TMP from within hello OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // hello local resource declaration must have been added toothe
            // service definition file for hello role named WorkerRole1:
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

            // hello rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="7aac7-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7aac7-118">Next steps</span></span>
<span data-ttu-id="7aac7-119">설명 하는 블로그 읽기 [tooincrease hello Azure 웹 역할 ASP.NET 임시 폴더의 크기를 hello 어떻게](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7aac7-119">Read a blog that describes [How tooincrease hello size of hello Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="7aac7-120">클라우드 서비스에 대한 [문제해결 문서](/?tag=top-support-issue&product=cloud-services) 를 더 봅니다.</span><span class="sxs-lookup"><span data-stu-id="7aac7-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="7aac7-121">toolearn tootroubleshoot 클라우드 서비스 역할을 Azure PaaS 컴퓨터 진단 데이터를 사용 하 여 발급 하는 방법을 보려면 [Kevin Williamson 블로그 시리즈](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7aac7-121">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
