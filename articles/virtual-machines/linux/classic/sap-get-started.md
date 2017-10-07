---
title: "Linux 가상 컴퓨터에서 SAP aaaUsing | Microsoft Docs"
description: "Microsoft Azure의 Linux VM(가상 컴퓨터)에서 SAP를 사용하는 방법을 알아봅니다."
services: virtual-machines-linux,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: f9cd93dc-71ad-48a4-8778-4e48aec484a6
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: a805cdecb515239057e185a92bf5c4d4e707f72f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a>Azure의 Linux 가상 컴퓨터에서 SAP 사용
클라우드 컴퓨팅은 toolarge 및 다국적 회사를 중소 기업에서 점점 더 많은 중요도 hello IT 업계 내에서 취소 하는 널리 사용 되는 용어입니다. Microsoft Azure는 hello 새로운 작업 방식을 폭넓게 제공 된 microsoft에서 클라우드 서비스 플랫폼입니다. 이제 고객은 수 toorapidly 프로 비전 및 프로 비전 해제 응용 프로그램 클라우드 서비스로 제한 된 tootechnical 또는 예산 제한 되지 않습니다. 하드웨어 인프라에 시간과 예산을 투자를 하는 대신 고객 및 사용자에 대 한 회사는 hello 응용 프로그램 및 비즈니스 프로세스의 장점에 집중할 수 있습니다.

Microsoft는 Microsoft Azure 가상 컴퓨터와 함께 포괄적인 IaaS(Infrastructure as a Service) 플랫폼을 제공합니다. SAP NetWeaver 기반 응용 프로그램은 Azure 가상 컴퓨터(IaaS)에서 지원됩니다. 아래 hello 백서 tooplan 및 구현 SAP NetWeaver 기반 Azure에서 Windows 가상 컴퓨터에 응용 프로그램에 방법을 설명 합니다. [Windows 가상 컴퓨터](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)에서 SAP NetWeaver 기반 응용 프로그램을 구현할 수도 있습니다.

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a>Azure SUSE Linux 가상 컴퓨터에서 SAP NetWeaver
제목: Microsoft Azure SUSE Linux Vm에서의 SAP NetWeaver aaaTesting

요약: 현 시점에는 Azure Linux VM에서의 SAP NetWeaver 실행에 대해 SAP에서 공식적으로 지원하지 않습니다. 그럼에도 불구 하 고 고객 toodo 일부 테스트 하거나 것을 고려할 수 toorun Azure Linux Vm에서 SAP 데모 또는 학습 시스템으로 SAP 지원 팀에 연락 하는 것에 대 한 필요가 없습니다. 이 문서는 Azure SUSE Linux Vm 설정 SAP를 실행 하는 데 도움이 됩니다 하 고 tooavoid 일반적인 잠재적인 문제 순서로 일부 기본적인 힌트를 제공 합니다.

업데이트한 날짜: 2015년 12월

[이 문서는 여기서 확인할 수 있습니다.](../../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

