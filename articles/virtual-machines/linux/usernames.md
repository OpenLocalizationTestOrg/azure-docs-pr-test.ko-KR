---
title: "aaaSelecting Linux에 대 한 사용자 이름 | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터에 대 한 tooselect 사용자 이름을 지정 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a>Azure에서 Linux용 사용자 이름 선택
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Azure에서 Linux 가상 컴퓨터를 프로 비전 할 때 toolog hello VM에 나중에 사용할 수 있는 루트가 아닌 사용자의 hello 이름을 지정 해야 합니다. Hello 새 사용자의 hello 이름을 선택할 수 있습니다 또는 경우 Azure 클래식 포털 hello를 통한 프로비저닝 그대로 hello 기본 이름 "azureuser"입니다.

대부분의 경우에서이 사용자 hello 기본 이미지에 존재 하지 않습니다 및 hello를 프로 비전 프로세스 중 생성 됩니다. Hello 사용자에 있으면 기본 VM 이미지 hello 다음 hello Azure Linux 에이전트 단순히 hello 암호 및/또는 hello VM을 만들 때 지정한 hello 정보에 따라 해당 사용자에 대 한 SSH 키를 구성 합니다.

**그러나**Linux에서는 사용해서는 안 되는 일련의 사용자 이름을 정의합니다. 프로세스는 프로 비전 하는 hello **실패** tooprovision UID 0에서 99 있는 사용자로 정의 된 기존 시스템 사용자를 사용 하 여 Linux VM을 시도 합니다. 일반적인 예로 hello `root` UID 0에는 사용자입니다.

* 참고 항목: [Linux 표준 기반 - 사용자 ID 범위](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)

hello 다음은 일반적인 기본 제공 시스템에 대 한 사용자 CentOS 및을 사용 하면 안 Azure에서 Linux 가상 컴퓨터를 프로 비전 할 때 Ubuntu 목록입니다. 이 목록은 예 시일 뿐에 toohello 설명서를 참조 배포 tooensure 해당 hello 사용자 이름을 기존 시스템 사용자와 충돌 하지 않는지를 선택 합니다.

## <a name="centos"></a>CentOS
* abrt
* adm
* audio
* bin
* cdrom
* cgred
* daemon
* dbus
* dialout
* dip
* disk
* floppy
* ftp
* ftp
* games
* gopher
* haldaemon
* halt
* kmem
* lock
* lp
* mail
* man
* mem
* nfsnobody
* nobody
* ntp
* operator
* oprofile
* postdrop
* postfix
* qpidd
* root
* rpc
* rpcuser
* saslauth
* shutdown
* slocate
* sshd
* stapdev
* stapusr
* sync
* sys
* tape
* test
* tcpdump
* tty
* users
* utempter
* utmp
* uucp
* vcsa
* video
* wheel

## <a name="ubuntu"></a>Ubuntu
* adm
* admin
* audio
* backup
* bin
* cdrom
* crontab
* daemon
* dialout
* dip
* disk
* fax
* floppy
* fuse
* games
* gnats
* irc
* kmem
* landscape
* libuuid
* list
* lp
* mail
* man
* messagebus
* mlocate
* netdev
* news
* nobody
* nogroup
* operator
* plugdev
* proxy
* root
* sasl
* shadow
* src
* ssh
* sshd
* staff
* sudo
* sync
* sys
* syslog
* tape
* tty
* users
* utmp
* uucp
* video
* voice
* whoopsie
* www-data

