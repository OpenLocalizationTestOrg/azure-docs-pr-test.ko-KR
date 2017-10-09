

VM 확장은 다음과 같은 작업에 도움이 될 수 있습니다.

* 보안 및 ID 기능 수정(예: 계정 값 재설정 및 맬웨어 방지 프로그램)
* 모니터링 및 진단 시작, 중지 또는 구성
* 연결 기능 재설정 또는 설치(예: RDP 및 SSH)
* VM 진단, 모니터링 및 관리

많은 다른 기능도 있습니다. 새 VM 확장 기능은 정기적으로 릴리스됩니다. 이 문서에서는 hello Azure VM 에이전트에 대 한 Windows 및 Linux 및 VM 확장 기능을 지 원하는 방법을 설명 합니다. 기능 범주별 VM 확장 목록은 [Azure VM 확장 및 기능](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.

## <a name="azure-vm-agents-for-windows-and-linux"></a>Windows 및 Linux 용 Azure VM 에이전트
hello Azure 가상 컴퓨터 에이전트 (VM 에이전트)는 설치, 구성 및 Azure 가상 컴퓨터의 인스턴스에서 VM 확장을 제거 하는 안전 하 고 간단한 프로세스입니다. VM 에이전트 hello Azure VM에 대 한 hello 보안 로컬 제어 서비스 역할을 합니다. hello 확장 hello 에이전트 로드 하는 특정 기능 tooincrease hello 인스턴스를 사용 하 여 생산성을 제공 합니다.

Windows VM용 에이전트와 Linux VM용 에이전트 등, 두 가지 Azure VM 에이전트가 있습니다.

VM 확장을 하나 이상 가상 컴퓨터 인스턴스 toouse 하려는 경우 설치 된 VM 에이전트 hello 인스턴스에 있어야 합니다. Azure 포털 hello 및 hello에서 이미지를 사용 하 여 만든 가상 컴퓨터 이미지 **마켓플레이스** hello 만들기 프로세스에 자동으로 VM 에이전트를 설치 합니다. 가상 컴퓨터 인스턴스에 없는 경우 VM 에이전트, hello 가상 컴퓨터 인스턴스가 만들어진 후 hello VM 에이전트를 설치할 수 있습니다. 또는 다음 업로드 하는 사용자 지정 VM 이미지에 hello 에이전트를 설치할 수 있습니다.

> [!IMPORTANT]
> 이러한 VM 에이전트는 가상 컴퓨터 인스턴스의 보안 관리를 구현하는 매우 가벼운 서비스입니다. 원하지 않는 hello VM 에이전트의 경우 있을 수 있습니다. 이 경우 hello hello Azure CLI 또는 PowerShell을 사용 하 여 설치 하는 VM 에이전트를 갖지 않는 있는지 toocreate Vm 수 있습니다. VM 에이전트 hello을 물리적으로 제거할 수 있지만 hello 인스턴스에서 VM 확장의 hello 동작이 정의 되지 않습니다. 결과적으로, 설치된 VM 에이전트의 제거는 지원되지 않습니다.
>

VM 에이전트 hello hello 다음 상황에서에서 사용 됩니다.

* Azure 포털 hello에서 이미지를 선택 하 고 사용 하 여 VM의 인스턴스를 만들 때 hello **마켓플레이스**,
* Hello를 사용 하 여 VM의 인스턴스를 만들 때 [New-azurevm](https://msdn.microsoft.com/library/azure/dn495254.aspx) 또는 hello [New-azurequickvm](https://msdn.microsoft.com/library/azure/dn495183.aspx) cmdlet. Hello를 추가 하 여 VM 에이전트 없이 VM을 만들 수 **– DisableGuestAgent** 매개 변수 toohello [Add-azureprovisioningconfig](https://msdn.microsoft.com/library/azure/dn495299.aspx) cmdlet

* 수동으로 다운로드 하 고 기존 VM 인스턴스에서 hello VM 에이전트를 설치 해 서 hello 설정 **ProvisionGuestAgent** 너무 값**true**합니다. PowerShell 명령 또는 REST를 호출을 사용하면 Windows 및 Linux 에이전트를 위한 이 명령을 사용할 수 있습니다. (Hello 설정 하지 않으면 **ProvisionGuestAgent** hello VM 에이전트가 제대로 검색 되지 않으면 hello hello 추가 VM 에이전트를 수동으로 설치한 후 값입니다.) 코드 예제에서 보여 주는 방법을 따르는 hello toodo이 여기서 hello PowerShell을 사용 하 여 `$svc` 및 `$name` 인수를 이미 확인:

      $vm = Get-AzureVM –ServiceName $svc –Name $name
      $vm.VM.ProvisionGuestAgent = $TRUE
      Update-AzureVM –Name $name –VM $vm.VM –ServiceName $svc

* 설치된 VM 에이전트를 포함하는 VM 이미지를 만들 때. Hello VM 에이전트를 사용 하 여 hello 이미지 있으면 해당 이미지 tooAzure 업로드할 수 있습니다. Windows VM에 대 한 다운로드 hello [Windows VM 에이전트.msi 파일](http://go.microsoft.com/fwlink/?LinkID=394789) hello VM 에이전트를 설치 합니다. Linux VM에 대 한 hello hello GitHub 리포지토리에서 VM 에이전트에 있는 설치 <https://github.com/Azure/WALinuxAgent>합니다. Tooinstall Linux에서 VM 에이전트를 hello 하는 방법에 대 한 자세한 내용은 참조 hello [Azure Linux VM 에이전트 사용자 가이드](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

> [!NOTE]
> Paas에서는 hello VM 에이전트 라고 **WindowsAzureGuestAgent**를 항상 웹 및 작업자 역할 Vm에서 사용할 수 있습니다. (자세한 내용은 참조 [Azure 역할 아키텍처](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx).) hello 역할 Vm 용 VM 에이전트가 hello에 이제 확장 toohello 클라우드 서비스 Vm을 추가할 수는 영구 가상 컴퓨터에 적용 되는 동일한 방식으로 합니다. Vm 역할 VM 확장과 영구 Vm 간의 가장 큰 차이점 hello 있으면 hello VM 확장 추가 됩니다. Vm 역할을 통해 확장에는 첫 번째 toohello 클라우드 서비스, 해당 클라우드 서비스 내에서 다음 toohello 배포 추가 됩니다.
>
> 사용 하 여 [Get-azureserviceavailableextension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet toolist 가능한 모든 역할 VM 확장 합니다.
>
>

## <a name="find-add-update-and-remove-vm-extensions"></a>VM 확장 찾기, 추가, 업데이트 및 제거
이러한 작업에 대한 자세한 내용은 [Azure VM 확장 추가, 찾기, 업데이트 및 제거](../articles/virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)를 참조하세요.
