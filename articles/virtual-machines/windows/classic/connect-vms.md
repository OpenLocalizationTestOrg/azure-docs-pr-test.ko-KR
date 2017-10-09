---
title: "클라우드 서비스에서 Windows Vm aaaConnect | Microsoft Docs"
description: "Hello 클래식 배포 모델 tooan Azure 클라우드 서비스 또는 가상 네트워크를 사용 하 여 만든 Windows 가상 컴퓨터를 연결 합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c1cbc802-4352-4d2e-9e49-4ccbd955324b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: d19dc555694eab8a7e790c970cfb5e6a53aa7a7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-virtual-machines-created-with-hello-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a>가상 네트워크 또는 클라우드 서비스와 hello 클래식 배포 모델을 사용 하 여 만든 Windows 가상 컴퓨터 연결
> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

Hello 클래식 배포 모델을 사용 하 여 만든 Windows 가상 컴퓨터는 항상 클라우드 서비스에 저장 됩니다. hello 클라우드 서비스 컨테이너 역할을 하 고 hello 인터넷을 통해 고유한 공용 DNS 이름, 공용 IP 주소 및 끝점 tooaccess hello 가상 컴퓨터의 집합을 제공 합니다. hello 클라우드 서비스가 가상 네트워크 수 있지만 필요 하지 않습니다. 또한 [Linux 가상 컴퓨터를 가상 네트워크 또는 클라우드 서비스와 연결](../../linux/classic/connect-vms.md)할 수도 있습니다.

가상 네트워크에 없는 클라우드 서비스를 *독립 실행형* 클라우드 서비스라고 합니다. hello 가상 컴퓨터가 독립 실행형 클라우드 서비스에 통신할 다른 가상 컴퓨터를 사용 하 여 다른 가상 컴퓨터의 공용 DNS names, hello 및 hello 트래픽 hello 인터넷을 통해 이동 합니다. 클라우드 서비스에에서 있으면 hello 가상 컴퓨터 가상 네트워크를 클라우드 서비스는 hello 인터넷을 통해 모든 트래픽을 전송 하지 않고 hello 가상 네트워크의 다른 모든 가상 컴퓨터와 통신할 수 있다는 점에서 합니다.

배치 하는 경우 가상 컴퓨터에 hello 같은 독립 실행형 클라우드 서비스, 부하 분산을 계속 사용할 수 있습니다 및 가용성 집합입니다. 자세한 내용은 참조 [부하 분산 가상 컴퓨터](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 및 [관리 가상 컴퓨터의 가용성을 hello](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 그러나 서브넷에 hello 가상 컴퓨터를 구성 하거나 독립 실행형 클라우드 서비스 tooyour 온-프레미스 네트워크 연결 수 없습니다. 예를 들면 다음과 같습니다.

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a>다음 단계
가상 컴퓨터를 만든 후는 것이 좋습니다 너무[데이터 디스크 추가](attach-disk.md) 서비스 및 작업에 위치 toostore 데이터 갖도록 합니다.
