---
title: "Windows 가상 컴퓨터에 SAP aaaUsing | Microsoft Docs"
description: "Microsoft Azure의 Windows VM(가상 컴퓨터)에서 SAP를 사용하는 방법을 알아봅니다."
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: 1b455be4-c02f-43e3-8d39-c2d5f216e646
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: 6c4d8a066a4a8805668e78e67fd2110f2000ee75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-windows-virtual-machines-in-azure"></a>Azure의 Windows 가상 컴퓨터에서 SAP 사용
클라우드 컴퓨팅은 toolarge 및 다국적 회사를 중소 기업에서 점점 더 많은 중요도 hello IT 업계 내에서 취소 하는 널리 사용 되는 용어입니다. Microsoft Azure는 hello 새로운 작업 방식을 폭넓게 제공 된 microsoft에서 클라우드 서비스 플랫폼입니다. 이제 고객은 수 toorapidly 프로 비전 및 프로 비전 해제 응용 프로그램 클라우드 서비스로 제한 된 tootechnical 또는 예산 제한 되지 않습니다. 하드웨어 인프라에 시간과 예산을 투자를 하는 대신 고객 및 사용자에 대 한 회사는 hello 응용 프로그램 및 비즈니스 프로세스의 장점에 집중할 수 있습니다.

Microsoft는 Microsoft Azure 가상 컴퓨터와 함께 포괄적인 IaaS(Infrastructure as a Service) 플랫폼을 제공합니다. SAP NetWeaver 기반 응용 프로그램은 Azure 가상 컴퓨터(IaaS)에서 지원됩니다. 아래 hello 백서 tooplan 및 구현 SAP NetWeaver 기반 Azure에서 Windows 가상 컴퓨터에 응용 프로그램에 방법을 설명 합니다. [Linux 가상 컴퓨터](../../linux/classic/sap-get-started.md)에서 SAP NetWeaver 기반 응용 프로그램을 구현할 수도 있습니다.

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure---ha"></a>Azure에서 SAP NetWeaver - HA
제목: Azure-SIOS datakeeper를 통해 Azure에서 Windows Server 장애 조치 클러스터를 사용 하 여 클러스터링 SAP ASCS/SCS 인스턴스에에서 NetWeaver aaaSAP

요약: '이 문서에서는 설명 방법을 toouse SIOS DataKeeper tooset Azure에서 항상 사용 가능한 SAP ASCS/SCS 구성 합니다. SAP는 공유 디스크를 필요로 하는 Windows Server 장애 조치 클러스터 구성으로 SAP ASCS/SCS 또는 Enqueue Replication Services와 같은 오류 구성 요소의 단일 지점을 보호합니다. 이러한 SAP 구성 요소는 SAP 시스템의 hello 기능에 필수적입니다. 따라서 toobe 모드로 항상 사용 가능한 기능 요구 배치 toomake 있는지 완전 및 Hyper-v 환경에 대 한 Windows 클러스터 구성으로 작업 하는 것 처럼 해당 구성 요소는 서버 또는 VM의 실패를 유지할 수 있습니다. 2015 년 8 월부터 Azure 자체 Windows hello에 필요한 공유 디스크 기반 이러한 주요 SAP 구성 요소에 필요한 항상 사용 가능한 구성으로 제공할 수 없습니다. 그러나 hello Azure IaaS 플랫폼에서 사용 하 여 hello SIOS DataKeeper hello 제품, SAP ASCS/SCS 필요에 따라 Windows Server 장애 조치 클러스터 구성은 빌드할 수 있습니다. 이 문서는 tooinstall 공유 디스크 되는 Windows Server 장애 조치 클러스터 구성을 제공 하는 방식을 하 여 Azure에서 SIOS Datakeeper 단계-단계 접근 방식에서 설명 합니다. hello 용지를 최적의 방식으로 작동 하는 hello 고가용성 구성을 hello Azure, Windows와 SAP 측면에서 구성에 대 한 세부 정보를 설명 합니다. hello 용지 보완 hello SAP 설치 설명서 및 SAP Note를 설치 및 배포에 SAP 소프트웨어에 대 한 기본 리소스 hello 플랫폼을 제공 합니다.

업데이트 날짜: 2015년 8월

[지금 이 가이드 다운로드](http://go.microsoft.com/fwlink/?LinkId=613056)

