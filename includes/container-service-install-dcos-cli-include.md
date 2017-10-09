---
title: DC/OS CLI aaaInstall hello | Microsoft Docs
description: "Hello DC/OS CLI를 설치 합니다."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "컨테이너, 마이크로 서비스, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2016
ms.author: rogardle
ms.openlocfilehash: b077c05beff9a5638486ea5efe9df31089e32701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
> [!NOTE]
> <span data-ttu-id="e23f7-104">DC/OS 기반 ACS 클러스터와 함께 작업하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e23f7-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="e23f7-105">방법이 없는 필요 toodo이 ACS 웜 기반 클러스터에 대 한입니다.</span><span class="sxs-lookup"><span data-stu-id="e23f7-105">There is no need toodo this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="e23f7-106">첫째, [tooyour DC/OS 기반 ACS 클러스터 연결](../articles/container-service/container-service-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e23f7-106">First, [connect tooyour DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="e23f7-107">이 작업을 수행 hello DC/OS CLI 아래 hello 명령 사용 하 여 클라이언트 컴퓨터에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23f7-107">Once you have done this, you can install hello DC/OS CLI on your client machine with hello commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="e23f7-108">이전 버전의 Python을 사용하는 경우 몇 가지 "InsecurePlatformWarnings"가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23f7-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="e23f7-109">무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23f7-109">You can safely ignore these.</span></span>

<span data-ttu-id="e23f7-110">셸에서 다시 시작 하지 않고 시작 순서 tooget에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e23f7-110">In order tooget started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="e23f7-111">이 단계는 새 셸을 시작할 때 반드시 필요하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e23f7-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="e23f7-112">이제 CLI가 설치 되어 해당 hello를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23f7-112">Now you can confirm that hello CLI is installed:</span></span>

```bash
dcos --help
```