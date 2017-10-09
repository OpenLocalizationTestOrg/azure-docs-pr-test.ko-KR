# <a name="common-errors-during-classic-tooazure-resource-manager-migration"></a><span data-ttu-id="4aa2d-101">클래식 tooAzure 리소스 관리자 마이그레이션 동안 일반적인 오류</span><span class="sxs-lookup"><span data-stu-id="4aa2d-101">Common errors during Classic tooAzure Resource Manager migration</span></span>
<span data-ttu-id="4aa2d-102">이 문서 카탈로그 Azure 클래식 배포 모델 toohello Azure 리소스 관리자 스택에서 IaaS 리소스 hello 마이그레이션하는 동안 가장 일반적인 오류 및 완화 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-102">This article catalogs hello most common errors and mitigations during hello migration of IaaS resources from Azure classic deployment model toohello Azure Resource Manager stack.</span></span>

## <a name="list-of-errors"></a><span data-ttu-id="4aa2d-103">오류 목록</span><span class="sxs-lookup"><span data-stu-id="4aa2d-103">List of errors</span></span>
| <span data-ttu-id="4aa2d-104">오류 문자열</span><span class="sxs-lookup"><span data-stu-id="4aa2d-104">Error string</span></span> | <span data-ttu-id="4aa2d-105">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4aa2d-105">Mitigation</span></span> |
| --- | --- |
| <span data-ttu-id="4aa2d-106">내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="4aa2d-106">Internal server error</span></span> |<span data-ttu-id="4aa2d-107">어떤 경우에는 다시 시도하면 사라지는 일시적인 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-107">In some cases, this is a transient error that goes away with a retry.</span></span> <span data-ttu-id="4aa2d-108">Toopersist, 계속 진행 하는 경우 [Azure 지원에 문의](../articles/azure-supportability/how-to-create-azure-support-request.md) 플랫폼 로그에 대 한 확인을 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-108">If it continues toopersist, [contact Azure support](../articles/azure-supportability/how-to-create-azure-support-request.md) as it needs investigation of platform logs.</span></span> <br><br> <span data-ttu-id="4aa2d-109">**참고:** hello 인시던트는 hello 지원 팀에서 추적 되 면 마십시오 된 자체 마이그레이션을이 할 수 있습니다 하는 대로 사용자 환경에서 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-109">**NOTE:** Once hello incident is tracked by hello support team, please do not attempt any self-mitigation as this might have unintended consequences on your environment.</span></span> |
| <span data-ttu-id="4aa2d-110">마이그레이션은 PaaS 배포(웹/작업자)이기 때문에 HostedService {hosted-service-name}에서 배포 {deployment-name}에 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-110">Migration is not supported for Deployment {deployment-name}  in HostedService {hosted-service-name} because it is a PaaS deployment (Web/Worker).</span></span> |<span data-ttu-id="4aa2d-111">배포가 웹/작업자 역할을 포함하는 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-111">This happens when a deployment contains a web/worker role.</span></span> <span data-ttu-id="4aa2d-112">마이그레이션은 가상 컴퓨터에만 지원 하므로 hello 웹/작업자 역할 hello 배포에서 제거 하 고 마이그레이션을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-112">Since migration is only supported for Virtual Machines, please remove hello web/worker role from hello deployment and try migration again.</span></span> |
| <span data-ttu-id="4aa2d-113">템플릿 {template-name} 배포에 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-113">Template {template-name} deployment failed.</span></span> <span data-ttu-id="4aa2d-114">CorrelationId={guid}</span><span class="sxs-lookup"><span data-stu-id="4aa2d-114">CorrelationId={guid}</span></span> |<span data-ttu-id="4aa2d-115">마이그레이션 서비스의 hello 백 엔드에 hello Azure 리소스 관리자 스택에서 Azure 리소스 관리자 템플릿 toocreate 리소스를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-115">In hello backend of migration service, we use Azure Resource Manager templates toocreate resources in hello Azure Resource Manager stack.</span></span> <span data-ttu-id="4aa2d-116">템플릿 idempotent 이므로 일반적으로 안전 하 게 다시 시도할 수 있습니다이 오류가 나타나면 hello 마이그레이션 작업 tooget 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-116">Since templates are idempotent, usually you can safely retry hello migration operation tooget past this error.</span></span> <span data-ttu-id="4aa2d-117">이 오류가 계속 발생 toopersist 경우 [Azure 지원에 문의](../articles/azure-supportability/how-to-create-azure-support-request.md) hello 상관 관계 Id를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-117">If this error continues toopersist, please [contact Azure support](../articles/azure-supportability/how-to-create-azure-support-request.md) and give them hello CorrelationId.</span></span> <br><br> <span data-ttu-id="4aa2d-118">**참고:** hello 인시던트는 hello 지원 팀에서 추적 되 면 마십시오 된 자체 마이그레이션을이 할 수 있습니다 하는 대로 사용자 환경에서 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-118">**NOTE:** Once hello incident is tracked by hello support team, please do not attempt any self-mitigation as this might have unintended consequences on your environment.</span></span> |
| <span data-ttu-id="4aa2d-119">hello 가상 네트워크 {가상 네트워크 이름 간} 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-119">hello virtual network {virtual-network-name} does not exist.</span></span> |<span data-ttu-id="4aa2d-120">이 hello 새 Azure 포털에 hello 가상 네트워크를 만든 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-120">This can happen if you created hello Virtual Network in hello new Azure portal.</span></span> <span data-ttu-id="4aa2d-121">hello 실제 가상 네트워크 이름 hello 패턴을 따르는 "그룹 * <VNET name>"</span><span class="sxs-lookup"><span data-stu-id="4aa2d-121">hello actual Virtual Network name follows hello pattern "Group * <VNET name>"</span></span> |
| <span data-ttu-id="4aa2d-122">HostedService {hosted-service-name}에서 VM {vm-name}에는 Azure Resource Manager에서 지원되지 않는 확장 {extension-name}이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-122">VM {vm-name} in HostedService {hosted-service-name} contains Extension {extension-name} which is not supported in Azure Resource Manager.</span></span> <span data-ttu-id="4aa2d-123">Toouninstall 좋습니다 마이그레이션을 사용 하 여 계속 하기 전에 VM hello 옵니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-123">It is recommended toouninstall it from hello VM before continuing with migration.</span></span> |<span data-ttu-id="4aa2d-124">BGInfo 1.*과 같은 XML 확장은 Azure Resource Manager에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-124">XML extensions such as BGInfo 1.* are not supported in Azure Resource Manager.</span></span> <span data-ttu-id="4aa2d-125">따라서 이러한 확장을 마이그레이션할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-125">Therefore, these extensions cannot be migrated.</span></span> <span data-ttu-id="4aa2d-126">이러한 확장은 가상 컴퓨터에 설치 된 hello 왼쪽된을 하는 경우는 hello 마이그레이션을 완료 하기 전에 자동으로 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-126">If these extensions are left installed on hello virtual machine, they are automatically uninstalled before completing hello migration.</span></span> |
| <span data-ttu-id="4aa2d-127">HostedService {hosted-service-name}에서 VM {vm-name}은 현재 마이그레이션에 지원되지 않는 VMSnapshot/VMSnapshotLinux 확장을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-127">VM {vm-name} in HostedService {hosted-service-name} contains Extension VMSnapshot/VMSnapshotLinux, which is currently not supported for Migration.</span></span> <span data-ttu-id="4aa2d-128">Hello VM에서에서 제거 하 고 hello 마이그레이션이 완료 된 후 Azure 리소스 관리자를 사용 하 여 다시 추가</span><span class="sxs-lookup"><span data-stu-id="4aa2d-128">Uninstall it from hello VM and add it back using Azure Resource Manager after hello Migration is Complete</span></span> |<span data-ttu-id="4aa2d-129">Azure 백업에 대 한 hello 가상 컴퓨터 구성 되어 있는 hello 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-129">This is hello scenario where hello virtual machine is configured for Azure Backup.</span></span> <span data-ttu-id="4aa2d-130">Https://aka.ms/vmbackupmigration에 hello 해결 방법 따라 이므로 현재 지원 되지 않는 시나리오</span><span class="sxs-lookup"><span data-stu-id="4aa2d-130">Since this is currently an unsupported scenario, please follow hello workaround at https://aka.ms/vmbackupmigration</span></span> |
| <span data-ttu-id="4aa2d-131">HostedService {호스팅된 서비스-이름}에서 {vm name} VM 확장 {확장 이름} 상태 hello VM에서에서 보고 되지 않습니다 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-131">VM {vm-name} in HostedService {hosted-service-name} contains Extension {extension-name} whose Status is not being reported from hello VM.</span></span> <span data-ttu-id="4aa2d-132">따라서 이 VM은 마이그레이션할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-132">Hence, this VM cannot be migrated.</span></span> <span data-ttu-id="4aa2d-133">보고 되 고 해당 hello 확장 상태를 확인 하거나 hello 확장 hello VM에서에서 제거한 마이그레이션을 다시 시도 하세요.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-133">Ensure that hello Extension status is being reported or uninstall hello extension from hello VM and retry migration.</span></span> <br><br> <span data-ttu-id="4aa2d-134">HostedService {hosted-service-name}에서 VM {vm-name}에는 확장 {extension-name} 보고 처리기 상태 {handler-status}가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-134">VM {vm-name} in HostedService {hosted-service-name} contains Extension {extension-name} reporting Handler Status: {handler-status}.</span></span> <span data-ttu-id="4aa2d-135">따라서 VM hello 마이그레이션할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-135">Hence, hello VM cannot be migrated.</span></span> <span data-ttu-id="4aa2d-136">Hello 확장 처리기 상태 보고 되 고 {처리기 status} 있는지 확인 하거나 hello VM에서에서 제거 하 고 마이그레이션을 다시 시도 하세요.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-136">Ensure that hello Extension handler status being reported is {handler-status} or uninstall it from hello VM and retry migration.</span></span> <br><br> <span data-ttu-id="4aa2d-137">HostedService {호스팅된 서비스-이름}에서 {vm name} VM 용 VM 에이전트가 보고 하는 hello 전반적인 에이전트 상태를 준비 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-137">VM Agent for VM {vm-name} in HostedService {hosted-service-name} is reporting hello overall agent status as Not Ready.</span></span> <span data-ttu-id="4aa2d-138">따라서 VM hello 마이그레이션할 수 없습니다, 문서가 마이그레이션할 확장명입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-138">Hence, hello VM may not be migrated, if it has a migratable extension.</span></span> <span data-ttu-id="4aa2d-139">VM 에이전트는 hello Ready로 전체 에이전트 상태를 보고 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-139">Ensure that hello VM Agent is reporting overall agent status as Ready.</span></span> <span data-ttu-id="4aa2d-140">Toohttps://aka.ms/classiciaasmigrationfaqs를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-140">Refer toohttps://aka.ms/classiciaasmigrationfaqs.</span></span> |<span data-ttu-id="4aa2d-141">Azure 게스트 에이전트 및 VM 확장의 상태 아웃 바운드 인터넷 액세스 toohello VM 저장소 계정 toopopulate 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-141">Azure guest agent & VM Extensions need outbound internet access toohello VM storage account toopopulate their status.</span></span> <span data-ttu-id="4aa2d-142">상태 실패의 일반적인 원인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-142">Common causes of status failure include</span></span> <li> <span data-ttu-id="4aa2d-143">toohello 아웃 바운드 액세스를 차단 하는 네트워크 보안 그룹 인터넷</span><span class="sxs-lookup"><span data-stu-id="4aa2d-143">a Network Security Group that blocks outbound access toohello internet</span></span> <li> <span data-ttu-id="4aa2d-144">Hello VNET에 온-프레미스 DNS 서버 및 DNS 연결 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-144">If hello VNET has on-prem DNS servers and DNS connectivity is lost</span></span> <br><br> <span data-ttu-id="4aa2d-145">Toosee 지원 되지 않는 상태를 계속 진행 하면이 검사 hello 확장 tooskip를 제거 하 고 마이그레이션을 사용 하 여 앞으로 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-145">If you continue toosee an unsupported status, you can uninstall hello extensions tooskip this check and move forward with migration.</span></span> |
| <span data-ttu-id="4aa2d-146">마이그레이션에는 여러 가용성 집합이 있기 때문에 HostedService {hosted-service-name}에서 배포 {deployment-name}에 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-146">Migration is not supported for Deployment {deployment-name} in HostedService {hosted-service-name} because it has multiple Availability Sets.</span></span> |<span data-ttu-id="4aa2d-147">현재, 1 이하의 가용성 집합을 가진 호스티드 서비스만 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-147">Currently, only hosted services that have 1 or less Availability sets can be migrated.</span></span> <span data-ttu-id="4aa2d-148">이 문제를 해결 toowork 가용성 집합 및 다른 가용성 집합 tooa 해당 가상 컴퓨터 호스 티 드 서비스에 추가 하는 hello를 이동 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-148">toowork around this problem, please move hello additional Availability sets and Virtual machines in those Availability sets tooa different hosted service.</span></span> |
| <span data-ttu-id="4aa2d-149">HostedService의 {배포 이름} 배포에 대 한 마이그레이션이 지원 되지 않습니다 {호스트-서비스-이름 hello HostedService 하나를 포함 하는 경우에 hello 가용성 집합의 일부가 아닌 Vm에 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-149">Migration is not supported for Deployment {deployment-name} in HostedService {hosted-service-name because it has VMs that are not part of hello Availability Set even though hello HostedService contains one.</span></span> |<span data-ttu-id="4aa2d-150">이 시나리오에 대 한 hello 해결은 tooeither 이동 단일 가용성에 모든 hello 가상 컴퓨터 설정 또는 hello hello 호스팅된 서비스의 가용성 집합에서 모든 가상 컴퓨터를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-150">hello workaround for this scenario is tooeither move all hello virtual machines into a single Availability set or remove all Virtual machines from hello Availability set in hello hosted service.</span></span> |
| <span data-ttu-id="4aa2d-151">저장소 계정/HostedService/가상 네트워크 {가상 네트워크 이름 간}는 마이그레이션 중 hello 프로세스 중에서 이므로 이므로 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-151">Storage account/HostedService/Virtual Network {virtual-network-name} is in hello process of being migrated and hence cannot be changed</span></span> |<span data-ttu-id="4aa2d-152">이 오류는 hello 리소스에 hello "준비" 마이그레이션 작업이 완료 되 고 toohello 리소스를 변경 하는 작업이 트리거될 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-152">This error happens when hello "Prepare" migration operation has been completed on hello resource and an operation that would make a change toohello resource is triggered.</span></span> <span data-ttu-id="4aa2d-153">"준비" 작업 후 hello 관리 평면에 hello 잠금 때문에 모든 변경 내용을 toohello 리소스 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-153">Because of hello lock on hello management plane after "Prepare" operation, any changes toohello resource are blocked.</span></span> <span data-ttu-id="4aa2d-154">toounlock hello 관리 평면 hello "커밋" 마이그레이션 작업 toocomplete 마이그레이션 실행할 수 있습니다 또는 hello "중단" 마이그레이션 작업 tooroll 다시 hello "준비" 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-154">toounlock hello management plane, you can run hello "Commit" migration operation toocomplete migration or hello "Abort" migration operation tooroll back hello "Prepare" operation.</span></span> |
| <span data-ttu-id="4aa2d-155">RoleStateUnknown 상태인 VM {vm-name}이 있기 때문에 HostedService {hosted-service-name}에 대한 마이그레이션이 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-155">Migration is not allowed for HostedService {hosted-service-name} because it has VM {vm-name} in State: RoleStateUnknown.</span></span> <span data-ttu-id="4aa2d-156">만 hello hello 다음 중 하나에 VM이 상태는 경우-실행 중, 중지 됨, 할당 취소 중지에서는 마이그레이션이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-156">Migration is allowed only when hello VM is in one of hello following states - Running, Stopped, Stopped Deallocated.</span></span> |<span data-ttu-id="4aa2d-157">hello VM 수 모드로 전환 hello HostedService 다시 부팅 등의 업데이트 작업 중 때 일반적으로 수행 됨 상태 전환을 통해 확장 등을 설치 합니다. 마이그레이션을 시도 하기 전에 hello HostedService에 업데이트 작업이 toocomplete hello에 대 한이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-157">hello VM might be undergoing through a state transition, which usually happens when during an update operation on hello HostedService such as a reboot, extension installation etc. It is recommended for hello update operation toocomplete on hello HostedService before trying migration.</span></span> |
| <span data-ttu-id="4aa2d-158">HostedService {호스팅된 서비스-이름}의 {배포 이름} 배포 인 물리적 blob 크기 {size-of-the-vhd-blob-backing-the-data-disk} 바이트 hello VM 데이터 디스크가 논리적 크기 {와 일치 하지 않습니다 데이터 디스크 {데이터 디스크 이름}와 {vm name}는 VM이 포함 size-of-the-data-disk-specified-in-the-vm-api} 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-158">Deployment {deployment-name} in HostedService {hosted-service-name} contains a VM {vm-name} with Data Disk {data-disk-name} whose physical blob size {size-of-the-vhd-blob-backing-the-data-disk} bytes does not match hello VM Data Disk logical size {size-of-the-data-disk-specified-in-the-vm-api} bytes.</span></span> <span data-ttu-id="4aa2d-159">마이그레이션은 hello Azure 리소스 관리자 VM에 대 한 hello 데이터 디스크에 대 한 크기를 지정 하지 않고 계속 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-159">Migration will proceed without specifying a size for hello data disk for hello Azure Resource Manager VM.</span></span> | <span data-ttu-id="4aa2d-160">이 오류는 hello VM API 모델의 hello 크기를 업데이트 하지 않고 hello VHD blob 크기를 조정할 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-160">This error happens if you've resized hello VHD blob without updating hello size in hello VM API model.</span></span> <span data-ttu-id="4aa2d-161">자세한 마이그레이션 단계는 [다음](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes)과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-161">Detailed mitigation steps are outlined [below](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes).</span></span>|
| <span data-ttu-id="4aa2d-162">클라우드 서비스 {클라우드 서비스 이름}에서 {VM 이름} VM에 대해 미디어 링크 {데이터 디스크 URI}를 사용하여 데이터 디스크 {데이터 디스크 이름}에 대해 유효성 검사를 수행하는 동안 저장소 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-162">A storage exception occurred while validating data disk {data disk name} with media link {data disk Uri} for VM {VM name} in Cloud Service {Cloud Service name}.</span></span> <span data-ttu-id="4aa2d-163">해당 hello VHD 미디어 링크는이 가상 컴퓨터에 액세스할 수 있는지 확인 하십시오</span><span class="sxs-lookup"><span data-stu-id="4aa2d-163">Please ensure that hello VHD media link is accessible for this virtual machine</span></span> | <span data-ttu-id="4aa2d-164">이 오류는 hello의 hello 디스크 VM 삭제 되었거나 더 이상 액세스할 수 없는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-164">This error can happen if hello disks of hello VM have been deleted or are not accessible anymore.</span></span> <span data-ttu-id="4aa2d-165">VM이 존재 하는 hello에 대 한 hello 디스크가 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-165">Please make sure hello disks for hello VM exist.</span></span>|
| <span data-ttu-id="4aa2d-166">HostedService {cloud-service-name}의 VM {vm-name}에는 Azure Resource Manager에서 지원되지 않는 BLOB 이름 {vhd-blob-name}의 MediaLink {vhd-uri}가 있는 디스크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-166">VM {vm-name} in HostedService {cloud-service-name} contains Disk with MediaLink {vhd-uri} which has blob name {vhd-blob-name}  that is not supported in Azure Resource Manager.</span></span> | <span data-ttu-id="4aa2d-167">Hello blob의 hello 이름에는 "/"를 현재 계산 리소스 공급자에서 지원 되지 않는 것이 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-167">This error occurs when hello name of hello blob has a "/" in it which is not supported in Compute Resource Provider currently.</span></span> |
| <span data-ttu-id="4aa2d-168">가 hello 지역 범위에 속하지 않으므로 HostedService {클라우드 서비스 이름}의 {배포 이름} 배포에 대 한 마이그레이션이 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-168">Migration is not allowed for Deployment {deployment-name} in HostedService {cloud-service-name} as it is not in hello regional scope.</span></span> <span data-ttu-id="4aa2d-169">이 배포 tooregional 범위를 이동 하기 위한 toohttp://aka.ms/regionalscope를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-169">Please refer toohttp://aka.ms/regionalscope for moving this deployment tooregional scope.</span></span> | <span data-ttu-id="4aa2d-170">2014에서 Azure는 네트워킹 리소스에서에서 이동 합니다. 클러스터 수준 범위 tooregional 범위를 발표 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-170">In 2014, Azure announced that networking resources will move from a cluster level scope tooregional scope.</span></span> <span data-ttu-id="4aa2d-171">자세한 내용은 [http://aka.ms/regionalscope]를 참조하세요(http://aka.ms/regionalscope).</span><span class="sxs-lookup"><span data-stu-id="4aa2d-171">See [http://aka.ms/regionalscope] for more details (http://aka.ms/regionalscope).</span></span> <span data-ttu-id="4aa2d-172">이 오류는 마이그레이션되는 hello 배포 하지 않았습니다. 업데이트 작업을 자동으로 tooa 지역 범위로 이동 하는 경우에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-172">This error happens when hello deployment being migrated has not had an update operation, which automatically moves it tooa regional scope.</span></span> <span data-ttu-id="4aa2d-173">최상의 방법은 tooeither 끝점 tooa VM을 추가 하거나 데이터는 toohello VM 디스크와 다음 마이그레이션을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-173">Best workaround is tooeither add an endpoint tooa VM or a data disk toohello VM and then retry migration.</span></span> <br> <span data-ttu-id="4aa2d-174">참조 [어떻게 azure에서 클래식 Windows 가상 컴퓨터 끝점을 tooset](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint) 또는 [hello 클래식 배포 모델을 사용 하 여 만든 데이터 디스크 tooa Windows 가상 컴퓨터를 연결 합니다.](../articles/virtual-machines/windows/classic/attach-disk.md)</span><span class="sxs-lookup"><span data-stu-id="4aa2d-174">See [How tooset up endpoints on a classic Windows virtual machine in Azure](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint) or [Attach a data disk tooa Windows virtual machine created with hello classic deployment model](../articles/virtual-machines/windows/classic/attach-disk.md)</span></span>|


## <a name="detailed-mitigations"></a><span data-ttu-id="4aa2d-175">자세한 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="4aa2d-175">Detailed mitigations</span></span>

### <a name="vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-hello-vm-data-disk-logical-size-bytes"></a><span data-ttu-id="4aa2d-176">데이터 디스크를 물리적 blob 크기 (바이트)를 사용 하 여 VM hello VM 데이터 디스크가 논리적 크기 (바이트)을 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-176">VM with Data Disk whose physical blob size bytes does not match hello VM Data Disk logical size bytes.</span></span>

<span data-ttu-id="4aa2d-177">이 hello 데이터 디스크의 논리 크기를 가져올 수 hello 실제 VHD blob 크기와 동기화 하는 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-177">This happens when hello Data disk logical size can get out of sync with hello actual VHD blob size.</span></span> <span data-ttu-id="4aa2d-178">이 쉽게 확인할 수 hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="4aa2d-178">This can be easily verified using hello following commands:</span></span>

#### <a name="verifying-hello-issue"></a><span data-ttu-id="4aa2d-179">Hello 문제를 확인 하는 중</span><span class="sxs-lookup"><span data-stu-id="4aa2d-179">Verifying hello issue</span></span>

```PowerShell
# Store hello VM details in hello VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

# Display hello data disk properties
# NOTE hello data disk LogicalDiskSizeInGB below which is 11GB. Also note hello MediaLink Uri of hello VHD blob as we'll use this in hello next step
$vm.VM.DataVirtualHardDisks


HostCaching         : None
DiskLabel           : 
DiskName            : coreosvm-coreosvm-0-201611230636240687
Lun                 : 0
LogicalDiskSizeInGB : 11
MediaLink           : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
SourceMediaLink     : 
IOType              : Standard
ExtensionData       : 

# Now get hello properties of hello blob backing hello data disk above
# NOTE hello size of hello blob is about 15 GB which is different from LogicalDiskSizeInGB above
$blob = Get-AzureStorageblob -Blob "coreosvm-dd1.vhd" -Container vhds 

$blob

ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudPageBlob
BlobType          : PageBlob
Length            : 16106127872
ContentType       : application/octet-stream
LastModified      : 11/23/2016 7:16:22 AM +00:00
SnapshotTime      : 
ContinuationToken : 
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.AzureStorageContext
Name              : coreosvm-dd1.vhd
```

#### <a name="mitigating-hello-issue"></a><span data-ttu-id="4aa2d-180">Hello 문제를 완화합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-180">Mitigating hello issue</span></span>

```PowerShell
# Convert hello blob size in bytes tooGB into a variable which we'll use later
$newSize = [int]($blob.Length / 1GB)

# See hello calculated size in GB
$newSize

15

# Store hello disk name of hello data disk as we'll use this tooidentify hello disk toobe updated
$diskName = $vm.VM.DataVirtualHardDisks[0].DiskName

# Identify hello LUN of hello data disk tooremove
$lunToRemove = $vm.VM.DataVirtualHardDisks[0].Lun

# Now remove hello data disk from hello VM so that hello disk isn't leased by hello VM and it's size can be updated
Remove-AzureDataDisk -LUN $lunToRemove -VM $vm | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       213xx1-b44b-1v6n-23gg-591f2a13cd16   Succeeded  

# Verify we have hello right disk that's going toobe updated
Get-AzureDisk -DiskName $diskName

AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : 
Location             : East US
DiskSizeInGB         : 11
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 0c56a2b7-a325-123b-7043-74c27d5a61fd
OperationStatus      : Succeeded

# Now update hello disk toohello new size
Update-AzureDisk -DiskName $diskName -ResizedSizeInGB $newSize -Label $diskName

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureDisk     cv134b65-1b6n-8908-abuo-ce9e395ac3e7 Succeeded 

# Now verify that hello "DiskSizeInGB" property of hello disk matches hello size of hello blob 
Get-AzureDisk -DiskName $diskName


AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : coreosvm-coreosvm-0-201611230636240687
Location             : East US
DiskSizeInGB         : 15
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 1v53bde5-cv56-5621-9078-16b9c8a0bad2
OperationStatus      : Succeeded

# Now we'll add hello disk back toohello VM as a data disk. First we need tooget an updated VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

Add-AzureDataDisk -Import -DiskName $diskName -LUN 0 -VM $vm -HostCaching ReadWrite | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       b0ad3d4c-4v68-45vb-xxc1-134fd010d0f8 Succeeded      
```

### <a name="moving-a-vm-tooa-different-subscription-after-completing-migration"></a><span data-ttu-id="4aa2d-181">마이그레이션을 완료 한 후 VM tooa 다른 구독 이동</span><span class="sxs-lookup"><span data-stu-id="4aa2d-181">Moving a VM tooa different subscription after completing migration</span></span>

<span data-ttu-id="4aa2d-182">Hello 마이그레이션 프로세스를 완료 한 후 toomove hello VM tooanother 구독을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-182">After you complete hello migration process, you may want toomove hello VM tooanother subscription.</span></span> <span data-ttu-id="4aa2d-183">그러나 암호/인증서에 있는 경우 참조 하는 주요 자격 증명 모음 리소스 hello VM 이동 hello 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-183">However, if you have a secret/certificate on hello VM that references a Key Vault resource, hello move is currently not supported.</span></span> <span data-ttu-id="4aa2d-184">아래 지침 hello tooworkaround hello 문제를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa2d-184">hello below instructions will allow you tooworkaround hello issue.</span></span> 

#### <a name="powershell"></a><span data-ttu-id="4aa2d-185">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4aa2d-185">PowerShell</span></span>
```powershell
$vm = Get-AzureRmVM -ResourceGroupName "MyRG" -Name "MyVM"
Remove-AzureRmVMSecret -VM $vm
Update-AzureRmVM -ResourceGroupName "MyRG" -VM $vm
```
#### <a name="azure-cli-20"></a><span data-ttu-id="4aa2d-186">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4aa2d-186">Azure CLI 2.0</span></span>

```bash
az vm update -g "myrg" -n "myvm" --set osProfile.Secrets=[]
```
