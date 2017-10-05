---
title: "Azure Cloud Shell(미리 보기) 빠른 시작 | Microsoft Docs"
description: "Azure Cloud Shell의 빠른 시작"
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
ms.openlocfilehash: 75676eb0ab784e2adbfd27b170c1dee5599b74ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-for-using-the-azure-cloud-shell"></a><span data-ttu-id="5b1c9-103">Azure Cloud Shell을 사용하는 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="5b1c9-103">Quickstart for using the Azure Cloud Shell</span></span>

<span data-ttu-id="5b1c9-104">이 문서에서는 [Azure Portal](https://ms.portal.azure.com/)에서 Azure Cloud Shell을 사용하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-104">This document details how to use the Azure Cloud Shell in the [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="5b1c9-105">Cloud Shell 시작</span><span class="sxs-lookup"><span data-stu-id="5b1c9-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="5b1c9-106">Azure Portal의 위쪽 탐색 모음에서 **Cloud Shell**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-106">Launch **Cloud Shell** from the top navigation of the Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="5b1c9-107">구독을 선택하여 저장소 계정 및 Azure 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="5b1c9-107">Select a subscription to create a storage account and Azure file share</span></span>
3. <span data-ttu-id="5b1c9-108">"저장소 만들기"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="5b1c9-109">모든 세션에서 Azure CLI 2.0에 대해 자동으로 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="5b1c9-110">구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-110">Set your subscription</span></span>
1. <span data-ttu-id="5b1c9-111">액세스할 수 있는 구독을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="5b1c9-112">기본 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="5b1c9-113">`/home/<user>/.azure/azureProfile.json`을 사용하여 이후 세션에서 구독을 기억합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="5b1c9-114">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="5b1c9-114">Create a resource group</span></span>
<span data-ttu-id="5b1c9-115">미국 서부에 “MyRG”라는 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="5b1c9-116">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="5b1c9-116">Create a Linux VM</span></span>
<span data-ttu-id="5b1c9-117">새 리소스 그룹에서 Ubuntu VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="5b1c9-118">Azure CLI 2.0은 SSH 키를 만들고 해당 키를 사용하여 VM을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-118">The Azure CLI 2.0 will create SSH keys and setup the VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="5b1c9-119">VM을 인증하는 데 사용된 공개 및 개인 키는 기본적으로 Azure CLI 2.0에 의해 `/User/.ssh/id_rsa` 및 `/User/.ssh/id_rsa.pub`에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-119">The public and private keys used to authenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="5b1c9-120">.ssh 폴더는 연결된 Azure 파일 공유의 5GB 이미지에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="5b1c9-121">이 VM의 사용자 이름은 Cloud Shell에서 사용되는 사용자 이름입니다($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="5b1c9-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="5b1c9-122">Linux VM으로 SSH</span><span class="sxs-lookup"><span data-stu-id="5b1c9-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="5b1c9-123">Azure Portal 검색 표시줄에서 VM 이름을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-123">Search for your VM name in the Azure portal search bar</span></span>
2. <span data-ttu-id="5b1c9-124">"연결"을 클릭하고 다음을 실행합니다.`ssh username@ipaddress`</span><span class="sxs-lookup"><span data-stu-id="5b1c9-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="5b1c9-125">SSH 연결을 설정할 때 Ubuntu 시작 프롬프트가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-125">Upon establishing the SSH connection, you should see the Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="5b1c9-126">정리</span><span class="sxs-lookup"><span data-stu-id="5b1c9-126">Cleaning up</span></span> 
<span data-ttu-id="5b1c9-127">리소스 그룹 및 해당 그룹 내의 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="5b1c9-128">`az group delete -n MyRG`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1c9-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b1c9-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5b1c9-129">Next Steps</span></span>
[<span data-ttu-id="5b1c9-130">Cloud Shell의 저장소 유지 알아보기</span><span class="sxs-lookup"><span data-stu-id="5b1c9-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="5b1c9-131">
[Azure CLI 2.0에 대해 알아보기](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="5b1c9-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="5b1c9-132">
[Azure File Storage에 대해 알아보기](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="5b1c9-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>