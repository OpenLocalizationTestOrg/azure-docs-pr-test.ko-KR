
# 개요
## [Azure Backup이란?](backup-introduction-to-azure-backup.md)

# 시작
## [Azure VM 백업](backup-azure-vms-first-look-arm.md)
## [Windows Server 또는 Windows 컴퓨터 백업](backup-try-azure-backup-in-10-mins.md)
## [VMware 서버 백업](backup-azure-backup-server-vmware.md)

# 방법

## Azure Backup 서버
### [Azure Backup Server 보호 매트릭스](backup-mabs-protection-matrix.md)
### 설치 또는 업그레이드
#### [Azure 포털에서 Azure Backup Server 작업 준비](backup-azure-microsoft-azure-backup.md)
#### [클래식 포털에서 Azure Backup Server 작업 준비](backup-azure-microsoft-azure-backup-classic.md)
#### [저장소 tooAzure 백업 서버를 추가 합니다.](backup-mabs-add-storage.md)
#### [Azure 백업 서버 toov.2 업그레이드](backup-mabs-upgrade-to-v2.md)
#### [Azure Backup Server의 무인 설치](backup-mabs-unattended-install.md)
### 워크로드 보호
#### [Azure 백업 서버 tooback VMware 서버를 사용 하 여](backup-azure-backup-server-vmware.md)
#### [Azure 백업 서버 tooback Exchange 사용 하 여](backup-azure-exchange-mabs.md)
#### [Azure 백업 서버 tooback를 사용 하 여 SharePoint 팜 구성](backup-azure-backup-sharepoint-mabs.md)
#### [Sql Azure 백업 서버 tooback를 사용 하 여](backup-azure-sql-mabs.md)
#### [시스템 상태 및 완전 복구 보호](backup-mabs-system-state-and-bmr.md)
### [Azure Backup Server에서 데이터 복구](backup-azure-alternate-dpm-server.md)

## Azure VM
### Hello VM 준비
#### [리소스 관리자가 배포된 가상 컴퓨터 준비](backup-azure-arm-vms-prepare.md)
#### [Linux VM의 응용 프로그램 일치 백업](backup-azure-linux-app-consistent.md)
#### [Azure 가상 컴퓨터 준비](backup-azure-vms-prepare.md)
### 환경 계획
#### [VM 백업 인프라 계획](backup-azure-vms-introduction.md)
### VM 백업
#### [Azure 가상 컴퓨터를 백업 tooa 복구 서비스 자격 증명 모음에](backup-azure-arm-vms.md)
#### [암호화된 가상 컴퓨터 백업](backup-azure-vms-encryption.md)
#### [Azure 가상 컴퓨터 백업](backup-azure-vms.md)
### VM 관리 및 모니터링
#### [Azure 포털에서 Azure VM 백업 관리](backup-azure-manage-vms.md)
#### [Azure 포털에서 Azure VM 백업에 대한 경고 모니터링](backup-azure-monitor-vms.md)
#### [클래식 포털에서 Azure VM 백업 관리 및 모니터링](backup-azure-manage-vms-classic.md)
### VM에서 데이터 복원
#### [Azure VM 백업에서 파일 복구](backup-azure-restore-files-from-vm.md)
#### [Azure 포털에서 Resource Manager 배포 VM 복구](backup-azure-arm-restore-vms.md)
#### [암호화된 가상 컴퓨터 복원](backup-azure-vms-encryption.md)
#### [Azure의 가상 컴퓨터 복원](backup-azure-restore-vms.md)
#### [암호화된 VM의 Key Vault 키 및 비밀 복원](backup-azure-restore-key-secret.md)

## Azure Backup 보고서 구성
### [Azure Backup 보고서 구성](backup-azure-configure-reports.md)
### [Azure Backup 보고서용 데이터 모델](backup-azure-reports-data-model.md)
### [Azure Backup용 Log Analytics 데이터 모델](backup-azure-log-analytics-data-model.md)

## Data Protection Manager
### [Azure 포털에서 DPM 작업 준비](backup-azure-dpm-introduction.md)
### [클래식 포털에서 DPM 작업 준비](backup-azure-dpm-introduction-classic.md)
### [Exchange server 사용 하 여 System Center DPM tooback](backup-azure-backup-exchange-server.md)
### [데이터 tooan 대체 DPM 서버 복구](backup-azure-alternate-dpm-server.md)
### [SQL Server 워크 로드를 사용 하 여 DPM tooback](backup-azure-backup-sql.md)
### [SharePoint 팜에를 사용 하 여 DPM tooback](backup-azure-backup-sharepoint.md)

## PowerShell 사용
### [Azure 포털의 Azure VM](backup-azure-vms-automation.md)
### [클래식 포털의 Azure VM](backup-azure-vms-classic-automation.md)
### [Azure 포털의 DPM](backup-dpm-automation.md)
### [클래식 포털의 DPM](backup-dpm-automation-classic.md)
### [Azure 포털의 Windows Server](backup-client-automation.md)
### [클래식 포털의 Windows Server](backup-client-automation-classic.md)

## Azure SQL Database
### [장기 백업 보존 구성](../sql-database/sql-database-configure-long-term-retention.md?toc=%2fazure%2fbackup%2ftoc.json)
### [Recovery Services 자격 증명 모음에서 백업 확인](../sql-database/sql-database-view-backups-in-vault.md?toc=%2fazure%2fbackup%2ftoc.json)
### [장기 백업 보존에서 복원](../sql-database/sql-database-restore-from-long-term-retention.md?toc=%2fazure%2fbackup%2ftoc.json)
### [장기 Azure SQL 백업 삭제](../sql-database/sql-database-long-term-retention-delete.md?toc=%2fazure%2fbackup%2ftoc.json)

## Windows Server
### [Windows Server 파일 및 폴더 백업](backup-configure-vault.md)
### [Windows Server 시스템 상태 백업](backup-azure-system-state.md)
### [Azure tooWindows 서버에서에서 파일을 복구 합니다.](backup-azure-restore-windows-server.md)
### [Windows Server 시스템 상태 복원](backup-azure-restore-system-state.md)
### [Recovery Services 자격 증명 모음 모니터링 및 관리](backup-azure-manage-windows-server.md)
### 백업 하 고 hello 클래식 포털을 사용 하 여 복원
#### [Hello 클래식 배포 모델을 사용 하 여 Windows Server](backup-configure-vault-classic.md)
#### [Hello 클래식 배포 모델을 사용 하 여 백업 자격 증명 모음 관리](backup-azure-manage-windows-server-classic.md)
#### [Windows Server 파일 tooa 복구 hello 클래식 배포 모델을 사용 하 여](backup-azure-restore-windows-server-classic.md)

## Recovery Services 자격 증명 모음
### [Recovery Services 자격 증명 모음 개요](backup-azure-recovery-services-vault-overview.md)
### [백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)
### [복구 서비스 자격 증명 모음 삭제](backup-azure-delete-vault.md)

## 문제 해결
### [Azure 포털에서 Azure VM 백업 문제](backup-azure-vms-troubleshoot.md)
### [클래식 포털에서 Azure VM 백업 문제](backup-azure-vms-troubleshoot-classic.md)
### [Azure VM 백업이 실패: 스냅숏 상태에 대 한 hello VM 에이전트와 통신할 수-스냅숏 VM 하위 작업이 시간 초과](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md)
### [Azure Backup에서 파일 및 폴더의 느린 백업](backup-azure-troubleshoot-slow-backup-performance-issue.md)
### [Azure Backup Server 문제 해결](backup-azure-mabs-troubleshoot.md)

# 개념

## FAQ
### [Recovery Services 자격 증명 모음에 대한 FAQ](backup-azure-backup-faq.md)
### [Azure VM 백업에 대한 FAQ](backup-azure-vm-backup-faq.md)
### [Azure Backup 에이전트를 사용하여 파일-폴더 백업에 대한 FAQ](backup-azure-file-folder-backup-faq.md)

## [역할 기반 액세스 제어](backup-rbac-rs-vault.md)
## [하이브리드 백업 보안](backup-azure-security-feature.md)
## [오프라인 백업 구성](backup-azure-backup-import-export.md)
## [테이프 라이브러리 교체](backup-azure-backup-cloud-as-tape.md)


# 참조
## [PowerShell](/powershell/module/azurerm.recoveryservices.backup)
## [.NET](/dotnet/api/microsoft.azure.management.recoveryservices.backup)

# 리소스
## [Azure 로드맵](https://azure.microsoft.com/roadmap/)
## [MSDN 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowsazureonlinebackup)
## [가격](https://azure.microsoft.com/pricing/details/backup/)
## [요금 계산기](https://azure.microsoft.com/pricing/calculator/)
## [서비스 업데이트](https://azure.microsoft.com/updates/?product=backup)
## [비디오](https://azure.microsoft.com/documentation/videos/index/?services=backup)
