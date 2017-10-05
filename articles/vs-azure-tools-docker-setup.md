---
title: "VirtualBox 및 Docker 호스트 구성 | Microsoft Docs"
description: "Docker 컴퓨터 및 VirtualBox를 사용하여 기본 Docker 인스턴스를 구성하는 단계별 지침입니다."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: e9465afb560a73d74f853c19094b3ee75b8c470c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="ed5c5-103">VirtualBox 및 Docker 호스트 구성</span><span class="sxs-lookup"><span data-stu-id="ed5c5-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="ed5c5-104">개요</span><span class="sxs-lookup"><span data-stu-id="ed5c5-104">Overview</span></span>
<span data-ttu-id="ed5c5-105">이 문서에서는 Docker 컴퓨터 및 VirtualBox를 사용하여 기본 Docker 인스턴스를 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5c5-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="ed5c5-106">[Windows 베타용 Docker](http://beta.docker.com/)를 사용하는 경우 이 구성은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5c5-106">If you’re using the [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed5c5-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ed5c5-107">Prerequisites</span></span>
<span data-ttu-id="ed5c5-108">다음과 같은 도구를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5c5-108">The following tools need to be installed.</span></span>

* [<span data-ttu-id="ed5c5-109">Docker 도구 상자</span><span class="sxs-lookup"><span data-stu-id="ed5c5-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-the-docker-client-with-windows-powershell"></a><span data-ttu-id="ed5c5-110">Windows PowerShell과 함께 Docker 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="ed5c5-110">Configuring the Docker client with Windows PowerShell</span></span>
<span data-ttu-id="ed5c5-111">Docker 클라이언트를 구성하려면 단순히 Windows PowerShell을 열고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5c5-111">To configure a Docker client, simply open Windows PowerShell, and perform the following steps:</span></span>

1. <span data-ttu-id="ed5c5-112">기본 docker 호스트 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed5c5-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="ed5c5-113">기본 인스턴스가 구성되어 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5c5-113">Verify the default instance is configured and running.</span></span> <span data-ttu-id="ed5c5-114">('기본'이라는 인스턴스가 실행되는 것이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed5c5-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker-machine ls output][0]
3. <span data-ttu-id="ed5c5-116">기본값을 현재 호스트로 설정하고 셸을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5c5-116">Set default as the current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="ed5c5-117">활성 Docker 컨테이너를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5c5-117">Display the active Docker containers.</span></span> <span data-ttu-id="ed5c5-118">목록이 비어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5c5-118">The list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps output][1]

> [!NOTE]
> <span data-ttu-id="ed5c5-120">개발 컴퓨터를 다시 부팅할 때마다 로컬 Docker 호스트를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5c5-120">Each time you reboot your development machine, you’ll need to restart your local docker host.</span></span>
> <span data-ttu-id="ed5c5-121">이렇게 하려면 명령 프롬프트에서 다음 명령을 실행합니다. `docker-machine start default`</span><span class="sxs-lookup"><span data-stu-id="ed5c5-121">To do this, issue the following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
