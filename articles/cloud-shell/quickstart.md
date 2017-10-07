---
title: "aaaAzure 클라우드 셸 (미리 보기) 빠른 시작 | Microsoft Docs"
description: "Azure 클라우드 셸 hello에 대 한 빠른 시작"
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
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a><span data-ttu-id="89855-103">Azure 클라우드 셸 hello를 사용 하 여에 대 한 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="89855-103">Quickstart for using hello Azure Cloud Shell</span></span>

<span data-ttu-id="89855-104">이 문서에 toouse Azure 클라우드 셸 hello에 hello 하는 방법을 자세히 설명 [Azure 포털](https://ms.portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="89855-104">This document details how toouse hello Azure Cloud Shell in hello [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="89855-105">Cloud Shell 시작</span><span class="sxs-lookup"><span data-stu-id="89855-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="89855-106">시작 **클라우드 셸** hello Azure 포털의 위쪽 탐색 hello에서</span><span class="sxs-lookup"><span data-stu-id="89855-106">Launch **Cloud Shell** from hello top navigation of hello Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="89855-107">구독 toocreate 저장소 계정 및 Azure 파일 공유 선택</span><span class="sxs-lookup"><span data-stu-id="89855-107">Select a subscription toocreate a storage account and Azure file share</span></span>
3. <span data-ttu-id="89855-108">"저장소 만들기"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89855-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="89855-109">모든 세션에서 Azure CLI 2.0에 대해 자동으로 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="89855-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="89855-110">구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="89855-110">Set your subscription</span></span>
1. <span data-ttu-id="89855-111">액세스할 수 있는 구독을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="89855-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="89855-112">기본 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="89855-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="89855-113">`/home/<user>/.azure/azureProfile.json`을 사용하여 이후 세션에서 구독을 기억합니다.</span><span class="sxs-lookup"><span data-stu-id="89855-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="89855-114">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="89855-114">Create a resource group</span></span>
<span data-ttu-id="89855-115">미국 서부에 “MyRG”라는 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89855-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="89855-116">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="89855-116">Create a Linux VM</span></span>
<span data-ttu-id="89855-117">새 리소스 그룹에서 Ubuntu VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89855-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="89855-118">이러한 SSH 키 및 설치 hello VM hello Azure CLI 2.0 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="89855-118">hello Azure CLI 2.0 will create SSH keys and setup hello VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="89855-119">VM에 배치 되는 사용 되는 공용 및 개인 키 tooauthenticate hello `/User/.ssh/id_rsa` 및 `/User/.ssh/id_rsa.pub` 기본적으로 Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="89855-119">hello public and private keys used tooauthenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="89855-120">.ssh 폴더는 연결된 Azure 파일 공유의 5GB 이미지에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="89855-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="89855-121">이 VM의 사용자 이름은 Cloud Shell에서 사용되는 사용자 이름입니다($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="89855-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="89855-122">Linux VM으로 SSH</span><span class="sxs-lookup"><span data-stu-id="89855-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="89855-123">Hello Azure 포털 검색 표시줄에서 VM 이름을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="89855-123">Search for your VM name in hello Azure portal search bar</span></span>
2. <span data-ttu-id="89855-124">"연결"을 클릭하고 다음을 실행합니다.`ssh username@ipaddress`</span><span class="sxs-lookup"><span data-stu-id="89855-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="89855-125">Hello SSH 연결을 설정할 때 Ubuntu 시작 프롬프트 hello 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89855-125">Upon establishing hello SSH connection, you should see hello Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="89855-126">정리</span><span class="sxs-lookup"><span data-stu-id="89855-126">Cleaning up</span></span> 
<span data-ttu-id="89855-127">리소스 그룹 및 해당 그룹 내의 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="89855-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="89855-128">`az group delete -n MyRG`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="89855-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="89855-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="89855-129">Next Steps</span></span>
[<span data-ttu-id="89855-130">Cloud Shell의 저장소 유지 알아보기</span><span class="sxs-lookup"><span data-stu-id="89855-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="89855-131">
[Azure CLI 2.0에 대해 알아보기](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="89855-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="89855-132">
[Azure File Storage에 대해 알아보기](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="89855-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>