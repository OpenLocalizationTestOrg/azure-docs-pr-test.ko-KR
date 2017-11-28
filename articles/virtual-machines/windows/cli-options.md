---
title: "Windows에서 Azure CLI 사용 | Microsoft Docs"
description: "Windows에서 Azure CLI 사용"
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
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: be02ad0d7752cb08f092deeb5a86dcd126403237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-on-windows"></a><span data-ttu-id="b1fd8-103">Windows에서 Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="b1fd8-103">Using the Azure CLI on Windows</span></span>

<span data-ttu-id="b1fd8-104">Azure CLI(명령줄 인터페이스)는 Azure 리소스를 만들고 관리하는 명령줄 및 스크립팅 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-104">The Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="b1fd8-105">Azure CLI는 macOS, Linux 및 Windows 운영 체제에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-105">The Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="b1fd8-106">하지만 이러한 운영 체제에서 CLI 명령은 동일하지만 운영 체제 특정 스크립팅 구문은 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-106">Across these operating systems, the CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="b1fd8-107">이 문서에서는 Windows에서 Azure CLI를 설치하고 실행할 수 있는 방법 및 각각에 대한 구문 관련 고려 사항을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-107">This document details the ways that the Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="b1fd8-108">Azure CLI 설명서에 대한 자세한 내용은 [Azure CLI 설명서]( https://docs.microsoft.com/en-us/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="b1fd8-109">Linux용 Windows 하위 시스템</span><span class="sxs-lookup"><span data-stu-id="b1fd8-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="b1fd8-110">Linux용 Windows 하위 시스템(WSL)는 Windows 10 Anniversary 및 이후 버전에서 Ubuntu Linux 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-110">The Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="b1fd8-111">WSL를 사용하도록 설정하면 네이티브 Bash 환경을 제공합니다. 이 기능은 Azure CLI 스크립트를 만들고 실행하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="b1fd8-112">WSL에서 네이티브 Bash 환경을 제공하기 때문에 Azure CLI 스크립트를 수정하지 않고 macOS, Linux 및 Windows 간에 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="b1fd8-113">WSL에서 Azure CLI를 사용하려면 다음을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-113">To use the Azure CLI in WSL, complete the following.</span></span>

|<span data-ttu-id="b1fd8-114">작업</span><span class="sxs-lookup"><span data-stu-id="b1fd8-114">Task</span></span> | <span data-ttu-id="b1fd8-115">지침</span><span class="sxs-lookup"><span data-stu-id="b1fd8-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="b1fd8-116">WSL 사용</span><span class="sxs-lookup"><span data-stu-id="b1fd8-116">Enable WSL</span></span> | [<span data-ttu-id="b1fd8-117">WSL 설명서 설치</span><span class="sxs-lookup"><span data-stu-id="b1fd8-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="b1fd8-118">Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="b1fd8-118">Install the Azure CLI</span></span> |[<span data-ttu-id="b1fd8-119">WSL/Ubuntu 14.04에서 CLI 설치</span><span class="sxs-lookup"><span data-stu-id="b1fd8-119">Install the CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="b1fd8-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1fd8-120">PowerShell</span></span>

<span data-ttu-id="b1fd8-121">Windows에서 기본적으로 Azure CLI를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-121">The Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="b1fd8-122">이 구성에서는 Windows 운영 체제에서 Azure CLI 패키지를 설치하고 PowerShell의 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-122">In this configuration, the Azure CLI package is installed on the Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="b1fd8-123">이 구성에서는 지원되는 버전의 Windows에서 Azure CLI 명령 및 스크립트를 실행할 수 있지만 플랫폼 지정 스크립트 구문이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="b1fd8-124">이런 이유로 macOS, Linux 및 Windows 스크립트를 모두 수정하지 않고 공유할 수 있는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="b1fd8-125">Windows에서 Azure CLI를 사용하려면 [Windows에서 CLI 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows)의 지침을 사용하여 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-125">To use the Azure CLI on Windows, install the package using these instructions, [Install the CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="b1fd8-126">Docker 이미지</span><span class="sxs-lookup"><span data-stu-id="b1fd8-126">Docker Image</span></span>

<span data-ttu-id="b1fd8-127">Windows용 Docker를 사용하여 Azure CLI를 포함하는 Docker 이미지를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-127">When using Docker for Windows, a Docker image can be started that includes the Azure CLI.</span></span> <span data-ttu-id="b1fd8-128">이 이미지는 Linux에서 기반으로 하며 네이티브 Bash 환경을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="b1fd8-129">Windows용 Docker 및 Azure CLI 이미지를 사용하면 스크립트를 macOS, Linux 및 Windows 간에 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-129">When using Docker for Windows and the Azure CLI image, scripts to be shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="b1fd8-130">Windows용 Docker에서 Azure CLI를 사용하려면 Windows용 Docker가 실행되고 있는지 확인하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-130">To use the Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run the following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="b1fd8-131">Bash 세션을 완료하면 Azure CLI 도구를 사용하여 미리 로드되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b1fd8-131">Once completed, a Bash session will start that is preloaded with the Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1fd8-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1fd8-132">Next Steps</span></span>

[<span data-ttu-id="b1fd8-133">Azure Virtual Machines에 대한 CLI 샘플</span><span class="sxs-lookup"><span data-stu-id="b1fd8-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="b1fd8-134">Azure Web Apps에 대한 CLI 샘플</span><span class="sxs-lookup"><span data-stu-id="b1fd8-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="b1fd8-135">Azure SQL에 대한 CLI 샘플</span><span class="sxs-lookup"><span data-stu-id="b1fd8-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
