---
title: "Azure에서 Linux 가상 컴퓨터에 대 한 진단 aaaBoot | Microsoft 문서"
description: "Azure에서 Linux 가상 컴퓨터에 대 한 hello 두 디버깅 기능 개요"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a>Toouse는 Azure에서 진단 tootroubleshoot Linux 가상 컴퓨터를 부팅 하는 방법

이제 Azure에서 두 가지 디버깅 기능에 대한 지원이 제공됩니다. Azure Virtual Machines Resource Manager 배포 모델에 대한 콘솔 출력 및 스크린샷 지원. 

설정할 때 사용자 고유의 이미지 tooAzure 이거나도 부팅 중 hello 플랫폼 이미지, 가상 컴퓨터를 부팅할 수 없는 상태로 가져옵니다 하는 이유는 여러 가지 이유가 있을 수 있습니다. Tooeasily 있습니다를 진단 하 고 가상 컴퓨터 부팅 실패에서 복구 이러한 기능 사용 합니다.

Linux 가상 컴퓨터에 대 한 hello 출력 hello 포털에서에서 콘솔 로그를 쉽게 볼 수 있습니다.

![Azure portal](./media/boot-diagnostics/screenshot1.png)
 
그러나 Windows와 Linux 가상 컴퓨터에 대 한 Azure가 해줍니다 toosee를 hello 하이퍼바이저에서 hello VM의 스크린샷:

![오류](./media/boot-diagnostics/screenshot2.png)

이 두 가지 기능이 모든 지역의 Azure Virtual Machines에서 지원됩니다. 참고, 스크린샷 및 출력 저장소 계정에 분 tooappear too10 차지할 수 있습니다.

## <a name="common-boot-errors"></a>일반적인 부팅 오류

- [파일 시스템 문제](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [커널 문제](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [FSTAB 오류](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>새 가상 컴퓨터에서 진단 사용
1. Hello 미리 보기 포털에서에서 새 가상 컴퓨터를 만들 때 선택 hello **Azure 리소스 관리자** hello 배포 모델 드롭다운에서:
 
    ![리소스 관리자](./media/boot-diagnostics/screenshot3.jpg)

2. 이러한 진단 파일 hello 모니터링 옵션 tooselect hello 저장소 계정 tooplace 하려는 위치를 구성 합니다.
 
    ![VM 만들기](./media/boot-diagnostics/screenshot4.jpg)

3. Azure 리소스 관리자 템플릿을 배포 하는 경우 tooyour 가상 컴퓨터 리소스를 이동 하 고 hello 진단 프로필 섹션을 추가 하세요. Toouse hello "2015-06-15" API 버전 헤더를 기억 합니다.

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. hello 진단 프로필 tooselect hello 저장소 계정을 저장할 tooput 이러한 로그 있습니다.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a>기존 가상 컴퓨터 업데이트

hello 포털을 통해 tooenable 부트 진단을 hello 포털을 통해 기존 가상 컴퓨터를 업데이트할 수도 있습니다. Hello 부트 진단이 저장 및 옵션을 선택 합니다. Hello VM tootake 효과 다시 시작 합니다.

![기본 VM 업데이트](./media/boot-diagnostics/screenshot5.png)