

## <a name="multi-and-single-instance-vms"></a>다중 및 단일 인스턴스 VM
실행 수를 Azure에 Vm 인해 toohello 가동 중지 시간-계획 된 유지 관리를 진행 하는 경우 예약할 수 중요 한 많은 고객 약 15 분-하는 동안 발생 유지 관리 합니다. 프로 비전 된 Vm에서 받을 계획 된 유지 관리 하는 경우 가용성 집합 toohelp 컨트롤을 사용할 수 있습니다.

Azure에서 실행되는 VM에 대한 두 가지 구성이 가능합니다. VM은 다중 인스턴스 또는 단일 인스턴스로 구성됩니다. VM이 가용성 집합에 있으면 해당 VM은 다중 인스턴스로 구성된 것입니다. 단일 VM도 가용성 집합에 배포할 수 있으며 다중 인스턴스로 취급됩니다. VM이 가용성 집합에 없으면 해당 VM은 단일 인스턴스로 구성된 것입니다.  가용성 집합에 대 한 자세한 내용은 참조 하십시오. [Windows 가상 컴퓨터의 가용성 관리 hello](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 또는 [Linux 가상 컴퓨터의 가용성 관리 hello](../articles/virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

Toosingle 인스턴스를 업데이트 하는 계획 된 유지 관리 하 고 다중 인스턴스 Vm을 개별적으로 발생 합니다. (있는 경우 다중 인스턴스)에 Vm toobe 단일 인스턴스를 다시 구성 하거나 toobe 다중 인스턴스 (단일 인스턴스 경우) 하 여 Vm hello 계획 된 유지 관리를 수신 하는 시기를 제어할 수 있습니다. Azure VM의 계획된 유지 관리에 대한 자세한 내용은 [Azure Linux 가상 컴퓨터에 대한 계획된 유지 관리](../articles/virtual-machines/linux/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [Windows Azure 가상 컴퓨터에 대한 계획된 유지 관리](../articles/virtual-machines/windows/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.

## <a name="for-multi-instance-configuration"></a>다중 인스턴스 구성의 경우
계획 된 유지 관리에는 가용성 집합에서 이러한 Vm을 제거 하 여 가용성 집합 구성에 배포 되는 Vm에 영향을 줍니다. hello 시간을 선택할 수 있습니다.

1. 전자 메일 7 일 전에 hello 계획 다중 인스턴스 구성에서 유지 관리 tooyour Vm tooyou를 전송 됩니다. 구독 Id를 hello 및 영향을 받는 hello 다중 인스턴스 Vm의 이름이 hello hello 전자 메일 본문에 포함 됩니다.
2. 이러한 7 일 동안 때 선택할 수 있습니다 hello 인스턴스는 가용성 집합에서 해당 지역에서 다중 인스턴스 Vm을 제거 하 여 업데이트 됩니다. 이 이렇게 구성 하면 다시 부팅 하면 가상 컴퓨터 hello로 이동 하며 하나의 물리적 호스트에서 유지 관리, 유지 관리에 대 한 대상 지정 되지 않았습니다 tooanother 실제 호스트에 대 한 대상 합니다.
3. Hello Azure 포털에서에서 설정 가능 여부에서 hello VM을 제거할 수 있습니다.

   1. Hello 포털에서 VM tooremove hello hello 가용성 집합에서 선택 합니다.  

   2. **설정** 아래에서 **가용성 집합**을 클릭합니다.

      ![가용성 집합 선택](./media/virtual-machines-planned-maintenance-schedule/availabilitysetselection.png)

   3. Hello 가용성 집합에 드롭다운 메뉴에서 "의 일부가 아닌 가용성 집합입니다."를 선택 합니다.

      ![집합에서 제거](./media/virtual-machines-planned-maintenance-schedule/availabilitysetwarning.png)

   4. Hello 위쪽 클릭 **저장**합니다. 클릭 **예** tooacknowledge이이 작업을 다시 시작 하는 hello VM입니다.

   >[!TIP]
   >나열 된 hello 가용성 집합 중 하나를 선택 하 여 hello VM toomulti 인스턴스를 나중에 구성할 수 있습니다.

4. 가용성 집합에서 제거 하는 Vm 이동된 tooSingle 인스턴스는 호스트가 및 hello 계획 된 유지 관리 tooAvailability 구성을 설정 하는 동안 업데이트 되지 않습니다.
5. Hello 업데이트 tooAvailability Vm 설정 완료 되 면 (tooschedule hello 원래 메일에서 설명에 따라)을 추가할지를 묻는 hello Vm의 가용성 집합에 다시 합니다. 가용성 집합의 멤버가 되 면 다중 인스턴스로 hello Vm을 다시 구성 하 고 다시 부팅을 유발 합니다. 일반적으로 hello 전체 Azure 환경에서 모든 다중 인스턴스 업데이트는 완료 되 면 단일 인스턴스 유지 관리를 따릅니다.

Azure PowerShell을 사용하여 가용성 집합에서 VM을 제거할 수도 있습니다.

```
Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Remove-AzureAvailabilitySet | Update-AzureVM
```

## <a name="for-single-instance-configuration"></a>단일 인스턴스 구성의 경우
계획 된 유지 관리에 영향을 줍니다 하면 Vm 단일 인스턴스 구성에서 이러한 Vm을 가용성 집합에 추가 하 여 hello 시간을 선택할 수 있습니다.

단계별 과정

1. 전자 메일 7 일 전에 hello 계획 단일 인스턴스 구성에서 유지 관리 tooVMs tooyou를 전송 됩니다. 구독 Id를 hello 및 hello 영향을 받는 단일 인스턴스 Vm의 이름이 hello hello 전자 메일 본문에 포함 됩니다.
2. 이러한 7 일 동안 때 선택할 수 있습니다 hello 인스턴스는 동일한 지역에 다시 부팅 하 여 단일 인스턴스 Vm tooan 가용성을 추가 하 여 설정 합니다. 이 이렇게 구성 하면 다시 부팅 하면 가상 컴퓨터 hello로 이동 하며 하나의 물리적 호스트에서 유지 관리, 유지 관리에 대 한 대상 지정 되지 않았습니다 tooanother 실제 호스트에 대 한 대상 합니다.
3. 지침에 따라 여기 tooadd hello Azure 포털 및 Azure PowerShell을 사용 하 여 가용성 집합에 Vm을 기존 합니다. (참조 hello Azure PowerShell 샘플은 다음이 단계입니다.)
4. 이러한 Vm은 다중 인스턴스로 다시 구성 됩니다, 되 면 hello 계획 된 유지 관리에서 제외 tooSingle 인스턴스 Vm입니다.
5. Hello 단일 인스턴스 VM 업데이트가 완료 되 면 (tooschedule hello 원래 메일에 따라) 반환할 수 있습니다 hello Vm toosingle 인스턴스 hello Vm을 가용성 집합에서 제거 하 여 합니다.

추가 VM tooan 가용성 집합도 액세스가 가능 Azure PowerShell을 사용 하 여:

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

<!--Anchors-->



<!--Link references-->
[Virtual Machines Manage Availability]: virtual-machines-windows-tutorial.md
[Understand planned versus unplanned maintenance]: virtual-machines-manage-availability.md#Understand-planned-versus-unplanned-maintenance/
