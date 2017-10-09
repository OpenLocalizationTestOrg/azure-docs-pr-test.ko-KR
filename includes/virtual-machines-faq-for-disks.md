# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="2f1ac-101">Azure IaaS VM 디스크와 관리 및 관리되지 않는 프리미엄 디스크에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="2f1ac-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="2f1ac-102">이 문서에서는 Azure Managed Disks 및 Azure Premium Storage에 대해 몇몇 자주 묻는 질문과 대답을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="2f1ac-103">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="2f1ac-103">Managed Disks</span></span>

<span data-ttu-id="2f1ac-104">**Azure Managed Disks란?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="2f1ac-105">Managed Disks는 저장소 계정 관리를 처리하여 Azure IaaS VM을 위한 디스크 관리를 간소화하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="2f1ac-106">자세한 내용은 참조 hello [관리 하는 디스크 개요](../articles/virtual-machines/windows/managed-disks-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-106">For more information, see hello [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="2f1ac-107">**80GB인 기존 VHD에서 표준 Managed Disk를 만들 경우 비용은 얼마나 드나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="2f1ac-108">80 GB VHD에서 만든 표준 관리 디스크는 S10 디스크 hello 다음 사용 가능한 표준 디스크 크기로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-108">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="2f1ac-109">에 따라 toohello S10 디스크 가격으로 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-109">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="2f1ac-110">자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-110">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="2f1ac-111">**표준 관리 디스크에 대한 트랜잭션 비용이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="2f1ac-112">예.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-112">Yes.</span></span> <span data-ttu-id="2f1ac-113">각 트랜잭션에 대해 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-113">You're charged for each transaction.</span></span> <span data-ttu-id="2f1ac-114">자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-114">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="2f1ac-115">**표준 관리 디스크에 대 한 됩니다 수수료를 지불 합니까 hello 디스크의 사용자를 프로 비전 하는 hello 용량 또는 hello hello hello 디스크 데이터의 실제 크기에 대 한?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-115">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="2f1ac-116">Hello 디스크의 hello 프로 비전 된 용량에 따라 요금이 부과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-116">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="2f1ac-117">자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-117">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="2f1ac-118">**프리미엄 Managed Disks의 가격은 관리되지 않는 디스크와 어떻게 다르게 책정되나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="2f1ac-119">관리 되지 않는 프리미엄 디스크와 동일 hello hello 관리 프리미엄 디스크의 가격입니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-119">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="2f1ac-120">**Hello 저장소 계정 유형 (Standard 또는 Premium) 내 관리 되는 디스크의 변경할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-120">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="2f1ac-121">예.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-121">Yes.</span></span> <span data-ttu-id="2f1ac-122">관리 되는 디스크의 저장소 계정 유형은 hello hello Azure 포털, PowerShell 또는 Azure CLI hello를 사용 하 여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-122">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="2f1ac-123">**방법이 있습니까는를 복사 하거나 관리 되는 디스크 tooa 개인 저장소 계정 내보낼 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-123">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="2f1ac-124">예.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-124">Yes.</span></span> <span data-ttu-id="2f1ac-125">Hello Azure 포털, PowerShell 또는 Azure CLI hello를 사용 하 여 관리 되는 디스크를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-125">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="2f1ac-126">**다른 구독으로 Azure 저장소 계정 toocreate 관리 되는 디스크에에서 VHD 파일을 사용할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-126">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="2f1ac-127">아니요.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-127">No.</span></span>

<span data-ttu-id="2f1ac-128">**다른 지역에 Azure 저장소 계정 toocreate 관리 되는 디스크에에서 VHD 파일을 사용할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="2f1ac-129">아니요.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-129">No.</span></span>

<span data-ttu-id="2f1ac-130">**고객이 Managed Disks를 사용하는 경우 규모 제한이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="2f1ac-131">관리 되는 디스크 저장소 계정과 연관 된 hello 제한을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-131">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="2f1ac-132">그러나 hello 수의 구독에 대해 관리 되는 디스크는 제한 too2, 기본적으로 000입니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-132">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="2f1ac-133">이 숫자 지원 tooincrease를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-133">You can call support tooincrease this number.</span></span>

<span data-ttu-id="2f1ac-134">**관리 디스크의 증분 스냅숏을 가져올 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="2f1ac-135">아니요.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-135">No.</span></span> <span data-ttu-id="2f1ac-136">hello 현재 스냅숏 기능이 관리 되는 디스크의 전체 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-136">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="2f1ac-137">그러나 toosupport 증분 스냅숏 hello 향후에 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-137">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="2f1ac-138">**관리 및 관리되지 않는 디스크를 조합하여 가용성 집합의 VM을 구성할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="2f1ac-139">아니요.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-139">No.</span></span> <span data-ttu-id="2f1ac-140">가용성 집합에 Vm hello 모든 관리 되는 디스크 또는 모든 관리 되지 않는 디스크 중 하나를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-140">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="2f1ac-141">디스크의 종류를 선택할 수는 가용성 집합을 만들 때 원하는 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-141">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="2f1ac-142">**Hello Azure 포털에서에서 관리 하는 디스크 hello 기본 옵션이입니다.**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-142">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="2f1ac-143">현재는 향후 hello에 hello 기본 사이트용으로 하지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-143">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="2f1ac-144">**내가 빈 관리 디스크를 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="2f1ac-145">예.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-145">Yes.</span></span> <span data-ttu-id="2f1ac-146">사용자가 빈 디스크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-146">You can create an empty disk.</span></span> <span data-ttu-id="2f1ac-147">관리 되는 디스크를 만들 수 있습니다는 VM을 독립적으로 예를 들어 tooa VM을 연결 하지 않고도.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-147">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="2f1ac-148">**관리 하는 디스크를 사용 하는 가용성 집합에 대 한 지원 hello 장애 도메인 수 란?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-148">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="2f1ac-149">관리 하는 디스크를 사용 하는 hello 가용성 집합 위치한 hello 지역에 따라 지원 hello 장애 도메인 수는 2 또는 3입니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-149">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="2f1ac-150">**진단 설정에 대 한 표준 저장소 계정이 hello는 어떻게 합니까?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-150">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="2f1ac-151">VM 진단을 위한 개인 저장소 계정을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="2f1ac-152">Hello 이후, tooswitch 진단 계획 tooManaged 디스크는 물론 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-152">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="2f1ac-153">**어떤 종류의 역할 기반 액세스 제어 지원을 Managed Disks에 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="2f1ac-154">Managed Disks에서는 세 가지 주요 기본 역할을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="2f1ac-155">소유자: 액세스를 포함한 모든 것을 관리할 수 있음</span><span class="sxs-lookup"><span data-stu-id="2f1ac-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="2f1ac-156">참여자: 액세스를 제외한 모든 것을 관리할 수 있음</span><span class="sxs-lookup"><span data-stu-id="2f1ac-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="2f1ac-157">읽기 권한자: 모든 항목을 볼 수 있지만 변경할 수 없음</span><span class="sxs-lookup"><span data-stu-id="2f1ac-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="2f1ac-158">**방법이 있습니까는를 복사 하거나 관리 되는 디스크 tooa 개인 저장소 계정 내보낼 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-158">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="2f1ac-159">읽기 전용 공유 액세스 서명을 사용 하 여 관리 하는 hello에 대 한 URI 디스크 toocopy hello 내용을 tooa 개인 저장소 계정 또는 온-프레미스 저장소를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-159">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="2f1ac-160">**내 관리 디스크의 복사본을 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="2f1ac-161">고객 수는 관리 되는 디스크의 스냅숏을 만들고 hello 스냅숏 toocreate 다른 관리 되는 디스크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-161">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="2f1ac-162">**관리되지 않는 디스크도 계속 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="2f1ac-163">예.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-163">Yes.</span></span> <span data-ttu-id="2f1ac-164">관리되지 않는 디스크 및 Managed Disks가 모두 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="2f1ac-165">새 워크 로드에 대 한 관리 되는 디스크를 사용 하 고 현재 작업 toomanaged 디스크를 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-165">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="2f1ac-166">**128 50GB 디스크를 만들고 다음 hello 크기 too130 GB를 늘려, 됩니다 수수료를 지불 합니까 hello 다음 디스크 크기 (512GB)에 대 한?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-166">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="2f1ac-167">예.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-167">Yes.</span></span>

<span data-ttu-id="2f1ac-168">**로컬 중복 저장소, 지역 중복 저장소 및 영역 중복 저장소 Managed Disks를 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="2f1ac-169">Azure Managed Disks에서는 현재 로컬 중복 저장소 Managed Disks만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="2f1ac-170">**Managed Disks를 축소하거나 크기를 줄일 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="2f1ac-171">아니요.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-171">No.</span></span> <span data-ttu-id="2f1ac-172">이 기능은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="2f1ac-173">**사용 되는 tooprovision VM을는 운영 체제 디스크는 특수화 된 (hello 시스템 준비 도구를 사용 하 여 생성 또는 범용으로 설정) 하는 경우 hello 컴퓨터 이름 속성 변경 합니까?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-173">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="2f1ac-174">아니요.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-174">No.</span></span> <span data-ttu-id="2f1ac-175">Hello 컴퓨터 이름 속성을 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-175">You can't update hello computer name property.</span></span> <span data-ttu-id="2f1ac-176">hello 새 VM 상속 hello 부모가 사용 되는 toocreate hello 운영 체제 디스크는 VM에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-176">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="2f1ac-177">**관리 되는 디스크와 Azure 리소스 관리자 템플릿 toocreate Vm을 샘플은 어디서 찾을 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-177">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="2f1ac-178">Managed Disks를 사용하는 템플릿 목록</span><span class="sxs-lookup"><span data-stu-id="2f1ac-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="2f1ac-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="2f1ac-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="2f1ac-180">Managed Disks 및 Storage 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="2f1ac-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="2f1ac-181">**Managed Disk를 만들 경우 Azure Storage 서비스 암호화를 기본적으로 사용하나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="2f1ac-182">예.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-182">Yes.</span></span>

<span data-ttu-id="2f1ac-183">**Hello 암호화 키를 관리 하는 사람?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-183">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="2f1ac-184">Microsoft은 hello 암호화 키를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-184">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="2f1ac-185">**내 Managed Disks에 Storage 서비스 암호화를 비활성화할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="2f1ac-186">아니요.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-186">No.</span></span>

<span data-ttu-id="2f1ac-187">**Storage 서비스 암호화는 특정 지역에서만 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="2f1ac-188">아니요.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-188">No.</span></span> <span data-ttu-id="2f1ac-189">것은 관리 하는 디스크를 사용할 수 있는 모든 hello 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-189">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="2f1ac-190">모든 공용 지역 및 독일에서 Managed Disks를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="2f1ac-191">**내 Managed Disk가 암호화되었는지 어떻게 확인할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="2f1ac-192">Hello 시간 hello Azure 포털, Azure CLI hello 및 PowerShell에서 관리 되는 디스크를 만들 때 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-192">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="2f1ac-193">Hello 시간은 2017 년 6 월 9 후 디스크에 암호화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-193">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="2f1ac-194">**2017년 6월 10일 이전에 만들어진 내 기존 디스크를 어떻게 암호화할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="2f1ac-195">2017 년 6 월 10부터 tooexisting 관리 되는 디스크에 기록 하는 새 데이터 자동으로 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-195">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="2f1ac-196">기존 데이터 용량의 tooencrypt 예정도 및 hello 암호화 hello 백그라운드에서 비동기적으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-196">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="2f1ac-197">이제 기존 데이터를 암호화해야 하는 경우 디스크의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="2f1ac-198">새 디스크가 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="2f1ac-199">Hello Azure CLI를 사용 하 여 관리 하는 디스크 복사</span><span class="sxs-lookup"><span data-stu-id="2f1ac-199">Copy managed disks by using hello Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="2f1ac-200">PowerShell을 사용하여 Managed Disks 복사</span><span class="sxs-lookup"><span data-stu-id="2f1ac-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="2f1ac-201">**관리되는 스냅숏 및 이미지가 암호화되나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="2f1ac-202">예.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-202">Yes.</span></span> <span data-ttu-id="2f1ac-203">2017년 6월 9일 이후에 만든 모든 관리되는 스냅숏 및 이미지는 자동으로 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="2f1ac-204">**추가 되거나 이전에 암호화 된 toomanaged 디스크인 저장소 계정에 있는 관리 되지 않는 디스크가 있는 Vm을 변환할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="2f1ac-205">예</span><span class="sxs-lookup"><span data-stu-id="2f1ac-205">Yes</span></span>

<span data-ttu-id="2f1ac-206">**Managed Disk 또는 스냅숏에서 내보낸 VHD도 암호화되나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="2f1ac-207">아니요.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-207">No.</span></span> <span data-ttu-id="2f1ac-208">VHD tooan 내보낼 경우 수는 스냅숏, 또는 암호화 된 관리 되는 디스크에서 저장소 계정 암호화 한 다음 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-208">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="2f1ac-209">프리미엄 디스크: 관리 및 관리되지 않는 디스크</span><span class="sxs-lookup"><span data-stu-id="2f1ac-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="2f1ac-210">**VM에서 DSv2와 같이 Premium Storage를 지원하는 크기를 사용하는 경우 프리미엄 및 표준 데이터 디스크를 모두 연결할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="2f1ac-211">예.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-211">Yes.</span></span>

<span data-ttu-id="2f1ac-212">**Premium 및 D, Dv2, G 또는 F 계열과 같이 프리미엄 저장소를 지원 하지 않는 표준 데이터 디스크 tooa 크기 계열 둘 다에 연결할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-212">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="2f1ac-213">아니요.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-213">No.</span></span> <span data-ttu-id="2f1ac-214">만 표준 데이터 디스크 tooVMs 지 프리미엄 저장소를 원하는 크기 시리즈를 사용 하지 않는 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-214">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="2f1ac-215">**80GB인 기존 VHD로 프리미엄 데이터 디스크를 만들 경우 비용은 얼마가 드나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="2f1ac-216">프리미엄 데이터 디스크를 80 GB VHD에서 만든 P10 디스크 hello 다음 사용 가능한 프리미엄 디스크 크기로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-216">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="2f1ac-217">에 따라 toohello P10 디스크 가격으로 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-217">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="2f1ac-218">**프리미엄 저장소 트랜잭션 비용 toouse 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-218">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="2f1ac-219">특정 한도의 IOPS 및 처리량이 프로비전되는 디스크 크기마다 고정 비용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="2f1ac-220">hello 기타 비용은 아웃 바운드 대역폭 및 스냅숏 용량을 해당 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-220">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="2f1ac-221">자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-221">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="2f1ac-222">**I hello 디스크 캐시에서 얻을 수 있는 처리량 및 IOPS에 대 한 hello 제한 사항은 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-222">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="2f1ac-223">캐시에 대 한 결합 된 제한을 hello 및 DS 시리즈에 대 한 로컬 SSD는 4, 000 IOPS 코어 수 및 코어당 초당 33MB 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-223">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="2f1ac-224">hello GS 시리즈 코어당 5,000 IOPS 및 초당 코어당 라이선스 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-224">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="2f1ac-225">**로컬 SSD 디스크 관리 되는 VM에 대해 지원 되는 hello?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-225">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="2f1ac-226">hello 로컬 SSD는 임시 저장소 디스크 관리 되는 VM에 포함 되어 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-226">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="2f1ac-227">이 임시 저장소에 대한 추가 비용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="2f1ac-228">사용 하지 않는 로컬 SSD toostore이 응용 프로그램 데이터 Azure Blob 저장소에 지속 되지 않으므로 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-228">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="2f1ac-229">**모든 영향 hello에 대 한 사용 TRIM의 프리미엄 디스크에?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-229">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="2f1ac-230">사용 되지 않지만 단점은 toohello TRIM Azure 디스크를 프리미엄 또는 표준 디스크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-230">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="2f1ac-231">새 디스크 크기: 관리 및 관리되지 않는 디스크</span><span class="sxs-lookup"><span data-stu-id="2f1ac-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="2f1ac-232">**Hello 운영 체제 및 데이터 디스크에 대해 지원 되는 가장 큰 디스크 크기는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-232">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="2f1ac-233">운영 체제 디스크에 대 한 Azure 지원 hello 파티션 유형은 hello 마스터 부트 레코드 (MBR)입니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-233">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="2f1ac-234">hello MBR 형식은 too2 TB 디스크 크기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-234">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="2f1ac-235">운영 체제 디스크에 대 한 Azure 지원 있는 hello 최대 크기는 2TB입니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-235">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="2f1ac-236">Azure는 데이터 디스크에 대 한 too4 TB를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-236">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="2f1ac-237">**Hello 가장 큰 페이지 blob 크기 지원 되는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-237">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="2f1ac-238">hello 가장 큰 페이지 blob 크기는 Azure 지원은 8TB (8,191 GB)입니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-238">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="2f1ac-239">데이터 또는 운영 체제 디스크 4TB (4, 095mb GB) 연결 된 tooa VM 보다 큰 페이지 blob 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-239">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="2f1ac-240">**필요한 toouse 새 버전의 Azure tools toocreate 연결, 크기 조정 및 1TB 보다 큰 디스크를 업로드?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-240">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="2f1ac-241">기존 Azure tools toocreate 프로그램 tooupgrade 필요 하지 않습니다, 연결, 또는 1TB 보다 큰 디스크의 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-241">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="2f1ac-242">파일을 VHD tooupload 온-프레미스 직접 tooAzure 페이지 blob 또는 관리 되지 않는 디스크, toouse hello 최신 도구 집합을 필요:</span><span class="sxs-lookup"><span data-stu-id="2f1ac-242">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="2f1ac-243">Azure 도구</span><span class="sxs-lookup"><span data-stu-id="2f1ac-243">Azure tools</span></span>      | <span data-ttu-id="2f1ac-244">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="2f1ac-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="2f1ac-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f1ac-245">Azure PowerShell</span></span> | <span data-ttu-id="2f1ac-246">버전 번호 4.1.0: 2017년 6월 릴리스 이상</span><span class="sxs-lookup"><span data-stu-id="2f1ac-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="2f1ac-247">Azure CLI v1</span><span class="sxs-lookup"><span data-stu-id="2f1ac-247">Azure CLI v1</span></span>     | <span data-ttu-id="2f1ac-248">버전 번호 0.10.13: 2017년 5월 릴리스 이상</span><span class="sxs-lookup"><span data-stu-id="2f1ac-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="2f1ac-249">AzCopy</span><span class="sxs-lookup"><span data-stu-id="2f1ac-249">AzCopy</span></span>           | <span data-ttu-id="2f1ac-250">버전 번호 6.1.0: 2017년 6월 릴리스 이상</span><span class="sxs-lookup"><span data-stu-id="2f1ac-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="2f1ac-251">Azure CLI v2 및 Azure 저장소 탐색기에 대 한 hello 지원이 곧 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-251">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="2f1ac-252">**P4 및 P6 디스크 크기가 관리되지 않는 디스크 또는 페이지 Blob에 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="2f1ac-253">아니요.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-253">No.</span></span> <span data-ttu-id="2f1ac-254">P4(32GB) 및 P6(64GB) 디스크 크기는 Managed Disks에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="2f1ac-255">관리되지 않는 디스크 및 페이지 Blob에도 곧 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="2f1ac-256">**관리 되는 기존 내 프리미엄 디스크 64GB hello 작은 디스크 (주위 2017 년 6 월 15) 사용 하기 전에 만들어진 보다 작은 경우 어떻게 것 청구?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-256">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="2f1ac-257">64 GB 보다 작은 기존 작은 프리미엄 디스크에 따라 요금이 청구 toobe toohello P10 가격 책정 계층을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-257">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="2f1ac-258">**P10 tooP4 또는 P6에서 64GB 미만인 작은 프리미엄 디스크의 디스크 계층 hello를 전환 하려면 어떻게 해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="2f1ac-258">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="2f1ac-259">작은 디스크의 스냅숏을 하 고 가격 계층 tooP4는 디스크 tooautomatically 스위치 hello를 만들 수 있습니다 또는 사용자를 프로 비전 하는 hello 크기에 따라 P6 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-259">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="2f1ac-260">여기서 내 질문에 대답하지 않으면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="2f1ac-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="2f1ac-261">질문하려는 내용이 아래 목록에 나와 있지 않으면 알려 주세요. 대답을 확인하는 방법을 알려 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="2f1ac-262">Hello 주석에서이 문서의 끝 hello에 질문을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-262">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="2f1ac-263">tooengage hello Azure 저장소 팀 및 다른 커뮤니티 구성원 들이 문서에 대 한 MSDN hello를 사용 하 여 [Azure 저장소 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-263">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="2f1ac-264">toorequest 기능 요청 및 아이디어 toohello 제출 [Azure 저장소 피드백 포럼](https://feedback.azure.com/forums/217298-storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ac-264">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
