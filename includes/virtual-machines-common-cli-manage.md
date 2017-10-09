hello Azure CLI 2.0 toocreate 있으며 macOS, Linux 및 Windows에서 Azure 리소스를 관리 합니다. 이 문서는 가장 일반적인 명령 toocreate hello 중 일부에 대해 자세히 설명 하 고 가상 컴퓨터 (Vm)를 관리 합니다.

이 문서는 hello Azure CLI 버전 2.0.4 필요 이상. 실행 `az --version` toofind hello 버전입니다. Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치](/cli/azure/install-azure-cli)합니다. 또한 브라우저에서 [Cloud Shell](/azure/cloud-shell/quickstart)을 사용할 수도 있습니다.

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Azure CLI의 기본 Azure Resource Manager 명령
Hello 온라인 명령 도움말 및 옵션을 입력 하 여 사용할 수 특정 명령줄 스위치 및 옵션에 대 한 도움 자세한 `az <command> <subcommand> --help`합니다.

### <a name="create-vms"></a>VM 만들기
| 작업 | Azure CLI 명령 |
| --- | --- |
| 리소스 그룹 만들기 | `az group create --name myResourceGroup --location eastus` |
| Linux VM 만들기 | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| Windows VM 만들기 | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a>VM 상태 관리
| 작업 | Azure CLI 명령 |
| --- | --- |
| VM 시작 | `az vm start --resource-group myResourceGroup --name myVM` |
| VM 중지 | `az vm stop --resource-group myResourceGroup --name myVM` |
| VM 할당 취소 | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| VM 다시 시작 | `az vm restart --resource-group myResourceGroup --name myVM` |
| VM 재배포 | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| VM 삭제 | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a>VM 정보 가져오기
| 작업 | Azure CLI 명령 |
| --- | --- |
| VM 나열 | `az vm list` |
| VM 관련 정보 가져오기 | `az vm show --resource-group myResourceGroup --name myVM` |
| VM 리소스 사용 | `az vm list-usage --location eastus` |
| 모든 사용 가능한 VM 크기 가져오기 | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a>디스크 및 이미지
| 작업 | Azure CLI 명령 |
| --- | --- |
| 데이터 디스크 tooa VM 추가 | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| VM에서 데이터 디스크 제거 | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| 디스크 크기 조정 | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| 디스크 스냅숏 | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| VM 이미지 만들기 | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| 이미지에서 VM 만들기 | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a>다음 단계
Hello CLI 명령의 추가 예 참조 hello [만들기 및 Azure CLI hello로 Linux Vm 관리](../articles/virtual-machines/linux/tutorial-manage-vm.md) 자습서입니다.

