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
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a><span data-ttu-id="d91c2-103">Python을 사용하여 Azure에서 Windows VM 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="d91c2-103">Create and manage Windows VMs in Azure using Python</span></span>

<span data-ttu-id="d91c2-104">[Azure VM(Virtual Machine)](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에 몇 가지 지원 Azure 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="d91c2-105">이 문서에서는 Python을 사용하여 VM 리소스 만들기, 관리 및 삭제에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-105">This article covers creating, managing, and deleting VM resources using Python.</span></span> <span data-ttu-id="d91c2-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d91c2-107">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="d91c2-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="d91c2-108">패키지 설치</span><span class="sxs-lookup"><span data-stu-id="d91c2-108">Install packages</span></span>
> * <span data-ttu-id="d91c2-109">자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="d91c2-109">Create credentials</span></span>
> * <span data-ttu-id="d91c2-110">리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="d91c2-110">Create resources</span></span>
> * <span data-ttu-id="d91c2-111">관리 작업 수행</span><span class="sxs-lookup"><span data-stu-id="d91c2-111">Perform management tasks</span></span>
> * <span data-ttu-id="d91c2-112">리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="d91c2-112">Delete resources</span></span>
> * <span data-ttu-id="d91c2-113">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d91c2-113">Run hello application</span></span>

<span data-ttu-id="d91c2-114">다음이 단계 toodo 약 20 분이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="d91c2-115">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="d91c2-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="d91c2-116">[Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio)를 아직 설치하지 않았으면 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="d91c2-117">선택 **Python 개발** 작업 페이지 hello 되 고 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-117">Select **Python development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="d91c2-118">Hello 요약을 볼 수 있습니다는 **Python 3 64 비트 (3.6.0)** 가 자동으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-118">In hello summary, you can see that **Python 3 64-bit (3.6.0)** is automatically selected for you.</span></span> <span data-ttu-id="d91c2-119">Visual Studio를 이미 설치한 경우 Visual Studio 시작 관리자 hello를 사용 하 여 hello Python 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-119">If you have already installed Visual Studio, you can add hello Python workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="d91c2-120">Visual Studio를 설치하고 시작한 후 **파일** > **신규** > **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-120">After installing and starting Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="d91c2-121">클릭 **템플릿** > **Python** > **Python 응용 프로그램**, 입력 *myPythonProject* hello 이름에 대 한 hello 프로젝트의 hello 프로젝트의 hello 위치를 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-121">Click **Templates** > **Python** > **Python Application**, enter *myPythonProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-packages"></a><span data-ttu-id="d91c2-122">패키지 설치</span><span class="sxs-lookup"><span data-stu-id="d91c2-122">Install packages</span></span>

1. <span data-ttu-id="d91c2-123">솔루션 탐색기에서 *myPythonProject* 아래에 있는 **Python 환경**을 마우스 오른쪽 단추로 클릭한 다음, **가상 환경 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-123">In Solution Explorer, under *myPythonProject*, right-click **Python Environments**, and then select **Add virtual environment**.</span></span>
2. <span data-ttu-id="d91c2-124">Hello 가상 환경 추가 화면에서의 hello 기본 이름을 적용 *env*, 다음 사항을 확인 *Python 3.6 (64 비트)* hello 기본 인터프리터를 선택한 다음 클릭 **만들기**.</span><span class="sxs-lookup"><span data-stu-id="d91c2-124">On hello Add Virtual Environment screen, accept hello default name of *env*, make sure that *Python 3.6 (64-bit)* is selected for hello base interpreter, and then click **Create**.</span></span>
3. <span data-ttu-id="d91c2-125">마우스 오른쪽 단추로 클릭 hello *env* 만든 환경 클릭 **Python 패키지 설치**, 입력 *azure* 검색 상자 hello와 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-125">Right-click hello *env* environment that you created, click **Install Python Package**, enter *azure* in hello search box, and then press Enter.</span></span>

<span data-ttu-id="d91c2-126">Azure hello 패키지가 성공적으로 설치 된 hello 출력 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-126">You should see in hello output windows that hello azure packages were successfully installed.</span></span> 

## <a name="create-credentials"></a><span data-ttu-id="d91c2-127">자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="d91c2-127">Create credentials</span></span>

<span data-ttu-id="d91c2-128">이 단계를 시작하기 전에 [Active Directory 서비스 주체](../../azure-resource-manager/resource-group-create-service-principal-portal.md)가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-128">Before you start this step, make sure that you have an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="d91c2-129">이후 단계에서 또한 hello 응용 프로그램 ID, 인증 키 hello 및 필요한 hello 테 넌 트 ID을 기록해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

1. <span data-ttu-id="d91c2-130">열기 *myPythonProject.py* 생성 된 파일을 다음 응용 프로그램 toorun 코드 tooenable이를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-130">Open *myPythonProject.py* file that was created, and then add this code tooenable your application toorun:</span></span>

    ```python
    if __name__ == "__main__":
    ```

2. <span data-ttu-id="d91c2-131">필요한 tooimport hello 코드 hello.py 파일의 이러한 문을 toohello 맨 위에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-131">tooimport hello code that is needed, add these statements toohello top of hello .py file:</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. <span data-ttu-id="d91c2-132">다음의 hello.py 파일 추가 변수에 toospecify 공통 값을 사용 하는 hello import 문의 hello 코드:</span><span class="sxs-lookup"><span data-stu-id="d91c2-132">Next in hello .py file, add variables after hello import statements toospecify common values used in hello code:</span></span>
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    <span data-ttu-id="d91c2-133">**subscription-id**를 구독 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-133">Replace **subscription-id** with your subscription identifier.</span></span>

4. <span data-ttu-id="d91c2-134">toocreate hello Active Directory 자격 증명 toomake 요청 해야 하는 hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-134">toocreate hello Active Directory credentials that you need toomake requests, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    <span data-ttu-id="d91c2-135">대체 **응용 프로그램 id**, **인증 키**, 및 **테 넌 트 id** Azure Active Directory를 만들 때 이전에 수집 하는 hello 값으로 서비스 보안 주체입니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-135">Replace **application-id**, **authentication-key**, and **tenant-id** with hello values that you previously collected when you created your Azure Active Directory service principal.</span></span>

5. <span data-ttu-id="d91c2-136">hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:</span><span class="sxs-lookup"><span data-stu-id="d91c2-136">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a><span data-ttu-id="d91c2-137">리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="d91c2-137">Create resources</span></span>
 
### <a name="initialize-management-clients"></a><span data-ttu-id="d91c2-138">관리 클라이언트 초기화</span><span class="sxs-lookup"><span data-stu-id="d91c2-138">Initialize management clients</span></span>

<span data-ttu-id="d91c2-139">관리 클라이언트는 필요한 toocreate 하 고 Azure의 hello Python SDK를 사용 하 여 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-139">Management clients are needed toocreate and manage resources using hello Python SDK in Azure.</span></span> <span data-ttu-id="d91c2-140">toocreate hello 관리 클라이언트 hello 아래이 코드를 추가 **경우** hello.py 파일 끝 다음에 문:</span><span class="sxs-lookup"><span data-stu-id="d91c2-140">toocreate hello management clients, add this code under hello **if** statement at then end of hello .py file:</span></span>

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

### <a name="create-hello-vm-and-supporting-resources"></a><span data-ttu-id="d91c2-141">Hello VM을 만들고 리소스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-141">Create hello VM and supporting resources</span></span>

<span data-ttu-id="d91c2-142">모든 리소스는 [리소스 그룹](../../azure-resource-manager/resource-group-overview.md)에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-142">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="d91c2-143">리소스 그룹 toocreate hello.py 파일의 hello 변수가 뒤이 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-143">toocreate a resource group, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. <span data-ttu-id="d91c2-144">hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:</span><span class="sxs-lookup"><span data-stu-id="d91c2-144">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

<span data-ttu-id="d91c2-145">[가용성 집합](tutorial-availability-sets.md) 쉽게 드립니다 toomaintain hello 가상 컴퓨터 응용 프로그램에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-145">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

1. <span data-ttu-id="d91c2-146">toocreate 가용성 설정 hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-146">toocreate an availability set, add this function after hello variables in hello .py file:</span></span>
   
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

2. <span data-ttu-id="d91c2-147">hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:</span><span class="sxs-lookup"><span data-stu-id="d91c2-147">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

<span data-ttu-id="d91c2-148">A [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) hello 가상 컴퓨터와 필요한 toocommunicate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-148">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

1. <span data-ttu-id="d91c2-149">toocreate hello 가상 컴퓨터에 대 한 공용 IP 주소를 hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-149">toocreate a public IP address for hello virtual machine, add this function after hello variables in hello .py file:</span></span>

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

2. <span data-ttu-id="d91c2-150">hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:</span><span class="sxs-lookup"><span data-stu-id="d91c2-150">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="d91c2-151">가상 컴퓨터는 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)의 서브넷에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-151">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="d91c2-152">toocreate 가상 네트워크를 hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-152">toocreate a virtual network, add this function after hello variables in hello .py file:</span></span>

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

2. <span data-ttu-id="d91c2-153">hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:</span><span class="sxs-lookup"><span data-stu-id="d91c2-153">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. <span data-ttu-id="d91c2-154">tooadd 서브넷 toohello 가상 네트워크를 hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-154">tooadd a subnet toohello virtual network, add this function after hello variables in hello .py file:</span></span>
    
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
        
4. <span data-ttu-id="d91c2-155">hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:</span><span class="sxs-lookup"><span data-stu-id="d91c2-155">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="d91c2-156">가상 컴퓨터에는 hello 가상 네트워크에서 네트워크 인터페이스 toocommunicate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-156">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

1. <span data-ttu-id="d91c2-157">네트워크 인터페이스 toocreate hello.py 파일에 있는 hello 변수 뒤이 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-157">toocreate a network interface, add this function after hello variables in hello .py file:</span></span>

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

2. <span data-ttu-id="d91c2-158">hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:</span><span class="sxs-lookup"><span data-stu-id="d91c2-158">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="d91c2-159">리소스를 지 원하는 모든 hello, 만든 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-159">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="d91c2-160">toocreate hello 가상 컴퓨터, hello.py 파일에 있는 hello 변수 뒤에이 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-160">toocreate hello virtual machine, add this function after hello variables in hello .py file:</span></span>
   
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
    > <span data-ttu-id="d91c2-161">이 자습서는 hello Windows Server 운영 체제의 버전을 실행 하는 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-161">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="d91c2-162">다른 이미지 선택에 대 한 더 toolearn 참조 [탐색 하 고 Windows PowerShell 및 Azure CLI hello를 사용 하 여 Azure 가상 컴퓨터 이미지 선택](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-162">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

2. <span data-ttu-id="d91c2-163">hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:</span><span class="sxs-lookup"><span data-stu-id="d91c2-163">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a><span data-ttu-id="d91c2-164">관리 작업 수행</span><span class="sxs-lookup"><span data-stu-id="d91c2-164">Perform management tasks</span></span>

<span data-ttu-id="d91c2-165">가상 컴퓨터의 hello 수명 주기 동안 시작, 중지, 또는 가상 컴퓨터를 삭제 하는 등의 toorun 관리 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-165">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="d91c2-166">또한 toocreate 코드 tooautomate 반복적 복잡 한 작업을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-166">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="d91c2-167">Hello VM에 대 한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="d91c2-167">Get information about hello VM</span></span>

1. <span data-ttu-id="d91c2-168">hello 가상 컴퓨터에 대 한 정보 tooget hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-168">tooget information about hello virtual machine, add this function after hello variables in hello .py file:</span></span>

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
2. <span data-ttu-id="d91c2-169">hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:</span><span class="sxs-lookup"><span data-stu-id="d91c2-169">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a><span data-ttu-id="d91c2-170">Hello VM 중지</span><span class="sxs-lookup"><span data-stu-id="d91c2-170">Stop hello VM</span></span>

<span data-ttu-id="d91c2-171">가상 컴퓨터를 중지 하 고 해당 설정을 모두 그대로 유지 하지만 계속 toobe 유료로 제공, 가상 컴퓨터를 중지 하 고 할당을 취소 하거나 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-171">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="d91c2-172">가상 컴퓨터를 할당을 해제하면 연결된 모든 리소스의 할당이 취소되고 대금 청구가 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-172">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="d91c2-173">toostop hello 가상 컴퓨터를 할당 취소 하지 않고 hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-173">toostop hello virtual machine without deallocating it, add this function after hello variables in hello .py file:</span></span>

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    <span data-ttu-id="d91c2-174">Toodeallocate hello 가상 컴퓨터를 하려면 hello power_off 통화 toothis 코드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-174">If you want toodeallocate hello virtual machine, change hello power_off call toothis code:</span></span>

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="d91c2-175">hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:</span><span class="sxs-lookup"><span data-stu-id="d91c2-175">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a><span data-ttu-id="d91c2-176">Hello VM 시작</span><span class="sxs-lookup"><span data-stu-id="d91c2-176">Start hello VM</span></span>

1. <span data-ttu-id="d91c2-177">toostart hello 가상 컴퓨터, hello.py 파일에 있는 hello 변수 뒤에이 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-177">toostart hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="d91c2-178">hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:</span><span class="sxs-lookup"><span data-stu-id="d91c2-178">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a><span data-ttu-id="d91c2-179">Hello VM의 크기를 조정합니다</span><span class="sxs-lookup"><span data-stu-id="d91c2-179">Resize hello VM</span></span>

<span data-ttu-id="d91c2-180">가상 컴퓨터의 크기를 결정할 때 배포의 여러 측면을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-180">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="d91c2-181">자세한 내용은 [VM 크기](sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d91c2-181">For more information, see [VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="d91c2-182">hello.py 파일의 hello 변수가 한 후이 함수를 추가 하는 hello 가상 컴퓨터의 toochange hello 크기:</span><span class="sxs-lookup"><span data-stu-id="d91c2-182">toochange hello size of hello virtual machine, add this function after hello variables in hello .py file:</span></span>

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

2. <span data-ttu-id="d91c2-183">hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:</span><span class="sxs-lookup"><span data-stu-id="d91c2-183">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="d91c2-184">데이터 디스크 toohello VM 추가</span><span class="sxs-lookup"><span data-stu-id="d91c2-184">Add a data disk toohello VM</span></span>

<span data-ttu-id="d91c2-185">가상 컴퓨터에도 VHD로 저장되는 [데이터 디스크](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)가 하나 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-185">Virtual machines can have one or more [data disks](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) that are stored as VHDs.</span></span>

1. <span data-ttu-id="d91c2-186">데이터 디스크 toohello 가상 컴퓨터를 tooadd hello.py 파일에 있는 hello 변수 뒤이 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-186">tooadd a data disk toohello virtual machine, add this function after hello variables in hello .py file:</span></span> 

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

2. <span data-ttu-id="d91c2-187">hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:</span><span class="sxs-lookup"><span data-stu-id="d91c2-187">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a><span data-ttu-id="d91c2-188">리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="d91c2-188">Delete resources</span></span>

<span data-ttu-id="d91c2-189">Azure에서 사용 되는 리소스에 대 한 요금이 청구 되므로 항상 것은 더 이상 필요 없는 것이 좋습니다 toodelete 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-189">Because you are charged for resources used in Azure, it's always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="d91c2-190">Toodelete hello 가상 컴퓨터 및 리소스를 지 원하는 모든 hello, 모든 있는 toodo hello 리소스 그룹 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-190">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="d91c2-191">toodelete hello 리소스 그룹 및 모든 리소스를 hello.py 파일의 hello 변수가 후이 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-191">toodelete hello resource group and all resources, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. <span data-ttu-id="d91c2-192">hello에서이 코드를 추가 하는 이전에 추가한 toocall hello 함수 **경우** hello hello.py 파일 끝에 문의:</span><span class="sxs-lookup"><span data-stu-id="d91c2-192">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    delete_resources(resource_group_client)
    ```

3. <span data-ttu-id="d91c2-193">*myPythonProject.py*를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-193">Save *myPythonProject.py*.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="d91c2-194">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d91c2-194">Run hello application</span></span>

1. <span data-ttu-id="d91c2-195">toorun hello 콘솔 응용 프로그램을 클릭 하 여 **시작** Visual Studio에서.</span><span class="sxs-lookup"><span data-stu-id="d91c2-195">toorun hello console application, click **Start** in Visual Studio.</span></span>

2. <span data-ttu-id="d91c2-196">키를 눌러 **Enter** 후 각 리소스의 hello 상태가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-196">Press **Enter** after hello status of each resource is returned.</span></span> <span data-ttu-id="d91c2-197">Hello 상태 정보에 표시 됩니다는 **Succeeded** 의 프로비저닝 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-197">In hello status information, you should see a **Succeeded** provisioning state.</span></span> <span data-ttu-id="d91c2-198">Hello 가상 컴퓨터를 만든 후 만든 모든 hello 리소스 hello 기회 toodelete 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-198">After hello virtual machine is created, you have hello opportunity toodelete all hello resources that you create.</span></span> <span data-ttu-id="d91c2-199">누르기 전에 **Enter** toostart 삭제 리소스를 가져올 수 있었습니다 몇 분 tooverify 생성 hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="d91c2-199">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify their creation in hello Azure portal.</span></span> <span data-ttu-id="d91c2-200">Azure 포털 열기 hello 있는, 경우에 toorefresh hello 블레이드 toosee 새 리소스를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-200">If you have hello Azure portal open, you might have toorefresh hello blade toosee new resources.</span></span>  

    <span data-ttu-id="d91c2-201">이 콘솔 응용 프로그램 toorun 시작 toofinish에서 완전히에 대 일 분 정도 취해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-201">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> <span data-ttu-id="d91c2-202">모든 hello 리소스 하기 전에 hello 응용 프로그램 완료 되었으며 hello 리소스 그룹이 삭제 된 후 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d91c2-202">It may take several minutes after hello application has finished before all hello resources and hello resource group are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d91c2-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d91c2-203">Next steps</span></span>

- <span data-ttu-id="d91c2-204">다음 단계에서 toolook 것 hello 배포 문제가 있는 경우 [Azure 포털을 사용 하는 리소스 그룹 배포 문제 해결](../../resource-manager-troubleshoot-deployments-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d91c2-204">If there were issues with hello deployment, a next step would be toolook at [Troubleshooting resource group deployments with Azure portal](../../resource-manager-troubleshoot-deployments-portal.md)</span></span>
- <span data-ttu-id="d91c2-205">Hello에 대 한 자세한 [Azure Python 라이브러리](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="d91c2-205">Learn more about hello [Azure Python Library](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span></span>

