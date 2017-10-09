---
title: "Azure에서 Windows VM에서 MongoDB aaaInstall | Microsoft Docs"
description: "Tooinstall MongoDB Azure VM에서 Windows Server를 실행 하는 hello 클래식 배포 모델을 사용 하 여 만든 하는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a>Azure에서 Windows VM에 MongoDB 설치
> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.  이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. tooinstall hello 리소스 관리자 배포 모델을 사용 하 여 MongoDB 구성, 참조 및 [이 여기서](../install-mongodb.md)합니다.

[MongoDB][MongoDB]는 인기 있는 고성능 오픈 소스 NoSQL 데이터베이스입니다. 이 여기서 만드는 과정을 안내 hello를 사용 하 여 Windows Server 가상 컴퓨터 (VM) [Azure 포털][AzurePortal]합니다. 그런 다음 만들고 데이터 디스크 toohello 설치 및 MongoDB 구성 하기 전에 VM을 연결 합니다. 바로 너무 건너뛸 수 있는 싶다는 의사를 toouse Azure에서 기존 VM 경우[설치 및 구성 MongoDB](#install-and-run-mongodb-on-the-virtual-machine)합니다.

## <a name="create-a-virtual-machine-running-windows-server"></a>Windows Server를 실행하는 가상 컴퓨터 만들기
이러한 지침은 toocreate 가상 컴퓨터를 따릅니다.

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> Hello 가상 컴퓨터를 만드는 동안 MongoDB에 대 한 끝점을 추가 하 고 다음과 같이 구성:로 이름을 **Mongo**를 사용 하 여 **TCP** hello 프로토콜 및 집합 hello 공용 및 개인 포트 너무 대로**27017**합니다.
>
>

## <a name="attach-a-data-disk"></a>데이터 디스크 연결
tooprovide 저장소 hello 가상 컴퓨터에 대 한 데이터 디스크를 연결 하 고 Windows에서 사용할 수 있도록 초기화 합니다. 데이터 디스크가 이미 있는 경우 해당 기존 디스크를 연결할 수도 있고 빈 디스크를 연결할 수도 있습니다.

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

참조에 대 한 지침은 hello 디스크 초기화, "하는 방법: Windows Server에서 새 데이터 디스크를 초기화"에 [tooattach 데이터 tooa Windows 가상 컴퓨터 디스크 하는 방법을](attach-disk.md)합니다.

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a>설치 하 고 MongoDB hello 가상 컴퓨터에서 실행
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a>요약
이 자습서에서는 어떻게 toocreate Windows Server를 실행 하는 가상 컴퓨터 원격으로 tooit를 연결 하 고 데이터 디스크를 연결 배웠습니다.  방법에 대해 배웠습니다 tooinstall MongoDB hello Windows 기반 가상 컴퓨터를 구성 하 고 있습니다. 이제 액세스할 수 있습니다 MongoDB hello Windows 기반 가상 컴퓨터에 의해 hello 고급 항목 hello에 다음 [MongoDB 설명서][MongoDocs]합니다.

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

