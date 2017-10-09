---
title: windows Azure CLI aaaUsing hello | Microsoft Docs
description: "Windows hello Azure CLI를 사용 하 여"
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
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a><span data-ttu-id="2e5fb-103">Windows hello Azure CLI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2e5fb-103">Using hello Azure CLI on Windows</span></span>

<span data-ttu-id="2e5fb-104">Azure 명령줄 인터페이스 (CLI) hello 명령줄 및 스크립팅 환경 만들기 및 Azure 리소스 관리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-104">hello Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="2e5fb-105">macOS, Linux 및 Windows 운영 체제에 대 한 hello Azure CLI ´ ù.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-105">hello Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="2e5fb-106">하지만 이러한 운영 체제에서 hello CLI 명령을 동일 운영 체제 특정 스크립팅 구문 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-106">Across these operating systems, hello CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="2e5fb-107">이 문서 정보 hello 방식 Azure CLI hello에 설치 하 고 각각에 대 한 구문 고려 사항 창과 세부 정보에서 실행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-107">This document details hello ways that hello Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="2e5fb-108">Azure CLI 설명서에 대한 자세한 내용은 [Azure CLI 설명서]( https://docs.microsoft.com/en-us/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="2e5fb-109">Linux용 Windows 하위 시스템</span><span class="sxs-lookup"><span data-stu-id="2e5fb-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="2e5fb-110">hello Windows 하위 시스템 Linux (WSL)는 Windows 10 Anniversary 및 이후 버전에서 Ubuntu Linux 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-110">hello Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="2e5fb-111">WSL를 사용하도록 설정하면 네이티브 Bash 환경을 제공합니다. 이 기능은 Azure CLI 스크립트를 만들고 실행하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="2e5fb-112">WSL에서 네이티브 Bash 환경을 제공하기 때문에 Azure CLI 스크립트를 수정하지 않고 macOS, Linux 및 Windows 간에 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="2e5fb-113">toouse hello Azure CLI WSL에 hello 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-113">toouse hello Azure CLI in WSL, complete hello following.</span></span>

|<span data-ttu-id="2e5fb-114">작업</span><span class="sxs-lookup"><span data-stu-id="2e5fb-114">Task</span></span> | <span data-ttu-id="2e5fb-115">지침</span><span class="sxs-lookup"><span data-stu-id="2e5fb-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="2e5fb-116">WSL 사용</span><span class="sxs-lookup"><span data-stu-id="2e5fb-116">Enable WSL</span></span> | [<span data-ttu-id="2e5fb-117">WSL 설명서 설치</span><span class="sxs-lookup"><span data-stu-id="2e5fb-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="2e5fb-118">Hello Azure CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-118">Install hello Azure CLI</span></span> |[<span data-ttu-id="2e5fb-119">WSL/Ubuntu 14.04에 hello CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-119">Install hello CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="2e5fb-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e5fb-120">PowerShell</span></span>

<span data-ttu-id="2e5fb-121">windows에서 hello Azure CLI를 고유 하 게 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-121">hello Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="2e5fb-122">이 구성에서는 hello Azure CLI 패키지 hello Windows 운영 체제에 설치 되어 및 PowerShell에서 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-122">In this configuration, hello Azure CLI package is installed on hello Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="2e5fb-123">이 구성에서는 지원되는 버전의 Windows에서 Azure CLI 명령 및 스크립트를 실행할 수 있지만 플랫폼 지정 스크립트 구문이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="2e5fb-124">이런 이유로 macOS, Linux 및 Windows 스크립트를 모두 수정하지 않고 공유할 수 있는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="2e5fb-125">이러한 지침을 사용 하 여 hello 패키지를 설치 하는 windows에서 Azure CLI toouse hello [설치 hello Windows에서 CLI](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-125">toouse hello Azure CLI on Windows, install hello package using these instructions, [Install hello CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="2e5fb-126">Docker 이미지</span><span class="sxs-lookup"><span data-stu-id="2e5fb-126">Docker Image</span></span>

<span data-ttu-id="2e5fb-127">Windows 용 Docker를 사용 하 여 hello Azure CLI를 포함 하는 Docker 이미지 수 있습니다. 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-127">When using Docker for Windows, a Docker image can be started that includes hello Azure CLI.</span></span> <span data-ttu-id="2e5fb-128">이 이미지는 Linux에서 기반으로 하며 네이티브 Bash 환경을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="2e5fb-129">Windows 용 Docker 및 hello Azure CLI 이미지, 스크립트 toobe macOS, Linux 및 Windows에서 공유할을 사용할 때</span><span class="sxs-lookup"><span data-stu-id="2e5fb-129">When using Docker for Windows and hello Azure CLI image, scripts toobe shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="2e5fb-130">Windows 용 Docker에 Azure CLI toouse hello Windows 용 Docker 실행 되 고 hello 다음 명령을 실행을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-130">toouse hello Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run hello following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="2e5fb-131">완료 되 면 시작 합니다 즉 Bash hello Azure CLI 도구와 함께 미리 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5fb-131">Once completed, a Bash session will start that is preloaded with hello Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e5fb-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2e5fb-132">Next Steps</span></span>

[<span data-ttu-id="2e5fb-133">Azure Virtual Machines에 대한 CLI 샘플</span><span class="sxs-lookup"><span data-stu-id="2e5fb-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="2e5fb-134">Azure Web Apps에 대한 CLI 샘플</span><span class="sxs-lookup"><span data-stu-id="2e5fb-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="2e5fb-135">Azure SQL에 대한 CLI 샘플</span><span class="sxs-lookup"><span data-stu-id="2e5fb-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
