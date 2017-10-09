


가용성 집합을 사용하면 유지 관리 중과 같은 가동 중지 시간 동안에도 가상 컴퓨터를 계속 사용할 수 있습니다. 가용성 집합에 두 개 이상의 비슷하게 구성 된 가상 컴퓨터를 배치 hello 필요한 중복 toomaintain 가용성을 가상 컴퓨터에서 실행 하는 hello 응용 프로그램이 나 서비스를 만듭니다. 이 과정에 대 한 세부 정보를 참조 하십시오. [관리 가상 컴퓨터의 가용성을 hello][Manage hello availability of virtual machines]합니다.

모범 사례 toouse는 가용성 집합 및 부하 분산 끝점 toohelp 모두 응용 프로그램을 항상 사용 가능 하 고 실행 중인 효율적으로 확인 합니다. 부하가 분산된 끝점에 대한 자세한 내용은 [Azure 인프라 서비스를 위한 부하 분산][Load balancing for Azure infrastructure services]을 참조하세요.

다음 두 옵션 중 하나를 사용하여 클래식 가상 컴퓨터를 가용성 집합에 추가할 수 있습니다.

* [옵션 1: 가상 컴퓨터를 만들고 가용성 동일 하 게 설정 hello에 시간][Option 1: Create a virtual machine and an availability set at hello same time]합니다. 그런 다음 이러한 가상 컴퓨터를 만들 때 설정 하는 새 가상 컴퓨터 toohello를 추가 합니다.
* [옵션 2: 기존 가상 컴퓨터 tooan 가용성 집합을 추가 하][Option 2: Add an existing virtual machine tooan availability set]합니다.

> [!NOTE]
> Hello 클래식 모델에 tooput 하려는 가상 컴퓨터 hello 동일한 가용성 집합 toohello 속해야 합니다. 동일한 클라우드 서비스입니다.
> 
> 

## <a id="createset"></a>옵션 1: 가상 컴퓨터를 만들고 가용성 동일 하 게 설정 hello에 시간
하거나 Azure PowerShell 명령 toodo이 등 어느 hello Azure 포털을 사용할 수 있습니다.

toouse hello Azure 포털:

1. 그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 클릭 **+ 새로 만들기**, 클릭 하 고 **가상 컴퓨터**합니다.
   
    ![대체 이미지 텍스트](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. 원하는 toouse hello 마켓플레이스 가상 컴퓨터 이미지를 선택 합니다. Toocreate Linux 또는 Windows 가상 컴퓨터를 선택할 수 있습니다.
4. 가상 컴퓨터를 선택 하는 hello에 대 한 해당 hello 배포 모델 너무 설정 되었는지 확인**클래식** 클릭 하 고 **만들기**
   
    ![대체 이미지 텍스트](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. 가상 컴퓨터 이름, 사용자 이름 및 암호(Window 컴퓨터) 또는 SSH 공개 키(Linux 컴퓨터)를 입력합니다. 
6. Hello v M 크기를 선택 하 고 클릭 한 다음 **선택** toocontinue 합니다.
7. 선택 **선택적 구성 > 가용성 집합**, hello 가용성 세트 tooadd hello 가상 컴퓨터를 선택 합니다.
   
    ![대체 이미지 텍스트](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. 구성 설정을 검토합니다. 완료하면 **만들기**를 클릭합니다.
9. Azure 가상 컴퓨터를 만드는 동안에 아래 hello 진행률을 추적할 수 **가상 컴퓨터** hello 허브 메뉴에서 합니다.

Azure PowerShell toouse toocreate Azure 가상 컴퓨터 명령 및 tooa 기존 또는 새 가용성 집합을 추가, 참조 [Azure PowerShell을 사용 하 여 toocreate 및 Windows 기반 가상 컴퓨터를 미리 구성](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a id="addmachine"></a>옵션 2: 기존 가상 컴퓨터 tooan 가용성 집합을 추가 합니다.
Hello Azure 포털에서에서 기존 클래식 가상 컴퓨터 tooan 기존 가용성 집합을 추가 하거나을 새로 만들 수 있습니다. (가상 컴퓨터에 hello hello 동일한 가용성 집합을 유의 toohello 속해야 합니다. 동일한 클라우드 서비스입니다.) hello 단계는 거의 같은 hello 됩니다. Azure PowerShell을 사용 하 여 hello 가상 컴퓨터 tooan 기존 가용성 집합을 추가할 수 있습니다.

1. 아직 수행 경우 toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 클릭 **가상 컴퓨터 (클래식)**합니다.
   
    ![대체 이미지 텍스트](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. 가상 컴퓨터의 hello 목록에서 원하는 tooadd toohello 집합 hello 가상 컴퓨터의 hello 이름을 선택 합니다.
4. 선택 **가용성 집합** hello 가상 컴퓨터에서 **설정을**합니다.
   
    ![대체 이미지 텍스트](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. Hello 가용성 세트 tooadd hello 가상 컴퓨터를 선택 합니다. 가상 컴퓨터 hello toohello 속해야 hello 가용성 집합으로 동일한 클라우드 서비스입니다.
   
    ![대체 이미지 텍스트](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. **Save**를 클릭합니다.

toouse Azure PowerShell 명령을 관리자 권한 Azure PowerShell 세션을 열고 다음 명령을 hello를 실행 합니다. Hello 자리 표시자에 대 한 (예: &lt;VmCloudServiceName&gt;), 교체를 hello < 및 > 문자를 포함 하 여 hello 따옴표 안의 hello로 이름을 수정 합니다.

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> hello 가상 컴퓨터를 다시 시작 toobe toofinish toohello 가용성 집합을 추가 있을 수 있습니다.
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

