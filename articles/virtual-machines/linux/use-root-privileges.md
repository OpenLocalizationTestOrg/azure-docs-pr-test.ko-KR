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
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a>Azure의 Linux 가상 컴퓨터에서 루트 권한 사용
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

기본적으로 hello `root` Azure에서 Linux 가상 컴퓨터에서 사용자가 비활성화 되어 있습니다. 사용자가 hello를 사용 하 여 상승 된 권한으로 명령에 실행할 수 `sudo` 명령입니다. 그러나 hello 경험 hello 시스템 프로 비전 된 방식에 따라 달라질 수 있습니다.

1. **SSH 키 및 암호 또는 암호 만으로** -hello 가상 컴퓨터는 인증서로 프로 비전 된 (`.CER` 파일) 또는 SSH 키 및 암호를 또는 사용자 이름 및 암호. 이 경우 `sudo` hello 명령을 실행 하기 전에 hello 사용자의 암호를 묻습니다.
2. **SSH 키만** -hello 가상 컴퓨터는 인증서로 프로 비전 된 (`.cer`, `.pem`, 또는 `.pub` 파일) 또는 SSH 키 있지만 암호가 없습니다.  이 경우 `sudo` **되지 것입니다** hello 명령을 실행 하기 전에 hello 사용자의 암호를 확인 합니다.

## <a name="ssh-key-and-password-or-password-only"></a>SSH 키 및 암호 또는 암호만
SSH 키 또는 암호 인증을 사용 하 여 hello Linux 가상 컴퓨터에 로그인 한 다음 명령을 사용 하 여 실행 `sudo`, 예:

    # sudo <command>
    [sudo] password for azureuser:

이 경우 hello 사용자 암호를 나타납니다. Hello 암호를 입력 한 후 `sudo` hello 명령을 실행 하는 `root` 권한.

Hello를 편집 하 여 passwordless sudo를 설정할 수도 있습니다 `/etc/sudoers.d/waagent` 파일 예:

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

"Azureuser" hello 사용자별 passwordless sudo에서 이러한 변경에 허용 합니다.

## <a name="ssh-key-only"></a>SSH 키만
SSH 키 인증을 사용 하 여 hello Linux 가상 컴퓨터에 로그인 한 다음 명령을 사용 하 여 실행 `sudo`, 예:

    # sudo <command>

이 경우 hello 사용자를 **하지** 암호를 입력 합니다. 눌러 `<enter>`, `sudo` hello 명령을 실행 하는 `root` 권한.

