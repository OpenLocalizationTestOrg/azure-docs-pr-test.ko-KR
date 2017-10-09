---
title: "CLI 샘플 Windows aaaAzure | Microsoft Docs"
description: "Azure CLI 샘플 Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1eef61a24d14897dd0a88a3f467854cc21b1938d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a><span data-ttu-id="d13bf-103">Windows 가상 컴퓨터에 대한 Azure CLI 샘플</span><span class="sxs-lookup"><span data-stu-id="d13bf-103">Azure CLI Samples for Windows virtual machines</span></span>

<span data-ttu-id="d13bf-104">hello 다음 표에 링크 toobash 있는 스크립트가 포함 되어 hello Azure CLI를 사용 하 여 빌드된 Windows 가상 컴퓨터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d13bf-104">hello following table includes links toobash scripts built using hello Azure CLI that deploy Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="d13bf-105">**가상 컴퓨터 만들기**</span><span class="sxs-lookup"><span data-stu-id="d13bf-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="d13bf-106">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="d13bf-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="d13bf-107">최소한의 구성으로 Windows 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d13bf-107">Creates a Windows virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="d13bf-108">완벽히 구성된 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="d13bf-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="d13bf-109">리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d13bf-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="d13bf-110">고가용성 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="d13bf-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="d13bf-111">고가용성의 부하가 분산된 구성으로 여러 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d13bf-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="d13bf-112">VM 만들기 및 구성 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="d13bf-112">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="d13bf-113">Hello Azure 사용자 지정 스크립트 확장 tooinstall IIS를 사용 하는 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d13bf-113">Creates a virtual machine and uses hello Azure Custom Script extension tooinstall IIS.</span></span> |
| [<span data-ttu-id="d13bf-114">VM 만들기 및 DSC 구성 실행</span><span class="sxs-lookup"><span data-stu-id="d13bf-114">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="d13bf-115">Hello Azure DSC 필요한 상태 구성 () 확장 tooinstall IIS를 사용 하는 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d13bf-115">Creates a virtual machine and uses hello Azure Desired State Configuration (DSC) extension tooinstall IIS.</span></span> |
|<span data-ttu-id="d13bf-116">**네트워크 가상 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="d13bf-116">**Network virtual machines**</span></span>||
| [<span data-ttu-id="d13bf-117">가상 컴퓨터 간의 네트워크 트래픽 보안</span><span class="sxs-lookup"><span data-stu-id="d13bf-117">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="d13bf-118">두 개의 가상 컴퓨터, 모든 관련된 리소스 및 내부 및 외부 NSG(네트워크 보안 그룹)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d13bf-118">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="d13bf-119">**가상 컴퓨터 보호**</span><span class="sxs-lookup"><span data-stu-id="d13bf-119">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="d13bf-120">VM 및 데이터 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="d13bf-120">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="d13bf-121">Azure Key Vault, 암호화 키 및 서비스 주체를 만든 다음 VM을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="d13bf-121">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="d13bf-122">**가상 컴퓨터 모니터링**</span><span class="sxs-lookup"><span data-stu-id="d13bf-122">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="d13bf-123">Operations Management Suite를 사용하여 VM 모니터링</span><span class="sxs-lookup"><span data-stu-id="d13bf-123">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="d13bf-124">가상 컴퓨터의 이름을 만들고 hello Operations Management Suite 에이전트를 설치 hello OMS 작업 영역에서 VM을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d13bf-124">Creates a virtual machine, installs hello Operations Management Suite agent, and enrolls hello VM in an OMS Workspace.</span></span>  |
| | |
