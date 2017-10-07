---
title: "aaaCreate Python을 사용 하 여 Azure에 Windows VM을 관리 하 고 | Microsoft Docs"
description: "Toouse Python toocreate 알아보고 Azure에서 Windows VM을 관리 합니다."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: davidmu
ms.openlocfilehash: c5553e4e7361e6b9a7183cd935be382f967160cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a>Python을 사용하여 Azure에서 Windows VM 만들기 및 관리

[Azure VM(Virtual Machine)](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에 몇 가지 지원 Azure 리소스가 필요합니다. 이 문서에서는 Python을 사용하여 VM 리소스 만들기, 관리 및 삭제에 대해 설명합니다. 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Visual Studio 프로젝트 만들기
> * 패키지 설치
> * 자격 증명 만들기
> * 리소스 만들기
> * 관리 작업 수행
> * 리소스 삭제
> * Hello 응용 프로그램 실행

다음이 단계 toodo 약 20 분이 필요합니다.

## <a name="create-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기

1. [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio)를 아직 설치하지 않았으면 설치합니다. 선택 **Python 개발** 작업 페이지 hello 되 고 클릭 **설치**합니다. Hello 요약을 볼 수 있습니다는 **Python 3 64 비트 (3.6.0)** 가 자동으로 선택 됩니다. Visual Studio를 이미 설치한 경우 Visual Studio 시작 관리자 hello를 사용 하 여 hello Python 작업을 추가할 수 있습니다.
2. Visual Studio를 설치하고 시작한 후 **파일** > **신규** > **프로젝트**를 클릭합니다.
3. 클릭 **템플릿** > **Python** > **Python 응용 프로그램**, 입력 *myPythonProject* hello 이름에 대 한 hello 프로젝트의 hello 프로젝트의 hello 위치를 선택 하 고 클릭 **확인**합니다.

## <a name="install-packages"></a>패키지 설치

1. 솔루션 탐색기에서 *myPythonProject* 아래에 있는 **Python 환경**을 마우스 오른쪽 단추로 클릭한 다음, **가상 환경 추가**를 선택합니다.
2. Hello 가상 환경 추가 화면에서의 hello 기본 이름을 적용 *env*, 다음 사항을 확인 *Python 3.6 (64 비트)* hello 기본 인터프리터를 선택한 다음 클릭 **만들기**.
3. 마우스 오른쪽 단추로 클릭 hello *env* 만든 환경 클릭 **Python 패키지 설치**, 입력 *azure* 검색 상자 hello와 다음 Enter 키를 누릅니다.

Azure hello 패키지가 성공적으로 설치 된 hello 출력 창에 표시 됩니다. 

## <a name="create-credentials"></a>자격 증명 만들기

이 단계를 시작하기 전에 [Active Directory 서비스 주체](../../azure-resource-manager/resource-group-create-service-principal-portal.md)가 있는지 확인합니다. 이후 단계에서 또한 hello 응용 프로그램 ID, 인증 키 hello 및 필요한 hello 테 넌 트 ID을 기록해 야 합니다.

1. 열기 *myPythonProject.py* 생성 된 파일을 다음 응용 프로그램 toorun 코드 tooenable이를 추가 합니다.

    ```python
    if __name__ == "__main__":
    ```

2. 필요한 tooimport hello 코드 hello.py 파일의 이러한 문을 toohello 맨 위에 추가 합니다.

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. 다음의 hello.py 파일 추가 변수에 toospecify 공통 값을 사용 하는 hello import 문의 hello 코드:
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    **subscription-id**를 구독 ID로 바꿉니다.

4. toocreate hello Active Directory 자격 증명 toomake 요청 해야 하는 hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    대체 **응용 프로그램 id**, **인증 키**, 및 **테 넌 트 id** Azure Active Directory를 만들 때 이전에 수집 하는 hello 값으로 서비스 보안 주체입니다.

5. hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a>리소스 만들기
 
### <a name="initialize-management-clients"></a>관리 클라이언트 초기화

관리 클라이언트는 필요한 toocreate 하 고 Azure의 hello Python SDK를 사용 하 여 리소스를 관리 합니다. toocreate hello 관리 클라이언트 hello 아래이 코드를 추가 **경우** hello.py 파일 끝 다음에 문:

```python
resource_group_client = ResourceManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
network_client = NetworkManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
compute_client = ComputeManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
```

### <a name="create-hello-vm-and-supporting-resources"></a>Hello VM을 만들고 리소스를 지원 합니다.

모든 리소스는 [리소스 그룹](../../azure-resource-manager/resource-group-overview.md)에 포함되어야 합니다.

1. 리소스 그룹 toocreate hello.py 파일의 hello 변수가 뒤이 함수를 추가 합니다.

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

[가용성 집합](tutorial-availability-sets.md) 쉽게 드립니다 toomaintain hello 가상 컴퓨터 응용 프로그램에서 사용 합니다.

1. toocreate 가용성 설정 hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.
   
    ```python
    def create_availability_set(compute_client):
        avset_params = {
            'location': LOCATION,
            'sku': { 'name': 'Aligned' },
            'platform_fault_domain_count': 3
        }
        availability_set_result = compute_client.availability_sets.create_or_update(
            GROUP_NAME,
            'myAVSet',
            avset_params
        )
    ```

2. hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

A [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) hello 가상 컴퓨터와 필요한 toocommunicate 됩니다.

1. toocreate hello 가상 컴퓨터에 대 한 공용 IP 주소를 hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.

    ```python
    def create_public_ip_address(network_client):
        public_ip_addess_params = {
            'location': LOCATION,
            'public_ip_allocation_method': 'Dynamic'
        }
        creation_result = network_client.public_ip_addresses.create_or_update(
            GROUP_NAME,
            'myIPAddress',
            public_ip_addess_params
        )

        return creation_result.result()
    ```

2. hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

가상 컴퓨터는 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)의 서브넷에 있어야 합니다.

1. toocreate 가상 네트워크를 hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.

    ```python
    def create_vnet(network_client):
        vnet_params = {
            'location': LOCATION,
            'address_space': {
                'address_prefixes': ['10.0.0.0/16']
            }
        }
        creation_result = network_client.virtual_networks.create_or_update(
            GROUP_NAME,
            'myVNet',
            vnet_params
        )
        return creation_result.result()
    ```

2. hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. tooadd 서브넷 toohello 가상 네트워크를 hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.
    
    ```python
    def create_subnet(network_client):
        subnet_params = {
            'address_prefix': '10.0.0.0/24'
        }
        creation_result = network_client.subnets.create_or_update(
            GROUP_NAME,
            'myVNet',
            'mySubnet',
            subnet_params
        )

        return creation_result.result()
    ```
        
4. hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

가상 컴퓨터에는 hello 가상 네트워크에서 네트워크 인터페이스 toocommunicate가 필요 합니다.

1. 네트워크 인터페이스 toocreate hello.py 파일에 있는 hello 변수 뒤이 함수를 추가 합니다.

    ```python
    def create_nic(network_client):
        subnet_info = network_client.subnets.get(
            GROUP_NAME, 
            'myVNet', 
            'mySubnet'
        )
        publicIPAddress = network_client.public_ip_addresses.get(
            GROUP_NAME,
            'myIPAddress'
        )
        nic_params = {
            'location': LOCATION,
            'ip_configurations': [{
                'name': 'myIPConfig',
                'public_ip_address': publicIPAddress,
                'subnet': {
                    'id': subnet_info.id
                }
            }]
        }
        creation_result = network_client.network_interfaces.create_or_update(
            GROUP_NAME,
            'myNic',
            nic_params
        )

        return creation_result.result()
    ```

2. hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

리소스를 지 원하는 모든 hello, 만든 가상 컴퓨터를 만들 수 있습니다.

1. toocreate hello 가상 컴퓨터, hello.py 파일에 있는 hello 변수 뒤에이 함수를 추가 합니다.
   
    ```python
    def create_vm(network_client, compute_client):  
        nic = network_client.network_interfaces.get(
            GROUP_NAME, 
            'myNic'
        )
        avset = compute_client.availability_sets.get(
            GROUP_NAME,
            'myAVSet'
        )
        vm_parameters = {
            'location': LOCATION,
            'os_profile': {
                'computer_name': VM_NAME,
                'admin_username': 'azureuser',
                'admin_password': 'Azure12345678'
            },
            'hardware_profile': {
                'vm_size': 'Standard_DS1'
            },
            'storage_profile': {
                'image_reference': {
                    'publisher': 'MicrosoftWindowsServer',
                    'offer': 'WindowsServer',
                    'sku': '2012-R2-Datacenter',
                    'version': 'latest'
                }
            },
            'network_profile': {
                'network_interfaces': [{
                    'id': nic.id
                }]
            },
            'availability_set': {
                'id': avset.id
            }
        }
        creation_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm_parameters
        )
    
        return creation_result.result()
    ```

    > [!NOTE]
    > 이 자습서는 hello Windows Server 운영 체제의 버전을 실행 하는 가상 컴퓨터를 만듭니다. 다른 이미지 선택에 대 한 더 toolearn 참조 [탐색 하 고 Windows PowerShell 및 Azure CLI hello를 사용 하 여 Azure 가상 컴퓨터 이미지 선택](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
    > 
    > 

2. hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a>관리 작업 수행

가상 컴퓨터의 hello 수명 주기 동안 시작, 중지, 또는 가상 컴퓨터를 삭제 하는 등의 toorun 관리 작업을 할 수 있습니다. 또한 toocreate 코드 tooautomate 반복적 복잡 한 작업을 지정할 수 있습니다.

### <a name="get-information-about-hello-vm"></a>Hello VM에 대 한 정보 가져오기

1. hello 가상 컴퓨터에 대 한 정보 tooget hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.

    ```python
    def get_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME, expand='instanceView')
        print("hardwareProfile")
        print("   vmSize: ", vm.hardware_profile.vm_size)
        print("\nstorageProfile")
        print("  imageReference")
        print("    publisher: ", vm.storage_profile.image_reference.publisher)
        print("    offer: ", vm.storage_profile.image_reference.offer)
        print("    sku: ", vm.storage_profile.image_reference.sku)
        print("    version: ", vm.storage_profile.image_reference.version)
        print("  osDisk")
        print("    osType: ", vm.storage_profile.os_disk.os_type.value)
        print("    name: ", vm.storage_profile.os_disk.name)
        print("    createOption: ", vm.storage_profile.os_disk.create_option.value)
        print("    caching: ", vm.storage_profile.os_disk.caching.value)
        print("\nosProfile")
        print("  computerName: ", vm.os_profile.computer_name)
        print("  adminUsername: ", vm.os_profile.admin_username)
        print("  provisionVMAgent: {0}".format(vm.os_profile.windows_configuration.provision_vm_agent))
        print("  enableAutomaticUpdates: {0}".format(vm.os_profile.windows_configuration.enable_automatic_updates))
        print("\nnetworkProfile")
        for nic in vm.network_profile.network_interfaces:
            print("  networkInterface id: ", nic.id)
        print("\nvmAgent")
        print("  vmAgentVersion", vm.instance_view.vm_agent.vm_agent_version)
        print("    statuses")
        for stat in vm_result.instance_view.vm_agent.statuses:
            print("    code: ", stat.code)
            print("    displayStatus: ", stat.display_status)
            print("    message: ", stat.message)
            print("    time: ", stat.time)
        print("\ndisks");
        for disk in vm.instance_view.disks:
            print("  name: ", disk.name)
            print("  statuses")
            for stat in disk.statuses:
                print("    code: ", stat.code)
                print("    displayStatus: ", stat.display_status)
                print("    time: ", stat.time)
        print("\nVM general status")
        print("  provisioningStatus: ", vm.provisioning_state)
        print("  id: ", vm.id)
        print("  name: ", vm.name)
        print("  type: ", vm.type)
        print("  location: ", vm.location)
        print("\nVM instance status")
        for stat in vm.instance_view.statuses:
            print("  code: ", stat.code)
            print("  displayStatus: ", stat.display_status)
    ```
2. hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a>Hello VM 중지

가상 컴퓨터를 중지 하 고 해당 설정을 모두 그대로 유지 하지만 계속 toobe 유료로 제공, 가상 컴퓨터를 중지 하 고 할당을 취소 하거나 수 있습니다. 가상 컴퓨터를 할당을 해제하면 연결된 모든 리소스의 할당이 취소되고 대금 청구가 끝납니다.

1. toostop hello 가상 컴퓨터를 할당 취소 하지 않고 hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    Toodeallocate hello 가상 컴퓨터를 하려면 hello power_off 통화 toothis 코드를 변경 합니다.

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a>Hello VM 시작

1. toostart hello 가상 컴퓨터, hello.py 파일에 있는 hello 변수 뒤에이 함수를 추가 합니다.

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a>Hello VM의 크기를 조정합니다

가상 컴퓨터의 크기를 결정할 때 배포의 여러 측면을 고려해야 합니다. 자세한 내용은 [VM 크기](sizes.md)를 참조하세요.

1. hello.py 파일의 hello 변수가 한 후이 함수를 추가 하는 hello 가상 컴퓨터의 toochange hello 크기:

    ```python
    def update_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        vm.hardware_profile.vm_size = 'Standard_DS3'
        update_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm
        )

    return update_result.result()
    ```

2. hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a>데이터 디스크 toohello VM 추가

가상 컴퓨터에도 VHD로 저장되는 [데이터 디스크](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)가 하나 이상 있을 수 있습니다.

1. 데이터 디스크 toohello 가상 컴퓨터를 tooadd hello.py 파일에 있는 hello 변수 뒤이 함수를 추가 합니다. 

    ```python
    def add_datadisk(compute_client):
        disk_creation = compute_client.disks.create_or_update(
            GROUP_NAME,
            'myDataDisk1',
            {
                'location': LOCATION,
                'disk_size_gb': 1,
                'creation_data': {
                    'create_option': DiskCreateOption.empty
                }
            }
        )
        data_disk = disk_creation.result()
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        add_result = vm.storage_profile.data_disks.append({
            'lun': 1,
            'name': 'myDataDisk1',
            'create_option': DiskCreateOption.attach,
            'managed_disk': {
                'id': data_disk.id
            }
        })
        add_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME,
            VM_NAME,
            vm)

        return add_result.result()
    ```

2. hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a>리소스 삭제

Azure에서 사용 되는 리소스에 대 한 요금이 청구 되므로 항상 것은 더 이상 필요 없는 것이 좋습니다 toodelete 리소스입니다. Toodelete hello 가상 컴퓨터 및 리소스를 지 원하는 모든 hello, 모든 있는 toodo hello 리소스 그룹 삭제 됩니다.

1. toodelete hello 리소스 그룹 및 모든 리소스를 hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:
   
    ```python
    delete_resources(resource_group_client)
    ```

3. *myPythonProject.py*를 저장합니다.

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행

1. toorun hello 콘솔 응용 프로그램을 클릭 하 여 **시작** Visual Studio에서.

2. 키를 눌러 **Enter** 후 각 리소스의 hello 상태가 반환 됩니다. Hello 상태 정보에 표시 됩니다는 **Succeeded** 의 프로비저닝 상태입니다. Hello 가상 컴퓨터를 만든 후 만든 모든 hello 리소스 hello 기회 toodelete 수 있습니다. 누르기 전에 **Enter** toostart 삭제 리소스를 가져올 수 있었습니다 몇 분 tooverify 생성 hello Azure 포털의에서. Azure 포털 열기 hello 있는, 경우에 toorefresh hello 블레이드 toosee 새 리소스를 할 수 있습니다.  

    이 콘솔 응용 프로그램 toorun 시작 toofinish에서 완전히에 대 일 분 정도 취해야 합니다. 모든 hello 리소스 하기 전에 hello 응용 프로그램 완료 되었으며 hello 리소스 그룹이 삭제 된 후 몇 분 정도 걸릴 수 있습니다.


## <a name="next-steps"></a>다음 단계

- 다음 단계에서 toolook 것 hello 배포 문제가 있는 경우 [Azure 포털을 사용 하는 리소스 그룹 배포 문제 해결](../../resource-manager-troubleshoot-deployments-portal.md)
- Hello에 대 한 자세한 [Azure Python 라이브러리](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)

