


이 문서에서는 사용자가 요청 hello 클래식 배포 모델을 사용 하 여 만든 Azure 가상 컴퓨터에 대 한 몇 가지 일반적인 질문 합니다.

## <a name="can-i-migrate-my-vm-created-in-hello-classic-deployment-model-toohello-new-resource-manager-model"></a>Hello 클래식 배포 모델 toohello 새 리소스 관리자 모델에서 만든 VM을 마이그레이션할 수 있습니까?
예. 방법에 대 한 지침은 toomigrate를 참조 하세요.

* [클래식 tooAzure Azure PowerShell을 사용 하 여 리소스 관리자에서에서 마이그레이션](../articles/virtual-machines/windows/migration-classic-resource-manager-ps.md)합니다.
* [클래식 tooAzure Azure CLI를 사용 하 여 리소스 관리자에서에서 마이그레이션](../articles/virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md)합니다.

## <a name="what-can-i-run-on-an-azure-vm"></a>Azure VM에서 무엇을 실행할 수 있습니까?
모든 구독자는 Azure 가상 컴퓨터에서 서버 소프트웨어를 실행할 수 있습니다. 최신 버전의 Windows Server뿐만 아니라 다양한 Linux 배포를 실행할 수 있습니다. 지원 세부 사항은, 다음을 참조하세요:

• Windows VM의 경우 -- [Azure Virtual Machines에 대한 Microsoft 서버 소프트웨어 지원](http://go.microsoft.com/fwlink/p/?LinkId=393550)

• Linux VM의 경우 -- [Azure 인증 배포의 Linux](http://go.microsoft.com/fwlink/p/?LinkId=393551)

Windows 클라이언트 이미지에 대 한 특정 버전의 Windows 7 및 Windows 8.1 사용할 수 있는 tooMSDN Azure 혜택 구독자와 MSDN 개발 및 테스트 종 량 제 구독자, 개발 및 테스트 작업에 대 한 합니다. 지침과 제한 사항을 포함한 자세한 내용은 [MSDN 구독자를 위한 Windows 클라이언트 이미지](https://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/)를 참조하세요.

## <a name="why-are-affinity-groups-being-deprecated"></a>왜 선호도 그룹이 사용되지 않나요?
선호도 그룹은 Azure 내 고객의 클라우드 서비스 배포 및 저장소 계정의 지리적 그룹화를 위한 레거시 개념입니다. 원래 hello 초기 Azure 네트워크 디자인에 tooimprove-VM 네트워크 성능을 제공 받은 합니다. 소규모 영역에는 하드웨어의 제한 된 tooa 된 가상 네트워크 (Vnet) hello 초기 릴리스도 지원 합니다.

hello 영역 내에서 현재 Azure 네트워크는 선호도 그룹은 필요 하지 않은 되도록 설계 되었습니다. 또한 가상 네트워크는 지역 범위에 있기 때문에 가상 네트워크를 사용하는 경우 선호도 그룹이 필요하지 않습니다. Toothese 향상, 인해 더 이상는 권장 고객 선호도 그룹 하므로 일부 시나리오에서는 제한 될 수 없습니다. 선호도 그룹을 사용 하 여 hello 다양 한 tooyou 사용할 수 있는 VM 크기를 제한 하는 Vm toospecific 하드웨어가 불필요 하 게 연결 합니다. Tooadd 거의 용량은 hello 특정 하드웨어 hello 선호도 그룹과 연결 된 경우 새 Vm을 시도할 때에 toocapacity 관련 오류가 발생할 수 있습니다 것입니다.

선호도 그룹 기능 hello Azure 포털 및 hello Azure 리소스 관리자 배포 모델에 이미 사용 되지 않습니다. Hello 클래식 Azure 포털에 대 한 선호도 그룹 만들기 및 저장소 리소스를 고정 된 tooan 선호도 그룹 만들기에 대 한 지원을 사용이 중지 하는 것입니다. 선호도 그룹을 사용 하는 toomodify 기존 클라우드 서비스를 필요 하지 않습니다. 그러나 Azure 기술 지원 엔지니어가 권장하지 않는 한 새 클라우드 서비스에 대한 선호도 그룹을 사용하지 않도록 합니다.

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>가상 컴퓨터에 얼마나 많은 용량의 저장소를 사용할 수 있습니까?
각 데이터 디스크는 too1 TB를 수 있습니다. 데이터 디스크를 사용할 수 있습니다 hello 수 hello hello 가상 컴퓨터 크기에 따라 다릅니다. 자세한 내용은 [Virtual Machines의 크기](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

Azure 저장소 계정을 hello 운영 체제 디스크 및 데이터 디스크에 대 한 저장소를 제공합니다. 각 디스크는 페이지 blob으로 저장된 .vhd 파일입니다. 가격 책정에 대한 자세한 내용은 [Storage 가격 세부 정보](http://go.microsoft.com/fwlink/p/?LinkId=396819)를 참조하세요.

## <a name="which-virtual-hard-disk-types-can-i-use"></a>어떤 가상 하드 디스크 유형을 사용할 수 있습니까?
Azure는 고정된 VHD 형식 가상 하드 디스크를 지원합니다. Toofirst 해야 원하는 toouse Azure에서 VHDX를 사용 하도록 설정한 경우 Hyper-v 관리자 또는 hello를 사용 하 여 변환 [CONVERT-VHD](http://go.microsoft.com/fwlink/p/?LinkId=393656) cmdlet. 사용 하는 작업을 수행한 후 [Add-azurevhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet (서비스 관리 모드)에서 tooupload hello VHD tooa 저장소 계정에서 Azure 가상 컴퓨터와 함께 사용할 수 있도록 합니다.

* Linux 지침은 [만들어 포함 된 가상 하드 디스크를 업로드 하는 Linux 운영 체제 hello](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.
* 자세한 내용은 Windows [만들기 및 업로드 Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

## <a name="are-these-virtual-machines-hello-same-as-hyper-v-virtual-machines"></a>이러한 가상 컴퓨터 hello Hyper-v 가상 컴퓨터로 동일한?
여러 가지 방법으로 너무 비슷한 하기가 있지만 "1 세대" Hyper-v Vm을 동일한 hello 정확 하 게 하는 합니다. 두 유형 모두 가상화 된 하드웨어를 제공 하 고 hello VHD 형식의 가상 하드 디스크는 호환 키를 누릅니다. 이 의미는 사용자가 Hyper-V 및 Azure 사이를 이동할 수 있다는 것입니다. Hyper-V 사용자에게 중요한 세 가지 차이점이 있습니다.

* Azure 콘솔 액세스 tooa 가상 컴퓨터를 제공 하지 않습니다. 완료 될 때까지 없는 방식으로 tooaccess VM는 부팅 합니다.
* 대부분의 [크기](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 가진 Azure VM에는 가상 네트워크 어댑터가 하나만 있습니다. 따라서 외부 IP 주소가 하나만 지정될 수 있습니다. (hello A8 및 A9 크기는 두 번째 네트워크 어댑터 응용 프로그램 간의 통신에 사용 제한 된 시나리오의 인스턴스.)
* Azure VM은 2세대 Hyper-V VM 기능을 지원하지 않습니다. 이러한 기능에 대한 자세한 내용은 [Hyper-v에 대한 가상 컴퓨터 사양](http://technet.microsoft.com/library/dn592184.aspx) 및 [2세대 가상 컴퓨터 개요](https://technet.microsoft.com/library/dn282285.aspx)를 참조하세요.

## <a name="can-these-virtual-machines-use-my-existing-on-premises-networking-infrastructure"></a>이러한 가상 컴퓨터는 현존하는 온-프레미스 네트워킹 인프라를 사용할 수 있습니까?
Hello 클래식 배포 모델에서 만든 가상 컴퓨터에 대 한 Azure 가상 네트워크 tooextend 기존 인프라를 사용할 수 있습니다. hello 방법은 지사를 설정과 유사 합니다. 있습니다 수 프로 비전 및 Azure에서 가상 사설망 (Vpn)을 관리으로 안전 하 게 tooon 온-프레미스 연결 IT 인프라입니다. 자세한 내용은 [Virtual Network 개요](../articles/virtual-network/virtual-networks-overview.md)를 참조하세요.

Toospecify hello 네트워크 hello 가상 컴퓨터를 만드는 가상 컴퓨터 toobelong toowhen hello 필요 합니다. 기존 가상 컴퓨터 tooa 가상 네트워크에 추가할 수 없습니다. 그러나 hello 가상 하드 디스크 (VHD) hello 기존 가상 컴퓨터에서 분리 하 여이 해결할 수 있으며 사용 하 여 새 가상 컴퓨터를 toocreate 원하는 hello 네트워킹 구성.

## <a name="how-can-i-access--my-virtual-machine"></a>나의 가상 컴퓨터에 액세스 하려면 어떻게 해야 합니까?
Linux VM에 대 한 SSH (보안 셸) 또는 Windows VM에 대 한 원격 데스크톱 연결을 사용 하 여 tooestablish toohello 가상 컴퓨터에서 원격 연결 toolog 해야 합니다. 자세한 내용은 다음을 참조하세요.

* [어떻게 tooa Windows Server를 실행 하는 가상 컴퓨터에 tooLog](../articles/virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다. Hello 서버를 원격 데스크톱 서비스 세션 호스트로 구성 되어 있지 않으면 최대 2 개의 동시 연결이 지원 됩니다.  
* [어떻게 tooa Linux를 실행 하는 가상 컴퓨터에 tooLog](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 기본적으로, SSH는 최대 10개의 동시 연결을 허용합니다. Hello 구성 파일을 편집 하 여이 번호를 늘릴 수 있습니다.

원격 데스크톱 또는 SSH에 문제가 있는 경우 설치 하 고 hello를 사용 하 여 [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 확장 toohelp 수정 hello 문제입니다.

Windows VM에 대한 추가 옵션은 다음과 같습니다.

* 에 Azure 클래식 포털 hello hello VM을 차례로 클릭 **원격 액세스를 다시 설정** hello 명령 모음에서 합니다.
* 검토 [Windows 기반 Azure 가상 컴퓨터 문제를 해결 하는 원격 데스크톱 연결 tooa](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
* Tooconnect toohello VM을 Windows PowerShell 원격을 사용 하거나 다른 리소스 tooconnect toohello VM에 대 한 추가 끝점을 만듭니다. 자세한 내용은 참조 [어떻게 tooSet 끝점 tooa 가상 컴퓨터](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

Hyper-v에 익숙한 경우 도구 비슷한 tooVMConnect에 대 한 보고 있을 수 있습니다. Azure 콘솔 액세스 tooa 가상 컴퓨터에서 지원 되지 않으므로 유사한 도구를 제공 하지 않습니다.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-for-windows-or-devsdb1-for-linux-toostore-data"></a>Hello 임시 디스크 (Windows 용 d: 드라이브 또는 /dev/sdb1 Linux 용 hello) toostore 데이터를 사용할 수 있습니까?
Hello 임시 디스크 (d: 드라이브에 대 한 Windows는 기본적으로 또는 /dev/sdb1 Linux 용 hello) toostore 데이터를 사용해 서는 안 됩니다. 해당 드라이브는 임시 저장소일 뿐이므로 복구할 수 없는 데이터가 손실될 위험이 있습니다. 이 가상 컴퓨터 hello tooa 다른 호스트를 이동할 때 발생할 수 있습니다. 가상 컴퓨터 크기 조정, hello 이유 가상 컴퓨터를 이동할 수 있는 몇 가지는 hello 호스트 또는 hello 호스트에서 하드웨어 오류를 업데이트 합니다.

## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Hello 임시 디스크의 hello 드라이브 문자를 변경 하려면 어떻게 해야 합니까?
Windows 가상 컴퓨터에서 hello 페이지 파일을 이동 하 여 hello 드라이브 문자 및 재할당 드라이브 문자를 변경할 수 있지만 단계는 특정 순서로 hello 수행 되었는지 toomake 필요 합니다. 자세한 내용은 [변경 hello Windows 임시 디스크의 드라이브 문자를 hello](../articles/virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

## <a name="how-can-i-upgrade-hello-guest-operating-system"></a>Hello 게스트 운영 체제를 업그레이드 하는 방법
hello 용어는 일반적으로 의미 이동 tooa 더 hello 하면서 사용 중인 운영 체제의 최신 릴리스를 동일한 하드웨어. Azure Vm에 대 한 hello tooa 이동 하기 위한 프로세스 보다 최근 릴리스로 Linux 및 Windows 용 달라 집니다.

* Linux Vm에 대 한 hello 패키지 관리 도구 및 hello 배포에 대 한 적절 한 절차를 사용 합니다.
* Windows 가상 컴퓨터를 다음과 같이 hello Windows Server 마이그레이션 도구를 사용 하 여 toomigrate hello 서버가 필요 합니다. Azure에 있는 동안 tooupgrade hello 게스트 OS 사용 하지 마십시오. Hello 액세스 toohello 가상 컴퓨터를 손실 될 위험이 때문에 두는 것이 없습니다. Hello 업그레이드 하는 동안 문제가 발생 하면 손실 될 수 있습니다 hello 기능 toostart 원격 데스크톱 세션 수 tootroubleshoot hello 문제 수 없게 하 고 있습니다.

Hello 도구 및 Windows Server로 마이그레이션하는 프로세스에 대 한 일반 정보를 참조 하십시오. [서버 역할 및 기능 마이그레이션 tooWindows](http://go.microsoft.com/fwlink/p/?LinkId=396940)합니다.

## <a name="whats-hello-default-user-name-and-password-on-hello-virtual-machine"></a>Hello 기본 사용자 이름 및 암호 hello 가상 컴퓨터에서 무엇 인가요?
Azure에서 제공 하는 hello 이미지 미리 구성 된 사용자 이름 및 암호 필요는 없습니다. 사용자 이름 및 암호를 사용 하 여 tooprovide 이러한 이미지 중 하나를 사용 하 여 가상 컴퓨터를 만들 때 필요 합니다 toolog toohello 가상 컴퓨터에 있습니다.

설치 하 고 hello를 사용 하 여 수 hello 사용자 이름 또는 암호가 잊었으며 hello VM 에이전트를 설치한 경우 [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 확장 toofix hello 문제입니다.

추가 정보:

* Hello Linux 이미지에 대 한 hello Azure 클래식 포털을 사용 하는 경우 'azureuser'를 기본 사용자 이름으로 지정 되었으나 hello 방식으로 toocreate hello 가상 컴퓨터로 ' 갤러리에서 ' 대신 ' 빨리 만들기 '를 사용 하 여이 변경할 수 있습니다. 갤러리에서 '를 사용 하 여 결정할 수도 있습니다 여부 toouse 암호, SSH 키 또는 둘 다 toolog에 있습니다. hello 사용자 계정이 권한 없는 사용자가 'sudo' 액세스 권한이 있는 toorun privileged 명령입니다. hello 'root' 계정은 비활성화 됩니다.
* Windows 이미지에 대 한 hello VM을 만들 때 tooprovide 사용자 이름 및 암호 필요 합니다. hello 계정 toohello 관리자 그룹에 추가 됩니다.

## <a name="can-azure-run-anti-virus-on-my-virtual-machines"></a>Azure가 내 가상 컴퓨터에서 바이러스 백신을 실행할 수 있습니까?
Azure는 바이러스 백신 솔루션에 대 한 몇 가지 옵션을 제공 하지만 tooyou toomanage를 하기. 예를 들어, 맬웨어 방지 프로그램 소프트웨어에 대 한 별도 구독을 할 수 있습니다 및 toorun 검색 및 업데이트를 설치할 때 toodecide가 필요 합니다. Windows 가상 컴퓨터를 만들 때 또는 나중에 Microsoft 맬웨어 방지 프로그램, Symantec Endpoint Protection 또는 TrendMicro Deep Security Agent에 대한 VM 확장으로 백신 프로그램 지원을 추가할 수 있습니다. hello Symantec 및 TrendMicro 확장 사용 기간이 제한 된 무료 평가판 구독 또는 기존 엔터프라이즈 구독을 사용할 수 있습니다. Microsoft 맬웨어 방지 프로그램은 무료입니다. 자세한 내용은 다음을 참조하세요.

* [어떻게 tooinstall Azure VM에서 Symantec Endpoint Protection을 구성 하 고](http://go.microsoft.com/fwlink/p/?LinkId=404207)
* [어떻게 tooinstall 하 고 서비스는 Azure VM에서 Trend Micro Deep Security 구성](http://go.microsoft.com/fwlink/p/?LinkId=404206)
* [Azure Virtual Machines에 맬웨어 방지 솔루션 배포](https://azure.microsoft.com/blog/2014/05/13/deploying-antimalware-solutions-on-azure-virtual-machines/)

## <a name="what-are-my-options-for-backup-and-recovery"></a>백업 및 복구에 대한 나의 옵션은 무엇입니까?
Azure Backup은 특정 지역에서 미리 보기로 제공됩니다. 자세한 내용은 [Azure 가상 컴퓨터 백업](../articles/backup/backup-azure-vms.md)을 참조하세요. 다른 솔루션은 인증된 파트너에서 사용할 수 있습니다. 현재 사용할 수 있는 항목을 toofind hello Azure 마켓플레이스를 검색 합니다.

추가 옵션은 blob 저장소의 toouse hello 스냅숏 기능. toodo이를 blob 스냅숏을 사용 하는 작업 하기 전에 VM hello 아래로 tooshut 필요 합니다. 이 보류 중인 데이터 쓰기가 저장 하 고 일관 된 상태로 hello 파일 시스템을 넣습니다.

## <a name="how-does-azure-charge-for-my-vm"></a>내 VM에 대한 Azure 청구를 수행하는 방법
Azure 요금 hello VM의 크기와 운영 체제에 따라는 시간당 요금. 부분 시간의 경우 Azure hello 사용 (분)에 대해서만 요금. 특정 사전 설치 된 소프트웨어가 포함 된 VM 이미지와 hello VM을 만드는 경우 추가 시간당 소프트웨어 요금이 적용 될 수 있습니다. Hello VM의 운영 체제 및 데이터 디스크용 저장소에 대해 별도로 요금이 청구 됩니다. 임시 디스크 저장소는 무료입니다.

Hello VM 상태가 실행 중 또는 중지됨인 이지만 hello VM 상태가 중지 되 면 청구 되지 않습니다 경우 요금이 청구 됩니다 (할당 취소) 합니다. tooput hello에서 VM 중지 (할당된 취소) 상태 hello 다음 중 하나를 수행 합니다.

* 종료 하거나 hello Azure 클래식 포털에서에서 VM hello를 삭제 합니다.
* Hello Azure PowerShell 모듈에서 사용할 수 있는 hello Stop-azurevm cmdlet을 사용 합니다.
* Hello 역할 종료 작업을 사용 하 여 서비스 관리 REST API hello에 하 고 hello PostShutdownAction 요소에 대해 StoppedDeallocated를 지정 합니다.

자세한 내용은 [가상 컴퓨터 가격 책정](https://azure.microsoft.com/pricing/details/virtual-machines/)을 참조하세요.

## <a name="will-azure-reboot-my-vm-for-maintenance"></a>Azure는 유지관리를 위해 내 VM을 다시 부팅합니까?
경우에 따라 azure는 hello Azure 데이터 센터에서에서 계획 된 정기 유지 관리 업데이트의 일부로 VM 다시 시작합니다.

Azure가 사용자의 VM에 영향을 주는 심각한 하드웨어 문제를 감지할 때 계획되지 않은 유지 관리 이벤트가 발생할 수 있습니다. 계획 되지 않은 이벤트에 대 한 Azure 자동으로 hello VM tooa 정상 상태의 호스트로 마이그레이션되고 hello VM을 다시 시작 합니다.

독립 실행형 VM에 대 한 (VM hello 가용성 집합의 일부가 아닌 의미), Azure에 게 알리는 hello 구독의 서비스 관리자 전자 메일을 통해 계획 된 유지 관리 하기 전에 최소한 한 주 Vm hello hello 업데이트 하는 동안 다시 시작 될 수 있으므로 합니다. Hello Vm에서 실행 중인 응용 프로그램에 가동 중지 시간이 발생할 수 있습니다.

사용할 수도 있습니다 hello Azure 클래식 포털 또는 Azure PowerShell tooview hello 다시 부팅 로그가 tooplanned 유지 관리 인해 발생 한 hello 다시 부팅 합니다. 자세한 내용은 [VM 다시 부팅 로그 보기](https://azure.microsoft.com/blog/2015/04/01/viewing-vm-reboot-logs/)를 참조하세요.

tooprovide 중복 두 put 또는 더 비슷하게 hello에 Vm을 구성 된 동일한 가용성 집합입니다. 이렇게 하면 계획된 또는 계획되지 않은 유지 관리를 하는 동안 적어도 하나 이상의 VM을 사용할 수 있습니다. Azure는 이 구성에 대해 특정한 수준의 VM 가용성을 보장합니다. 자세한 내용은 참조 [관리 가상 컴퓨터의 가용성을 hello](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

## <a name="additional-resources"></a>추가 리소스
[Azure Virtual Machines 정보](../articles/virtual-machines/virtual-machines-linux-about.md)

[만들고 있는 Linux Vm 관리 hello Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Azure PowerShell을 사용하여 Windows VM 만들기 및 관리](../articles/virtual-machines/windows/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

