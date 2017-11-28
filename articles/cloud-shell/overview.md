---
title: "aaaAzure 클라우드 셸 (미리 보기) 개요 | Microsoft Docs"
description: "Azure 클라우드 셸 hello 간략하게 설명 합니다."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="a5e36-103">Azure Cloud Shell(미리 보기) 개요</span><span class="sxs-lookup"><span data-stu-id="a5e36-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="a5e36-104">Azure Cloud Shell은 Azure 리소스를 관리하기 위한 브라우저에서 액세스할 수 있는 대화형 셸입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="a5e36-105">기능</span><span class="sxs-lookup"><span data-stu-id="a5e36-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="a5e36-106">브라우저 기반 셸 환경</span><span class="sxs-lookup"><span data-stu-id="a5e36-106">Browser-based shell experience</span></span>
<span data-ttu-id="a5e36-107">셸 수 있도록 액세스 tooa 브라우저 기반 명령줄 환경을 Azure 관리 작업을 고려를 사용 하 여 빌드한 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-107">Cloud Shell enables access tooa browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="a5e36-108">Hello 클라우드만 제공할 수 방식으로 로컬 컴퓨터에서 제한 되지 않는 클라우드 셸 toowork를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-108">Leverage Cloud Shell toowork untethered from a local machine in a way only hello cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="a5e36-109">Azure 미리 구성된 워크스테이션</span><span class="sxs-lookup"><span data-stu-id="a5e36-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="a5e36-110">사용자가 더 빠르게 작업할 수 있도록 Cloud Shell은 널리 사용되는 명령줄 도구 및 언어 지원이 미리 설치되어 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="a5e36-111">보기 hello 전체 도구 목록 Azure 클라우드 셸용 여기입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-111">View hello full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="a5e36-112">자동 인증</span><span class="sxs-lookup"><span data-stu-id="a5e36-112">Automatic authentication</span></span>
<span data-ttu-id="a5e36-113">클라우드 셸을 안전 하 게 Azure CLI 2.0 hello 통해 즉시 액세스 tooyour 리소스에 대 한 각 세션에서 자동으로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-113">Cloud Shell securely authenticates automatically on each session for instant access tooyour resources through hello Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="a5e36-114">Azure File Storage 연결</span><span class="sxs-lookup"><span data-stu-id="a5e36-114">Connect your Azure File storage</span></span>
<span data-ttu-id="a5e36-115">클라우드 셸 컴퓨터 임시 되며 결과적으로 Azure 파일 공유 toobe로 탑재 해야 `clouddrive` toopersist $Home 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-115">Cloud Shell machines are temporary and as a result require an Azure file share toobe mounted as `clouddrive` toopersist your $Home directory.</span></span>
<span data-ttu-id="a5e36-116">첫 번째 실행에서 클라우드 셸 메시지 toocreate 사용자 대신 리소스 그룹, 저장소 계정 및 파일 공유를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-116">On first launch Cloud Shell prompts toocreate a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="a5e36-117">이는 일회성 단계이며 모든 세션에서 자동으로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="a5e36-118">새 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="a5e36-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="a5e36-119">Azure 파일 공유를 사용하여 기본 5GB 디스크 이미지를 포함하는 LRS(로컬 중복 저장소) 계정이 자동으로 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="a5e36-120">hello 파일 공유로 탑재할 `clouddrive` 파일에 대 한 공유 hello 디스크 이미지와의 상호 작용 사용된 toosync 되 고 $Home 디렉터리를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-120">hello file share mounts as `clouddrive` for file share interaction with hello disk image being used toosync and persist your $Home directory.</span></span> <span data-ttu-id="a5e36-121">일반 저장소 비용이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-121">Regular storage costs apply.</span></span>

<span data-ttu-id="a5e36-122">세 가지 리소스가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="a5e36-123">리소스 그룹: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="a5e36-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="a5e36-124">저장소 계정: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="a5e36-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="a5e36-125">파일 공유: `cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="a5e36-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="a5e36-126">SSH 키와 같이 $Home 디렉터리의 모든 파일은 탑재된 파일 공유에 저장된 사용자 디스크 이미지에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="a5e36-127">$Home 디렉터리 및 탑재된 파일 공유에서 파일을 저장하는 경우 모범 사례를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="a5e36-128">기존 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="a5e36-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="a5e36-129">고급 옵션에는 가능 하면 tooassociate 기존 리소스 tooCloud 셸도 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-129">An advanced option is also provided allowing you tooassociate existing resources tooCloud Shell.</span></span> <span data-ttu-id="a5e36-130">Hello 저장소 설정 프롬프트가 나타나면 "Show advanced settings" tooselect 추가 옵션을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-130">When presented with hello storage setup prompt, click "Show advanced settings" tooselect additional options.</span></span> <span data-ttu-id="a5e36-131">드롭다운이 필터링되면서 할당된 Cloud Shell 하위 지역 및 로컬/전역 중복 저장소 계정이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="a5e36-132">[Cloud Shell 저장소, 파일 공유 업데이트 및 파일 업로드/다운로드에 대해 자세히 알아봅니다.](persisting-shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="a5e36-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="a5e36-133">개념</span><span class="sxs-lookup"><span data-stu-id="a5e36-133">Concepts</span></span>
* <span data-ttu-id="a5e36-134">Cloud Shell은 세션 별, 사용자 단위 기준으로 제공된 임시 컴퓨터에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="a5e36-135">Cloud Shell은 대화형 작업 없이 20분 후에 시간이 초과됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="a5e36-136">Cloud Shell은 첨부된 파일 공유를 사용하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="a5e36-137">Cloud Shell은 사용자 계정 별로 하나의 컴퓨터를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="a5e36-138">사용 권한은 일반적인 Linux 사용자로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="a5e36-139">Cloud Shell의 모든 기능에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="a5e36-140">예</span><span class="sxs-lookup"><span data-stu-id="a5e36-140">Examples</span></span>
* <span data-ttu-id="a5e36-141">만들기 또는 편집 스크립트 tooautomate Azure 관리</span><span class="sxs-lookup"><span data-stu-id="a5e36-141">Create or edit scripts tooautomate Azure management</span></span>
* <span data-ttu-id="a5e36-142">Azure Portal 및 Azure CLI 2.0을 통해 리소스를 동시에 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="a5e36-143">Azure CLI를 2.0을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="a5e36-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="a5e36-144">Hello 셸 클라우드 빠른 시작에서 이러한 모든 예를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-144">Try out all these examples at hello Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="a5e36-145">가격</span><span class="sxs-lookup"><span data-stu-id="a5e36-145">Pricing</span></span>
<span data-ttu-id="a5e36-146">클라우드 셸을 호스트 하는 hello 컴퓨터는 무료, 탑재 된 Azure 파일의 필수 공유 toopersist $Home 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-146">hello machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share toopersist your $Home directory.</span></span> <span data-ttu-id="a5e36-147">일반 저장소 비용이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="a5e36-148">지원되는 브라우저</span><span class="sxs-lookup"><span data-stu-id="a5e36-148">Supported browsers</span></span>
<span data-ttu-id="a5e36-149">Cloud Shell은 Chrome, Edge 및 Safari에 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="a5e36-150">클라우드 Shell은 Chrome, Firefox, Safari, IE, 및 가장자리에 대 한 지원 되지만, 클라우드 셸은 주체 toospecific 브라우저 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject toospecific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a5e36-151">문제 해결</span><span class="sxs-lookup"><span data-stu-id="a5e36-151">Troubleshooting</span></span>
1. <span data-ttu-id="a5e36-152">Azure Active Directory 구독을 사용할 경우 저장소를 만들 수 없는 경우 due tooError: 400 DisallowedOperation 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-152">When using an Azure Active Directory subscription, I cannot create storage due tooError: 400 DisallowedOperation.</span></span> <span data-ttu-id="a5e36-153">tooresolve이 저장소 리소스를 만들 수 있는 Azure 구독을 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a5e36-153">tooresolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="a5e36-154">AD 구독 수 없습니다. toocreate Azure 리소스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5e36-154">AD subscriptions are not able toocreate Azure resources.</span></span>

<span data-ttu-id="a5e36-155">알려진 특별한 제한 사항은 [Cloud Shell 제한 사항](limitations.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="a5e36-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
