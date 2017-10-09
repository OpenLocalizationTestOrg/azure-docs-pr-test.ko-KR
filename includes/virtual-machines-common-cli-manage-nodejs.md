리소스 관리자 명령 및 템플릿 toodeploy Azure 사용 하려면 먼저 hello Azure CLI 리소스 및 리소스 그룹을 사용 하는 작업 azure 계정이 필요 합니다. 계정이 없는 경우 [여기에서 무료 Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 얻을 수 있습니다.

Hello Azure CLI 및 연결 된 tooyour 구독을 이미 설치 참조 [설치 hello Azure CLI](../articles/cli-install-nodejs.md) 너무 hello 모드 설정`arm` 와 `azure config mode arm`, tooAzure hello를 사용 하 여 연결 하 고 `azure login` 명령입니다.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- Azure CLI 10-우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](../articles/virtual-machines/linux/cli-manage.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Azure CLI의 기본 Azure Resource Manager 명령
이 문서에서는 Azure CLI toomanage와 toouse 원하는 이며, Azure 구독에서 리소스 (주로 Vm)와 상호 작용 하는 기본 명령을 설명 합니다.  Hello 온라인 명령 도움말 및 옵션을 입력 하 여 사용할 수 특정 명령줄 스위치 및 옵션에 대 한 도움 자세한 `azure <command> <subcommand> --help` 또는 `azure help <command> <subcommand>`합니다.

> [!NOTE]
> 이러한 예제에는 템플릿 기반 작업이 포함되지 않으며 이 작업은 일반적으로 리소스 관리자의 VM 배포에 사용하는 것이 좋습니다. 정보를 참조 하십시오. [Azure CLI Azure 리소스 관리자와 함께 사용 하 여 hello](../articles/xplat-cli-azure-resource-manager.md) 및 [배포 및 Azure 리소스 관리자 템플릿을 사용 하 여 가상 컴퓨터를 관리 하 고 Azure CLI hello](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
> 
> 

| 작업 | 리소스 관리자 |
| --- | --- | --- |
| 만드는 가장 기본적인 VM hello |`azure vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password>`<br/><br/>(Hello 가져올 `image-urn` hello에서 `azure vm image list` 명령입니다. 예제는 [이 문서](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 를 참조하세요.) |
| Linux VM 만들기 |`azure  vm create [options] <resource-group> <name> <location> -y "Linux"` |
| Windows VM 만들기 |`azure  vm create [options] <resource-group> <name> <location> -y "Windows"` |
| VM 나열 |`azure  vm list [options]` |
| VM에 대한 정보 가져오기 |`azure  vm show [options] <resource_group> <name>` |
| VM 시작 |`azure vm start [options] <resource_group> <name>` |
| VM 중지 |`azure vm stop [options] <resource_group> <name>` |
| VM 할당 취소 |`azure vm deallocate [options] <resource-group> <name>` |
| VM 다시 시작 |`azure vm restart [options] <resource_group> <name>` |
| VM 삭제 |`azure vm delete [options] <resource_group> <name>` |
| VM 캡처 |`azure vm capture [options] <resource_group> <name>` |
| 사용자 이미지에서 VM 만들기 |`azure  vm create [options] –q <image-name> <resource-group> <name> <location> <os-type>` |
| 특수한 디스크에서 VM 만들기 |`azue  vm create [options] –d <os-disk-vhd> <resource-group> <name> <location> <os-type>` |
| 데이터 디스크 tooa VM 추가 |`azure  vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]` |
| VM에서 데이터 디스크 제거 |`azure  vm disk detach [options] <resource-group> <vm-name> <lun>` |
| 제네릭 확장 tooa VM 추가 |`azure  vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>` |
| VM 액세스 확장 tooa VM 추가 |`azure vm reset-access [options] <resource-group> <name>` |
| Docker 확장 tooa VM 추가 |`azure  vm docker create [options] <resource-group> <name> <location> <os-type>` |
| VM 확장 제거 |`azure  vm extension set [options] –u <resource-group> <vm-name> <name> <publisher-name> <version>` |
| VM 리소스 사용 |`azure vm list-usage [options] <location>` |
| 모든 사용 가능한 VM 크기 가져오기 |`azure vm sizes [options]` |

## <a name="next-steps"></a>다음 단계
* 기본 VM 관리 이상인 hello CLI 명령의 추가 예제를 참조 하십시오. [hello를 사용 하 여 Azure 리소스 관리자와 Azure CLI](../articles/virtual-machines/azure-cli-arm-commands.md)합니다.
