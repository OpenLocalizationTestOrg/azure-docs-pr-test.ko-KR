---
title: "VM 확장을 사용 하 여 Linux VM aaaMonitoring | Microsoft Docs"
description: "Linux 진단 확장 toomonitor hello 성능 및 진단 데이터 Azure에서 Linux VM의 toouse hello 하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a><span data-ttu-id="d1d1e-103">Hello Linux 진단 확장 toomonitor hello 성능과 Linux VM의 진단 데이터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d1d1e-103">Use hello Linux Diagnostic Extension toomonitor hello performance and diagnostic data of a Linux VM</span></span>

<span data-ttu-id="d1d1e-104">이 문서에서는 버전 2.3 hello Linux 진단 확장을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-104">This document describes version 2.3 of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1d1e-105">이 버전은 사용이 중단되었으며 2018년 6월 30일 이후에 언제든지 게시가 취소될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-105">This version is deprecated, and it may be unpublished any time after June 30, 2018.</span></span> <span data-ttu-id="d1d1e-106">이 버전은 버전 3.0으로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-106">It has been replaced by version 3.0.</span></span> <span data-ttu-id="d1d1e-107">자세한 내용은 참조 hello [hello Linux 진단 확장의 버전 3.0 설명서](../diagnostic-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-107">For more information, see hello [documentation for version 3.0 of hello Linux Diagnostic Extension](../diagnostic-extension.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="d1d1e-108">소개</span><span class="sxs-lookup"><span data-stu-id="d1d1e-108">Introduction</span></span>

<span data-ttu-id="d1d1e-109">(**참고**: Linux 진단 확장에서 오픈 소스는 hello [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) hello hello 확장에서 최신 정보를 처음 게시 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-109">(**Note**: hello Linux Diagnostic Extension is open-sourced on [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) where hello most current information on hello extension is first published.</span></span> <span data-ttu-id="d1d1e-110">Toocheck hello 경우가 [GitHub 페이지](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) 첫 번째.)</span><span class="sxs-lookup"><span data-stu-id="d1d1e-110">You might want toocheck hello [GitHub page](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) first.)</span></span>

<span data-ttu-id="d1d1e-111">hello Linux 진단 확장은 사용자 모니터 hello Linux Vm의 경우 Microsoft Azure에서 실행 되는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-111">hello Linux Diagnostic Extension helps a user monitor hello Linux VMs that are running on Microsoft Azure.</span></span> <span data-ttu-id="d1d1e-112">기능을 수행 하는 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-112">It has hello following capabilities:</span></span>

* <span data-ttu-id="d1d1e-113">수집 하 고 진단 및 syslog 정보를 포함 하는 hello Linux VM toohello 사용자의 저장소 테이블에서 hello 시스템 성능 정보를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-113">Collects and uploads hello system performance information from hello Linux VM toohello user's storage table, including diagnostic and syslog information.</span></span>
* <span data-ttu-id="d1d1e-114">수집 되어 업로드 하는 사용자가 toocustomize hello 데이터 메트릭을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-114">Enables users toocustomize hello data metrics that will be collected and uploaded.</span></span>
* <span data-ttu-id="d1d1e-115">사용자가 tooupload 지정 된 로그 파일 tooa 지정 된 저장소 테이블을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-115">Enables users tooupload specified log files tooa designated storage table.</span></span>

<span data-ttu-id="d1d1e-116">Hello 현재 버전 2.3에에서 hello 데이터 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-116">In hello current version 2.3, hello data includes:</span></span>

* <span data-ttu-id="d1d1e-117">시스템, 보안 및 응용 프로그램 로그를 비롯한 모든 Linux Rsyslog 로그.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-117">All Linux Rsyslog logs, including system, security, and application logs.</span></span>
* <span data-ttu-id="d1d1e-118">에 지정 된 모든 시스템 데이터 [hello System Center 플랫폼 크로스 솔루션 사이트](https://scx.codeplex.com/wikipage?title=xplatproviders)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-118">All system data that's specified on [hello System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
* <span data-ttu-id="d1d1e-119">사용자가 지정한 로그 파일.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-119">User-specified log files.</span></span>

<span data-ttu-id="d1d1e-120">이 확장 프로그램은 클래식 hello와 리소스 관리자 배포 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-120">This extension works with both hello classic and Resource Manager deployment models.</span></span>

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a><span data-ttu-id="d1d1e-121">현재 버전의 hello 확장 및 이전 버전의 사용 중단</span><span class="sxs-lookup"><span data-stu-id="d1d1e-121">Current version of hello extension and deprecation of old versions</span></span>

<span data-ttu-id="d1d1e-122">hello hello 확장의 최신 버전은 **2.3**, 및 **(2.0, 2.1 및 2.2)에 있는 이전 버전이 더 이상 사용 되지 되 고 끝날 때 올해 (2017) 게시 되지 않은**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-122">hello latest version of hello extension is **2.3**, and **any old versions (2.0, 2.1, and 2.2) will be deprecated and unpublished by end of this year (2017)**.</span></span> <span data-ttu-id="d1d1e-123">사용 하지 않도록 설정 하는 자동으로 부 버전 업그레이드를 hello Linux 진단 확장을 설치한 경우 hello 확장을 제거 하 고 사용 하도록 설정 하는 자동으로 부 버전 업그레이드를 다시 설치 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-123">If you installed hello Linux Diagnostic extension with automatic minor version upgrade disabled, it's strongly recommended that you uninstall hello extension and reinstall it with automatic minor version upgrade enabled.</span></span> <span data-ttu-id="d1d1e-124">클래식 (ASM) Vm에서이 Azure XPLAT CLI 또는 Powershell을 통해 hello 확장을 설치 하는 경우 '2.*' hello 버전으로 지정 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-124">On classic (ASM) VMs, you can achieve this by specifying '2.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span> <span data-ttu-id="d1d1e-125">ARM Vm에서이 위해서는 포함 하 여 ' "autoUpgradeMinorVersion": true' hello VM 배포 템플릿에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-125">On ARM VMs, you can achieve this by including '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span> <span data-ttu-id="d1d1e-126">또한 새 hello 확장이 설치 되어 있는 모든 hello 자동 부 버전 업그레이드 옵션 설정 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-126">Also, any new installation of hello extension should have hello auto minor version upgrade option turned on.</span></span>

## <a name="enable-hello-extension"></a><span data-ttu-id="d1d1e-127">Hello 확장 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d1d1e-127">Enable hello extension</span></span>

<span data-ttu-id="d1d1e-128">Hello를 사용 하 여이 확장을 사용 하도록 설정할 수 있습니다 [Azure 포털](https://portal.azure.com/#), Azure PowerShell 또는 Azure CLI 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-128">You can enable this extension by using hello [Azure portal](https://portal.azure.com/#), Azure PowerShell, or Azure CLI scripts.</span></span>

<span data-ttu-id="d1d1e-129">tooview hello 시스템을 구성 하 고 성능 데이터를 직접 hello Azure 포털에서에서 수행 [hello Azure 블로그에서 이러한 단계](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-129">tooview and configure hello system and performance data directly from hello Azure portal, follow [these steps on hello Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span></span>

<span data-ttu-id="d1d1e-130">이 문서는 방법에 중점을 둡니다 tooenable Azure CLI 명령을 사용 하 여 hello 확장을 구성 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-130">This article focuses on how tooenable and configure hello extension by using Azure CLI commands.</span></span> <span data-ttu-id="d1d1e-131">이렇게 하면 tooread hello 데이터 보려면 hello 저장소 테이블에서 직접 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-131">This allows you tooread and view hello data directly from hello storage table.</span></span>

<span data-ttu-id="d1d1e-132">Note hello Azure 포털에 대 한 여기에서 설명 하는 hello 구성 메서드 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-132">Note that hello configuration methods that are described here won't work for hello Azure portal.</span></span> <span data-ttu-id="d1d1e-133">tooview hello Azure 포털에서 직접 hello 시스템 및 성능 데이터를 구성 하 고, hello 확장 hello 포털을 통해 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-133">tooview and configure hello system and performance data directly from hello Azure portal, hello extension must be enabled through hello portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1d1e-134">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d1d1e-134">Prerequisites</span></span>

* <span data-ttu-id="d1d1e-135">**Azure Linux 에이전트 버전 2.0.6 이상**.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-135">**Azure Linux Agent version 2.0.6 or later**.</span></span>

  <span data-ttu-id="d1d1e-136">대부분의 Azure VM Linux 갤러리 이미지에는 2.0.6 이후 버전이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-136">Note that most Azure VM Linux gallery images include version 2.0.6 or later.</span></span> <span data-ttu-id="d1d1e-137">실행할 수 있습니다 **WAAgent-버전** tooconfirm hello VM에 설치 된 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-137">You can run **WAAgent -version** tooconfirm which version is installed on hello VM.</span></span> <span data-ttu-id="d1d1e-138">Hello VM 2.0.6 이전 버전을 실행 하는 경우 참고할 수 [GitHub에서 이러한 지침](https://github.com/Azure/WALinuxAgent "지침") tooupdate 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-138">If hello VM is running a version that's earlier than 2.0.6, you can follow [these instructions on GitHub](https://github.com/Azure/WALinuxAgent "instructions") tooupdate it.</span></span>
* <span data-ttu-id="d1d1e-139">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-139">**Azure CLI**.</span></span> <span data-ttu-id="d1d1e-140">에 따라 [CLI를 설치 하는 데이 지침은](../../../cli-install-nodejs.md) tooset hello Azure CLI 환경 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-140">Follow [this guidance for installing CLI](../../../cli-install-nodejs.md) tooset up hello Azure CLI environment on your machine.</span></span> <span data-ttu-id="d1d1e-141">Hello Azure CLI를 설치한 후 사용할 수 있습니다 **azure** 명령줄 인터페이스 (예: Bash, 터미널, 또는 명령 프롬프트) tooaccess hello Azure CLI 명령의 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-141">After Azure CLI is installed, you can use hello **azure** command from your command-line interface (Bash, Terminal, or command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="d1d1e-142">예:</span><span class="sxs-lookup"><span data-stu-id="d1d1e-142">For example:</span></span>

  * <span data-ttu-id="d1d1e-143">자세한 도움말 정보는 **azure vm extension set –help** 를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-143">Run **azure vm extension set --help** for detailed help information.</span></span>
  * <span data-ttu-id="d1d1e-144">실행 **azure 로그인** toosign tooAzure에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-144">Run **azure login** toosign in tooAzure.</span></span>
  * <span data-ttu-id="d1d1e-145">실행 **azure vm 목록** toolist 모든 hello Azure에 있는 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-145">Run **azure vm list** toolist all hello virtual machines that you have on Azure.</span></span>
* <span data-ttu-id="d1d1e-146">저장소 계정 toostore hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-146">A storage account toostore hello data.</span></span> <span data-ttu-id="d1d1e-147">이전에 만든 저장소 계정 이름 및 액세스 키 tooupload hello 데이터 tooyour 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-147">You will need a storage account name that was created previously and an access key tooupload hello data tooyour storage.</span></span>

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a><span data-ttu-id="d1d1e-148">Hello Azure CLI 명령을 tooenable hello Linux 진단 확장을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d1d1e-148">Use hello Azure CLI command tooenable hello Linux Diagnostic Extension</span></span>

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a><span data-ttu-id="d1d1e-149">시나리오 1.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-149">Scenario 1.</span></span> <span data-ttu-id="d1d1e-150">Hello 확장 hello 기본 데이터 집합으로 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d1d1e-150">Enable hello extension with hello default data set</span></span>

<span data-ttu-id="d1d1e-151">2.3 이상 버전에서 수집 되는 hello 기본 데이터에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-151">In version 2.3 or later, hello default data that will be collected includes:</span></span>

* <span data-ttu-id="d1d1e-152">모든 Rsyslog 정보(시스템, 보안 및 응용 프로그램 로그 포함)</span><span class="sxs-lookup"><span data-stu-id="d1d1e-152">All Rsyslog information (including system, security, and application logs).</span></span>  
* <span data-ttu-id="d1d1e-153">기본 시스템 데이터의 핵심 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-153">A core set of basis system data.</span></span> <span data-ttu-id="d1d1e-154">전체 데이터 집합을 hello는 hello에 설명 되어 [System Center 플랫폼 크로스 솔루션 사이트](https://scx.codeplex.com/wikipage?title=xplatproviders)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-154">Note that hello full data set is described on hello [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
  <span data-ttu-id="d1d1e-155">Tooenable 하려는 경우 추가 데이터 시나리오 2와 3 hello 단계로 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-155">If you want tooenable extra data, continue with hello steps in Scenarios 2 and 3.</span></span>

<span data-ttu-id="d1d1e-156">1단계.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-156">Step 1.</span></span> <span data-ttu-id="d1d1e-157">콘텐츠는 다음 hello로 PrivateConfig.json 이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-157">Create a file named PrivateConfig.json with hello following content:</span></span>

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

<span data-ttu-id="d1d1e-158">2단계.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-158">Step 2.</span></span> <span data-ttu-id="d1d1e-159">**azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-159">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span></span>

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a><span data-ttu-id="d1d1e-160">시나리오 2.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-160">Scenario 2.</span></span> <span data-ttu-id="d1d1e-161">Hello 성능 모니터 메트릭 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="d1d1e-161">Customize hello performance monitor metrics</span></span>

<span data-ttu-id="d1d1e-162">이 섹션에서는 성능 및 진단 데이터 테이블 toocustomize hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-162">This section describes how toocustomize hello performance and diagnostic data table.</span></span>

<span data-ttu-id="d1d1e-163">1단계.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-163">Step 1.</span></span> <span data-ttu-id="d1d1e-164">시나리오 1에 설명 된 hello 콘텐츠로 PrivateConfig.json 이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-164">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="d1d1e-165">또한 PublicConfig.json이라는 파일도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-165">Also create a file named PublicConfig.json.</span></span> <span data-ttu-id="d1d1e-166">원하는 toocollect hello 특정 데이터를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-166">Specify hello particular data you want toocollect.</span></span>

<span data-ttu-id="d1d1e-167">지원 되는 모든 공급자 및 변수에 대 한 참조 hello [System Center 플랫폼 크로스 솔루션 사이트](https://scx.codeplex.com/wikipage?title=xplatproviders)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-167">For all supported providers and variables, reference hello [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span> <span data-ttu-id="d1d1e-168">여러 개의 쿼리를 포함할 수 있으며 더 많은 쿼리 toohello 스크립트를 추가 하 여 여러 테이블에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-168">You can have multiple queries and store them in multiple tables by appending more queries toohello script.</span></span>

<span data-ttu-id="d1d1e-169">기본적으로 hello Rsyslog 데이터가 항상 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-169">By default, hello Rsyslog data is always collected.</span></span>

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


<span data-ttu-id="d1d1e-170">2단계.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-170">Step 2.</span></span> <span data-ttu-id="d1d1e-171">**azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-171">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

### <a name="scenario-3-upload-your-own-log-files"></a><span data-ttu-id="d1d1e-172">시나리오 3.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-172">Scenario 3.</span></span> <span data-ttu-id="d1d1e-173">고유한 로그 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="d1d1e-173">Upload your own log files</span></span>

<span data-ttu-id="d1d1e-174">이 섹션에서는 toocollect 및 업로드 특정 로그 파일을 저장소 계정 tooyour 방법 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-174">This section describes how toocollect and upload specific log files tooyour storage account.</span></span> <span data-ttu-id="d1d1e-175">Toospecify 모두 hello tooyour 로그 파일과 hello의 경로 이름 hello 저장할 테이블 toostore 로그 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-175">You need toospecify both hello path tooyour log file and hello name of hello table where you want toostore your log.</span></span> <span data-ttu-id="d1d1e-176">파일/테이블에서 여러 개의 항목 toohello 스크립트를 추가 하 여 여러 개의 로그 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-176">You can create multiple log files by adding multiple file/table entries toohello script.</span></span>

<span data-ttu-id="d1d1e-177">1단계.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-177">Step 1.</span></span> <span data-ttu-id="d1d1e-178">시나리오 1에 설명 된 hello 콘텐츠로 PrivateConfig.json 이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-178">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="d1d1e-179">그런 다음 다음 hello로 PublicConfig.json 라는 다른 파일 콘텐츠 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-179">Then create another file named PublicConfig.json with hello following content:</span></span>

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

<span data-ttu-id="d1d1e-180">2단계.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-180">Step 2.</span></span> <span data-ttu-id="d1d1e-181">`azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-181">Run `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span></span>

<span data-ttu-id="d1d1e-182">유의 hello 확장 버전 이전 too2.3에서이 설정을 사용 하 여 모든 로그를 기록 너무`/var/log/mysql.err` 너무 중복 될 수도 있습니다`/var/log/syslog` (또는 `/var/log/messages` hello Linux 배포판에 따라)도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-182">Note that with this setting on hello extension versions prior too2.3, all logs written too`/var/log/mysql.err` might be duplicated too`/var/log/syslog` (or `/var/log/messages` depending on hello Linux distro) as well.</span></span> <span data-ttu-id="d1d1e-183">원하는 tooavoid 로깅이 복제본의 로깅을 제외할 수 있습니다 `local6` 시설 rsyslog 구성에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-183">If you'd like tooavoid this duplicate logging, you can exclude logging of `local6` facility logs in your rsyslog configuration.</span></span> <span data-ttu-id="d1d1e-184">Hello Linux 배포판에 의존 하지만 Ubuntu 14.04 시스템에서 hello 파일 toomodify이 `/etc/rsyslog.d/50-default.conf` hello 줄을 바꿀 수 있습니다 및 `*.*;auth,authpriv.none -/var/log/syslog` 너무`*.*;auth,authpriv,local6.none -/var/log/syslog`합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-184">It depends on hello Linux distro, but on an Ubuntu 14.04 system, hello file toomodify is `/etc/rsyslog.d/50-default.conf` and you can replace hello line `*.*;auth,authpriv.none -/var/log/syslog` too`*.*;auth,authpriv,local6.none -/var/log/syslog`.</span></span> <span data-ttu-id="d1d1e-185">2.3 (2.3.9007)의 hello 최신 핫픽스 릴리스에서이 문제는 해결 되므로 hello 확장 버전 2.3 설정한 경우이 문제가 발생 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-185">This issue is fixed in hello latest hotfix release of 2.3 (2.3.9007), so if you have hello extension version 2.3, this issue should not happen.</span></span> <span data-ttu-id="d1d1e-186">이 VM을 다시 시작 후에 여전히 용어가 들어 문의 hello 최신 핫픽스 버전을 자동으로 설치 되지 않는 문제 해결 하는 데 도움이 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-186">If it still does even after restarting your VM, please contact us and help us troubleshoot why hello latest hotfix version is not installed automatically.</span></span>

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a><span data-ttu-id="d1d1e-187">시나리오 4.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-187">Scenario 4.</span></span> <span data-ttu-id="d1d1e-188">Hello 확장에서 로그 수집을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-188">Stop hello extension from collecting any logs</span></span>

<span data-ttu-id="d1d1e-189">이 섹션에서 수집 toostop hello 확장 기록 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-189">This section describes how toostop hello extension from collecting logs.</span></span> <span data-ttu-id="d1d1e-190">Hello 모니터링 에이전트 프로세스는 이러한 재구성 된 경우에 계속 작동 하 고 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-190">Note that hello monitoring agent process will be still up and running even with this reconfiguration.</span></span> <span data-ttu-id="d1d1e-191">모니터링 에이전트 프로세스를 완전히 toostop hello를 원하는 경우 hello 확장을 사용 하지 않도록 설정 하 여 그렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-191">If you'd like toostop hello monitoring agent process completely, you can do so by disabling hello extension.</span></span> <span data-ttu-id="d1d1e-192">hello 명령 toodisable hello 확장은 `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-192">hello command toodisable hello extension is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span></span>

<span data-ttu-id="d1d1e-193">1단계.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-193">Step 1.</span></span> <span data-ttu-id="d1d1e-194">시나리오 1에 설명 된 hello 콘텐츠로 PrivateConfig.json 이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-194">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="d1d1e-195">콘텐츠를 수행 하는 hello로 PublicConfig.json 라는 다른 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-195">Create another file named PublicConfig.json with hello following content:</span></span>

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


<span data-ttu-id="d1d1e-196">2단계.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-196">Step 2.</span></span> <span data-ttu-id="d1d1e-197">**azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-197">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

## <a name="review-your-data"></a><span data-ttu-id="d1d1e-198">데이터 검토</span><span class="sxs-lookup"><span data-stu-id="d1d1e-198">Review your data</span></span>

<span data-ttu-id="d1d1e-199">hello 성능 및 진단 데이터는 Azure 저장소 테이블에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-199">hello performance and diagnostic data are stored in an Azure Storage table.</span></span> <span data-ttu-id="d1d1e-200">검토 [어떻게 toouse Ruby에서 Azure 테이블 저장소](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn tooaccess hello 저장소의에서 데이터를 hello Azure CLI 스크립트를 사용 하 여 테이블 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-200">Review [How toouse Azure Table Storage from Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn how tooaccess hello data in hello storage table by using Azure CLI scripts.</span></span>

<span data-ttu-id="d1d1e-201">또한 다음 UI 도구 tooaccess hello 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-201">In addition, you can use following UI tools tooaccess hello data:</span></span>

1. <span data-ttu-id="d1d1e-202">Visual Studio 서버 탐색기.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-202">Visual Studio Server Explorer.</span></span> <span data-ttu-id="d1d1e-203">저장소 계정 tooyour 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-203">Go tooyour storage account.</span></span> <span data-ttu-id="d1d1e-204">Hello VM 약 5 분 동안 실행 된 후 4 hello 기본 테이블 표시 됩니다: "LinuxCpu", "LinuxDisk", "LinuxMemory" 및 "Linuxsyslog"입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-204">After hello VM runs for about five minutes, you'll see hello four default tables: “LinuxCpu”, ”LinuxDisk”, ”LinuxMemory”, and ”Linuxsyslog”.</span></span> <span data-ttu-id="d1d1e-205">Hello 테이블 이름 tooview hello 데이터를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-205">Double-click hello table names tooview hello data.</span></span>
1. <span data-ttu-id="d1d1e-206">[Azure 저장소 탐색기](https://azurestorageexplorer.codeplex.com/ "Azure 저장소 탐색기")에 지정된 모든 시스템 데이터.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-206">[Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

![이미지](./media/diagnostic-extension/no1.png)

<span data-ttu-id="d1d1e-208">FileCfg 또는 perfCfg (시나리오 2와 3 단계에서 설명)으로 설정한 경우에 Visual Studio 서버 탐색기 및 Azure 저장소 탐색기 tooview 기본이 아닌 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-208">If you've enabled fileCfg or perfCfg (as described in Scenarios 2 and 3), you can use Visual Studio Server Explorer and Azure Storage Explorer tooview non-default data.</span></span>

## <a name="known-issues"></a><span data-ttu-id="d1d1e-209">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="d1d1e-209">Known issues</span></span>

* <span data-ttu-id="d1d1e-210">hello Rsyslog 정보 및 사용자 지정 로그 파일 스크립팅을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d1e-210">hello Rsyslog information and customer-specified log file can only be accessed via scripting.</span></span>
