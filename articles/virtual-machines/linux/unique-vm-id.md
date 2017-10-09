---
title: Azure Linux VM ID aaaGet | Microsoft Docs
description: "설명 방법을 사용 하 여 tooget Azure Linux VM 고유 id입니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a>Azure VM 고유 ID 액세스 및 사용
Azure VM 고유 ID는 128비트 식별자로 인코딩된 후 모든 Azure IaaS VM의 SMBIOS에 저장되며, 현재 플랫폼 BIOS 명령을 사용하여 읽을 수 있습니다.

Azure VM 고유 ID는 읽기 전용 속성입니다. Azure 고유 VM ID는 재부팅 종료(계획된 경우 또는 계획되지 않은 경우), 할당 해제 시작/중지, 서비스 복구 또는 위치로 복원 시 변경되지 않습니다. 그러나 VM hello 스냅숏 형식과 복사 toocreate 새 인스턴스를 새 Azure VM ID 구성 됩니다.

> [!NOTE]
> VM tooautomatically Azure는 고유 ID를 가져올 이전 vm이 생성 하 고 다시 시작 하십시오이 새로운 기능 (를) 가져왔습니다 (2014 년 9 월 18 일)에 전달 하므로 실행 하는 경우
> 
> 

tooaccess Azure에서 고유한 VM ID hello VM 내:

## <a name="create-a-vm"></a>VM 만들기
자세한 내용은 [가상 컴퓨터 만들기](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

## <a name="connect-toohello-vm"></a>Toohello VM 연결
자세한 내용은 [Linux의 SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

## <a name="query-vm-unique-id"></a>VM 고유 ID 쿼리
명령(예제에서는 **Ubuntu**사용):

```bash
sudo dmidecode | grep UUID
```

예제의 예상 결과:

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

TooBig Endian 비트 순서 인해 hello 실제 고유 VM ID이 경우 됩니다.

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

Hello VM Azure에서 실행 되 고 또는 온-프레미스 및 라이선스 보고 또는 일반 추적 요구 사항을 Azure IaaS 배포에 있을 수 있습니다 수 있는지 여부를 다양 한 시나리오에서 azure VM의 고유 ID는 사용할 수 있습니다. 많은 독립 소프트웨어 공급 업체 응용 프로그램을 구축 하 고 azure에 인증할 hello VM 다른 클라우드 공급자 또는 Azure에서 온-프레미스에서 실행 중인 경우 Azure VM의 수명 주기 및 tootell 전체 tooidentify가 필요할 수 있습니다. Hello 소프트웨어 올바르게 사용이 허가 하는 경우 검색 또는 toocorrelate tooassist hello 오른쪽 플랫폼과 tootrack에 대 한 hello 오른쪽 메트릭을 설정 등 모든 VM 데이터 tooits 소스 도움말과 이러한 메트릭 간에 상관 관계를 지정의 예를 들어이 플랫폼 식별자 활용 다른 사용 합니다.

