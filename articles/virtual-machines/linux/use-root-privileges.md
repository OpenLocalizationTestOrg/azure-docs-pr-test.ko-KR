---
title: "Linux 가상 컴퓨터에 대 한 루트 권한이 aaaUse | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터에서 toouse 루트 권한 하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="ae21e-103">Azure의 Linux 가상 컴퓨터에서 루트 권한 사용</span><span class="sxs-lookup"><span data-stu-id="ae21e-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="ae21e-104">기본적으로 hello `root` Azure에서 Linux 가상 컴퓨터에서 사용자가 비활성화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae21e-104">By default, hello `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="ae21e-105">사용자가 hello를 사용 하 여 상승 된 권한으로 명령에 실행할 수 `sudo` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ae21e-105">Users can run commands with elevated privileges by using hello `sudo` command.</span></span> <span data-ttu-id="ae21e-106">그러나 hello 경험 hello 시스템 프로 비전 된 방식에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae21e-106">However, hello experience may vary depending on how hello system was provisioned.</span></span>

1. <span data-ttu-id="ae21e-107">**SSH 키 및 암호 또는 암호 만으로** -hello 가상 컴퓨터는 인증서로 프로 비전 된 (`.CER` 파일) 또는 SSH 키 및 암호를 또는 사용자 이름 및 암호.</span><span class="sxs-lookup"><span data-stu-id="ae21e-107">**SSH key and password OR password only** - hello virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="ae21e-108">이 경우 `sudo` hello 명령을 실행 하기 전에 hello 사용자의 암호를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="ae21e-108">In this case `sudo` will prompt for hello user's password before executing hello command.</span></span>
2. <span data-ttu-id="ae21e-109">**SSH 키만** -hello 가상 컴퓨터는 인증서로 프로 비전 된 (`.cer`, `.pem`, 또는 `.pub` 파일) 또는 SSH 키 있지만 암호가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae21e-109">**SSH key only** - hello virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="ae21e-110">이 경우 `sudo` **되지 것입니다** hello 명령을 실행 하기 전에 hello 사용자의 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae21e-110">In this case `sudo` **will not** prompt for hello user's password before executing hello command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="ae21e-111">SSH 키 및 암호 또는 암호만</span><span class="sxs-lookup"><span data-stu-id="ae21e-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="ae21e-112">SSH 키 또는 암호 인증을 사용 하 여 hello Linux 가상 컴퓨터에 로그인 한 다음 명령을 사용 하 여 실행 `sudo`, 예:</span><span class="sxs-lookup"><span data-stu-id="ae21e-112">Log into hello Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="ae21e-113">이 경우 hello 사용자 암호를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ae21e-113">In this case hello user will be prompted for a password.</span></span> <span data-ttu-id="ae21e-114">Hello 암호를 입력 한 후 `sudo` hello 명령을 실행 하는 `root` 권한.</span><span class="sxs-lookup"><span data-stu-id="ae21e-114">After entering hello password `sudo` will run hello command with `root` privileges.</span></span>

<span data-ttu-id="ae21e-115">Hello를 편집 하 여 passwordless sudo를 설정할 수도 있습니다 `/etc/sudoers.d/waagent` 파일 예:</span><span class="sxs-lookup"><span data-stu-id="ae21e-115">You can also enable passwordless sudo by editing hello `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="ae21e-116">"Azureuser" hello 사용자별 passwordless sudo에서 이러한 변경에 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae21e-116">This change will allow for passwordless sudo by hello user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="ae21e-117">SSH 키만</span><span class="sxs-lookup"><span data-stu-id="ae21e-117">SSH Key Only</span></span>
<span data-ttu-id="ae21e-118">SSH 키 인증을 사용 하 여 hello Linux 가상 컴퓨터에 로그인 한 다음 명령을 사용 하 여 실행 `sudo`, 예:</span><span class="sxs-lookup"><span data-stu-id="ae21e-118">Log into hello Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="ae21e-119">이 경우 hello 사용자를 **하지** 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae21e-119">In this case hello user will **not** be prompted for a password.</span></span> <span data-ttu-id="ae21e-120">눌러 `<enter>`, `sudo` hello 명령을 실행 하는 `root` 권한.</span><span class="sxs-lookup"><span data-stu-id="ae21e-120">After pressing `<enter>`, `sudo` will run hello command with `root` privileges.</span></span>

