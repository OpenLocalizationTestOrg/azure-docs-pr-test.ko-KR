---
title: "aaaAzure 계산-Linux 진단 확장 | Microsoft Docs"
description: "Tooconfigure는 Azure Linux 진단 확장 (했다) toocollect 메트릭 hello 방법과 Azure에서 실행 중인 Linux Vm에서 이벤트를 기록 합니다."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a><span data-ttu-id="41989-103">Linux 진단 확장 toomonitor 메트릭 및 로그를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="41989-103">Use Linux Diagnostic Extension toomonitor metrics and logs</span></span>

<span data-ttu-id="41989-104">이 문서에서는 버전 3.0 이상 hello Linux 진단 확장을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-104">This document describes version 3.0 and newer of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41989-105">2.3 이하 버전에 대한 내용은 [이 문서](./classic/diagnostic-extension-v2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41989-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="41989-106">소개</span><span class="sxs-lookup"><span data-stu-id="41989-106">Introduction</span></span>

<span data-ttu-id="41989-107">Linux 진단 확장 hello Microsoft Azure에서 실행 되는 Linux VM의 사용자 모니터 hello 상태는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-107">hello Linux Diagnostic Extension helps a user monitor hello health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="41989-108">기능을 수행 하는 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-108">It has hello following capabilities:</span></span>

* <span data-ttu-id="41989-109">Hello VM에서에서 시스템 성능 메트릭을 수집 하 고 지정 된 저장소 계정에 특정 테이블에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-109">Collects system performance metrics from hello VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="41989-110">Syslog에서 이벤트 로그를 검색 하 고 저장소 계정을 지정 하는 hello의 특정 테이블에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-110">Retrieves log events from syslog and stores them in a specific table in hello designated storage account.</span></span>
* <span data-ttu-id="41989-111">수집 되 고 업로드 하는 사용자가 toocustomize hello 데이터 메트릭을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-111">Enables users toocustomize hello data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="41989-112">사용자가 toocustomize hello syslog 기능 및 수집 되 고 업로드 하는 이벤트의 심각도 수준이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-112">Enables users toocustomize hello syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="41989-113">사용자가 tooupload 지정 된 로그 파일 tooa 지정 된 저장소 테이블을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-113">Enables users tooupload specified log files tooa designated storage table.</span></span>
* <span data-ttu-id="41989-114">저장소 계정을 지정 하는 hello에 메트릭 및 로그 이벤트 tooarbitrary EventHub 끝점 및 JSON 형식의 blob를 전송 지원.</span><span class="sxs-lookup"><span data-stu-id="41989-114">Supports sending metrics and log events tooarbitrary EventHub endpoints and JSON-formatted blobs in hello designated storage account.</span></span>

<span data-ttu-id="41989-115">이 확장은 Azure 배포 모델 모두에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-hello-extension-in-your-vm"></a><span data-ttu-id="41989-116">VM에서 hello 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-116">Installing hello extension in your VM</span></span>

<span data-ttu-id="41989-117">Hello Azure PowerShell cmdlet, Azure CLI 스크립트 또는 Azure 배포 템플릿을 사용 하 여이 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-117">You can enable this extension by using hello Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="41989-118">자세한 내용은 [확장 기능](./extensions-features.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41989-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="41989-119">hello Azure 포털은 했다 3.0 구성 하거나 사용된 tooenable 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-119">hello Azure portal cannot be used tooenable or configure LAD 3.0.</span></span> <span data-ttu-id="41989-120">대신 버전 2.3을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="41989-121">Azure 포털 그래프 및 경고 hello 확장의 두 버전의 데이터로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-121">Azure portal graphs and alerts work with data from both versions of hello extension.</span></span>

<span data-ttu-id="41989-122">이러한 설치 지침 및 [다운로드 가능한 샘플 구성](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json)은 다음을 수행할 수 있도록 LAD 3.0을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="41989-123">캡처 및 저장소 했다 2.3;에서 제공 하는 대로 동일한 메트릭을 hello합니다</span><span class="sxs-lookup"><span data-stu-id="41989-123">capture and store hello same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="41989-124">유용한 메트릭 집합을 파일 시스템, 새 tooLAD 3.0; 캡처</span><span class="sxs-lookup"><span data-stu-id="41989-124">capture a useful set of file system metrics, new tooLAD 3.0;</span></span>
* <span data-ttu-id="41989-125">캡처 hello 기본 syslog 수집 했다 2.3;으로 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="41989-125">capture hello default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="41989-126">차트 및 VM 메트릭에 대해 경고에 대 한 Azure 포털 환경 hello를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-126">enable hello Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="41989-127">다운로드 가능한 구성 hello은 예 시일 뿐입니다. toosuit 수정 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-127">hello downloadable configuration is just an example; modify it toosuit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="41989-128">필수 조건</span><span class="sxs-lookup"><span data-stu-id="41989-128">Prerequisites</span></span>

* <span data-ttu-id="41989-129">**Azure Linux 에이전트 버전 2.2.0 이상**.</span><span class="sxs-lookup"><span data-stu-id="41989-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="41989-130">대부분의 Azure VM Linux 갤러리 이미지에는 2.2.7 이후 버전이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="41989-131">실행 `/usr/sbin/waagent -version` tooconfirm hello 버전 hello VM에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-131">Run `/usr/sbin/waagent -version` tooconfirm hello version installed on hello VM.</span></span> <span data-ttu-id="41989-132">Hello VM은 이전 버전의 hello 게스트 에이전트를 실행 하는 경우에 따라 [이러한 지침](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-132">If hello VM is running an older version of hello guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate it.</span></span>
* <span data-ttu-id="41989-133">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="41989-133">**Azure CLI**.</span></span> <span data-ttu-id="41989-134">[Hello Azure CLI 2.0 설정](https://docs.microsoft.com/cli/azure/install-azure-cli) 환경 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-134">[Set up hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="41989-135">아직 없는 경우 wget 명령 hello: 실행 `sudo apt-get install wget`합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-135">hello wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="41989-136">기존 Azure 구독 및 기존 저장소 계정 내 toostore hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-136">An existing Azure subscription and an existing storage account within it toostore hello data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="41989-137">샘플 설치</span><span class="sxs-lookup"><span data-stu-id="41989-137">Sample installation</span></span>

<span data-ttu-id="41989-138">처음 세 줄 hello hello에 올바른 매개 변수를 채웁니다 루트로이 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-138">Fill in hello correct parameters on hello first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="41989-139">hello 샘플 구성에 대 한 hello URL 및 해당 콘텐츠를 주제 toochange 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-139">hello URL for hello sample configuration, and its contents, are subject toochange.</span></span> <span data-ttu-id="41989-140">Hello 포털 설정 JSON 파일의 복사본을 다운로드 하 고 필요에 따라 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-140">Download a copy of hello portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="41989-141">템플릿 또는 자동화를 생성할 때마다 해당 URL을 다운로드하는 대신 고유한 복사본을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-hello-extension-settings"></a><span data-ttu-id="41989-142">Hello 확장 프로그램 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="41989-142">Updating hello extension settings</span></span>

<span data-ttu-id="41989-143">Protected 또는 공용 설정을 변경한 후 배포할지 toohello VM을 실행 하 여 hello 동일한 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-143">After you've changed your Protected or Public settings, deploy them toohello VM by running hello same command.</span></span> <span data-ttu-id="41989-144">Hello 설정에서 변경 된 사항이 업데이트 hello 설정은 toohello 확장을 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-144">If anything changed in hello settings, hello updated settings are sent toohello extension.</span></span> <span data-ttu-id="41989-145">Hello 구성 다시 로드 하 고 자체적으로 다시 시작 하는 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-145">LAD reloads hello configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-hello-extension"></a><span data-ttu-id="41989-146">Hello 확장의 이전 버전에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="41989-146">Migration from previous versions of hello extension</span></span>

<span data-ttu-id="41989-147">hello hello 확장의 최신 버전은 **3.0**합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-147">hello latest version of hello extension is **3.0**.</span></span> <span data-ttu-id="41989-148">**모든 이전 버전(2.x)은 사용되지 않으며 2018년 7월 31일부터는 게시되지 않을 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="41989-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41989-149">이 확장 프로그램에서는 hello 확장의 주요 변경 내용 toohello 구성을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-149">This extension introduces breaking changes toohello configuration of hello extension.</span></span> <span data-ttu-id="41989-150">한 이러한 변경의 hello 확장; tooimprove hello 보안 결과적으로, 이전 버전과 호환성 2.x 하지 관리할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-150">One such change was made tooimprove hello security of hello extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="41989-151">또한이 확장에 대 한 hello 확장 게시자는 hello 2.x 버전에 대 한 hello 게시자와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="41989-151">Also, hello Extension Publisher for this extension is different than hello publisher for hello 2.x versions.</span></span>
>
> <span data-ttu-id="41989-152">2.x toothis 새 버전의 hello 확장 프로그램에서 toomigrate, (hello 이전 게시자 이름에서) 이전 확장명 hello 다음 버전 3 hello 확장의 설치 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-152">toomigrate from 2.x toothis new version of hello extension, you must uninstall hello old extension (under hello old publisher name), then install version 3 of hello extension.</span></span>

<span data-ttu-id="41989-153">권장 사항:</span><span class="sxs-lookup"><span data-stu-id="41989-153">Recommendations:</span></span>

* <span data-ttu-id="41989-154">사용 하도록 설정 하는 자동으로 부 버전 업그레이드를 hello 확장을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-154">Install hello extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="41989-155">클래식 배포 모델 Vm에 Azure XPLAT CLI 또는 Powershell을 통해 hello 확장을 설치 하는 경우 '3.*' hello 버전으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-155">On classic deployment model VMs, specify '3.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="41989-156">Azure 리소스 관리자 배포에서 Vm 모델을 포함 ' "autoUpgradeMinorVersion": true' hello VM 배포 템플릿에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span>
* <span data-ttu-id="41989-157">LAD 3.0에 대해 새 저장소 계정 또는 다른 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="41989-158">LAD 2.3과 LAD 3.0 간에 다음과 같은 몇 가지 사소한 비호환성 문제가 있어 계정 공유에 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="41989-159">LAD 3.0은 syslog 이벤트를 이름이 다른 테이블에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="41989-160">에 대 한 문자열 hello counterSpecifier `builtin` 메트릭 했다 3.0에서 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="41989-160">hello counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="41989-161">보호 설정</span><span class="sxs-lookup"><span data-stu-id="41989-161">Protected settings</span></span>

<span data-ttu-id="41989-162">이 구성 정보 집합에는 공용 보기로부터 보호해야 하는 중요한 정보(예: 저장소 자격 증명)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="41989-163">이러한 설정은 전송 된 tooand hello 확장 암호화 된 형식에 의해 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-163">These settings are transmitted tooand stored by hello extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="41989-164">이름</span><span class="sxs-lookup"><span data-stu-id="41989-164">Name</span></span> | <span data-ttu-id="41989-165">값</span><span class="sxs-lookup"><span data-stu-id="41989-165">Value</span></span>
---- | -----
<span data-ttu-id="41989-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="41989-166">storageAccountName</span></span> | <span data-ttu-id="41989-167">hello hello 저장소 계정의 이름으로 hello 확장에 의해 데이터가 쓰여집니다.</span><span class="sxs-lookup"><span data-stu-id="41989-167">hello name of hello storage account in which data is written by hello extension.</span></span>
<span data-ttu-id="41989-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="41989-168">storageAccountEndPoint</span></span> | <span data-ttu-id="41989-169">(선택 사항) hello 끝점을 식별 하는 hello 저장소 계정이 존재 하는 hello 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-169">(optional) hello endpoint identifying hello cloud in which hello storage account exists.</span></span> <span data-ttu-id="41989-170">했다 toohello Azure 공용 클라우드에서 기본적으로이 설정이 없으면 `https://core.windows.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-170">If this setting is absent, LAD defaults toohello Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="41989-171">독일 Azure, Azure Government 또는 Azure 중국에 저장소 계정을 toouse 그에 따라이 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-171">toouse a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="41989-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="41989-172">storageAccountSasToken</span></span> | <span data-ttu-id="41989-173">[계정 SAS 토큰](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) Blob 및 테이블 서비스에 대 한 (`ss='bt'`), 해당 toocontainers 및 개체 (`srt='co'`), 어떤 부여 추가, 생성, 목록, 업데이트 및 쓰기 권한이 (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="41989-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable toocontainers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="41989-174">수행 *하지* hello 앞에 오는 물음표 (?)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-174">Do *not* include hello leading question-mark (?).</span></span>
<span data-ttu-id="41989-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="41989-175">mdsdHttpProxy</span></span> | <span data-ttu-id="41989-176">(선택 사항) HTTP 프록시는 데 필요한 정보 tooenable hello 확장 tooconnect toohello 저장소 계정 및 끝점을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-176">(optional) HTTP proxy information needed tooenable hello extension tooconnect toohello specified storage account and endpoint.</span></span>
<span data-ttu-id="41989-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="41989-177">sinksConfig</span></span> | <span data-ttu-id="41989-178">(선택 사항) 대체 대상 toowhich 메트릭 및 이벤트의 세부 정보를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-178">(optional) Details of alternative destinations toowhich metrics and events can be delivered.</span></span> <span data-ttu-id="41989-179">hello hello 확장이 지 원하는 각 데이터 싱크에 대 한 특정 세부 정보는 다음에 나오는 hello 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-179">hello specific details of each data sink supported by hello extension are covered in hello sections that follow.</span></span>

<span data-ttu-id="41989-180">Hello Azure 포털을 통해 필요한 hello SAS 토큰을 쉽게 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-180">You can easily construct hello required SAS token through hello Azure portal.</span></span>

1. <span data-ttu-id="41989-181">Hello 일반적인 용도의 스토리지 계정 toowhich hello 확장 toowrite 원하는 선택</span><span class="sxs-lookup"><span data-stu-id="41989-181">Select hello general-purpose storage account toowhich you want hello extension toowrite</span></span>
1. <span data-ttu-id="41989-182">"공유 액세스 서명" hello 왼쪽된 메뉴의 hello 설정 부분에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-182">Select "Shared access signature" from hello Settings part of hello left menu</span></span>
1. <span data-ttu-id="41989-183">앞에서 설명한 대로 hello 적절 한 섹션을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="41989-183">Make hello appropriate sections as previously described</span></span>
1. <span data-ttu-id="41989-184">Hello "생성 SAS" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-184">Click hello "Generate SAS" button.</span></span>

![이미지](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="41989-186">복사 hello hello storageAccountSasToken 필드로; SAS 생성 hello 앞에 오는 물음표를 제거 ("?").</span><span class="sxs-lookup"><span data-stu-id="41989-186">Copy hello generated SAS into hello storageAccountSasToken field; remove hello leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="41989-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="41989-187">sinksConfig</span></span>

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

<span data-ttu-id="41989-188">이 선택적 섹션이 toowhich hello 확장 보냅니다 수집한 정보는 hello 기타 대상을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-188">This optional section defines additional destinations toowhich hello extension sends hello information it collects.</span></span> <span data-ttu-id="41989-189">hello "sink" 배열에 각각의 추가 데이터 싱크에 대 한 개체를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-189">hello "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="41989-190">"type" 특성을 결정 하는 hello hello hello 개체의 다른 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-190">hello "type" attribute determines hello other attributes in hello object.</span></span>

<span data-ttu-id="41989-191">요소</span><span class="sxs-lookup"><span data-stu-id="41989-191">Element</span></span> | <span data-ttu-id="41989-192">값</span><span class="sxs-lookup"><span data-stu-id="41989-192">Value</span></span>
------- | -----
<span data-ttu-id="41989-193">name</span><span class="sxs-lookup"><span data-stu-id="41989-193">name</span></span> | <span data-ttu-id="41989-194">Hello 확장 구성의 다른 곳에서 toorefer toothis 싱크를 사용 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-194">A string used toorefer toothis sink elsewhere in hello extension configuration.</span></span>
<span data-ttu-id="41989-195">type</span><span class="sxs-lookup"><span data-stu-id="41989-195">type</span></span> | <span data-ttu-id="41989-196">정의 되 고 싱크의 hello 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-196">hello type of sink being defined.</span></span> <span data-ttu-id="41989-197">이 형식의 인스턴스 (있는 경우) 다른 값을 hello을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-197">Determines hello other values (if any) in instances of this type.</span></span>

<span data-ttu-id="41989-198">Hello Linux 진단 확장의 버전 3.0에는 두 싱크 유형을 지원: EventHub, 및 JsonBlob 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-198">Version 3.0 of hello Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="hello-eventhub-sink"></a><span data-ttu-id="41989-199">hello EventHub 싱크</span><span class="sxs-lookup"><span data-stu-id="41989-199">hello EventHub sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

<span data-ttu-id="41989-200">hello "sasURL" 항목 포함 hello hello 이벤트 허브 toowhich 데이터에 대 한 SAS 토큰을 포함 한 전체 URL을 게시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-200">hello "sasURL" entry contains hello full URL, including SAS token, for hello Event Hub toowhich data should be published.</span></span> <span data-ttu-id="41989-201">했다는 hello 송신 클레임을 사용 하는 정책을 명명 SAS 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-201">LAD requires a SAS naming a policy that enables hello Send claim.</span></span> <span data-ttu-id="41989-202">예제:</span><span class="sxs-lookup"><span data-stu-id="41989-202">An example:</span></span>

* <span data-ttu-id="41989-203">호출된 Event Hubs 네임스페이스 만들기`contosohub`</span><span class="sxs-lookup"><span data-stu-id="41989-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="41989-204">호출 하는 hello 네임 스페이스에서 이벤트 허브를 만듭니다.`syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="41989-204">Create an Event Hub in hello namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="41989-205">Hello 라는 이벤트 허브에서 공유 액세스 정책을 만들고 `writer` 하면 송신 클레임 hello는</span><span class="sxs-lookup"><span data-stu-id="41989-205">Create a Shared access policy on hello Event Hub named `writer` that enables hello Send claim</span></span>

<span data-ttu-id="41989-206">만든 경우 SAS 좋은 2018, 년 1 월 1 UTC 자정까지 hello sasURL 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-206">If you created a SAS good until midnight UTC on January 1, 2018, hello sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="41989-207">Event Hubs에 대한 SAS 토큰을 생성하는 방법에 대한 자세한 내용은 [이 웹 페이지](../../event-hubs/event-hubs-authentication-and-security-model-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41989-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="hello-jsonblob-sink"></a><span data-ttu-id="41989-208">hello JsonBlob 싱크</span><span class="sxs-lookup"><span data-stu-id="41989-208">hello JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="41989-209">데이터 전송 tooa JsonBlob 싱크는 Azure 저장소의 blob에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-209">Data directed tooa JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="41989-210">각 LAD 인스턴스는 매시간 각 싱크 이름에 대한 Blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41989-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="41989-211">각 Blob에는 항상 구문상 유효한 JSON 배열의 개체가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="41989-212">새 항목 toohello 배열을 추가 원자적으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-212">New entries are atomically added toohello array.</span></span> <span data-ttu-id="41989-213">Blob 이름이 hello 싱크 hello 사용 하 여 컨테이너에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-213">Blobs are stored in a container with hello same name as hello sink.</span></span> <span data-ttu-id="41989-214">blob 컨테이너 이름은 JsonBlob 싱크 toohello 이름에 대 한 Azure 저장소 규칙 hello: ASCII 소문자 영숫자와 또는 대시만 3에서 63 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-214">hello Azure storage rules for blob container names apply toohello names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="41989-215">공용 설정</span><span class="sxs-lookup"><span data-stu-id="41989-215">Public settings</span></span>

<span data-ttu-id="41989-216">이 구조는 hello 확장에 의해 수집 된 hello 정보를 제어 하는 설정의 다양 한 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-216">This structure contains various blocks of settings that control hello information collected by hello extension.</span></span> <span data-ttu-id="41989-217">각 설정은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-217">Each setting is optional.</span></span> <span data-ttu-id="41989-218">`ladCfg`를 지정할 경우 `StorageAccount`도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="41989-219">요소</span><span class="sxs-lookup"><span data-stu-id="41989-219">Element</span></span> | <span data-ttu-id="41989-220">값</span><span class="sxs-lookup"><span data-stu-id="41989-220">Value</span></span>
------- | -----
<span data-ttu-id="41989-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="41989-221">StorageAccount</span></span> | <span data-ttu-id="41989-222">hello hello 저장소 계정의 이름으로 hello 확장에 의해 데이터가 쓰여집니다.</span><span class="sxs-lookup"><span data-stu-id="41989-222">hello name of hello storage account in which data is written by hello extension.</span></span> <span data-ttu-id="41989-223">해야 hello에 지정 되어 이름과 같은 이름을 hello [보호 설정을](#protected-settings)합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-223">Must be hello same name as is specified in hello [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="41989-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="41989-224">mdsdHttpProxy</span></span> | <span data-ttu-id="41989-225">(선택 사항) Hello와 같이 동일한 [보호 설정을](#protected-settings)합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-225">(optional) Same as in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="41989-226">hello 공개 값이 경우 hello 개인 값으로 재정의 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-226">hello public value is overridden by hello private value, if set.</span></span> <span data-ttu-id="41989-227">Hello에 암호와 같은 암호를 포함 하는 프록시 설정을 [보호 설정을](#protected-settings)합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-227">Place proxy settings that contain a secret, such as a password, in hello [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="41989-228">hello 나머지 요소는 hello 다음 섹션에서에서 자세히 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-228">hello remaining elements are described in detail in hello following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="41989-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="41989-229">ladCfg</span></span>

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

<span data-ttu-id="41989-230">이 선택적 구조 컨트롤 hello 수집 메트릭 및 배달 toohello Azure 메트릭 서비스와 tooother 데이터에 대 한 로그 싱크 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-230">This optional structure controls hello gathering of metrics and logs for delivery toohello Azure Metrics service and tooother data sinks.</span></span> <span data-ttu-id="41989-231">`performanceCounters`나 `syslogEvents` 또는 둘 다 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="41989-232">Hello를 지정 해야 `metrics` 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-232">You must specify hello `metrics` structure.</span></span>

<span data-ttu-id="41989-233">요소</span><span class="sxs-lookup"><span data-stu-id="41989-233">Element</span></span> | <span data-ttu-id="41989-234">값</span><span class="sxs-lookup"><span data-stu-id="41989-234">Value</span></span>
------- | -----
<span data-ttu-id="41989-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="41989-235">eventVolume</span></span> | <span data-ttu-id="41989-236">(선택 사항) 컨트롤 hello hello 저장소 테이블 내에서 만든 파티션의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-236">(optional) Controls hello number of partitions created within hello storage table.</span></span> <span data-ttu-id="41989-237">`"Large"`, `"Medium"` 또는 `"Small"` 중 하나여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="41989-238">Hello 기본값은 지정 하지 않으면 `"Medium"`합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-238">If not specified, hello default value is `"Medium"`.</span></span>
<span data-ttu-id="41989-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="41989-239">sampleRateInSeconds</span></span> | <span data-ttu-id="41989-240">(선택 사항) hello 기본 간격 (집계) 원시 메트릭 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-240">(optional) hello default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="41989-241">가장 작은 지원 hello 샘플링 주기 15 초입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-241">hello smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="41989-242">Hello 기본값은 지정 하지 않으면 `15`합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-242">If not specified, hello default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="41989-243">메트릭</span><span class="sxs-lookup"><span data-stu-id="41989-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="41989-244">요소</span><span class="sxs-lookup"><span data-stu-id="41989-244">Element</span></span> | <span data-ttu-id="41989-245">값</span><span class="sxs-lookup"><span data-stu-id="41989-245">Value</span></span>
------- | -----
<span data-ttu-id="41989-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="41989-246">resourceId</span></span> | <span data-ttu-id="41989-247">hello Azure 리소스 관리자 리소스 ID hello 가상 컴퓨터 크기 또는 hello VM의 VM 속한 toowhich hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-247">hello Azure Resource Manager resource ID of hello VM or of hello virtual machine scale set toowhich hello VM belongs.</span></span> <span data-ttu-id="41989-248">이 설정은 해야도 JsonBlob 싱크 hello 구성에 사용 되는 경우를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-248">This setting must be also specified if any JsonBlob sink is used in hello configuration.</span></span>
<span data-ttu-id="41989-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="41989-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="41989-250">계산 하 고 tooAzure 메트릭, 8601는 시간 간격으로 표현 된 전송 하는 집계 메트릭을 toobe을는 hello 빈도.</span><span class="sxs-lookup"><span data-stu-id="41989-250">hello frequency at which aggregate metrics are toobe computed and transferred tooAzure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="41989-251">hello 가장 짧은 전송 기간은 60 초, 즉, PT1M를입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-251">hello smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="41989-252">하나 이상의 scheduledTransferPeriod를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="41989-253">샘플 hello 샘플링 주기 hello 카운터에 대해 명시적으로 정의 된 또는의 hello hello performanceCounters 섹션에 지정 된 메트릭 15 초 마다 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-253">Samples of hello metrics specified in hello performanceCounters section are collected every 15 seconds or at hello sample rate explicitly defined for hello counter.</span></span> <span data-ttu-id="41989-254">여러 scheduledTransferPeriod 주파수 예와 같이 hello 없으면 각 집계는 독립적으로 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-254">If multiple scheduledTransferPeriod frequencies appear (as in hello example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="41989-255">performanceCounters</span><span class="sxs-lookup"><span data-stu-id="41989-255">performanceCounters</span></span>

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

<span data-ttu-id="41989-256">이 선택적 섹션이 메트릭 hello 컬렉션을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-256">This optional section controls hello collection of metrics.</span></span> <span data-ttu-id="41989-257">각각에 대해 집계 되는 원시 샘플 [scheduledTransferPeriod](#metrics) tooproduce 이러한 값:</span><span class="sxs-lookup"><span data-stu-id="41989-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) tooproduce these values:</span></span>

* <span data-ttu-id="41989-258">평균</span><span class="sxs-lookup"><span data-stu-id="41989-258">mean</span></span>
* <span data-ttu-id="41989-259">minimum</span><span class="sxs-lookup"><span data-stu-id="41989-259">minimum</span></span>
* <span data-ttu-id="41989-260">maximum</span><span class="sxs-lookup"><span data-stu-id="41989-260">maximum</span></span>
* <span data-ttu-id="41989-261">마지막으로 수집된 값</span><span class="sxs-lookup"><span data-stu-id="41989-261">last-collected value</span></span>
* <span data-ttu-id="41989-262">원시 샘플 수 toocompute hello 집계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-262">count of raw samples used toocompute hello aggregate</span></span>

<span data-ttu-id="41989-263">요소</span><span class="sxs-lookup"><span data-stu-id="41989-263">Element</span></span> | <span data-ttu-id="41989-264">값</span><span class="sxs-lookup"><span data-stu-id="41989-264">Value</span></span>
------- | -----
<span data-ttu-id="41989-265">sinks</span><span class="sxs-lookup"><span data-stu-id="41989-265">sinks</span></span> | <span data-ttu-id="41989-266">(선택 사항) 이름의 쉼표로 구분 된 목록을 싱크에서 toowhich 했다 집계 된 메트릭 결과 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="41989-266">(optional) A comma-separated list of names of sinks toowhich LAD sends aggregated metric results.</span></span> <span data-ttu-id="41989-267">모든 집계 된 메트릭 나열 하는 게시 된 tooeach 싱크 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-267">All aggregated metrics are published tooeach listed sink.</span></span> <span data-ttu-id="41989-268">[sinksConfig](#sinksconfig)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41989-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="41989-269">예: `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="41989-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="41989-270">type</span><span class="sxs-lookup"><span data-stu-id="41989-270">type</span></span> | <span data-ttu-id="41989-271">Hello hello 메트릭의 실제 공급자를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-271">Identifies hello actual provider of hello metric.</span></span>
<span data-ttu-id="41989-272">class</span><span class="sxs-lookup"><span data-stu-id="41989-272">class</span></span> | <span data-ttu-id="41989-273">"Counter"와 함께 hello 공급자의 네임 스페이스 내에서 특정 메트릭을 hello를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-273">Together with "counter", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="41989-274">counter</span><span class="sxs-lookup"><span data-stu-id="41989-274">counter</span></span> | <span data-ttu-id="41989-275">"Class"와 함께 hello 공급자의 네임 스페이스 내에서 특정 메트릭을 hello를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-275">Together with "class", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="41989-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="41989-276">counterSpecifier</span></span> | <span data-ttu-id="41989-277">Hello Azure 메트릭 네임 스페이스 내에서 특정 메트릭을 hello를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-277">Identifies hello specific metric within hello Azure Metrics namespace.</span></span>
<span data-ttu-id="41989-278">condition</span><span class="sxs-lookup"><span data-stu-id="41989-278">condition</span></span> | <span data-ttu-id="41989-279">(선택 사항) 가 선택 되어 해당 개체의 모든 인스턴스에서 집계 hello 또는 선택 hello 개체 toowhich hello 메트릭의 특정 인스턴스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-279">(optional) Selects a specific instance of hello object toowhich hello metric applies or selects hello aggregation across all instances of that object.</span></span> <span data-ttu-id="41989-280">자세한 내용은 참조 hello [ `builtin` 메트릭 정의](#metrics-supported-by-builtin)합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-280">For more information, see hello [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="41989-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="41989-281">sampleRate</span></span> | <span data-ttu-id="41989-282">이 메트릭은 대 한 원시 샘플에서 수집 하는 hello 속도 설정 하는 8601 간격이입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-282">IS 8601 interval that sets hello rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="41989-283">을 설정 하지 경우 hello 컬렉션 간격이 hello 값으로 설정 되어 [sampleRateInSeconds](#ladcfg)합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-283">If not set, hello collection interval is set by hello value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="41989-284">지원 되는 샘플링 주기를 가장 짧은 hello은 15 초 (PT15S).</span><span class="sxs-lookup"><span data-stu-id="41989-284">hello shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="41989-285">단위</span><span class="sxs-lookup"><span data-stu-id="41989-285">unit</span></span> | <span data-ttu-id="41989-286">문자열 "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond" 중 하나여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="41989-287">Hello 메트릭에 대 한 hello 단위를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-287">Defines hello unit for hello metric.</span></span> <span data-ttu-id="41989-288">수집 된 hello 데이터 소비자에 수집 된 데이터 값 toomatch이이 단위 hello 있기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-288">Consumers of hello collected data expect hello collected data values toomatch this unit.</span></span> <span data-ttu-id="41989-289">LAD는 이 필드를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-289">LAD ignores this field.</span></span>
<span data-ttu-id="41989-290">displayName</span><span class="sxs-lookup"><span data-stu-id="41989-290">displayName</span></span> | <span data-ttu-id="41989-291">hello 언어로 hello hello 관련된 로캘을 설정으로 지정 된 레이블 toobe Azure 메트릭에서 toothis 데이터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-291">hello label (in hello language specified by hello associated locale setting) toobe attached toothis data in Azure Metrics.</span></span> <span data-ttu-id="41989-292">LAD는 이 필드를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-292">LAD ignores this field.</span></span>

<span data-ttu-id="41989-293">hello counterSpecifier는 파일과 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-293">hello counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="41989-294">Azure 포털 차트 및 경고 기능을 hello 처럼 메트릭의 소비자 메트릭 또는 메트릭 인스턴스를 식별 하는 "키" hello로 counterSpecifier를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-294">Consumers of metrics, like hello Azure portal charting and alerting feature, use counterSpecifier as hello "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="41989-295">`builtin` 메트릭의 경우 `/builtin/`으로 시작하는 counterSpecifier 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="41989-296">특정 인스턴스 메트릭 수집 하는 경우 hello 인스턴스 toohello counterSpecifier 값의 hello 식별자를 연결 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-296">If you are collecting a specific instance of a metric, we recommend you attach hello identifier of hello instance toohello counterSpecifier value.</span></span> <span data-ttu-id="41989-297">일부 사례:</span><span class="sxs-lookup"><span data-stu-id="41989-297">Some examples:</span></span>

* <span data-ttu-id="41989-298">`/builtin/Processor/PercentIdleTime` - 모든 코어의 평균 유휴 시간</span><span class="sxs-lookup"><span data-stu-id="41989-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="41989-299">`/builtin/Disk/FreeSpace(/mnt)`-Hello /mnt 파일 시스템에 대 한 사용 가능한 공간</span><span class="sxs-lookup"><span data-stu-id="41989-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for hello /mnt filesystem</span></span>
* <span data-ttu-id="41989-300">`/builtin/Disk/FreeSpace` - 탑재된 모든 파일 시스템의 평균 사용 가능한 공간</span><span class="sxs-lookup"><span data-stu-id="41989-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="41989-301">했다 아니고 hello Azure 포털 hello counterSpecifier 값 toomatch 임의의 패턴이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-301">Neither LAD nor hello Azure portal expects hello counterSpecifier value toomatch any pattern.</span></span> <span data-ttu-id="41989-302">일관된 방법으로 counterSpecifier 값을 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="41989-303">지정 하는 경우 `performanceCounters`, 했다 Azure 저장소에 항상 tooa 테이블 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="41989-303">When you specify `performanceCounters`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="41989-304">있습니다 수 있는 hello 동일 tooJSON blob 및/또는 이벤트 허브에 기록 된 데이터는 있지만 저장 데이터 tooa 테이블을 비활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-304">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="41989-305">Hello 구성 된 진단 확장 toouse 함수의 모든 인스턴스의 동일한 저장소 계정 이름 및 끝점 추가 자신의 메트릭 및 로그 toohello hello 같은 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-305">All instances of hello diagnostic extension configured toouse hello same storage account name and endpoint add their metrics and logs toohello same table.</span></span> <span data-ttu-id="41989-306">너무 많은 Vm을 작성 하는 조절 하 여 동일한 테이블 파티션에 Azure toohello toothat 파티션을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-306">If too many VMs are writing toohello same table partition, Azure can throttle writes toothat partition.</span></span> <span data-ttu-id="41989-307">1 (소량), (중간), 10 또는 100 (큼) 서로 다른 파티션을 분산 하는 hello eventVolume 원인을 항목 toobe를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-307">hello eventVolume setting causes entries toobe spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="41989-308">일반적으로 "중간"는 충분 한 tooensure 트래픽이 조절 되 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-308">Usually, "Medium" is sufficient tooensure traffic is not throttled.</span></span> <span data-ttu-id="41989-309">hello Azure 포털의 hello Azure 메트릭 기능은 hello 또는의 데이터를이 테이블 tooproduce 그래프 tootrigger 경고를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-309">hello Azure Metrics feature of hello Azure portal uses hello data in this table tooproduce graphs or tootrigger alerts.</span></span> <span data-ttu-id="41989-310">hello 테이블 이름은 이러한 문자열의 hello 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-310">hello table name is hello concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="41989-311">hello "scheduledTransferPeriod" hello에 대 한 집계 hello 테이블에 저장 된 값</span><span class="sxs-lookup"><span data-stu-id="41989-311">hello "scheduledTransferPeriod" for hello aggregated values stored in hello table</span></span>
* `P10DV2S`
* <span data-ttu-id="41989-312">Hello 형태로 "YYYYMMDD" 10 일 마다 변경 날짜</span><span class="sxs-lookup"><span data-stu-id="41989-312">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="41989-313">예에는 `WADMetricsPT1HP10DV2S20170410` 및 `WADMetricsPT1MP10DV2S20170609`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="41989-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="41989-314">syslogEvents</span></span>

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

<span data-ttu-id="41989-315">이 선택적 섹션이 syslog에서 이벤트 로그의 hello 컬렉션을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-315">This optional section controls hello collection of log events from syslog.</span></span> <span data-ttu-id="41989-316">Hello 섹션을 생략 하면 syslog 이벤트를 전혀 캡처되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-316">If hello section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="41989-317">hello syslogEventConfiguration 컬렉션에 관심 있는 각 syslog 기능에 대 한 하나의 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-317">hello syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="41989-318">MinSeverity는 특정 기능에 대 한 "NONE" 또는 해당 기능이 표시 되지 않으면 hello 요소에 전혀 해당 시설에서 이벤트가 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in hello element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="41989-319">요소</span><span class="sxs-lookup"><span data-stu-id="41989-319">Element</span></span> | <span data-ttu-id="41989-320">값</span><span class="sxs-lookup"><span data-stu-id="41989-320">Value</span></span>
------- | -----
<span data-ttu-id="41989-321">sinks</span><span class="sxs-lookup"><span data-stu-id="41989-321">sinks</span></span> | <span data-ttu-id="41989-322">이름의 쉼표로 구분 된 목록을 싱크에서 toowhich 개별 로그에 이벤트 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-322">A comma-separated list of names of sinks toowhich individual log events are published.</span></span> <span data-ttu-id="41989-323">SyslogEventConfiguration의 hello 제한 일치 하는 모든 로그 이벤트는 나열 된 게시 된 tooeach 싱크입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-323">All log events matching hello restrictions in syslogEventConfiguration are published tooeach listed sink.</span></span> <span data-ttu-id="41989-324">예: "EHforsyslog"</span><span class="sxs-lookup"><span data-stu-id="41989-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="41989-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="41989-325">facilityName</span></span> | <span data-ttu-id="41989-326">syslog 기능 이름입니다(예: "LOG\_USER" 또는 "LOG\_LOCAL0").</span><span class="sxs-lookup"><span data-stu-id="41989-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="41989-327">Hello의 hello "기능" 섹션을 참조 [syslog 매뉴얼 페이지](http://man7.org/linux/man-pages/man3/syslog.3.html) hello 전체 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-327">See hello "facility" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span>
<span data-ttu-id="41989-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="41989-328">minSeverity</span></span> | <span data-ttu-id="41989-329">syslog 심각도 수준입니다(예: "LOG\_ERR" 또는 "LOG\_INFO").</span><span class="sxs-lookup"><span data-stu-id="41989-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="41989-330">Hello의 hello "수준" 섹션을 참조 [syslog 매뉴얼 페이지](http://man7.org/linux/man-pages/man3/syslog.3.html) hello 전체 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-330">See hello "level" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span> <span data-ttu-id="41989-331">hello 확장에 전송 되는 이벤트 toohello 시설 캡처하거나 hello 위에 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-331">hello extension captures events sent toohello facility at or above hello specified level.</span></span>

<span data-ttu-id="41989-332">지정 하는 경우 `syslogEvents`, 했다 Azure 저장소에 항상 tooa 테이블 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="41989-332">When you specify `syslogEvents`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="41989-333">있습니다 수 있는 hello 동일 tooJSON blob 및/또는 이벤트 허브에 기록 된 데이터는 있지만 저장 데이터 tooa 테이블을 비활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-333">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="41989-334">이 테이블에 대 한 동작을 분할 하는 hello에 대 한 설명 된 대로 동일한 hello은 `performanceCounters`합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-334">hello partitioning behavior for this table is hello same as described for `performanceCounters`.</span></span> <span data-ttu-id="41989-335">hello 테이블 이름은 이러한 문자열의 hello 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-335">hello table name is hello concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="41989-336">Hello 형태로 "YYYYMMDD" 10 일 마다 변경 날짜</span><span class="sxs-lookup"><span data-stu-id="41989-336">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="41989-337">예에는 `LinuxSyslog20170410` 및 `LinuxSyslog20170609`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="41989-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="41989-338">perfCfg</span></span>

<span data-ttu-id="41989-339">이 선택적 섹션은 임의의 [OMI](https://github.com/Microsoft/omi) 쿼리 실행을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

<span data-ttu-id="41989-340">요소</span><span class="sxs-lookup"><span data-stu-id="41989-340">Element</span></span> | <span data-ttu-id="41989-341">값</span><span class="sxs-lookup"><span data-stu-id="41989-341">Value</span></span>
------- | -----
<span data-ttu-id="41989-342">namespace</span><span class="sxs-lookup"><span data-stu-id="41989-342">namespace</span></span> | <span data-ttu-id="41989-343">(선택 사항) hello OMI 네임 스페이스는 hello 내에서 쿼리 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-343">(optional) hello OMI namespace within which hello query should be executed.</span></span> <span data-ttu-id="41989-344">지정 하지 않으면 hello 기본값은 "루트/scx", hello 구현한 [System Center 플랫폼 공급자](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation)합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-344">If unspecified, hello default value is "root/scx", implemented by hello [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="41989-345">쿼리</span><span class="sxs-lookup"><span data-stu-id="41989-345">query</span></span> | <span data-ttu-id="41989-346">hello OMI 쿼리 toobe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-346">hello OMI query toobe executed.</span></span>
<span data-ttu-id="41989-347">테이블</span><span class="sxs-lookup"><span data-stu-id="41989-347">table</span></span> | <span data-ttu-id="41989-348">(선택 사항) hello Azure 저장소 테이블 저장소 계정을 지정 하는 hello (참조 [보호 설정을](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="41989-348">(optional) hello Azure storage table, in hello designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="41989-349">frequency</span><span class="sxs-lookup"><span data-stu-id="41989-349">frequency</span></span> | <span data-ttu-id="41989-350">(선택 사항) hello 개수 hello 쿼리의 실행 간격 (초)입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-350">(optional) hello number of seconds between execution of hello query.</span></span> <span data-ttu-id="41989-351">기본값은 300(5분)이고 최소값은 15초입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="41989-352">sinks</span><span class="sxs-lookup"><span data-stu-id="41989-352">sinks</span></span> | <span data-ttu-id="41989-353">(선택 사항) 추가 싱크 toowhich 원시 샘플 메트릭 결과의 이름의 쉼표로 구분 된 목록을 게시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-353">(optional) A comma-separated list of names of additional sinks toowhich raw sample metric results should be published.</span></span> <span data-ttu-id="41989-354">Hello 확장명 또는 Azure 메트릭을 원시 이러한 샘플의 집계가 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-354">No aggregation of these raw samples is computed by hello extension or by Azure Metrics.</span></span>

<span data-ttu-id="41989-355">"table"이나 "sinks" 또는 둘 다 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="41989-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="41989-356">fileLogs</span></span>

<span data-ttu-id="41989-357">로그 파일의 컨트롤 hello를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-357">Controls hello capture of log files.</span></span> <span data-ttu-id="41989-358">했다는 텍스트 줄 바꿈을 toohello 파일에 작성 된 것 처럼 캡처하고 tootable 행 및/또는 모든 지정 된 싱크 (JsonBlob 또는 EventHub) 씁니다.</span><span class="sxs-lookup"><span data-stu-id="41989-358">LAD captures new text lines as they are written toohello file and writes them tootable rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="41989-359">요소</span><span class="sxs-lookup"><span data-stu-id="41989-359">Element</span></span> | <span data-ttu-id="41989-360">값</span><span class="sxs-lookup"><span data-stu-id="41989-360">Value</span></span>
------- | -----
<span data-ttu-id="41989-361">file</span><span class="sxs-lookup"><span data-stu-id="41989-361">file</span></span> | <span data-ttu-id="41989-362">로그 파일 toobe hello의 전체 경로 이름을 hello 조사를 캡처한 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-362">hello full pathname of hello log file toobe watched and captured.</span></span> <span data-ttu-id="41989-363">hello pathname 단일 파일의 이름 이어야 합니다. 디렉터리의 이름을 두거나 와일드 카드를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-363">hello pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="41989-364">테이블</span><span class="sxs-lookup"><span data-stu-id="41989-364">table</span></span> | <span data-ttu-id="41989-365">(선택 사항) hello Azure 저장소 테이블 hello 지정 된 저장소 계정 (지정 된 대로 보호 된 hello 구성에서), 새 줄에 hello 작성 된 "비상" hello 파일에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-365">(optional) hello Azure storage table, in hello designated storage account (as specified in hello protected configuration), into which new lines from hello "tail" of hello file are written.</span></span>
<span data-ttu-id="41989-366">sinks</span><span class="sxs-lookup"><span data-stu-id="41989-366">sinks</span></span> | <span data-ttu-id="41989-367">(선택 사항) 추가 싱크 toowhich 로그 선의 이름의 쉼표로 구분 된 목록을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-367">(optional) A comma-separated list of names of additional sinks toowhich log lines sent.</span></span>

<span data-ttu-id="41989-368">"table"이나 "sinks" 또는 둘 다 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-hello-builtin-provider"></a><span data-ttu-id="41989-369">Hello 기본 제공 공급자가 지 원하는 메트릭</span><span class="sxs-lookup"><span data-stu-id="41989-369">Metrics supported by hello builtin provider</span></span>

<span data-ttu-id="41989-370">hello builtin 메트릭 공급자가 메트릭 가장 흥미로운 tooa 광범위 한 사용자 집합의 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-370">hello builtin metric provider is a source of metrics most interesting tooa broad set of users.</span></span> <span data-ttu-id="41989-371">이러한 메트릭은 다음과 같은 다섯 가지 광범위한 클래스에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="41989-372">프로세서</span><span class="sxs-lookup"><span data-stu-id="41989-372">Processor</span></span>
* <span data-ttu-id="41989-373">메모리</span><span class="sxs-lookup"><span data-stu-id="41989-373">Memory</span></span>
* <span data-ttu-id="41989-374">네트워크</span><span class="sxs-lookup"><span data-stu-id="41989-374">Network</span></span>
* <span data-ttu-id="41989-375">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="41989-375">Filesystem</span></span>
* <span data-ttu-id="41989-376">디스크</span><span class="sxs-lookup"><span data-stu-id="41989-376">Disk</span></span>

### <a name="builtin-metrics-for-hello-processor-class"></a><span data-ttu-id="41989-377">hello 프로세서 클래스에 대 한 기본 제공 된 메트릭</span><span class="sxs-lookup"><span data-stu-id="41989-377">builtin metrics for hello Processor class</span></span>

<span data-ttu-id="41989-378">hello 프로세서 클래스 메트릭 VM hello 프로세서 사용에 대 한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-378">hello Processor class of metrics provides information about processor usage in hello VM.</span></span> <span data-ttu-id="41989-379">백분율을 집계 하는 경우에 hello 결과 모든 Cpu에서 hello 평균 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-379">When aggregating percentages, hello result is hello average across all CPUs.</span></span> <span data-ttu-id="41989-380">두 개의 코어 VM에서에서 한 코어 100% 사용 중 이며 다른 hello 100% 유휴 hello 보고 PercentIdleTime 50이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-380">In a two core VM, if one core was 100% busy and hello other was 100% idle, hello reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="41989-381">각 코어에 대 한 사용 중 50%가 hello 동일한 기간 hello 보고 결과 50도 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-381">If each core was 50% busy for hello same period, hello reported result would also be 50.</span></span> <span data-ttu-id="41989-382">4 코어 VM, 단일 코어 100% 사용 중 및 hello 유휴 상태, 다른 hello 보고 PercentIdleTime 75 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-382">In a four core VM, with one core 100% busy and hello others idle, hello reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="41989-383">counter</span><span class="sxs-lookup"><span data-stu-id="41989-383">counter</span></span> | <span data-ttu-id="41989-384">의미</span><span class="sxs-lookup"><span data-stu-id="41989-384">Meaning</span></span>
------- | -------
<span data-ttu-id="41989-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="41989-385">PercentIdleTime</span></span> | <span data-ttu-id="41989-386">Hello 집계 창 프로세서가 hello 커널 유휴 루프를 실행 하는 동안 있는 시간의 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-386">Percentage of time during hello aggregation window that processors were executing hello kernel idle loop</span></span>
<span data-ttu-id="41989-387">PercentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="41989-387">PercentProcessorTime</span></span> | <span data-ttu-id="41989-388">비 유휴 스레드를 실행하는 시간의 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="41989-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="41989-389">PercentIOWaitTime</span></span> | <span data-ttu-id="41989-390">IO 작업 toocomplete에 대 한 대기 시간의 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-390">Percentage of time waiting for IO operations toocomplete</span></span>
<span data-ttu-id="41989-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="41989-391">PercentInterruptTime</span></span> | <span data-ttu-id="41989-392">하드웨어/소프트웨어 인터럽트 및 DPC(지연된 프로시저 호출)를 실행하는 시간의 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="41989-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="41989-393">PercentUserTime</span></span> | <span data-ttu-id="41989-394">Hello 집계 기간 동안 유휴 상태가 아닌 시간 보통 우선 순위로 보다 사용자에 소요 된 시간의 hello 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-394">Of non-idle time during hello aggregation window, hello percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="41989-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="41989-395">PercentNiceTime</span></span> | <span data-ttu-id="41989-396">비 유휴 시간의 낮아진된 (좋은) 우선 순위에 소요 된 hello 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-396">Of non-idle time, hello percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="41989-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="41989-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="41989-398">비 유휴 시간의 권한 (커널) 모드에 소요 된 hello 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-398">Of non-idle time, hello percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="41989-399">hello 처음 네 개의 카운터 합계 too100%입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-399">hello first four counters should sum too100%.</span></span> <span data-ttu-id="41989-400">hello 마지막 세 개의 카운터를 합계 too100%; 이러한 세분화 PercentProcessorTime, PercentIOWaitTime, 및 PercentInterruptTime hello 합계입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-400">hello last three counters also sum too100%; they subdivide hello sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="41989-401">모든 프로세서에서 단일 메트릭을 집계 tooobtain 설정 `"condition": "IsAggregate=TRUE"`합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-401">tooobtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="41989-402">특정 프로세서에 대 한 메트릭을 tooobtain hello 두 번째 논리 프로세서의 4 코어 VM을 같은 설정 `"condition": "Name=\\"1\\""`합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-402">tooobtain a metric for a specific processor, such as hello second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="41989-403">Hello 범위에 있는 논리 프로세서 번호 `[0..n-1]`합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-403">Logical processor numbers are in hello range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-hello-memory-class"></a><span data-ttu-id="41989-404">hello 메모리 클래스에 대 한 기본 제공 된 메트릭</span><span class="sxs-lookup"><span data-stu-id="41989-404">builtin metrics for hello Memory class</span></span>

<span data-ttu-id="41989-405">hello 메트릭 메모리 클래스 메모리 사용률, 페이징 및 교환에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-405">hello Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="41989-406">counter</span><span class="sxs-lookup"><span data-stu-id="41989-406">counter</span></span> | <span data-ttu-id="41989-407">의미</span><span class="sxs-lookup"><span data-stu-id="41989-407">Meaning</span></span>
------- | -------
<span data-ttu-id="41989-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="41989-408">AvailableMemory</span></span> | <span data-ttu-id="41989-409">사용 가능한 실제 메모리(MiB)</span><span class="sxs-lookup"><span data-stu-id="41989-409">Available physical memory in MiB</span></span>
<span data-ttu-id="41989-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="41989-410">PercentAvailableMemory</span></span> | <span data-ttu-id="41989-411">총 메모리 중 사용 가능한 실제 메모리의 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="41989-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="41989-412">UsedMemory</span></span> | <span data-ttu-id="41989-413">사용 중인 실제 메모리(MiB)</span><span class="sxs-lookup"><span data-stu-id="41989-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="41989-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="41989-414">PercentUsedMemory</span></span> | <span data-ttu-id="41989-415">총 메모리 중 사용 중인 실제 메모리의 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="41989-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="41989-416">PagesPerSec</span></span> | <span data-ttu-id="41989-417">총 페이징(읽기/쓰기)</span><span class="sxs-lookup"><span data-stu-id="41989-417">Total paging (read/write)</span></span>
<span data-ttu-id="41989-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="41989-418">PagesReadPerSec</span></span> | <span data-ttu-id="41989-419">백업 저장소(스왑 파일, 프로그램 파일, 매핑된 파일 등)에서 읽은 페이지</span><span class="sxs-lookup"><span data-stu-id="41989-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="41989-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="41989-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="41989-421">Toobacking 쓴 페이지 저장소 (스왑 파일, 매핑된 파일 등)</span><span class="sxs-lookup"><span data-stu-id="41989-421">Pages written toobacking store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="41989-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="41989-422">AvailableSwap</span></span> | <span data-ttu-id="41989-423">사용하지 않는 스왑 공간(MiB)</span><span class="sxs-lookup"><span data-stu-id="41989-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="41989-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="41989-424">PercentAvailableSwap</span></span> | <span data-ttu-id="41989-425">총 스왑 중 사용하지 않은 스왑 공간의 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="41989-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="41989-426">UsedSwap</span></span> | <span data-ttu-id="41989-427">사용 중인 스왑 공간(MiB)</span><span class="sxs-lookup"><span data-stu-id="41989-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="41989-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="41989-428">PercentUsedSwap</span></span> | <span data-ttu-id="41989-429">총 스왑 중 사용 중인 스왑 공간의 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="41989-430">이 메트릭 클래스에는 인스턴스가 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="41989-431">hello "조건" 특성에 유용한 설정이 없는 및 생략 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-431">hello "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-hello-network-class"></a><span data-ttu-id="41989-432">hello 네트워크 클래스에 대 한 기본 제공 된 메트릭</span><span class="sxs-lookup"><span data-stu-id="41989-432">builtin metrics for hello Network class</span></span>

<span data-ttu-id="41989-433">hello 네트워크 클래스입니다. 메트릭 부팅 후 경과 개별 네트워크 인터페이스에 네트워크 작업에 대 한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-433">hello Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="41989-434">LAD는 대역폭 메트릭을 노출하지 않으며 이는 호스트 메트릭에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="41989-435">counter</span><span class="sxs-lookup"><span data-stu-id="41989-435">counter</span></span> | <span data-ttu-id="41989-436">의미</span><span class="sxs-lookup"><span data-stu-id="41989-436">Meaning</span></span>
------- | -------
<span data-ttu-id="41989-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="41989-437">BytesTransmitted</span></span> | <span data-ttu-id="41989-438">부팅 이후 보낸 총 바이트</span><span class="sxs-lookup"><span data-stu-id="41989-438">Total bytes sent since boot</span></span>
<span data-ttu-id="41989-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="41989-439">BytesReceived</span></span> | <span data-ttu-id="41989-440">부팅 이후 받은 총 바이트</span><span class="sxs-lookup"><span data-stu-id="41989-440">Total bytes received since boot</span></span>
<span data-ttu-id="41989-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="41989-441">BytesTotal</span></span> | <span data-ttu-id="41989-442">부팅 이후 보내거나 받은 총 바이트</span><span class="sxs-lookup"><span data-stu-id="41989-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="41989-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="41989-443">PacketsTransmitted</span></span> | <span data-ttu-id="41989-444">부팅 이후 보낸 총 패킷</span><span class="sxs-lookup"><span data-stu-id="41989-444">Total packets sent since boot</span></span>
<span data-ttu-id="41989-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="41989-445">PacketsReceived</span></span> | <span data-ttu-id="41989-446">부팅 이후 받은 총 패킷</span><span class="sxs-lookup"><span data-stu-id="41989-446">Total packets received since boot</span></span>
<span data-ttu-id="41989-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="41989-447">TotalRxErrors</span></span> | <span data-ttu-id="41989-448">부팅 이후 수신 오류 수</span><span class="sxs-lookup"><span data-stu-id="41989-448">Number of receive errors since boot</span></span>
<span data-ttu-id="41989-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="41989-449">TotalTxErrors</span></span> | <span data-ttu-id="41989-450">부팅 이후 전송 오류 수</span><span class="sxs-lookup"><span data-stu-id="41989-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="41989-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="41989-451">TotalCollisions</span></span> | <span data-ttu-id="41989-452">부팅 후 경과 hello 네트워크 포트에서 보고 된 충돌 수</span><span class="sxs-lookup"><span data-stu-id="41989-452">Number of collisions reported by hello network ports since boot</span></span>

 <span data-ttu-id="41989-453">이 클래스가 인스턴스화되더라도 LAD는 모든 네트워크 장치에서 집계되는 네트워크 메트릭을 캡처하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="41989-454">t h 0, 등의 특정 인터페이스에 대 한 tooobtain hello 메트릭을 설정 `"condition": "InstanceID=\\"eth0\\""`합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-454">tooobtain hello metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-hello-filesystem-class"></a><span data-ttu-id="41989-455">파일 시스템 클래스 hello에 대 한 기본 제공 메트릭</span><span class="sxs-lookup"><span data-stu-id="41989-455">builtin metrics for hello Filesystem class</span></span>

<span data-ttu-id="41989-456">hello 메트릭의 파일 시스템 클래스는 파일 시스템 사용에 대 한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-456">hello Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="41989-457">Absolute 및 백분율 값 표시 tooan 일반 사용자 (루트)와 같이 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-457">Absolute and percentage values are reported as they'd be displayed tooan ordinary user (not root).</span></span>

<span data-ttu-id="41989-458">counter</span><span class="sxs-lookup"><span data-stu-id="41989-458">counter</span></span> | <span data-ttu-id="41989-459">의미</span><span class="sxs-lookup"><span data-stu-id="41989-459">Meaning</span></span>
------- | -------
<span data-ttu-id="41989-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="41989-460">FreeSpace</span></span> | <span data-ttu-id="41989-461">사용 가능한 디스크 공간(바이트)</span><span class="sxs-lookup"><span data-stu-id="41989-461">Available disk space in bytes</span></span>
<span data-ttu-id="41989-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="41989-462">UsedSpace</span></span> | <span data-ttu-id="41989-463">사용된 디스크 공간(바이트)</span><span class="sxs-lookup"><span data-stu-id="41989-463">Used disk space in bytes</span></span>
<span data-ttu-id="41989-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="41989-464">PercentFreeSpace</span></span> | <span data-ttu-id="41989-465">사용 가능한 공간의 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-465">Percentage free space</span></span>
<span data-ttu-id="41989-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="41989-466">PercentUsedSpace</span></span> | <span data-ttu-id="41989-467">사용된 공간의 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-467">Percentage used space</span></span>
<span data-ttu-id="41989-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="41989-468">PercentFreeInodes</span></span> | <span data-ttu-id="41989-469">사용하지 않은 inode의 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-469">Percentage of unused inodes</span></span>
<span data-ttu-id="41989-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="41989-470">PercentUsedInodes</span></span> | <span data-ttu-id="41989-471">모든 파일 시스템에서 합한 할당된(사용 중인) inode의 백분율</span><span class="sxs-lookup"><span data-stu-id="41989-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="41989-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="41989-472">BytesReadPerSecond</span></span> | <span data-ttu-id="41989-473">초당 읽은 바이트</span><span class="sxs-lookup"><span data-stu-id="41989-473">Bytes read per second</span></span>
<span data-ttu-id="41989-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="41989-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="41989-475">초당 쓴 바이트</span><span class="sxs-lookup"><span data-stu-id="41989-475">Bytes written per second</span></span>
<span data-ttu-id="41989-476">초당 바이트 수</span><span class="sxs-lookup"><span data-stu-id="41989-476">BytesPerSecond</span></span> | <span data-ttu-id="41989-477">초당 읽거나 쓴 바이트</span><span class="sxs-lookup"><span data-stu-id="41989-477">Bytes read or written per second</span></span>
<span data-ttu-id="41989-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="41989-478">ReadsPerSecond</span></span> | <span data-ttu-id="41989-479">초당 읽기 작업</span><span class="sxs-lookup"><span data-stu-id="41989-479">Read operations per second</span></span>
<span data-ttu-id="41989-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="41989-480">WritesPerSecond</span></span> | <span data-ttu-id="41989-481">초당 쓰기 작업</span><span class="sxs-lookup"><span data-stu-id="41989-481">Write operations per second</span></span>
<span data-ttu-id="41989-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="41989-482">TransfersPerSecond</span></span> | <span data-ttu-id="41989-483">초당 읽기 또는 쓰기 작업</span><span class="sxs-lookup"><span data-stu-id="41989-483">Read or write operations per second</span></span>

<span data-ttu-id="41989-484">`"condition": "IsAggregate=True"`로 설정하면 모든 파일 시스템에서 집계된 값을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="41989-485">`"condition": 'Name="/mnt"'`로 설정하면 특정 탑재된 파일 시스템(예: "/mnt")에 대한 값을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-hello-disk-class"></a><span data-ttu-id="41989-486">hello 디스크 클래스에 대 한 기본 제공 된 메트릭</span><span class="sxs-lookup"><span data-stu-id="41989-486">builtin metrics for hello Disk class</span></span>

<span data-ttu-id="41989-487">hello 메트릭 디스크 클래스 디스크 장치 사용에 대 한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-487">hello Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="41989-488">이러한 통계는 toohello 전체 드라이브를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-488">These statistics apply toohello entire drive.</span></span> <span data-ttu-id="41989-489">장치에서 여러 파일 시스템이 있는 경우 해당 장치에 대 한 hello 카운터 인 효과적으로 모두에 걸쳐 집계 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-489">If there are multiple file systems on a device, hello counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="41989-490">counter</span><span class="sxs-lookup"><span data-stu-id="41989-490">counter</span></span> | <span data-ttu-id="41989-491">의미</span><span class="sxs-lookup"><span data-stu-id="41989-491">Meaning</span></span>
------- | -------
<span data-ttu-id="41989-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="41989-492">ReadsPerSecond</span></span> | <span data-ttu-id="41989-493">초당 읽기 작업</span><span class="sxs-lookup"><span data-stu-id="41989-493">Read operations per second</span></span>
<span data-ttu-id="41989-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="41989-494">WritesPerSecond</span></span> | <span data-ttu-id="41989-495">초당 쓰기 작업</span><span class="sxs-lookup"><span data-stu-id="41989-495">Write operations per second</span></span>
<span data-ttu-id="41989-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="41989-496">TransfersPerSecond</span></span> | <span data-ttu-id="41989-497">초당 총 작업</span><span class="sxs-lookup"><span data-stu-id="41989-497">Total operations per second</span></span>
<span data-ttu-id="41989-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="41989-498">AverageReadTime</span></span> | <span data-ttu-id="41989-499">읽기 작업당 평균 시간(초)</span><span class="sxs-lookup"><span data-stu-id="41989-499">Average seconds per read operation</span></span>
<span data-ttu-id="41989-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="41989-500">AverageWriteTime</span></span> | <span data-ttu-id="41989-501">쓰기 작업당 평균 시간(초)</span><span class="sxs-lookup"><span data-stu-id="41989-501">Average seconds per write operation</span></span>
<span data-ttu-id="41989-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="41989-502">AverageTransferTime</span></span> | <span data-ttu-id="41989-503">작업당 평균 시간(초)</span><span class="sxs-lookup"><span data-stu-id="41989-503">Average seconds per operation</span></span>
<span data-ttu-id="41989-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="41989-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="41989-505">대기 중인 디스크 작업의 평균 수</span><span class="sxs-lookup"><span data-stu-id="41989-505">Average number of queued disk operations</span></span>
<span data-ttu-id="41989-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="41989-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="41989-507">초당 읽은 바이트 수</span><span class="sxs-lookup"><span data-stu-id="41989-507">Number of bytes read per second</span></span>
<span data-ttu-id="41989-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="41989-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="41989-509">초당 쓴 바이트 수</span><span class="sxs-lookup"><span data-stu-id="41989-509">Number of bytes written per second</span></span>
<span data-ttu-id="41989-510">초당 바이트 수</span><span class="sxs-lookup"><span data-stu-id="41989-510">BytesPerSecond</span></span> | <span data-ttu-id="41989-511">초당 읽거나 쓴 바이트 수</span><span class="sxs-lookup"><span data-stu-id="41989-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="41989-512">`"condition": "IsAggregate=True"`로 설정하면 모든 디스크에서 집계된 값을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="41989-513">tooget 정보 (예를 들어/개발/sdf1), 특정 장치에 대 한 설정 `"condition": "Name=\\"/dev/sdf1\\""`합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-513">tooget information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="41989-514">CLI를 통해 LAD 3.0 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="41989-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="41989-515">보호 된 설정을 PrivateConfig.json hello 파일에 있으며 PublicConfig.json에 공용 구성 정보는 라고 가정할 경우이 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-515">Assuming your protected settings are in hello file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="41989-516">hello 명령은 hello Azure CLI의 hello Azure 리소스 관리 모드 (arm)를 사용 하는 것을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-516">hello command assumes you are using hello Azure Resource Management mode (arm) of hello Azure CLI.</span></span> <span data-ttu-id="41989-517">클래식 배포에 대 한 했다 tooconfigure (ASM) Vm 모델, 너무 전환 "asm" 모드 (`azure config mode asm`) hello 명령에 hello 리소스 그룹 이름은 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-517">tooconfigure LAD for classic deployment model (ASM) VMs, switch too"asm" mode (`azure config mode asm`) and omit hello resource group name in hello command.</span></span> <span data-ttu-id="41989-518">자세한 내용은 참조 hello [CLI 설명서의 플랫폼 간](https://docs.microsoft.com/azure/xplat-cli-connect)합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-518">For more information, see hello [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="41989-519">LAD 3.0 구성 예제</span><span class="sxs-lookup"><span data-stu-id="41989-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="41989-520">Hello 앞에와 몇 가지 설명 했다 3.0 확장 샘플 구성이 정의 여기의 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-520">Based on hello preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="41989-521">tooapply이 샘플 tooyour 사례 EventHubs SAS 토큰 및 저장소 계정 이름을 사용 하 여, SAS 토큰을 계정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-521">tooapply this sample tooyour case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="41989-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="41989-522">PrivateConfig.json</span></span>

<span data-ttu-id="41989-523">개인 설정은 다음을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-523">These private settings configure:</span></span>

* <span data-ttu-id="41989-524">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="41989-524">a storage account</span></span>
* <span data-ttu-id="41989-525">일치하는 계정 SAS 토큰</span><span class="sxs-lookup"><span data-stu-id="41989-525">a matching account SAS token</span></span>
* <span data-ttu-id="41989-526">여러 싱크(SAS 토큰이 있는 EventHubs 또는 JsonBlob)</span><span class="sxs-lookup"><span data-stu-id="41989-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a><span data-ttu-id="41989-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="41989-527">PublicConfig.json</span></span>

<span data-ttu-id="41989-528">공용 설정으로 LAD는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="41989-529">% 프로세서 시간 및 디스크 사용-공간 메트릭을 toohello 업로드 `WADMetrics*` 테이블</span><span class="sxs-lookup"><span data-stu-id="41989-529">Upload percent-processor-time and used-disk-space metrics toohello `WADMetrics*` table</span></span>
* <span data-ttu-id="41989-530">메시지에서 syslog 기능 "user" 및 심각도 "info" toohello 업로드 `LinuxSyslog*` 테이블</span><span class="sxs-lookup"><span data-stu-id="41989-530">Upload messages from syslog facility "user" and severity "info" toohello `LinuxSyslog*` table</span></span>
* <span data-ttu-id="41989-531">원시 OMI 쿼리 결과 (PercentProcessorTime 및 PercentIdleTime) toohello 라는 업로드 `LinuxCPU` 테이블</span><span class="sxs-lookup"><span data-stu-id="41989-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) toohello named `LinuxCPU` table</span></span>
* <span data-ttu-id="41989-532">파일에서 추가 된 줄 업로드 `/var/log/myladtestlog` toohello `MyLadTestLog` 테이블</span><span class="sxs-lookup"><span data-stu-id="41989-532">Upload appended lines in file `/var/log/myladtestlog` toohello `MyLadTestLog` table</span></span>

<span data-ttu-id="41989-533">각각의 경우 데이터는 다음으로 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="41989-534">Azure Blob 저장소 (컨테이너 이름은 hello JsonBlob 싱크에 정의 된 대로)</span><span class="sxs-lookup"><span data-stu-id="41989-534">Azure Blob storage (container name is as defined in hello JsonBlob sink)</span></span>
* <span data-ttu-id="41989-535">EventHubs 끝점 (지정 된 대로 hello EventHubs 싱크에서)</span><span class="sxs-lookup"><span data-stu-id="41989-535">EventHubs endpoint (as specified in hello EventHubs sink)</span></span>

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

<span data-ttu-id="41989-536">hello `resourceId` hello에서 구성 설정의 hello VM 또는 hello 가상 컴퓨터 크기는 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-536">hello `resourceId` in hello configuration must match that of hello VM or hello virtual machine scale set.</span></span>

* <span data-ttu-id="41989-537">Azure 플랫폼 메트릭 차트 및 경고의 VM에서 작업 하는 hello hello resourceId를 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-537">Azure platform metrics charting and alerting knows hello resourceId of hello VM you're working on.</span></span> <span data-ttu-id="41989-538">Hello resourceId hello 조회 키를 사용 하 여 VM에 대 한 toofind hello 데이터를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-538">It expects toofind hello data for your VM using hello resourceId hello lookup key.</span></span>
* <span data-ttu-id="41989-539">Azure 자동 크기 조정을 사용 하는 경우 hello 자동 크기 조정 구성에 hello resourceId hello resourceId 했다에서 사용 하는 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-539">If you use Azure autoscale, hello resourceId in hello autoscale configuration must match hello resourceId used by LAD.</span></span>
* <span data-ttu-id="41989-540">hello resourceId 했다 기록한 JsonBlobs의 hello 이름으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="41989-540">hello resourceId is built into hello names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="41989-541">데이터 보기</span><span class="sxs-lookup"><span data-stu-id="41989-541">View your data</span></span>

<span data-ttu-id="41989-542">Hello Azure 포털 tooview 성능 데이터를 사용 하 여 또는 알림 설정:</span><span class="sxs-lookup"><span data-stu-id="41989-542">Use hello Azure portal tooview performance data or set alerts:</span></span>

![이미지](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="41989-544">hello `performanceCounters` 데이터는 항상 Azure 저장소 테이블에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41989-544">hello `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="41989-545">Azure Storage API는 다양한 언어 및 플랫폼에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="41989-546">데이터 전송 tooJsonBlob 싱크 hello에 명명 된 hello 저장소 계정에서 blob에 저장 됩니다 [보호 설정을](#protected-settings)합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-546">Data sent tooJsonBlob sinks is stored in blobs in hello storage account named in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="41989-547">모든 Azure Blob 저장소 Api를 사용 하 여 hello blob 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-547">You can consume hello blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="41989-548">또한 Azure 저장소에 이러한 UI 도구 tooaccess hello 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41989-548">In addition, you can use these UI tools tooaccess hello data in Azure Storage:</span></span>

* <span data-ttu-id="41989-549">Visual Studio 서버 탐색기.</span><span class="sxs-lookup"><span data-stu-id="41989-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="41989-550">[Microsoft Azure Storage 탐색기](https://azurestorageexplorer.codeplex.com/ "Azure Storage 탐색기").</span><span class="sxs-lookup"><span data-stu-id="41989-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="41989-551">이 스냅숏을 Microsoft Azure 저장소 탐색기 세션의 테스트 VM에서 올바르게 구성 된 했다 3.0 확장 프로그램에서 Azure 저장소 테이블 및 컨테이너를 생성 하는 hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-551">This snapshot of a Microsoft Azure Storage Explorer session shows hello generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="41989-552">hello 이미지 hello 정확히 일치 하지 않습니다. [샘플 했다 3.0 구성](#an-example-lad-30-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-552">hello image doesn't match exactly with hello [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![이미지](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="41989-554">Hello 관련 참조 [EventHubs 설명서](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn tooconsume 메시지 tooan EventHubs 끝점을 게시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="41989-554">See hello relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn how tooconsume messages published tooan EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41989-555">다음 단계</span><span class="sxs-lookup"><span data-stu-id="41989-555">Next steps</span></span>

* <span data-ttu-id="41989-556">메트릭 경고를 만들 [Azure 모니터](../../monitoring-and-diagnostics/insights-alerts-portal.md) hello 메트릭 수집에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for hello metrics you collect.</span></span>
* <span data-ttu-id="41989-557">메트릭에 대한 [모니터링 차트](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41989-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="41989-558">너무 방법에 대해 알아봅니다[가상 컴퓨터 크기 집합을 만들](/azure/virtual-machines/linux/tutorial-create-vmss) 메트릭 toocontrol 자동 크기 조정을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="41989-558">Learn how too[create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics toocontrol autoscaling.</span></span>
