---
title: "aaaCreate 및 Azure에서 Linux VHD 업로드"
description: "Toocreate 알아보고 업로드는 Azure 가상 하드 디스크 (VHD)는 Linux 운영 체제를 포함 합니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: d351396c-95a0-4092-b7bf-c6aae0bbd112
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 208e15c035edb5520fc29ba8e4e71c42b041864d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="information-for-non-endorsed-distributions"></a>보증되지 않는 배포에 대한 정보
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

hello Azure 플랫폼 SLA 적용 hello 한 경우에 Linux 운영 체제를 실행 하는 toovirtual 컴퓨터의 hello [보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 사용 됩니다. Hello Azure 이미지 갤러리는 제공 되는 모든 Linux 배포판 보증 hello 필요한 구성으로 배포 합니다.

* [Azure의 Linux - 보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Microsoft Azure의 Linux 이미지 지원](https://support.microsoft.com/kb/2941892)

Azure에서 실행 되는 모든 분포에는 다양 한 필수 구성 요소 toohave hello 플랫폼에서 실행 가능성이 tooproperly toomeet이 필요 합니다.  이 문서는 결코 포괄적인 모든 분포는 다릅니다. 및 모든 hello 아래 조건 것은 아니며 있어야를 충족 하는 경우에 toosignificantly 조정 hello 플랫폼에서 올바르게 실행 하 여 Linux 시스템 tooensure 가능 합니다.

따라서 가능한 경우 [Azure 보증 배포판의 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 중 하나를 사용하여 시작하는 것이 좋습니다. hello 다음 문서를 안내할 어떻게 tooprepare hello 다양 한 Azure에서 지원 되는 Linux 배포판을 보증 합니다.

* **[CentOS 기반 배포](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES 및 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

이 문서의 나머지 부분 hello 중점적으로 Azure에서 Linux 배포판을 실행 하기 위한 일반 지침입니다.

## <a name="general-linux-installation-notes"></a>일반 Linux 설치 참고 사항
* hello VHDX 형식은 지원 되지 않습니다 Azure에서만 **고정 VHD**합니다.  Hyper-v 관리자를 사용 하 여 hello 디스크 tooVHD 형식을 변환 하거나 convert vhd cmdlet hello 수 있습니다. VirtualBox를 사용 하는 경우 선택 하는 것이 즉 **고정 크기** 으로 반대로 toohello 기본 hello 디스크를 만들 때 동적으로 할당 합니다.
* Azure에서는 1세대 가상 컴퓨터만 지원합니다. 가상 컴퓨터 1 및 고정 tooa 동적 확장 VHDX toohello VHD 파일 형식에서 디스크 크기의 세대를 변환할 수 있습니다. 하지만 가상 컴퓨터의 세대를 변경할 수 없습니다. 자세한 내용은 [Hyper-V에 1 또는 2세대 가상 컴퓨터를 만들어야 합니까?](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)를 참조하세요.
* hello 최대 허용 크기 hello에 대 한 VHD는 1, 023 GB입니다.
* hello Linux 시스템을 설치할 때 *권장* LVM (종종 대부분의 설치에 대 한 hello 기본값) 보다는 표준 파티션을 사용 하면 됩니다. OS 디스크 연결 toobe tooanother 해야 합니다. 경우에 특히 복제 된 Vm과 LVM 이름 충돌을 방지 합니다이 문제 해결을 위해 동일한 VM입니다. 데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.
* UDF 파일 시스템 탑재에 대한 커널 지원이 필요합니다. 첫 번째 부팅 Azure hello에-프로비저닝 구성 toohello Linux VM은 연결 된 toohello 게스트 UDF로 포맷 된 미디어를 통해 전달 됩니다. hello Azure Linux 에이전트는 해당 구성을 수 toomount hello UDF 파일 시스템 tooread 수 하 고 hello VM을 프로 비전 해야 합니다.
* 2.6.37 버전 미만의 Linux 커널은 VM 크기가 더 클 때 Hyper-V에서 NUMA를 지원하지 않습니다. 이 문제를 주로 영향 업스트림 hello를 사용 하 여 이전 분포 Red Hat 2.6.32 커널 RHEL 6.6 (커널 2.6.32 504)에서 수정 되었습니다. 2.6.32-504 설정 해야 하는 보다 2.6.37, 다음 보다 오래 된 사용자 지정 커널 또는 이전 RHEL 기반 커널을 실행 하는 시스템 부팅 매개 변수를 hello `numa=off` hello 커널 grub.conf의 명령줄입니다. 자세한 내용은 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.
* 스왑 파티션을 hello OS 디스크에 구성 하지 마십시오. hello Linux 에이전트 구성된 toocreate hello 일시적인 리소스 디스크의 스왑 파일 일 수 있습니다.  이 대 한 자세한 내용은 아래 hello 단계에서 찾을 수 있습니다.
* 모든 hello Vhd 크기를 1MB의 배수인가 있어야 합니다.

### <a name="installing-kernel-modules-without-hyper-v"></a>Hyper-V 없이 커널 모듈 설치
Azure는 Linux 특정 커널 모듈이 순서 toorun azure에서에 설치 되어 있어야 하므로 hello Hyper-v 하이퍼바이저에서 실행 됩니다. Hyper-v 외부에서 생성 된 VM이 있는 경우 hello Linux 설치 관리자 포함시킬지 여부 hello 드라이버 Hyper-v에 대 한 hello 초기 ramdisk (initrd 또는 initramfs)에서 실행 중인 없지 않은 한는 Hyper-v 환경입니다. 다른 가상화 시스템 (예: Virtualbox, KVM 등) tooprepare Linux 이미지를 사용할 때는 hello 이상 toorebuild hello initrd tooensure 할 수 있습니다 `hv_vmbus` 및 `hv_storvsc` 커널 모듈은 hello 초기 ramdisk에서 사용할 수 있습니다.  이것은 알려진된 문제 이상 hello 업스트림 Red Hat 분포에 따라 시스템에 있습니다.

hello initrd 또는 initramfs 이미지를 다시 작성 하기 위한 hello 메커니즘 hello 배포에 따라 달라질 수 있습니다. 분포의 설명서를 참조 하거나 hello 적절 한 절차에 대 한 지원 하십시오.  다음은 toorebuild initrd hello를 사용 하 여 hello 하는 방법에 대 한 하나의 예 `mkinitrd` 유틸리티:

먼저, hello 기존 initrd 이미지를 백업 합니다.

    # cd /boot
    # sudo cp initrd-`uname -r`.img  initrd-`uname -r`.img.bak

다음으로 hello initrd hello로 다시 작성 `hv_vmbus` 및 `hv_storvsc` 커널 모듈:

    # sudo mkinitrd --preload=hv_storvsc --preload=hv_vmbus -v -f initrd-`uname -r`.img `uname -r`


### <a name="resizing-vhds"></a>VHD 크기 조정
Azure에서 VHD 이미지를 정렬 하는 실제 크기 too1MB 있어야 합니다.  일반적으로 Hyper-V를 사용하여 만든 VHD는 이미 올바르게 조정되어 있습니다.  오류 메시지와 비슷한 toohello 다음 toocreate 할 때 나타날 수 있습니다 다음 VHD hello 올바르게 정렬 되지 않은 경우는 *이미지* VHD에서:

    "hello VHD http://<mystorageaccount>.blob.core.windows.net/vhds/MyLinuxVM.vhd has an unsupported virtual size of 21475270656 bytes. hello size must be a whole number (in MBs).”

tooremedy hello Hyper-v 관리자 콘솔 이나 hello를 사용 하 여 VM 크기를 조정할 수 있습니다이 hello [RESIZE-VHD](http://technet.microsoft.com/library/hh848535.aspx) Powershell cmdlet.  Windows 환경에서 실행 되지 않는 경우 다음 것은 toouse qemu img tooconvert (필요한 경우)이 좋으며 hello VHD의 크기를 조정 합니다.

> [!NOTE]
> VHD 형식이 잘못 지정되는 qemu-img 버전 >=2.2.1에 알려진 버그가 있습니다. QEMU 2.6에서 hello 문제가 해결 되었습니다. Toouse 좋습니다 qemu-img 2.2.0 또는 소문자 또는 업데이트 too2.6 이상. 참조: https://bugs.launchpad.net/qemu/+bug/1490611
> 
> 

1. VHD를 사용 하 여 직접 도구와 같은 hello 크기 조정 `qemu-img` 또는 `vbox-manage` 부팅할 수 VHD 발생할 수 있습니다.  따라서 toofirst convert hello VHD tooa 원시 디스크 이미지 좋습니다.  원시 디스크 이미지 (KVM 같은 하이퍼바이저에 대 한 hello 기본값)로 이미 hello VM 이미지를 만든 경우이 단계를 건너뛸 수 있습니다.
   
       # qemu-img convert -f vpc -O raw MyLinuxVM.vhd MyLinuxVM.raw

2. Hello 필요한 실제 크기 hello hello 디스크 이미지 tooensure의 크기는 정렬 된 too1MB을 계산 합니다.  hello bash 셸 스크립트를 따라이 도움이 될 수 있습니다.  hello 스크립트 사용 하 여 "`qemu-img info`" toodetermine hello 디스크 이미지의 크기를 가상 hello hello 크기 toohello 계산 되며 다음 1MB:
   
       rawdisk="MyLinuxVM.raw"
       vhddisk="MyLinuxVM.vhd"
   
       MB=$((1024*1024))
       size=$(qemu-img info -f raw --output json "$rawdisk" | \
              gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
   
       rounded_size=$((($size/$MB + 1)*$MB))
       echo "Rounded Size = $rounded_size"

3. $Rounded_size를 사용 하 여 스크립트 위에 hello에 설정 된 대로 hello 원시 디스크의 크기를 조정 합니다.
   
       # qemu-img resize MyLinuxVM.raw $rounded_size

4. Hello 원시 디스크 백 tooa를 변환 크기가 고정 된 VHD:
   
       # qemu-img convert -f raw -o subformat=fixed -O vpc MyLinuxVM.raw MyLinuxVM.vhd

   또는 qemu 버전과 **2.6 +** hello 포함 `force_size` 옵션:

       # qemu-img convert -f raw -o subformat=fixed,force_size -O vpc MyLinuxVM.raw MyLinuxVM.vhd

## <a name="linux-kernel-requirements"></a>Linux 커널 요구 사항
hello Hyper-v와 Azure에 대 한 Linux 통합 서비스 (LIS) 드라이버 기여 하 직접 toohello 업스트림 Linux 커널을 합니다. 최신 Linux 커널 버전(예: 3.x)을 포함하는 대부분의 배포에서는 이러한 드라이버가 이미 제공되거나 이러한 드라이버의 백 포트 버전이 커널과 함께 제공됩니다.  이들이 드라이버 지속적으로 업데이트 하는 중에 새로운 수정 및 기능을 사용 하 여 hello 업스트림 커널 하므로 가능 하면 toorun 좋습니다는 [배포 보증](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 이러한 수정 및 업데이트를 포함 합니다.

Red Hat Enterprise Linux 버전의 변형을 실행 하는 경우 **6.0-6.3**를 Hyper-v 용 LIS 드라이버 최신 tooinstall hello를 해야 합니다. hello 드라이버를 찾을 수 [이 위치의](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409)합니다. RHEL 기준으로 **6.4 +** (및 파생물) hello LIS 드라이버에 이미 포함 되어 있으므로 추가 설치 패키지 및 hello 커널 필요한 toorun Azure에서 해당 시스템 됩니다.

사용자 지정에 대 한 커널 필요한 경우에 보다 최신 커널 버전 toouse 것이 좋습니다 (즉, **3.8 +**). 이러한 분포 또는 자신의 커널 유지 관리 하는 공급 업체에 대 한 작업에 필요한 tooregularly backport hello LIS 드라이버 커널에서 hello 업스트림 커널 tooyour 사용자 지정 됩니다.  비교적 최근 커널 버전을 이미 실행 중인 경우에 tookeep 트랙의 업스트림의 수정 hello LIS 드라이버 및 backport 것 필요에 따라 것이 좋습니다. hello LIS 드라이버 소스 파일의 hello 위치가 hello에서 사용할 수 있는 [유지 관리자](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS) hello Linux 커널 소스 트리에 파일:

    F:    arch/x86/include/asm/mshyperv.h
    F:    arch/x86/include/uapi/asm/hyperv.h
    F:    arch/x86/kernel/cpu/mshyperv.c
    F:    drivers/hid/hid-hyperv.c
    F:    drivers/hv/
    F:    drivers/input/serio/hyperv-keyboard.c
    F:    drivers/net/hyperv/
    F:    drivers/scsi/storvsc_drv.c
    F:    drivers/video/fbdev/hyperv_fb.c
    F:    include/linux/hyperv.h
    F:    tools/hv/

최소한, 패치 다음 hello hello 없는 경우 Azure에서 toocause 문제 알려진는 하며 하므로 이러한 포함 되어야 합니다 hello 커널에 합니다. 이 목록에는 모든 배포에 대해 완전한 전체 정보가 포함되어 있지는 않습니다.

* [ata_piix: 기본적으로 디스크 toohello Hyper-v 드라이버를 연기](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/ata/ata_piix.c?id=cd006086fa5d91414d8ff9ff2b78fbb593878e3c)
* [storvsc: hello 재설정 경로에서 전송 중인 패킷의 대 한 계정](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/scsi/storvsc_drv.c?id=5c1b10ab7f93d24f29b5630286e323d1c5802d5c)
* [storvsc: WRITE_SAME을 사용하지 마세요.](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=3e8f4f4065901c8dfc51407e1984495e1748c090)
* [storvsc: RAID 및 가상 호스트 어댑터 드라이버에 대한 WRITE SAME 해제](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=54b2b50c20a61b51199bedb6e5d2f8ec2568fb43)
* [storvsc: NULL 포인터 역참조 수정](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=b12bb60d6c350b348a4e1460cd68f97ccae9822e)
* [storvsc: 링 버퍼 오류로 I/O가 중지됨](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=e86fb5e8ab95f10ec5f2e9430119d5d35020c951)
* [scsi_sysfs: __scsi_remove_device 이중 실행 방지](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/scsi_sysfs.c?id=be821fd8e62765de43cc4f0e2db363d0e30a7e9b)

## <a name="hello-azure-linux-agent"></a>hello Azure Linux 에이전트
hello [Azure Linux 에이전트](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (waagent)가 필요 tooproperly Azure에서 Linux 가상 컴퓨터를 프로 비전 합니다. Hello 최신 버전 가져오기, 파일 문제 또는 hello에 대 한 끌어오기 요청을 제출할 수 [Linux 에이전트 GitHub 리포지토리](https://github.com/Azure/WALinuxAgent)합니다.

* hello Linux 에이전트는 hello Apache 2.0 라이선스에 따라 해제 됩니다. 많은 배포 이미 RPM deb 패키지에 대 한 제공 hello 에이전트 및 하므로 경우에 따라이 설치 하 고 업데이트할 수 약간의 노력으로 합니다.
* hello Azure Linux 에이전트는 Python v2.6 + 필요합니다.
* hello 에이전트는 hello python pyasn1 모듈도 필요합니다. 대부분의 배포에서는 이 모듈이 설치 가능한 별도의 패키지로 제공됩니다.
* 일부 경우에 hello Azure Linux 에이전트 NetworkManager와 호환 되지 않을 수 있습니다. 다양 한 배포에서 제공 하는 hello RPM/Deb 패키지 충돌 toohello waagent 패키지로 NetworkManager를 구성 하 고 따라서 제거 하므로 NetworkManager hello Linux 에이전트 패키지를 설치 하는 경우.

## <a name="general-linux-system-requirements"></a>일반 Linux 시스템 요구 사항

* GRUB 또는 GRUB2 tooinclude hello 매개 변수 뒤에 hello 커널 부팅 줄을 수정 합니다. 또한 이렇게 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 문제를 디버깅 지원:
  
        console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300
  
    또한 이렇게 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 문제를 디버깅 지원 합니다.
  
    또한 위의 toohello, 것이 좋습니다 너무*제거* 있을 경우 매개 변수 다음 hello:
  
        rhgb quiet crashkernel=auto
  
    그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다. hello `crashkernel` 옵션이 수 있습니다, 원하는 경우 구성 하는 왼쪽 이지만이 매개 변수 감소할 hello hello 128MB 이상의 VM에서에서 사용 가능한 메모리 크기는 hello 더 작은 VM 크기에 문제가 될 수 있습니다.

* Hello Azure Linux 에이전트를 설치합니다.
  
    hello Azure Linux 에이전트는 Azure에서 Linux 이미지를 프로 비전 필요 합니다.  많은 배포 RPM 또는 Deb 패키지로 hello 에이전트 제공 (hello 패키지는 일반적으로 라고 'WALinuxAgent' 또는 'walinuxagent').  hello 에이전트 설치할 수도 있습니다 수동으로 hello에 hello 단계에 따라 [Linux 에이전트 가이드](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

* 해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.  일반적으로 hello 기본값입니다.

* Hello OS 디스크에 스왑 공간을 만들지 마십시오
  
    hello Azure Linux 에이전트 Azure에서 프로 비전 한 후 연결 된 toohello VM은 hello 로컬 리소스 디스크를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다. 해당 하는 hello 로컬 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다. Hello Azure Linux 에이전트를 설치한 후 (이전 단계 참조) hello /etc/waagent.conf에 매개 변수를 적절 하 게 뒤 수정:
  
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

* 마지막 단계로 hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 합니다.
  
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
  
  > [!NOTE]
  > Virtualbox hello 실행 한 후 다음 오류가 표시 될 수 있습니다 ' waagent-force-deprovision': `[Errno 5] Input/output error`합니다. 이 오류 메시지는 중요하지 않으므로 무시할 수 있습니다.
  > 
  > 

* 그런 다음 hello 가상 컴퓨터를 tooshut 필요 하 고 hello VHD tooAzure 업로드 됩니다.

