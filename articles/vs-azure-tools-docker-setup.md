---
title: "Docker 호스트를 VirtualBox aaaConfigure | Microsoft Docs"
description: "단계별 지침은 tooconfigure 기본 Docker는 Docker 컴퓨터 및 VirtualBox 사용 하 여 인스턴스"
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
ms.openlocfilehash: 1df2da4482444a803d05e413e019edcc57269062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="6ce97-103">VirtualBox 및 Docker 호스트 구성</span><span class="sxs-lookup"><span data-stu-id="6ce97-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="6ce97-104">개요</span><span class="sxs-lookup"><span data-stu-id="6ce97-104">Overview</span></span>
<span data-ttu-id="6ce97-105">이 문서에서는 Docker 컴퓨터 및 VirtualBox를 사용하여 기본 Docker 인스턴스를 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="6ce97-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="6ce97-106">Hello를 사용 하 여 [Windows 용 Docker beta](http://beta.docker.com/),이 구성은 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ce97-106">If you’re using hello [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ce97-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6ce97-107">Prerequisites</span></span>
<span data-ttu-id="6ce97-108">hello 다음과 같은 도구가 필요 toobe 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ce97-108">hello following tools need toobe installed.</span></span>

* [<span data-ttu-id="6ce97-109">Docker 도구 상자</span><span class="sxs-lookup"><span data-stu-id="6ce97-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a><span data-ttu-id="6ce97-110">Windows PowerShell을 사용 하 여 hello Docker 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="6ce97-110">Configuring hello Docker client with Windows PowerShell</span></span>
<span data-ttu-id="6ce97-111">tooconfigure Docker 클라이언트 하기만 하면 Windows PowerShell을 열고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ce97-111">tooconfigure a Docker client, simply open Windows PowerShell, and perform hello following steps:</span></span>

1. <span data-ttu-id="6ce97-112">기본 docker 호스트 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ce97-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="6ce97-113">Hello 기본 인스턴스는 구성 하 고 실행을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ce97-113">Verify hello default instance is configured and running.</span></span> <span data-ttu-id="6ce97-114">('기본'이라는 인스턴스가 실행되는 것이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ce97-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker-machine ls output][0]
3. <span data-ttu-id="6ce97-116">Hello 현재 호스트와 기본값을 설정 하 고 셸에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ce97-116">Set default as hello current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="6ce97-117">Hello 활성 Docker 컨테이너를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ce97-117">Display hello active Docker containers.</span></span> <span data-ttu-id="6ce97-118">hello 목록 비어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ce97-118">hello list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps output][1]

> [!NOTE]
> <span data-ttu-id="6ce97-120">개발 컴퓨터를 다시 부팅 될 때마다 해야 toorestart 로컬 docker 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ce97-120">Each time you reboot your development machine, you’ll need toorestart your local docker host.</span></span>
> <span data-ttu-id="6ce97-121">toodo 다음 명령을 명령 프롬프트에서이, 문제 hello: `docker-machine start default`합니다.</span><span class="sxs-lookup"><span data-stu-id="6ce97-121">toodo this, issue hello following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
