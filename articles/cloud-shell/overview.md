---
title: "Azure Cloud Shell(미리 보기) 개요 | Microsoft Docs"
description: "Azure Cloud Shell의 개요입니다."
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
ms.openlocfilehash: 7165633cd354eeea2e3619f839338e6af1524e56
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="1c6d1-103">Azure Cloud Shell(미리 보기) 개요</span><span class="sxs-lookup"><span data-stu-id="1c6d1-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="1c6d1-104">Azure Cloud Shell은 Azure 리소스를 관리하기 위한 브라우저에서 액세스할 수 있는 대화형 셸입니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="1c6d1-105">기능</span><span class="sxs-lookup"><span data-stu-id="1c6d1-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="1c6d1-106">브라우저 기반 셸 환경</span><span class="sxs-lookup"><span data-stu-id="1c6d1-106">Browser-based shell experience</span></span>
<span data-ttu-id="1c6d1-107">Cloud Shell은 Azure 관리 작업을 사용하여 빌드된 브라우저 기반 명령줄 환경에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-107">Cloud Shell enables access to a browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="1c6d1-108">Cloud Shell을 활용하여 클라우드가 제공할 수 있는 방식으로 로컬 컴퓨터에서 제한되지 않고 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-108">Leverage Cloud Shell to work untethered from a local machine in a way only the cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="1c6d1-109">Azure 미리 구성된 워크스테이션</span><span class="sxs-lookup"><span data-stu-id="1c6d1-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="1c6d1-110">사용자가 더 빠르게 작업할 수 있도록 Cloud Shell은 널리 사용되는 명령줄 도구 및 언어 지원이 미리 설치되어 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="1c6d1-111">여기에서 Azure Cloud Shell의 전체 도구 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-111">View the full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="1c6d1-112">자동 인증</span><span class="sxs-lookup"><span data-stu-id="1c6d1-112">Automatic authentication</span></span>
<span data-ttu-id="1c6d1-113">Cloud Shell은 Azure CLI 2.0을 통해 리소스에 즉시 액세스하도록 각 세션에서 자동으로 안전하게 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-113">Cloud Shell securely authenticates automatically on each session for instant access to your resources through the Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="1c6d1-114">Azure File Storage 연결</span><span class="sxs-lookup"><span data-stu-id="1c6d1-114">Connect your Azure File storage</span></span>
<span data-ttu-id="1c6d1-115">Cloud Shell 컴퓨터는 임시이며 결과적으로 Azure 파일 공유를 `clouddrive`로 탑재하도록 하여 $Home 디렉터리를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-115">Cloud Shell machines are temporary and as a result require an Azure file share to be mounted as `clouddrive` to persist your $Home directory.</span></span>
<span data-ttu-id="1c6d1-116">Cloud Shell를 첫 번째로 시작할 때 리소스 그룹, 저장소 계정 및 파일 공유를 만들라는 메시지가 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-116">On first launch Cloud Shell prompts to create a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="1c6d1-117">이는 일회성 단계이며 모든 세션에서 자동으로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="1c6d1-118">새 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="1c6d1-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="1c6d1-119">Azure 파일 공유를 사용하여 기본 5GB 디스크 이미지를 포함하는 LRS(로컬 중복 저장소) 계정이 자동으로 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="1c6d1-120">파일 공유는 $Home 디렉터리를 동기화하고 유지하는 데 사용되는 디스크 이미지와의 파일 공유 상호 작용을 위해 `clouddrive`로 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-120">The file share mounts as `clouddrive` for file share interaction with the disk image being used to sync and persist your $Home directory.</span></span> <span data-ttu-id="1c6d1-121">일반 저장소 비용이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-121">Regular storage costs apply.</span></span>

<span data-ttu-id="1c6d1-122">세 가지 리소스가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="1c6d1-123">리소스 그룹: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="1c6d1-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="1c6d1-124">저장소 계정: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="1c6d1-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="1c6d1-125">파일 공유: `cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="1c6d1-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="1c6d1-126">SSH 키와 같이 $Home 디렉터리의 모든 파일은 탑재된 파일 공유에 저장된 사용자 디스크 이미지에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="1c6d1-127">$Home 디렉터리 및 탑재된 파일 공유에서 파일을 저장하는 경우 모범 사례를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="1c6d1-128">기존 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="1c6d1-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="1c6d1-129">기존 리소스를 Cloud Shell에 연결할 수 있도록 하는 고급 옵션도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-129">An advanced option is also provided allowing you to associate existing resources to Cloud Shell.</span></span> <span data-ttu-id="1c6d1-130">저장소 설정 프롬프트가 나타나면 "고급 설정 표시"를 클릭하여 추가 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-130">When presented with the storage setup prompt, click "Show advanced settings" to select additional options.</span></span> <span data-ttu-id="1c6d1-131">드롭다운이 필터링되면서 할당된 Cloud Shell 하위 지역 및 로컬/전역 중복 저장소 계정이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="1c6d1-132">[Cloud Shell 저장소, 파일 공유 업데이트 및 파일 업로드/다운로드에 대해 자세히 알아봅니다.](persisting-shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="1c6d1-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="1c6d1-133">개념</span><span class="sxs-lookup"><span data-stu-id="1c6d1-133">Concepts</span></span>
* <span data-ttu-id="1c6d1-134">Cloud Shell은 세션 별, 사용자 단위 기준으로 제공된 임시 컴퓨터에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="1c6d1-135">Cloud Shell은 대화형 작업 없이 20분 후에 시간이 초과됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="1c6d1-136">Cloud Shell은 첨부된 파일 공유를 사용하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="1c6d1-137">Cloud Shell은 사용자 계정 별로 하나의 컴퓨터를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="1c6d1-138">사용 권한은 일반적인 Linux 사용자로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="1c6d1-139">Cloud Shell의 모든 기능에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="1c6d1-140">예</span><span class="sxs-lookup"><span data-stu-id="1c6d1-140">Examples</span></span>
* <span data-ttu-id="1c6d1-141">스크립트를 만들거나 편집하여 Azure 관리 자동화</span><span class="sxs-lookup"><span data-stu-id="1c6d1-141">Create or edit scripts to automate Azure management</span></span>
* <span data-ttu-id="1c6d1-142">Azure Portal 및 Azure CLI 2.0을 통해 리소스를 동시에 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="1c6d1-143">Azure CLI를 2.0을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="1c6d1-144">Cloud Shell 빠른 시작에서 이러한 모든 예제를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-144">Try out all these examples at the Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="1c6d1-145">가격</span><span class="sxs-lookup"><span data-stu-id="1c6d1-145">Pricing</span></span>
<span data-ttu-id="1c6d1-146">$Home 디렉터리를 유지하기 위해 탑재된 Azure 파일 공유의 필수 구성 요소를 포함하여 Cloud Shell을 호스팅하는 컴퓨터는 추가 비용 없이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-146">The machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share to persist your $Home directory.</span></span> <span data-ttu-id="1c6d1-147">일반 저장소 비용이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="1c6d1-148">지원되는 브라우저</span><span class="sxs-lookup"><span data-stu-id="1c6d1-148">Supported browsers</span></span>
<span data-ttu-id="1c6d1-149">Cloud Shell은 Chrome, Edge 및 Safari에 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="1c6d1-150">Cloud Shell은 Chrome, Firefox, Safari, IE 및 Edge에서 지원되지만 특정 브라우저 설정에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject to specific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1c6d1-151">문제 해결</span><span class="sxs-lookup"><span data-stu-id="1c6d1-151">Troubleshooting</span></span>
1. <span data-ttu-id="1c6d1-152">Azure Active Directory 구독을 사용할 경우 오류: 400 DisallowedOperation으로 인해 저장소를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-152">When using an Azure Active Directory subscription, I cannot create storage due to Error: 400 DisallowedOperation.</span></span> <span data-ttu-id="1c6d1-153">이 문제를 해결하려면 저장소 리소스를 만들 수 있는 Azure 구독을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-153">To resolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="1c6d1-154">AD 구독으로는 Azure 리소스를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-154">AD subscriptions are not able to create Azure resources.</span></span>

<span data-ttu-id="1c6d1-155">알려진 특별한 제한 사항은 [Cloud Shell 제한 사항](limitations.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
