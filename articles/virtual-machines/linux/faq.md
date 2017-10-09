---
title: "Azure에서 Linux Vm에 대 한 질문과 aaaFrequently | Microsoft Docs"
description: "Hello hello 리소스 관리자 모델을 사용 하 여 만든 Linux 가상 컴퓨터에 대 한 일반적인 질문과 대답 toosome를 제공 합니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a>Linux 가상 컴퓨터에 대한 질문과 대답
이 문서 hello 리소스 관리자 배포 모델을 사용 하 여 Azure에서 만든 Linux 가상 컴퓨터에 대 한 몇 가지 일반적인 질문을 해결 합니다. 이 항목의 hello Windows 버전을 참조 하십시오. [질문 Windows 가상 컴퓨터에 대 한 질문과 대답](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>Azure VM에서 무엇을 실행할 수 있습니까?
모든 구독자는 Azure 가상 컴퓨터에서 서버 소프트웨어를 실행할 수 있습니다. 자세한 내용은 [Azure 인증 배포의 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>가상 컴퓨터에 얼마나 많은 용량의 저장소를 사용할 수 있습니까?
각 데이터 디스크는 too1 TB를 수 있습니다. 데이터 디스크를 사용할 수 있습니다 hello 수 hello hello 가상 컴퓨터 크기에 따라 다릅니다. 자세한 내용은 [Virtual Machines의 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

Azure 저장소 계정을 hello 운영 체제 디스크 및 데이터 디스크에 대 한 저장소를 제공합니다. 각 디스크는 페이지 blob으로 저장된 .vhd 파일입니다. 가격 책정에 대한 자세한 내용은 [저장소 가격 세부 정보](https://azure.microsoft.com/pricing/details/storage/)를 참조하세요.

## <a name="how-can-i-access-my-virtual-machine"></a>나의 가상 컴퓨터에 액세스 하려면 어떻게 해야 합니까?
SSH (보안 셸)를 사용 하 여 toohello 가상 컴퓨터 원격 연결 toolog를 설정 합니다. 방법에 hello 지침을 참조 하십시오. tooconnect [Windows에서](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [Linux 및 Mac에서](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 기본적으로, SSH는 최대 10개의 동시 연결을 허용합니다. Hello 구성 파일을 편집 하 여이 번호를 늘릴 수 있습니다.

문제가 있는 경우 [SSH(Secure Shell) 연결 문제 해결](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 확인하세요.

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a>Hello 임시 디스크 (/ 개발/sdb1) toostore 데이터를 사용할 수 있습니까?
Hello 임시 디스크 (/ 개발/sdb1) toostore 데이터를 사용 하지 마십시오. 임시 디스크는 임시 저장소로만 사용해야 합니다. 복구할 수 없는 데이터는 손실될 위험이 있습니다.

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>기존 Azure VM을 복사 또는 복제할 수 있나요?
예. 자세한 내용은 [toocreate 복사본에서 Linux 가상 컴퓨터의 리소스 관리자 배포 모델을 hello 어떻게](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Azure Resource Manager를 통해 캐나다 중부 및 캐나다 동부 지역이 보이지 않는 이유가 무엇인가요?
캐나다 중앙 및 캐나다 동부 hello 두 개의 새 영역 기존 Azure 구독에 대 한 가상 컴퓨터 만들기에 자동으로 등록 되지 않습니다. 이 등록을 통해 가상 컴퓨터를 배포할 때 자동으로 수행 되며 hello Azure 포털 tooany Azure 리소스 관리자를 사용 하 여 다른 영역입니다. 후 가상 컴퓨터는 배포 된 tooany 다른 Azure 지역 hello 새 영역 이후 가상 컴퓨터에 사용할 수 있어야 합니다.

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>만든 후 NIC toomy VM 추가 합니까?
예, 이제 가능합니다. hello VM 첫 번째 요구 toobe 중지 할당 해제 합니다. 그런 다음 추가 하거나 NIC를 제거할 수 있습니다 (경우가 아니라면 hello VM에서 마지막 NIC hello). 

## <a name="are-there-any-computer-name-requirements"></a>컴퓨터 이름 요구 사항이 있나요?
예. hello 컴퓨터 이름은 최대 64 자 수 있습니다. [명명 규칙 및 제한 사항](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하여 리소스 이름 지정에 대해 자세히 알아보세요.

## <a name="are-there-any-resource-group-name-requirements"></a>리소스 그룹 이름에 대한 요구 사항이 있나요?
예. hello 리소스 그룹 이름은 최대 90 자 수 있습니다. [명명 규칙 및 제한 사항](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하여 리소스 그룹에 대해 자세히 알아보세요.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>VM을 만들 때 hello username 요구 사항은 무엇입니까?
사용자 이름은 1~64자 사이로 지정해야 합니다.

사용자 이름은 다음 hello 허용 되지 않습니다.

<table>
    <tr>
        <td style="text-align:center">관리자 역할 </td><td style="text-align:center"> 관리자 </td><td style="text-align:center"> 사용자 </td><td style="text-align:center"> user1</td>
    </tr>
    <tr>
        <td style="text-align:center">test </td><td style="text-align:center"> user2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>
    <tr>
        <td style="text-align:center">admin1 </td><td style="text-align:center"> 1 </td><td style="text-align:center"> 123 </td><td style="text-align:center"> a</td>
    </tr>
    <tr>
        <td style="text-align:center">actuser  </td><td style="text-align:center"> adm </td><td style="text-align:center"> admin2 </td><td style="text-align:center"> aspnet</td>
    </tr>
    <tr>
        <td style="text-align:center">backup </td><td style="text-align:center"> console </td><td style="text-align:center"> david </td><td style="text-align:center"> guest</td>
    </tr>
    <tr>
        <td style="text-align:center">john </td><td style="text-align:center"> owner </td><td style="text-align:center"> root </td><td style="text-align:center"> server</td>
    </tr>
    <tr>
        <td style="text-align:center">sql </td><td style="text-align:center"> support </td><td style="text-align:center"> support_388945a0 </td><td style="text-align:center"> sys</td>
    </tr>
    <tr>
        <td style="text-align:center">test2 </td><td style="text-align:center"> test3 </td><td style="text-align:center"> user4 </td><td style="text-align:center"> user5</td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a>VM을 만들 때 hello 암호 요구 사항은 무엇입니까?
암호는 6 72 자가 하 여야 하 고 4 복잡성 요구 사항을 준수 하는 hello 부족 3 충족 해야 합니다.

* 소문자 포함
* 대문자 포함
* 숫자 포함
* 특수 문자 포함(정규식 일치 [\W_])

암호를 다음 hello 허용 되지 않습니다.

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center">P@$$w0rd</td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center">Pa$$word</td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center">Password!</td>
        <td style="text-align:center">Password1</td>
        <td style="text-align:center">Password22</td>
        <td style="text-align:center">iloveyou!</td>
    </tr>
</table>
