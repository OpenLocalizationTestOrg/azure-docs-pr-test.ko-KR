---
title: "Azure에서 Linux 가상 컴퓨터 문제를 배포 하는 aaaTroubleshoot | Microsoft Docs"
description: "Azure Resource Manager 배포 모델에서 Linux 가상 컴퓨터 배포 문제를 해결합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a>Azure에서 Linux 가상 컴퓨터 배포 문제 해결

azure에서 가상 컴퓨터 (VM) 배포 문제 tootroubleshoot hello 검토 [문제 상위](#top-issues) 일반적인 오류 및 해결 방법에 대 한 합니다.

이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure 및 스택 오버플로 포럼 hello](https://azure.microsoft.com/support/forums/)합니다. 또는 Azure 기술 지원 인시던트를 제출할 수 있습니다. Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 선택 **Get Support**합니다.

## <a name="top-issues"></a>주요 문제
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a>hello 클러스터를 지원할 수 없는 hello 요청 된 VM 크기
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- 더 작은 VM 크기를 사용 하 여 hello 요청을 다시 시도 하십시오.
- Hello 크기인 요청한 경우 hello VM을 변경할 수 없습니다.
    - Hello 가용성 집합에 있는 모든 hello Vm을 중지 합니다. **리소스 그룹** > 사용자의 리소스 그룹 > **리소스** > 사용자의 가용성 집합 > **Virtual Machines** > 사용자의 가상 컴퓨터 > **중지**를 클릭합니다.
    - 모든 Vm 중지 hello, hello 원하는 크기의 hello VM을 만듭니다.
    - 시작 새 VM을 먼저 hello 한 후 각 선택 hello의 Vm을 중지 하 고 시작을 클릭 합니다.


## <a name="hello-cluster-does-not-have-free-resources"></a>hello 클러스터 리소스를 해제가 없습니다.
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Hello 요청을 나중에 다시 시도 하십시오.
- Hello 새 VM 수 있는 경우 다른 가용성의 일부 설정 합니까
    - 다른 가용성 집합에서 VM을 만듭니다 (hello에 동일한 지역).
    - 새 VM toohello hello 추가 동일한 가상 네트워크입니다.

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Visual Studio Enterprise(BizSpark)에 대한 월간 크레딧을 활성화하는 방법

tooactivate 하면 월별 신용이 [문서](https://azure.microsoft.com/offers/ms-azr-0064p/)합니다.

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a>이유 하지 설치할 수 hello GPU 드라이버는 Ubuntu NV VM에 대 한?

현재 Linux GPU 지원은 Ubuntu Server 16.04 LTS를 실행하는 Azure NC VM에서만 사용할 수 있습니다. 자세한 내용은 [Linux가 실행되는 N 시리즈 VM의 GPU 드라이버 설정](n-series-driver-setup.md)을 참조하세요.

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a>내 드라이버가 Linux N 시리즈 VM에 누락되었습니다.

Linux 기반 VM용 드라이버가 [여기](n-series-driver-setup.md)에 위치합니다. 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>N 시리즈 VM 내에서 GPU 인스턴스를 찾을 수 없습니다.

Windows Server 2016을 실행 하는 Azure N 시리즈 Vm의 hello GPU 기능을 활용 tootake 또는 Windows Server 2012 R2 배포 후 각 VM에 NVIDIA 그래픽 드라이버를 설치 해야 합니다. [Windows VM](../windows/n-series-driver-setup.md) 및 [Linux VM](n-series-driver-setup.md)에 대한 드라이버 설치 정보를 사용할 수 있습니다.

## <a name="is-n-series-vms-available-in-my-region"></a>N 시리즈 VM을 내 지역에서 사용할 수 있나요?

Hello에서 hello 가용성을 확인할 수 있습니다 [region 테이블에서 사용할 수 있는 제품](https://azure.microsoft.com/regions/services), 가격 및 [여기](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series)합니다.

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>VM 크기를 조정 하면 원하는 수 toosee VM 크기 제품군 없는 경우

VM 실행 중인 경우 배포 된 tooa 물리적 서버 있습니다. Azure 지역에서 물리적 서버 hello 일반적인 물리적 하드웨어의 클러스터로 그룹화 됩니다. Hello VM 이동 toobe toodifferent 하드웨어 클러스터 요구 하는 VM의 크기를 조정 하는 것은 어떤 배포 모델을 사용 하는 toodeploy hello VM에 따라 다릅니다.

- 클래식 배포 모델을 hello 클라우드 서비스 배포에 배포 된 Vm 제거 해야 하 고 다른 크기 제품군의 toochange hello Vm tooa 크기를 다시 배포 합니다.

- 리소스 관리자 배포 모델에서 배포 된 Vm을 hello 가용성 hello hello 가용성 집합의 모든 VM 크기를 변경 하기 전에 설정의 모든 Vm을 중지 해야 합니다.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>hello 나열 된 VM 크기가 지원 되지 않음을 가용성 집합에 배포 하는 중입니다.

Hello 가용성 집합의 클러스터에서 사용할 수 있는 크기를 선택 합니다. 것을 만들 때 한 가용성 집합 toochoose hello 가장 큰 VM 크기를 하 고 있는 가용성 집합에 첫 번째 배포 toohello 수입니다.

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a>Azure에서 지원되는 Linux 배포/버전은 무엇인가요?

Linux에서 hello 목록에서 찾을 수 있습니다 [Azure-Endorsed 분포](endorsed-distros.md)합니다.

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>기존 클래식 VM tooan 가용성 집합을 추가할 수 있습니까?

예. 기존 클래식 VM tooa 새를 추가할 수 있습니다 또는 기존 가용성 집합입니다. 자세한 내용은 참조 [기존 가상 컴퓨터 tooan 가용성 집합을 추가](../windows/classic/configure-availability.md#addmachine)합니다.


## <a name="next-steps"></a>다음 단계
이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure 및 스택 오버플로 포럼 hello](https://azure.microsoft.com/support/forums/)합니다.

또는 Azure 기술 지원 인시던트를 제출할 수 있습니다. Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 선택 **Get Support**합니다.
