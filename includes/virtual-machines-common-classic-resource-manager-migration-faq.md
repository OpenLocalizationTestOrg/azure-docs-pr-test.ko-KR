# <a name="frequently-asked-questions-about-classic-tooazure-resource-manager-migration"></a>클래식 tooAzure 리소스 관리자 마이그레이션에 대 한 질문과 대답

## <a name="does-this-migration-plan-affect-any-of-my-existing-services-or-applications-that-run-on-azure-virtual-machines"></a>이 마이그레이션 계획이 Azure 가상 컴퓨터에서 실행되는 기존 서비스 또는 응용 프로그램에 영향을 미치나요? 

아니요. hello Vm (클래식)는 일반 공급에서 완벽 하 게 지원 되는 서비스입니다. 이러한 리소스 tooexpand toouse를 계속할 수 있습니다 Microsoft Azure에서 사용 하 여 공간입니다.

## <a name="what-happens-toomy-vms-if-i-dont-plan-on-migrating-in-hello-near-future"></a>Toomy Vm hello 가까운 미래에에서 마이그레이션하는 방법에 않을 어떻게 됩니까? 

우리는 hello 기존 클래식 Api 및 리소스 모델 사용이 중지 되지 않습니다. 원하는 toomake 마이그레이션 쉽게 hello hello 리소스 관리자 배포 모델에서 사용할 수 있는 고급 기능을 고려 합니다. 검토 하는 것이 좋습니다 [일부 hello 발전이](../articles/azure-resource-manager/resource-manager-deployment-model.md) IaaS에서 리소스 관리자의 일부인 합니다.

## <a name="what-does-this-migration-plan-mean-for-my-existing-tooling"></a>이 마이그레이션 계획으로 기존 도구는 어떻게 되나요? 

도구 toohello 리소스 관리자 배포 모델을 업데이트 마이그레이션 계획에 대 한 tooaccount 있는 hello 가장 중요 한 변경 내용 중 하나입니다.

## <a name="how-long-will-hello-management-plane-downtime-be"></a>시간 hello 관리 평면 가동 중지 시간 됩니까? 

Hello 마이그레이션되고 있는 리소스 수에 따라 다릅니다. 소규모 배포 (수십 Vm)에 대 한 전체 마이그레이션 hello 1 시간 미만 수행 해야 합니다. 대규모 배포 (수백 Vm)에 대 한 hello 마이그레이션 몇 시간이 걸릴 수 있습니다.

## <a name="can-i-roll-back-after-my-migrating-resources-are-committed-in-resource-manager"></a>Resource Manager에서 마이그레이션 리소스를 커밋한 다음 롤백할 수 있나요? 

Hello 리소스가 hello 준비 상태에에서 있는으로 마이그레이션을 중단할 수 있습니다. Rollback은 hello 리소스 성공적으로 마이그레이션한 후 hello 커밋 작업을 통해 지원 되지 않습니다.

## <a name="can-i-roll-back-my-migration-if-hello-commit-operation-fails"></a>롤백할 수 있습니까 내 마이그레이션 hello 커밋 작업이 실패 한 경우? 

Hello 커밋 작업이 실패 한 경우 마이그레이션을 중단할 수 없습니다. Hello 커밋 작업을 비롯 한 모든 마이그레이션 작업은 idempotent. 따라서 짧은 시간 후 hello 작업을 다시 시도 하는 것이 좋습니다. 오류를 여전히 발생 하면 지원 티켓을 만드세요 만들거나 포럼 게시물 ClassicIaaSMigration 태그에 hello로 취급 [VM 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows)합니다.

## <a name="do-i-have-toobuy-another-express-route-circuit-if-i-have-toouse-iaas-under-resource-manager"></a>용량은 toobuy 다른 express 경로 회로 toouse IaaS 리소스 관리자에서이 있는 경우 

아니요. 최근에 활성화 [hello 클래식 toohello 리소스 관리자 배포 모델에서 ExpressRoute 회로 이동](../articles/expressroute/expressroute-move.md)합니다. 없는 toobuy 새 ExpressRoute 회로 이미 있는 경우.

## <a name="what-if-i-had-configured-role-based-access-control-policies-for-my-classic-iaas-resources"></a>클래식 IaaS 리소스에 대해 역할 기반 Access Control 정책을 구성한 경우 어떻게 되나요? 

마이그레이션하는 동안 hello 리소스 클래식 tooResource 관리자에서에서 변환합니다. 따라서 마이그레이션 후 toohappen 필요한 hello RBAC 정책 업데이트를 계획 하는 것이 좋습니다.

## <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>Backup 자격 증명 모음에 내 클래식 VM을 백업했습니다. 클래식 모드 tooResource 관리자 모드에서 내 Vm 마이그레이션을 복구 서비스 자격 증명 모음에서 보호할 수 있습니까? 

백업 자격 증명 모음에 클래식 VM 복구 지점을 클래식 tooResource 관리자 모드에서에서 hello VM을 이동할 때 tooa 복구 서비스 자격 증명 모음을 자동으로 마이그레이션합니다 하지 않습니다. 이러한 단계 tootransfer VM 백업을 수행 합니다.

1. Hello 백업 자격 증명 모음에서 이동 toohello **보호 된 항목** 탭 하 고 hello VM을 선택 합니다. [보호 중지](../articles/backup/backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines)를 클릭합니다. *연결된 백업 데이터 삭제* 옵션을 **검사하지 않음**으로 둡니다.
2. Hello VM에서에서 hello 백업/스냅숏 확장을 삭제 합니다.
3. 클래식 모드 tooResource 관리자 모드에서 hello 가상 컴퓨터를 마이그레이션하십시오. 해당 toohello 가상 컴퓨터가 이기도 hello 저장소 및 네트워크 정보 tooResource 관리자 모드 마이그레이션 되었는지 확인 합니다.
4. 복구 서비스 자격 증명 모음 만들기 및 구성 hello에 백업 마이그레이션된 가상 컴퓨터를 사용 하 여 **백업** 자격 증명 모음 대시보드를 기반으로 동작 합니다. 자격 증명 모음에 대 한 자세한 내용은 VM tooa 복구 서비스를 백업, hello 문서 참조 [복구 서비스 자격 증명 모음 Azure Vm 보호](../articles/backup/backup-azure-vms-first-look-arm.md)합니다.

## <a name="can-i-validate-my-subscription-or-resources-toosee-if-theyre-capable-of-migration"></a>있습니까 유효성을 검사할 수 내 구독 또는 리소스 toosee 마이그레이션 수 있는 경우? 

예. Hello 플랫폼에서 지 원하는 마이그레이션 옵션을 마이그레이션을 준비 hello 첫 번째 단계는 hello 리소스를 마이그레이션 수 있는 toovalidate을 것입니다. Hello 작업이 실패의 유효성을 검사 하는 경우 메시지가 모든 hello 이유로 hello 마이그레이션을 완료할 수 없습니다.

## <a name="what-happens-if-i-run-into-a-quota-error-while-preparing-hello-iaas-resources-for-migration"></a>마이그레이션에 대 한 hello는 IaaS 리소스를 준비 하는 동안 할당량 오류에 직면 하는 경우 어떻게 됩니까? 

마이그레이션을 중단 후 지원 요청 tooincrease hello 할당량 hello 지역 마이그레이션 hello Vm의 현재 위치에서 로그인 하는 것이 좋습니다. Hello 할당량 요청이 승인 되 면 hello 마이그레이션 단계를 다시 실행을 시작할 수 있습니다.

## <a name="how-do-i-report-an-issue"></a>문제를 보고하려면 어떻게 해야 하나요? 

문제 및 마이그레이션 tooour에 대 한 질문을 게시 [VM 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows), ClassicIaaSMigration hello 키워드를 사용 합니다. 이 포럼에 모든 질문을 게시하는 것이 좋습니다. 지원 계약이 있는 경우 시작 toolog 지원 티켓도 것입니다.

## <a name="what-if-i-dont-like-hello-names-of-hello-resources-that-hello-platform-chose-during-migration"></a>마이그레이션 도중에 선택한 경우에 어떻게 플랫폼 hello hello 리소스의 hello 이름이 마음에 들지 않으면? 

마이그레이션 중에 대 한 hello 클래식 배포 모델의 이름을 명시적으로 제공 하는 hello 리소스를 모두 유지 됩니다. 새 리소스가 생성되는 경우도 있습니다. 예를 들어 모든 VM에 대해 네트워크 인터페이스가 생성됩니다. 마이그레이션 중에 만들어진 이러한 새 리소스의 hello 기능 toocontrol hello 이름을 현재 지원 되지 않습니다. Hello에이 기능에 대 한 사용자 응답을 기록 [Azure 피드백 포럼](http://feedback.azure.com)합니다.

## <a name="can-i-migrate-expressroute-circuits-used-across-subscriptions-with-authorization-links"></a>권한 부여 링크를 통해 구독에서 사용되는 ExpressRoute 회로를 마이그레이션할 수 있습니까? 

구독 간 권한 부여 링크를 사용하는 ExpressRoute 회로는 가동 중지 시간 없이 자동으로 마이그레이션할 수 없습니다. 여기에서는 수동 단계를 사용하여 마이그레이션하는 방법을 소개합니다. 참조 [마이그레이션할 ExpressRoute 회로 및 가상 네트워크를 hello 클래식 toohello 리소스 관리자 배포 모델에서 연결 된](../articles/expressroute/expressroute-migration-classic-resource-manager.md) 단계 및 추가 정보에 대 한 합니다.

## <a name="i-got-a-message-vm-is-reporting-hello-overall-agent-status-as-not-ready-hence-hello-vm-cannot-be-migrated-ensure-that-hello-vm-agent-is-reporting-overall-agent-status-as-ready-or-vm-contains-extension-whose-status-is-not-being-reported-from-hello-vm-hence-this-vm-cannot-be-migrated-"></a>메시지 수신 됨 *"hello를 보고 하는 VM으로 전반적인 에이전트 상태가 준비 되지 않았습니다. 따라서 VM hello 마이그레이션할 수 없습니다. VM 에이전트는 hello Ready로 전체 에이전트 상태를 보고 확인"* 또는 *"VM 상태가 hello VM에서에서 보고 되지 않습니다 확장을 포함 하는 데 사용 합니다. 따라서 이 VM은 마이그레이션할 수 없습니다."라는 메시지를 받았습니다. *

아웃 바운드 연결 toohello hello VM에 없을 때이 메시지를 수신 인터넷 합니다. hello VM 에이전트는 5 분 마다 hello 에이전트 상태를 업데이트 하기 위한 아웃 바운드 연결 tooreach hello Azure 저장소 계정을 사용 합니다.
