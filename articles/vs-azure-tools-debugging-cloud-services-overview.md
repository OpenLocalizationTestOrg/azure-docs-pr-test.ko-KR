---
title: "Azure 디버깅을 위해 aaaOptions 클라우드 서비스 | Microsoft Docs"
description: "Azure Cloud Services 디버깅"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/18/2017
ms.author: kraigb
ms.openlocfilehash: 8b7779ca33cfd82fd5fbccf229ea822c311bdea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-hello-various-ways-toodebug-an-azure-cloud-service"></a>Hello 다양 한 방법에 알아봅니다 toodebug Azure 클라우드 서비스
이 문서에서는 링크 toohello 다양 한 방법으로 toodebug Azure 클라우드 서비스입니다. 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>Visual Studio에서 Azure 클라우드 서비스 디버깅
저장할 수 있습니다 시간과 비용 hello Azure 계산 에뮬레이터 toodebug를 사용 하 여 클라우드 서비스는 로컬 컴퓨터에서. 배포하기 전에 로컬로 서비스를 디버깅하면, 계산 시간이 소요되지 않고 안정성과 성능을 향상할 수 있습니다. 그러나, Azure에서 클라우드 서비스를 실행하는 경우, 일부 오류가 발생할 수 있습니다. 사용자가 서비스를 게시할 때 원격 디버깅을 hello 디버거 tooa 역할 인스턴스를 한 다음 연결을 사용 하 여 Azure에서 클라우드 서비스를 실행 하는 경우에 발생 하는 오류를 디버그할 수 있습니다. 자세한 내용은 [로컬 컴퓨터에서 클라우드 서비스 디버그](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer)를 참조하세요.

## <a name="using-azure-diagnostics"></a>Azure 진단 사용 
Azure 진단을 사용 하 여 hello 역할이 hello 개발 환경에서 또는 Azure에서 실행 되는 여부 toolog 자세한 역할 내에서 코드 실행 정보입니다. 자세한 내용은 [Azure 클라우드 서비스에서 Azure 진단 사용](http://go.microsoft.com/fwlink/p/?LinkId=400450)을 참조하세요.

## <a name="using-intellitrace"></a>IntelliTrace 사용 
사용 중인 경우 Visual Studio Enterprise toowrite 역할 대상이.NET Framework 4.5, Visual Studio에서 Azure 클라우드 서비스를 배포 하는 hello 시간에 IntelliTrace를 사용할 수 있습니다. IntelliTrace에 대 한 로그 제공는 경우 사용할 수 있습니다 Visual Studio toodebug와 응용 프로그램으로 Azure에서 실행 중인 것입니다. 자세한 내용은 [IntelliTrace 및 Visual Studio를 사용하여 게시된 클라우드 서비스 디버깅](http://go.microsoft.com/fwlink/p/?LinkId=623016)을 참조하십시오.

## <a name="remote-debugging"></a>원격 디버깅 
Visual Studio에서 hello 클라우드 서비스를 배포 하는 경우 hello 시간에 클라우드 서비스에서 원격 디버깅을 사용할 수 있습니다. 원격 배포에 대 한 디버깅 tooenable을 선택 하면 원격 디버깅 서비스가 각 역할 인스턴스를 실행 하는 hello 가상 컴퓨터에 설치 됩니다. `msvsmon.exe` 같은 서비스는 성능에 영향을 주지 않거나 추가 비용이 발생하지 않습니다. 자세한 내용은 [Azure에서 클라우드 서비스 디버그](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure)를 참조하세요.

## <a name="next-steps"></a>다음 단계
- [Azure 클라우드 서비스 또는 VM Visual Studio에서 디버깅](./vs-azure-tools-debug-cloud-services-virtual-machines.md) -어떻게 toodebug Azure 클라우드 서비스의 hello 세부 정보에 알아봅니다.
