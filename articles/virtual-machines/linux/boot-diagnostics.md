---
title: "Azure에서 Linux 가상 컴퓨터의 부팅 진단 | Microsoft Docs"
description: "Azure의 Linux 가상 컴퓨터에 대한 두 가지 디버깅 기능 개요"
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
ms.openlocfilehash: 70254d39b5c6326166f7e29fdfc99533835502f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-boot-diagnostics-to-troubleshoot-linux-virtual-machines-in-azure"></a>부팅 진단을 사용하여 Azure의 Linux 가상 컴퓨터 문제를 해결하는 방법

이제 Azure에서 두 가지 디버깅 기능에 대한 지원이 제공됩니다. Azure Virtual Machines Resource Manager 배포 모델에 대한 콘솔 출력 및 스크린샷 지원. 

자신의 이미지를 Azure로 가져 오거나 플랫폼 이미지 중 하나를 부팅 할 때 Virtual Machines가 부팅 불가능한 상태가 되는 데에는 많은 이유가 있을 수 있습니다. 이 기능을 사용하면 부팅 오류에서 Virtual Machines를 쉽게 진단하고 복구할 수 있습니다.

Linux Virtual Machines의 경우 포털에서 콘솔 로그의 출력을 쉽게 볼 수 있습니다.

![Azure Portal](./media/boot-diagnostics/screenshot1.png)
 
그러나 Windows 및 Linux Virtual Machines의 경우 Azure를 사용하면 하이퍼바이저에서 VM의 스크린샷을 볼 수도 있습니다.

![오류](./media/boot-diagnostics/screenshot2.png)

이 두 가지 기능이 모든 지역의 Azure Virtual Machines에서 지원됩니다. 참고로, 스크린샷 및 출력을 저장소 계정에 표시하는 데 최대 10분이 소요될 수 있습니다.

## <a name="common-boot-errors"></a>일반적인 부팅 오류

- [파일 시스템 문제](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [커널 문제](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [FSTAB 오류](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>새 가상 컴퓨터에서 진단 사용
1. Preview 포털에서 새 Virtual Machine을 만드는 경우 배포 모델 드롭다운에서 **Azure Resource Manager**를 선택합니다.
 
    ![리소스 관리자](./media/boot-diagnostics/screenshot3.jpg)

2. 이러한 진단 파일을 저장할 저장소 계정을 선택하려면 모니터링 옵션을 구성합니다.
 
    ![VM 만들기](./media/boot-diagnostics/screenshot4.jpg)

3. Azure Resource Manager 템플릿에서 배포하는 경우 Virtual Machine 리소스로 이동하고 진단 프로필 섹션을 추가합니다. "2015-06-15" API 버전 헤더를 사용해야 합니다.

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. 진단 프로필을 사용하면 이러한 로그를 저장할 저장소 계정을 선택할 수 있습니다.

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

포털을 통해 부팅 진단을 활성화하려면 포털을 통해 기존 가상 컴퓨터를 업데이트할 수도 있습니다. 부팅 진단 옵션을 선택하고 저장합니다. 적용하려면 VM을 다시 시작합니다.

![기본 VM 업데이트](./media/boot-diagnostics/screenshot5.png)