

이미지는 Azure tooprovide에 사용 되는 운영 체제와 새 가상 컴퓨터. 이미지에는 데이터 디스크가 하나 이상 있을 수 있습니다. 이미지는 여러 원본에서 사용할 수 있습니다.

* Azure hello에서 이미지를 제공 [마켓플레이스](https://azure.microsoft.com/gallery/virtual-machines/)합니다. 최신 버전의 Windows Server 및 hello Linux 운영 체제의 배포판 있습니다. 일부 이미지에는 SQL Server와 같은 응용 프로그램이 포함되어 있습니다. MSDN 혜택 및 MSDN 종 량 제 구독자 액세스 tooadditional 이미지입니다.
* hello 오픈 소스 커뮤니티는 이미지를 통해 [VM Depot](http://vmdepot.msopentech.com/List/Index)합니다.
* Azure에서 기존 Azure 가상 컴퓨터를 캡처하여 이미지로 사용하거나 이미지를 업로드하여 직접 이미지를 저장하고 사용할 수도 있습니다.

## <a name="about-vm-images-and-os-images"></a>VM 이미지 및 OS 이미지 정보
Azure에서 *VM 이미지* 및 *OS 이미지*의 두 가지 이미지 형식을 사용할 수 있습니다. VM 이미지는 운영 체제를 포함 하 고 hello 이미지를 만들 때 모든 디스크가 tooa 가상 컴퓨터를 연결 합니다. VM 이미지는 이미지의 hello 최신 형식입니다. VM 이미지가 도입되기 전에는 Azure에서 이미지에 일반화된 운영 체제만 포함할 수 있었고 추가 디스크가 없었습니다. 일반화 된 운영 체제만 포함 하는 VM 이미지는 기본적으로 hello hello OS 이미지가 이미지의 원본 형식과 동일 hello 합니다.

Azure의 가상 컴퓨터나 다른 곳에서 실행 중이지만 복사하여 업로드한 가상 컴퓨터를 기반으로 직접 이미지를 만들 수도 있습니다. Tooprepare 하나 이상의 가상 컴퓨터 이미지 toocreate toouse을 원하는 경우 해야 간에 일반화 하 여 이미지 형식으로 사용 하기 위해 합니다. Windows Server 이미지 toocreate 실행된 hello Sysprep 명령을 hello 서버 toogeneralize 것 hello.vhd 파일을 업로드 하기 전에 됩니다. Sysprep에 대 한 세부 정보를 참조 하십시오. [어떻게 tooUse Sysprep: 소개](http://go.microsoft.com/fwlink/p/?LinkId=392030) 및 [서버 역할에 대 한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)합니다. Sysprep를 실행 하기 전에 hello VM 백업 합니다. Linux 이미지를 만드는 작업은 배포판에 따라 다릅니다. 일반적으로 특정 toohello 배포 되 고 hello Azure Linux 에이전트를 실행 하는 명령 집합을 toorun을 해야 합니다.
