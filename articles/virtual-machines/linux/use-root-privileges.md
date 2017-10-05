---
title: "Linux 가상 컴퓨터에서 루트 권한 사용 | Microsoft Docs"
description: "Azure의 Linux 가상 컴퓨터에서 루트 권한을 사용하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: dc39db1f5fecffb60499a5420bfe72850e2fffd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a>Azure의 Linux 가상 컴퓨터에서 루트 권한 사용
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

기본적으로 `root` 사용자는 Azure의 Linux 가상 컴퓨터에서는 사용되지 않도록 설정됩니다. 사용자는 `sudo` 명령을 사용하여 승격된 권한으로 명령을 실행할 수 있습니다. 그러나 환경은 시스템이 프로비전된 방법에 따라 다릅니다.

1. **SSH 키 및 암호 또는 암호만** - 가상 컴퓨터가 인증서(`.CER` 파일) 또는 SSH 키와 암호를 함께 사용하거나 사용자 이름 및 암호만 사용하여 프로비전되었습니다. 이 경우 `sudo` 에서 명령을 실행하기 전에 사용자 암호를 묻는 메시지를 표시합니다.
2. **SSH 키만** - 가상 컴퓨터가 암호 없이 인증서(`.cer`, `.pem` 또는 `.pub` 파일)만 사용하여 프로비전되었습니다.  이 경우 `sudo` **않습니다** .

## <a name="ssh-key-and-password-or-password-only"></a>SSH 키 및 암호 또는 암호만
SSH 키 또는 암호 인증을 사용하여 Linux 가상 컴퓨터에 로그인한 후 `sudo`를 사용하여 명령을 실행합니다. 예를 들면 다음과 같습니다.

    # sudo <command>
    [sudo] password for azureuser:

이 경우에는 사용자에게 암호를 묻는 메시지가 표시됩니다. 암호가 입력되면 `sudo`에서 `root` 권한으로 명령을 실행합니다.

`/etc/sudoers.d/waagent` 파일을 편집하여 암호 없는 sudo를 사용하도록 설정할 수도 있습니다. 예를 들면 다음과 같습니다.

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

이렇게 변경하면 "azureuser" 사용자가 암호 없는 sudo를 사용할 수 있습니다.

## <a name="ssh-key-only"></a>SSH 키만
SSH 키 인증을 사용하여 Linux 가상 컴퓨터에 로그인한 후 `sudo`를 사용하여 명령을 실행합니다. 예를 들면 다음과 같습니다.

    # sudo <command>

이 경우에는 사용자에게 암호를 묻는 메시지가 **표시되지 않습니다** . `<enter>`를 누르면 `sudo`에서 `root` 권한으로 명령을 실행합니다.

