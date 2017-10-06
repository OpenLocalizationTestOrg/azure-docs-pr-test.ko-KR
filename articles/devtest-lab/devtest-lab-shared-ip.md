---
title: "aaaUnderstand Azure DevTest Labs에서 IP 주소를 공유 | Microsoft Docs"
description: "Azure DevTest Labs 사용 하는 방법을 공유 IP 주소 toominimize hello 공용 IP 주소가 필요한 tooaccess 랩 Vm에 알아봅니다."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a>Azure DevTest Labs에서 공유 IP 주소 이해

동일한 공용 IP 주소 toominimize hello 수의 공용 IP 주소가 필요한 tooaccess 개별 랩 Vm hello 하는 azure DevTest Labs 하면 랩 Vm 공유 합니다.  이 문서에서는 공유 IP의 작동 방식과 관련 구성 옵션에 대해 설명합니다.

## <a name="shared-ip-setting"></a>공유 IP 설정

랩을 만들면 가상 네트워크의 서브넷에 상주합니다.  기본적으로이 서브넷을 만든 **공용 IP를 공유 하는 활성화** 도*예*합니다.  이 구성은 hello 전체 서브넷에 대 한 공용 IP 주소를 하나 만듭니다.  가상 네트워크 및 서브넷 구성에 대한 자세한 내용은 [Azure DevTest Labs에서 가상 네트워크 구성](devtest-lab-configure-vnet.md)을 참조하세요.

![새 랩 서브넷](media/devtest-lab-shared-ip/lab-subnet.png)

기존 랩의 경우 **구성 및 정책 > Virtual Networks**를 선택하여 이 옵션을 사용하도록 설정할 수 있습니다. 그런 다음 hello 목록에서 가상 네트워크를 선택 하 고 선택 **공유 공용 IP를 사용 하도록 설정** 선택한 서브넷에 대 한 합니다. 랩 Vm에서 공용 IP 주소를 tooshare 않으려는 경우에 모든 랩에이 옵션을 해제할 수 있습니다.

모든 Vm 공유 IP이 랩 기본 toousing에 만들어집니다.  이 설정은 hello에서 관측할 수 hello VM을 만들 때 **고급 설정** 아래 블레이드 **IP 주소 구성을**합니다.

![새 VM](media/devtest-lab-shared-ip/new-vm.png)

- **공유:** **공유**로 생성된 모든 VM은 하나의 리소스 그룹(RG)에 배치됩니다. 단일 IP 주소는 RG hello RG에 있는 모든 Vm은 사용 해당 IP 주소 할당 됩니다.
- **공개:** 만든 각 VM에 자체 IP 주소가 있으며 자체 리소스 그룹에 생성됩니다.
- **비공개:** 만든 각 VM이 개인 IP 주소를 사용합니다. Hello에서 직접 VM 수 tooconnect toothis 됩니다 인터넷 원격 데스크톱을 사용 합니다.

사용 하도록 설정 하는 공유 IP 사용 하 여 VM toohello 서브넷을 추가할 때마다 DevTest Labs 자동으로 hello VM tooa 부하 분산 장치 더하고 toohello hello VM의 RDP 포트 전달 hello 공용 IP 주소에 TCP 포트 번호를 할당 합니다.  

## <a name="using-hello-shared-ip"></a>IP 공유 hello를 사용 하 여

- **Linux 사용자:** hello IP 주소 또는 정규화 된 도메인 이름, 그 뒤에 콜론을 사용 하 여 SSH toohello VM hello 포트 옵니다. 예를 들어 아래 hello 이미지 hello RDP 중점적으로 다루고 tooconnect toohello VM은 `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`합니다.

  ![VM 예](media/devtest-lab-shared-ip/vm-info.png)

- **Windows 사용자에 게:** 선택 hello **연결** 미리 구성 된 RDP 파일을 Azure 포털 toodownload hello에서 단추 및 hello VM에 액세스 합니다.

## <a name="next-steps"></a>다음 단계

* [Azure DevTest Labs에서 랩 정책 정의](devtest-lab-set-lab-policy.md)
* [Azure DevTest Labs에서 가상 네트워크 구성](devtest-lab-configure-vnet.md)





