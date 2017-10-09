---
title: "Azure의 Windows Vm에 대 한 aaaFAQ | Microsoft Docs"
description: "Hello hello 리소스 관리자 모델을 사용 하 여 만든 Windows 가상 컴퓨터에 대 한 일반적인 질문과 대답 toosome를 제공 합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 757da816-a050-4889-a010-6f75d7978eb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: cynthn
ms.openlocfilehash: ee366a04bda347ce2be07bde4fc6bad306cc1da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-windows-virtual-machines"></a>Windows 가상 컴퓨터에 대한 자주 묻는 질문과 대답
이 문서 hello 리소스 관리자 배포 모델을 사용 하 여 Azure에서 만든 Windows 가상 컴퓨터에 대 한 몇 가지 일반적인 질문을 해결 합니다. 이 항목의 hello Linux 버전을 참조 하십시오. [질문 Linux 가상 컴퓨터에 대 한 질문과 대답](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>Azure VM에서 무엇을 실행할 수 있습니까?
모든 구독자는 Azure 가상 컴퓨터에서 서버 소프트웨어를 실행할 수 있습니다. Azure에서 실행 중인 Microsoft 서버 소프트웨어에 대 한 지원 정책 hello에 대 한 정보를 참조 하십시오. [Azure 가상 컴퓨터에 대 한 Microsoft 서버 소프트웨어 지원](https://support.microsoft.com/kb/2721672)

특정 버전의 Windows 7, Windows 8.1 및 Windows 10은 사용할 수 있는 tooMSDN Azure 혜택 구독자 및 개발 및 테스트 작업에 대 한 MSDN 개발 및 테스트 종 량 제 구독자입니다. 지침과 제한 사항을 포함한 자세한 내용은 [MSDN 구독자를 위한 Windows 클라이언트 이미지](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/)를 참조하세요. 

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>가상 컴퓨터에 얼마나 많은 용량의 저장소를 사용할 수 있습니까?
각 데이터 디스크는 too1 TB를 수 있습니다. 데이터 디스크를 사용할 수 있습니다 hello 수 hello hello 가상 컴퓨터 크기에 따라 다릅니다. 자세한 내용은 [Virtual Machines의 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.

Azure 관리 되는 디스크에는 hello 새롭고 권장 디스크 제공 하는 저장소 사용 하기 위해 Azure 가상 컴퓨터 데이터의 영구 저장소에 대 한 개가 있습니다. 각 가상 컴퓨터와 함께 여러 Managed Disks를 사용할 수 있습니다. Managed Disks는 프리미엄 Managed Disks와 표준 Managed Disks 등 내구성이 뛰어난 두 가지 저장소 옵션을 제공합니다. 가격 책정 정보는 [Managed Disks 가격 책정](https://azure.microsoft.com/pricing/details/managed-disks)을 참조하세요.

Azure 저장소 계정 hello 운영 체제 디스크 및 데이터 디스크에 대 한 저장소를 제공할 수도 있습니다. 각 디스크는 페이지 blob으로 저장된 .vhd 파일입니다. 가격 책정에 대한 자세한 내용은 [저장소 가격 세부 정보](https://azure.microsoft.com/pricing/details/storage/)를 참조하세요.

## <a name="how-can-i-access-my-virtual-machine"></a>나의 가상 컴퓨터에 액세스 하려면 어떻게 해야 합니까?
RDP(원격 데스크톱 연결)를 사용하여 Windows VM에 대한 원격 연결을 설정합니다. 자세한 내용은 [어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 원격 데스크톱 서비스 세션 호스트로 hello 서버를 구성 하지 않으면 두 개의 동시 연결이 최대 지원 됩니다.  

원격 데스크톱에 문제가 있는 경우 참조 [Windows 기반 Azure 가상 컴퓨터 문제를 해결 하는 원격 데스크톱 연결 tooa](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 

Hyper-v에 익숙한 경우 도구 비슷한 tooVMConnect에 대 한 보고 있을 수 있습니다. Azure 콘솔 액세스 tooa 가상 컴퓨터에서 지원 되지 않으므로 유사한 도구를 제공 하지 않습니다.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-by-default-toostore-data"></a>Hello 임시 디스크 (d: 드라이브 기본적으로 hello) toostore 데이터를 사용할 수 있습니까?
Hello 임시 디스크 toostore 데이터를 사용 하지 마십시오. 해당 드라이브는 임시 저장소일 뿐이므로 복구할 수 없는 데이터가 손실될 위험이 있습니다. Hello 가상 컴퓨터가 tooa 다른 호스트를 이동 하는 경우 데이터 손실이 발생할 수 있습니다. 가상 컴퓨터 크기 조정, hello 이유 가상 컴퓨터를 이동할 수 있는 몇 가지는 hello 호스트 또는 hello 호스트에서 하드웨어 오류를 업데이트 합니다.

Toouse hello d: 드라이브 문자가 필요 하는 응용 프로그램의 경우에 사용할 수 있도록 hello 임시 디스크 이외의 노드 d: 드라이브 문자를 재할당할 수 있습니다. 자세한 내용은 [변경 hello Windows 임시 디스크의 드라이브 문자를 hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.


## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Hello 임시 디스크의 hello 드라이브 문자를 변경 하려면 어떻게 해야 합니까?
Hello 페이지 파일을 이동 하 여 hello 드라이브 문자 및 재할당 드라이브 문자를 변경할 수는 있지만 toomake 있는지 단계는 특정 순서로 hello 수행 해야 합니다. 자세한 내용은 [변경 hello Windows 임시 디스크의 드라이브 문자를 hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

## <a name="can-i-add-an-existing-vm-tooan-availability-set"></a>기존 VM tooan 가용성 집합을 추가할 수 있습니까?
아니요. 가용성 집합의 VM toobe 파트를 표시할 경우 hello 집합 내에서 VM toocreate hello를 해야 합니다. 현재 방식으로 tooadd 만들어진 후에 설정할 VM tooan 가용성 없습니다.

## <a name="can-i-upload-a-virtual-machine-tooazure"></a>가상 컴퓨터 tooAzure를 업로드할 수 있나요?
예. 자세한 내용은 [마이그레이션 온-프레미스 Vm tooAzure](on-prem-to-azure.md)합니다.

## <a name="can-i-resize-hello-os-disk"></a>Hello OS 디스크 크기 조정 수 있습니까?
예. 자세한 내용은 [어떻게 tooexpand hello Azure 리소스 그룹에 가상 컴퓨터의 운영 체제 드라이브](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>기존 Azure VM을 복사 또는 복제할 수 있나요?
예. 관리 되는 이미지를 사용 하 여 하면 가상 컴퓨터의 이미지 만들고 사용 하 여 hello 이미지 toobuild 여러 새 Vm 수 있습니다. 자세한 내용은 [VM의 사용자 지정 이미지 만들기](tutorial-custom-images.md)를 참조하세요.

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Azure Resource Manager를 통해 캐나다 중부 및 캐나다 동부 지역이 보이지 않는 이유가 무엇인가요?

캐나다 중앙 및 캐나다 동부 hello 두 개의 새 영역 기존 Azure 구독에 대 한 가상 컴퓨터 만들기에 자동으로 등록 되지 않습니다. 이 등록을 통해 가상 컴퓨터를 배포할 때 자동으로 수행 되며 hello Azure 포털 tooany Azure 리소스 관리자를 사용 하 여 다른 영역입니다. 후 가상 컴퓨터는 배포 된 tooany 다른 Azure 지역 hello 새 영역 이후 가상 컴퓨터에 사용할 수 있어야 합니다.

## <a name="does-azure-support-linux-vms"></a>Azure에서 Linux VM을 지원하나요?
예. tooquickly 만들 참조 아웃 Linux VM tootry [hello 포털을 사용 하 여 Azure에서 Linux VM을 만들](../linux/quick-create-portal.md)합니다.

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>만든 후 NIC toomy VM 추가 합니까?
예, 이제 가능합니다. hello VM 첫 번째 요구 toobe 중지 할당 해제 합니다. 그런 다음 추가 하거나 NIC를 제거할 수 있습니다 (경우가 아니라면 hello VM에서 마지막 NIC hello). 

## <a name="are-there-any-computer-name-requirements"></a>컴퓨터 이름 요구 사항이 있나요?
예. hello 컴퓨터 이름은 길이가 15 자까지 가능 합니다. [명명 규칙 및 제한 사항](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하여 리소스 이름 지정에 대해 자세히 알아보세요.

## <a name="are-there-any-resource-group-name-requirements"></a>리소스 그룹 이름에 대한 요구 사항이 있나요?
예. hello 리소스 그룹 이름은 최대 90 자 수 있습니다. [명명 규칙 및 제한 사항](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하여 리소스 그룹에 대해 자세히 알아보세요.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>VM을 만들 때 hello username 요구 사항은 무엇입니까?

사용자 이름은 20자까지 지정할 수 있으며 마침표(".")로 끝날 수 없습니다. 


사용자 이름은 다음 hello 허용 되지 않습니다.
<table>
    <tr>
        <td style="text-align:center">관리자 역할 </td><td style="text-align:center"> 관리자 </td><td style="text-align:center"> 사용자 </td><td style="text-align:center"> user1</td>
    </tr>
    <tr>
        <td style="text-align:center">test </td><td style="text-align:center"> user2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>    <tr>
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
암호는 12 123 자가 하 여야 하 고 4 복잡성 요구 사항을 준수 하는 hello 부족 3 충족 해야 합니다.

* 소문자 포함
* 대문자 포함
* 숫자 포함
* 특수 문자 포함(정규식 일치 [\W_])

암호를 다음 hello 허용 되지 않습니다.

<table>
    <tr>
        <td>abc@123 </td>
        <td>P@$$w0rd </td>
        <td>P@ssw0rd </td>
        <td>P@ssword123 </td>
        <td>Pa$$word </td>
    </tr>
    <tr>
        <td>pass@word1 </td>
        <td>Password! </td>
        <td>Password1 </td>
        <td>Password22 </td>
        <td>iloveyou! </td>
    </tr>
</table>
