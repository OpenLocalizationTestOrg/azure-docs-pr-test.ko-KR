---
title: "Azure microservices 위한 개발 환경을 aaaSet | Microsoft Docs"
description: "Hello 런타임, SDK 및 도구를 설치 하 고 로컬 개발 클러스터를 만듭니다. 이 설치를 완료 한 후 응용 프로그램 준비 toobuild 됩니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="8e081-104">개발 환경 준비</span><span class="sxs-lookup"><span data-stu-id="8e081-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e081-105">Windows</span><span class="sxs-lookup"><span data-stu-id="8e081-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="8e081-106">Linux</span><span class="sxs-lookup"><span data-stu-id="8e081-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="8e081-107">OSX</span><span class="sxs-lookup"><span data-stu-id="8e081-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="8e081-108">toobuild 실행 [Azure 서비스 패브릭 응용 프로그램] [ 1] 하려면 개발 컴퓨터에 hello 런타임, SDK 및 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-108">toobuild and run [Azure Service Fabric applications][1] on your development machine, install hello runtime, SDK, and tools.</span></span> <span data-ttu-id="8e081-109">Tooenable hello SDK에에서 포함 된 hello Windows PowerShell 스크립트를 실행을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-109">You also need tooenable execution of hello Windows PowerShell scripts included in hello SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e081-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8e081-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="8e081-111">지원되는 운영 체제 버전</span><span class="sxs-lookup"><span data-stu-id="8e081-111">Supported operating system versions</span></span>
<span data-ttu-id="8e081-112">운영 체제 버전에 따라 hello 개발을 위해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-112">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="8e081-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="8e081-113">Windows 7</span></span>
* <span data-ttu-id="8e081-114">Windows 8/Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="8e081-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="8e081-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="8e081-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="8e081-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8e081-116">Windows Server 2016</span></span>
* <span data-ttu-id="8e081-117">윈도우 10</span><span class="sxs-lookup"><span data-stu-id="8e081-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="8e081-118">Windows 7은 기본적으로 Windows PowerShell 2.0만을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="8e081-119">서비스 패브릭 PowerShell cmdlet에는 PowerShell 3.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="8e081-120">있습니다 수 [Windows PowerShell 5.0 다운로드] [ powershell5-download] hello Microsoft 다운로드 센터에서에서.</span><span class="sxs-lookup"><span data-stu-id="8e081-120">You can [download Windows PowerShell 5.0][powershell5-download] from hello Microsoft Download Center.</span></span>
> 
> 

## <a name="install-hello-sdk-and-tools"></a><span data-ttu-id="8e081-121">Hello SDK 및 도구 설치</span><span class="sxs-lookup"><span data-stu-id="8e081-121">Install hello SDK and tools</span></span>
### <a name="toouse-visual-studio-2017"></a><span data-ttu-id="8e081-122">Visual Studio 2017 toouse</span><span class="sxs-lookup"><span data-stu-id="8e081-122">toouse Visual Studio 2017</span></span>
<span data-ttu-id="8e081-123">서비스 패브릭 도구는 Visual Studio 2017 hello Azure 개발 및 관리 작업 부하의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-123">Service Fabric Tools are part of hello Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="8e081-124">이 워크로드를 Visual Studio 설치의 일부로 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="8e081-125">또한 Microsoft Azure 서비스 패브릭 SDK에서 웹 플랫폼 설치 관리자를 사용 하 여 tooinstall hello를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-125">In addition, you need tooinstall hello Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="8e081-126">[Hello Microsoft Azure Service Fabric SDK 설치][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="8e081-126">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="8e081-127">toouse Visual Studio 2015 (Visual Studio 2015 업데이트 2 이상 필요)</span><span class="sxs-lookup"><span data-stu-id="8e081-127">toouse Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="8e081-128">서비스 패브릭 도구는 Visual Studio 2015에 대 한 hello hello 웹 플랫폼 설치 관리자를 사용 하 여 SDK와 함께 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-128">For Visual Studio 2015, Service Fabric tools are installed together with hello SDK, using hello Web Platform Installer:</span></span>

* <span data-ttu-id="8e081-129">[Microsoft Azure Service Fabric SDK hello 및 도구 설치][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="8e081-129">[Install hello Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="8e081-130">SDK 설치만</span><span class="sxs-lookup"><span data-stu-id="8e081-130">SDK installation only</span></span>
<span data-ttu-id="8e081-131">Hello SDK 하기만 하면,이 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-131">If you only need hello SDK, you can install this package:</span></span>
* <span data-ttu-id="8e081-132">[Hello Microsoft Azure Service Fabric SDK 설치][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="8e081-132">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="8e081-133">hello 현재 버전이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-133">hello current versions are:</span></span>
* <span data-ttu-id="8e081-134">Service Fabric SDK 2.7.198</span><span class="sxs-lookup"><span data-stu-id="8e081-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="8e081-135">Service Fabric 런타임 5.7.198</span><span class="sxs-lookup"><span data-stu-id="8e081-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="8e081-136">Visual Studio 2015 1.7.50721용 Service Fabric 도구</span><span class="sxs-lookup"><span data-stu-id="8e081-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="8e081-137">Visual Studio 2017 업데이트 2에는 Visual Studio 1.6.20170504용 Service Fabric 도구가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="8e081-138">Visual Studio 2017 업데이트 3 미리 보기 7(15.3.0 미리 보기 7.0)에는 Visual Studio 1.7.20170721용 Service Fabric 도구가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="8e081-139">지원되는 버전 목록은 [Service Fabric 지원](service-fabric-support.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e081-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="8e081-140">PowerShell 스크립트 실행 활성화</span><span class="sxs-lookup"><span data-stu-id="8e081-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="8e081-141">서비스 패브릭은 로컬 개발 클러스터를 만들고 Visual Studio에서 응용 프로그램을 배포하기 위해 Windows PowerShell 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="8e081-142">기본적으로 Windows에서는 이러한 스크립트의 실행을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="8e081-143">tooenable PowerShell 실행 정책 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-143">tooenable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="8e081-144">관리자 권한으로 PowerShell을 열고 다음 명령을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-144">Open PowerShell as an administrator and enter hello following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="8e081-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e081-145">Next steps</span></span>
<span data-ttu-id="8e081-146">개발 환경의 설정을 마쳤으므로 앱을 빌드하고 실행하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="8e081-147">Visual Studio에서 서비스 패브릭 응용 프로그램 처음 만들기</span><span class="sxs-lookup"><span data-stu-id="8e081-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="8e081-148">자세한 내용은 방법 toodeploy 로컬 클러스터에 응용 프로그램 및 관리</span><span class="sxs-lookup"><span data-stu-id="8e081-148">Learn how toodeploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="8e081-149">Hello 프로그래밍 모델에 대 한 자세한 내용은: 신뢰할 수 있는 서비스 및 Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="8e081-149">Learn about hello programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="8e081-150">서비스 패브릭 hello GitHub의 코드 샘플 확인</span><span class="sxs-lookup"><span data-stu-id="8e081-150">Check out hello Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="8e081-151">서비스 패브릭 탐색기를 사용하여 클러스터 시각화</span><span class="sxs-lookup"><span data-stu-id="8e081-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="8e081-152">서비스 패브릭 경로 tooget 광범위 한 소개 toohello 플랫폼 학습 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e081-152">Follow hello Service Fabric learning path tooget a broad introduction toohello platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="8e081-153">[Service Fabric 지원 옵션](service-fabric-support.md) 알아보기</span><span class="sxs-lookup"><span data-stu-id="8e081-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric 캠페인 페이지"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI 링크"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI 링크"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI 링크"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
