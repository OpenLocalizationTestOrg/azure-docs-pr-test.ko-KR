---
title: "aaaInstall OpenSUSE VM에서 MySQL | Microsoft Docs"
description: "Azure에서 Linux VMirtual OpenSUSE 컴퓨터 tooinstall MySQL에 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1594e10e-c314-455a-9efb-a89441de364b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/19/2016
ms.author: cynthn
ms.openlocfilehash: 8f96d29f29cb9c466dd7fdaf92b378783fdaacd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a>Azure에서 OpenSUSE Linux를 실행하는 가상 컴퓨터에 MySQL 설치
[MySQL][MySQL]은 인기 있는 오픈 소스 SQL Database입니다. 이 자습서에서는 어떻게 toocreate OpenSUSE Linux를 실행 하는 가상 컴퓨터 MySQL를 다음 설치 합니다.

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a>OpenSUSE Linux를 실행하는 가상 컴퓨터 만들기
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-hello-virtual-machine"></a>설치 하 고 MySQL hello 가상 컴퓨터에서 실행
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a>다음 단계
MySQL에 대 한 자세한 참조 hello [MySQL 설명서][MySQLDocs]합니다.

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

