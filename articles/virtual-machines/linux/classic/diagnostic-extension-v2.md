---
title: "VM 확장을 사용하여 Linux VM 모니터링 | Microsoft Docs"
description: "Linux 진단 확장을 사용하여 Azure Linux VM의 성능 및 진단 데이터를 모니터링하는 방법을 알아봅니다."
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
ms.openlocfilehash: b8c6e2e22d8478b6e92e7b7942f15d37a840fed3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-linux-diagnostic-extension-to-monitor-the-performance-and-diagnostic-data-of-a-linux-vm"></a><span data-ttu-id="eafab-103">Linux 진단 확장을 사용하여 Linux VM의 성능 및 진단 데이터 모니터링</span><span class="sxs-lookup"><span data-stu-id="eafab-103">Use the Linux Diagnostic Extension to monitor the performance and diagnostic data of a Linux VM</span></span>

<span data-ttu-id="eafab-104">이 문서에서는 Linux 진단 확장 버전 2.3에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-104">This document describes version 2.3 of the Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eafab-105">이 버전은 사용이 중단되었으며 2018년 6월 30일 이후에 언제든지 게시가 취소될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-105">This version is deprecated, and it may be unpublished any time after June 30, 2018.</span></span> <span data-ttu-id="eafab-106">이 버전은 버전 3.0으로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-106">It has been replaced by version 3.0.</span></span> <span data-ttu-id="eafab-107">자세한 내용은 [Linux 진단 확장 버전 3.0에 대한 설명서](../diagnostic-extension.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eafab-107">For more information, see the [documentation for version 3.0 of the Linux Diagnostic Extension](../diagnostic-extension.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="eafab-108">소개</span><span class="sxs-lookup"><span data-stu-id="eafab-108">Introduction</span></span>

<span data-ttu-id="eafab-109">(**참고**: Linux 진단 확장은 [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic)의 오픈 소스이며 확장에 대한 대부분의 최신 정보가 GitHub에 가장 먼저 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-109">(**Note**: The Linux Diagnostic Extension is open-sourced on [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) where the most current information on the extension is first published.</span></span> <span data-ttu-id="eafab-110">[GitHub 페이지](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic)를 가장 먼저 확인하세요.)</span><span class="sxs-lookup"><span data-stu-id="eafab-110">You might want to check the [GitHub page](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) first.)</span></span>

<span data-ttu-id="eafab-111">Linux 진단 확장을 통해 사용자는 Microsoft Azure에서 실행하는 Linux VM을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-111">The Linux Diagnostic Extension helps a user monitor the Linux VMs that are running on Microsoft Azure.</span></span> <span data-ttu-id="eafab-112">제공되는 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-112">It has the following capabilities:</span></span>

* <span data-ttu-id="eafab-113">Linux VM에서 사용자의 저장소 테이블로 진단 및 syslog 정보를 포함하여 시스템 성능 정보를 수집하고 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-113">Collects and uploads the system performance information from the Linux VM to the user's storage table, including diagnostic and syslog information.</span></span>
* <span data-ttu-id="eafab-114">사용자가 수집 및 업로드된 데이터 메트릭을 사용자 지정할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-114">Enables users to customize the data metrics that will be collected and uploaded.</span></span>
* <span data-ttu-id="eafab-115">사용자가 지정된 저장소 테이블에 지정된 로그 파일을 업로드할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-115">Enables users to upload specified log files to a designated storage table.</span></span>

<span data-ttu-id="eafab-116">최신 2.3 버전에는 다음 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-116">In the current version 2.3, the data includes:</span></span>

* <span data-ttu-id="eafab-117">시스템, 보안 및 응용 프로그램 로그를 비롯한 모든 Linux Rsyslog 로그.</span><span class="sxs-lookup"><span data-stu-id="eafab-117">All Linux Rsyslog logs, including system, security, and application logs.</span></span>
* <span data-ttu-id="eafab-118">[System Center 플랫폼 간 솔루션 사이트](https://scx.codeplex.com/wikipage?title=xplatproviders)에 지정된 모든 시스템 데이터.</span><span class="sxs-lookup"><span data-stu-id="eafab-118">All system data that's specified on [the System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
* <span data-ttu-id="eafab-119">사용자가 지정한 로그 파일.</span><span class="sxs-lookup"><span data-stu-id="eafab-119">User-specified log files.</span></span>

<span data-ttu-id="eafab-120">이 확장은 클래식 및 리소스 관리자 배포 모델 둘 다에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-120">This extension works with both the classic and Resource Manager deployment models.</span></span>

### <a name="current-version-of-the-extension-and-deprecation-of-old-versions"></a><span data-ttu-id="eafab-121">확장의 최신 버전 및 이전 버전의 사용 중단</span><span class="sxs-lookup"><span data-stu-id="eafab-121">Current version of the extension and deprecation of old versions</span></span>

<span data-ttu-id="eafab-122">확장의 최신 버전은 **2.3**이며, **모든 이전 버전(2.0, 2.1 및 2.2)은 올해(2017년) 말에 사용이 중단되고 게시되지 않을 예정입니다**.</span><span class="sxs-lookup"><span data-stu-id="eafab-122">The latest version of the extension is **2.3**, and **any old versions (2.0, 2.1, and 2.2) will be deprecated and unpublished by end of this year (2017)**.</span></span> <span data-ttu-id="eafab-123">자동 부 버전 업그레이드가 비활성화된 Linux 진단 확장을 설치한 경우 확장을 제거한 후 자동 부 버전 업그레이드를 활성화하여 다시 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-123">If you installed the Linux Diagnostic extension with automatic minor version upgrade disabled, it's strongly recommended that you uninstall the extension and reinstall it with automatic minor version upgrade enabled.</span></span> <span data-ttu-id="eafab-124">Azure XPLAT CLI 또는 Powershell을 통해 확장을 설치하는 경우 클래식(ASM) VM에서 버전으로 '2.*'를 지정하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-124">On classic (ASM) VMs, you can achieve this by specifying '2.*' as the version if you are installing the extension through Azure XPLAT CLI or Powershell.</span></span> <span data-ttu-id="eafab-125">ARM VM에서 VM 배포 템플릿에 '"autoUpgradeMinorVersion": true'를 포함하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-125">On ARM VMs, you can achieve this by including '"autoUpgradeMinorVersion": true' in the VM deployment template.</span></span> <span data-ttu-id="eafab-126">또한 새로 설치되는 확장에서 자동 부 버전 업그레이드 옵션이 켜져 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-126">Also, any new installation of the extension should have the auto minor version upgrade option turned on.</span></span>

## <a name="enable-the-extension"></a><span data-ttu-id="eafab-127">확장 사용</span><span class="sxs-lookup"><span data-stu-id="eafab-127">Enable the extension</span></span>

<span data-ttu-id="eafab-128">[Azure 포털](https://portal.azure.com/#), Azure PowerShell 또는 Azure CLI 스크립트를 통해 확장을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-128">You can enable this extension by using the [Azure portal](https://portal.azure.com/#), Azure PowerShell, or Azure CLI scripts.</span></span>

<span data-ttu-id="eafab-129">Azure Portal에서 직접 시스템 및 성능 데이터를 보고 구성하려면 다음 [Azure 블로그의 단계](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/)를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="eafab-129">To view and configure the system and performance data directly from the Azure portal, follow [these steps on the Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span></span>

<span data-ttu-id="eafab-130">이 문서는 Azure CLI 명령을 사용하여 확장을 사용하도록 설정하고 구성하는 방법에 중점을 두고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-130">This article focuses on how to enable and configure the extension by using Azure CLI commands.</span></span> <span data-ttu-id="eafab-131">이렇게 하면 저장소 테이블에서 직접 데이터를 읽고 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-131">This allows you to read and view the data directly from the storage table.</span></span>

<span data-ttu-id="eafab-132">여기서 설명된 구성 방법은 Azure 포털에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-132">Note that the configuration methods that are described here won't work for the Azure portal.</span></span> <span data-ttu-id="eafab-133">Azure 포털에서 직접 시스템 및 성능 데이터를 보고 구성하려면 Azure 포털을 통해 확장할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-133">To view and configure the system and performance data directly from the Azure portal, the extension must be enabled through the portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eafab-134">필수 조건</span><span class="sxs-lookup"><span data-stu-id="eafab-134">Prerequisites</span></span>

* <span data-ttu-id="eafab-135">**Azure Linux 에이전트 버전 2.0.6 이상**.</span><span class="sxs-lookup"><span data-stu-id="eafab-135">**Azure Linux Agent version 2.0.6 or later**.</span></span>

  <span data-ttu-id="eafab-136">대부분의 Azure VM Linux 갤러리 이미지에는 2.0.6 이후 버전이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-136">Note that most Azure VM Linux gallery images include version 2.0.6 or later.</span></span> <span data-ttu-id="eafab-137">**WAAgent -version** 을 실행하여 VM에 설치된 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-137">You can run **WAAgent -version** to confirm which version is installed on the VM.</span></span> <span data-ttu-id="eafab-138">VM 2.0.6보다 이전 버전을 실행하는 경우 다음 [GitHub의 이러한 지침](https://github.com/Azure/WALinuxAgent "지침") 을 따라 이를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-138">If the VM is running a version that's earlier than 2.0.6, you can follow [these instructions on GitHub](https://github.com/Azure/WALinuxAgent "instructions") to update it.</span></span>
* <span data-ttu-id="eafab-139">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="eafab-139">**Azure CLI**.</span></span> <span data-ttu-id="eafab-140">[CLI 설치 지침](../../../cli-install-nodejs.md) 을 따라 컴퓨터에 Azure CLI 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-140">Follow [this guidance for installing CLI](../../../cli-install-nodejs.md) to set up the Azure CLI environment on your machine.</span></span> <span data-ttu-id="eafab-141">Azure CLI가 설치되었으면 명령줄 인터페이스(Bash, 터미널, 명령 프롬프트)에서 **azure** 명령을 사용하여 Azure CLI 명령에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-141">After Azure CLI is installed, you can use the **azure** command from your command-line interface (Bash, Terminal, or command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="eafab-142">예:</span><span class="sxs-lookup"><span data-stu-id="eafab-142">For example:</span></span>

  * <span data-ttu-id="eafab-143">자세한 도움말 정보는 **azure vm extension set –help** 를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-143">Run **azure vm extension set --help** for detailed help information.</span></span>
  * <span data-ttu-id="eafab-144">Azure에 로그인하려면 **azure login** 을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-144">Run **azure login** to sign in to Azure.</span></span>
  * <span data-ttu-id="eafab-145">Azure에 있는 모든 가상 컴퓨터를 나열하려면 **azure vm list** 를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-145">Run **azure vm list** to list all the virtual machines that you have on Azure.</span></span>
* <span data-ttu-id="eafab-146">데이터를 저장할 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-146">A storage account to store the data.</span></span> <span data-ttu-id="eafab-147">데이터를 저장소에 업로드하려면 이전에 생성된 저장소 계정 이름과 선택키가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-147">You will need a storage account name that was created previously and an access key to upload the data to your storage.</span></span>

## <a name="use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension"></a><span data-ttu-id="eafab-148">Azure CLI 명령을 사용하여 Linux 진단 확장을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="eafab-148">Use the Azure CLI command to enable the Linux Diagnostic Extension</span></span>

### <a name="scenario-1-enable-the-extension-with-the-default-data-set"></a><span data-ttu-id="eafab-149">시나리오 1.</span><span class="sxs-lookup"><span data-stu-id="eafab-149">Scenario 1.</span></span> <span data-ttu-id="eafab-150">기본 데이터 집합으로 확장을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="eafab-150">Enable the extension with the default data set</span></span>

<span data-ttu-id="eafab-151">버전 2.3 이상의 경우 수집되는 기본 데이터에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-151">In version 2.3 or later, the default data that will be collected includes:</span></span>

* <span data-ttu-id="eafab-152">모든 Rsyslog 정보(시스템, 보안 및 응용 프로그램 로그 포함)</span><span class="sxs-lookup"><span data-stu-id="eafab-152">All Rsyslog information (including system, security, and application logs).</span></span>  
* <span data-ttu-id="eafab-153">기본 시스템 데이터의 핵심 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-153">A core set of basis system data.</span></span> <span data-ttu-id="eafab-154">전체 데이터 집합은 [System Center 플랫폼 간 솔루션 사이트](https://scx.codeplex.com/wikipage?title=xplatproviders)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-154">Note that the full data set is described on the [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
  <span data-ttu-id="eafab-155">추가 데이터를 사용하도록 설정하려는 경우 시나리오 2와 3의 단계를 계속 진행하세요.</span><span class="sxs-lookup"><span data-stu-id="eafab-155">If you want to enable extra data, continue with the steps in Scenarios 2 and 3.</span></span>

<span data-ttu-id="eafab-156">1단계.</span><span class="sxs-lookup"><span data-stu-id="eafab-156">Step 1.</span></span> <span data-ttu-id="eafab-157">다음과 같은 내용으로 PrivateConfig.json라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-157">Create a file named PrivateConfig.json with the following content:</span></span>

    {
        "storageAccountName" : "the storage account to receive data",
        "storageAccountKey" : "the key of the account"
    }

<span data-ttu-id="eafab-158">2단계.</span><span class="sxs-lookup"><span data-stu-id="eafab-158">Step 2.</span></span> <span data-ttu-id="eafab-159">**azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-159">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span></span>

### <a name="scenario-2-customize-the-performance-monitor-metrics"></a><span data-ttu-id="eafab-160">시나리오 2.</span><span class="sxs-lookup"><span data-stu-id="eafab-160">Scenario 2.</span></span> <span data-ttu-id="eafab-161">성능 모니터 메트릭 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="eafab-161">Customize the performance monitor metrics</span></span>

<span data-ttu-id="eafab-162">이 섹션은 성능 및 진단 데이터 테이블을 사용자가 지정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-162">This section describes how to customize the performance and diagnostic data table.</span></span>

<span data-ttu-id="eafab-163">1단계.</span><span class="sxs-lookup"><span data-stu-id="eafab-163">Step 1.</span></span> <span data-ttu-id="eafab-164">시나리오 1에서 설명한 내용으로 PrivateConfig.json이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-164">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="eafab-165">또한 PublicConfig.json이라는 파일도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-165">Also create a file named PublicConfig.json.</span></span> <span data-ttu-id="eafab-166">수집하려는 특정 데이터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-166">Specify the particular data you want to collect.</span></span>

<span data-ttu-id="eafab-167">지원되는 모든 공급자 및 변수에 대해서는 [System Center 플랫폼 간 솔루션 사이트](https://scx.codeplex.com/wikipage?title=xplatproviders)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eafab-167">For all supported providers and variables, reference the [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span> <span data-ttu-id="eafab-168">스크립트에 더 많은 쿼리를 추가하여 여러 쿼리를 포함하고 여러 테이블에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-168">You can have multiple queries and store them in multiple tables by appending more queries to the script.</span></span>

<span data-ttu-id="eafab-169">기본적으로 Rsyslog 데이터는 항상 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-169">By default, the Rsyslog data is always collected.</span></span>

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


<span data-ttu-id="eafab-170">2단계.</span><span class="sxs-lookup"><span data-stu-id="eafab-170">Step 2.</span></span> <span data-ttu-id="eafab-171">**azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-171">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

### <a name="scenario-3-upload-your-own-log-files"></a><span data-ttu-id="eafab-172">시나리오 3.</span><span class="sxs-lookup"><span data-stu-id="eafab-172">Scenario 3.</span></span> <span data-ttu-id="eafab-173">고유한 로그 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="eafab-173">Upload your own log files</span></span>

<span data-ttu-id="eafab-174">이 섹션은 저장소 계정에 특정 로그 파일을 수집하고 업로드하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-174">This section describes how to collect and upload specific log files to your storage account.</span></span> <span data-ttu-id="eafab-175">로그 파일의 경로와 로그를 저장하고자 하는 테이블 이름을 모두 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-175">You need to specify both the path to your log file and the name of the table where you want to store your log.</span></span> <span data-ttu-id="eafab-176">스크립트에 여러 파일/테이블 항목을 추가하여 여러 로그 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-176">You can create multiple log files by adding multiple file/table entries to the script.</span></span>

<span data-ttu-id="eafab-177">1단계.</span><span class="sxs-lookup"><span data-stu-id="eafab-177">Step 1.</span></span> <span data-ttu-id="eafab-178">시나리오 1에서 설명한 내용으로 PrivateConfig.json이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-178">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="eafab-179">그런 다음 다음과 같은 내용으로 PublicConfig.json이라는 다른 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-179">Then create another file named PublicConfig.json with the following content:</span></span>

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

<span data-ttu-id="eafab-180">2단계.</span><span class="sxs-lookup"><span data-stu-id="eafab-180">Step 2.</span></span> <span data-ttu-id="eafab-181">`azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-181">Run `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span></span>

<span data-ttu-id="eafab-182">2.3 이전의 확장 버전에서 이 설정을 사용하면 `/var/log/mysql.err`에 기록된 모든 로그가 `/var/log/syslog`(또는 Linux 배포판에 따라 `/var/log/messages`)와 중복될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-182">Note that with this setting on the extension versions prior to 2.3, all logs written to `/var/log/mysql.err` might be duplicated to `/var/log/syslog` (or `/var/log/messages` depending on the Linux distro) as well.</span></span> <span data-ttu-id="eafab-183">중복 로깅을 피하려면 rsyslog 구성에서 `local6` 기능 로깅을 제외하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-183">If you'd like to avoid this duplicate logging, you can exclude logging of `local6` facility logs in your rsyslog configuration.</span></span> <span data-ttu-id="eafab-184">Linux 배포판에 따라 다르지만 Ubuntu 14.04 시스템에서는 `/etc/rsyslog.d/50-default.conf` 파일을 수정해야 하며 `*.*;auth,authpriv.none -/var/log/syslog` 줄을 `*.*;auth,authpriv,local6.none -/var/log/syslog` 줄로 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-184">It depends on the Linux distro, but on an Ubuntu 14.04 system, the file to modify is `/etc/rsyslog.d/50-default.conf` and you can replace the line `*.*;auth,authpriv.none -/var/log/syslog` to `*.*;auth,authpriv,local6.none -/var/log/syslog`.</span></span> <span data-ttu-id="eafab-185">최신 핫픽스 릴리스 2.3 (2.3.9007) 릴리스에서 이 문제가 해결되므로 확장 버전 2.3을 가졌다면 이 문제는 발생하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-185">This issue is fixed in the latest hotfix release of 2.3 (2.3.9007), so if you have the extension version 2.3, this issue should not happen.</span></span> <span data-ttu-id="eafab-186">VM을 다시 시작한 후에도 여전히 그런 경우 문의하시면 최신 핫픽스 버전이 자동으로 설치되지 않는 원인을 해결해 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-186">If it still does even after restarting your VM, please contact us and help us troubleshoot why the latest hotfix version is not installed automatically.</span></span>

### <a name="scenario-4-stop-the-extension-from-collecting-any-logs"></a><span data-ttu-id="eafab-187">시나리오 4.</span><span class="sxs-lookup"><span data-stu-id="eafab-187">Scenario 4.</span></span> <span data-ttu-id="eafab-188">모든 로그 수집에서 확장 중지</span><span class="sxs-lookup"><span data-stu-id="eafab-188">Stop the extension from collecting any logs</span></span>

<span data-ttu-id="eafab-189">이 섹션에서는 로그 수집에서 확장을 중지하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-189">This section describes how to stop the extension from collecting logs.</span></span> <span data-ttu-id="eafab-190">이러한 재구성에도 모니터링 에이전트 프로세스는 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-190">Note that the monitoring agent process will be still up and running even with this reconfiguration.</span></span> <span data-ttu-id="eafab-191">모니터링 에이전트 프로세스는 완전히 중지하려는 경우 확장을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-191">If you'd like to stop the monitoring agent process completely, you can do so by disabling the extension.</span></span> <span data-ttu-id="eafab-192">확장을 사용하지 않도록 설정하는 명령은 `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`입니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-192">The command to disable the extension is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span></span>

<span data-ttu-id="eafab-193">1단계.</span><span class="sxs-lookup"><span data-stu-id="eafab-193">Step 1.</span></span> <span data-ttu-id="eafab-194">시나리오 1에서 설명한 내용으로 PrivateConfig.json이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-194">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="eafab-195">다음과 같은 내용으로 PublicConfig.json이라는 다른 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-195">Create another file named PublicConfig.json with the following content:</span></span>

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


<span data-ttu-id="eafab-196">2단계.</span><span class="sxs-lookup"><span data-stu-id="eafab-196">Step 2.</span></span> <span data-ttu-id="eafab-197">**azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-197">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

## <a name="review-your-data"></a><span data-ttu-id="eafab-198">데이터 검토</span><span class="sxs-lookup"><span data-stu-id="eafab-198">Review your data</span></span>

<span data-ttu-id="eafab-199">성능 및 진단 데이터는 Azure 저장소 테이블에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-199">The performance and diagnostic data are stored in an Azure Storage table.</span></span> <span data-ttu-id="eafab-200">Azure CLI 스크립트를 사용하여 저장소 테이블의 데이터에 액세스 하는 방법을 알아보려면 [Ruby에서 Azure 테이블 저장소를 사용하는 방법](../../../cosmos-db/table-storage-how-to-use-ruby.md) 을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="eafab-200">Review [How to use Azure Table Storage from Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) to learn how to access the data in the storage table by using Azure CLI scripts.</span></span>

<span data-ttu-id="eafab-201">또한 다음 UI 도구를 사용하여 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-201">In addition, you can use following UI tools to access the data:</span></span>

1. <span data-ttu-id="eafab-202">Visual Studio 서버 탐색기.</span><span class="sxs-lookup"><span data-stu-id="eafab-202">Visual Studio Server Explorer.</span></span> <span data-ttu-id="eafab-203">저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-203">Go to your storage account.</span></span> <span data-ttu-id="eafab-204">VM을 약 5분 정도 실행하고 나면 "LinuxCpu", "LinuxDisk", "LinuxMemory" 및 "Linuxsyslog" 등 네 개의 기본 테이블이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-204">After the VM runs for about five minutes, you'll see the four default tables: “LinuxCpu”, ”LinuxDisk”, ”LinuxMemory”, and ”Linuxsyslog”.</span></span> <span data-ttu-id="eafab-205">데이터를 볼 테이블 이름을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-205">Double-click the table names to view the data.</span></span>
1. <span data-ttu-id="eafab-206">[Azure 저장소 탐색기](https://azurestorageexplorer.codeplex.com/ "Azure 저장소 탐색기")에 지정된 모든 시스템 데이터.</span><span class="sxs-lookup"><span data-stu-id="eafab-206">[Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

![이미지](./media/diagnostic-extension/no1.png)

<span data-ttu-id="eafab-208">(시나리오 2와 3에 설명된 대로) FileCfg 또는 perfCfg를 사용하도록 설정한다면, 기본이 아닌 데이터를 Visual Studio 서버 탐색기 및 Azure 저장소 탐색기를 사용하여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-208">If you've enabled fileCfg or perfCfg (as described in Scenarios 2 and 3), you can use Visual Studio Server Explorer and Azure Storage Explorer to view non-default data.</span></span>

## <a name="known-issues"></a><span data-ttu-id="eafab-209">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="eafab-209">Known issues</span></span>

* <span data-ttu-id="eafab-210">스크립팅을 통해 Rsyslog 정보 및 고객이 지정한 로그 파일에만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafab-210">The Rsyslog information and customer-specified log file can only be accessed via scripting.</span></span>
