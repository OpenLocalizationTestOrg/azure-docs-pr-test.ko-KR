



환경 및 선택 사항에 따라 hello 스크립트 hello Azure 가상 네트워크, 저장소 계정, 클라우드 서비스, 도메인 컨트롤러, 원격 또는 로컬 SQL 데이터베이스, 헤드 노드 및 추가 클러스터를 포함 하 여 모든 hello 클러스터 인프라를 만들 수 있습니다. 노드입니다. 또는 hello 스크립트는 기존 Azure 인프라를 사용 하 고만 hello HPC 클러스터 노드를 만들 수 있습니다.

HPC Pack 클러스터를 계획 하는 방법에 대 한 배경 정보를 참조 hello [제품 평가 및 계획](https://technet.microsoft.com/library/jj899596.aspx) 및 [시작](https://technet.microsoft.com/library/jj899590.aspx) hello HPC Pack 2012 R2 TechNet 라이브러리에서에서 콘텐츠입니다.

## <a name="prerequisites"></a>필수 조건
* **Azure 구독**: 어느 hello Azure Global 또는 Azure China 서비스에서에서 구독을 사용할 수 있습니다. 구독 제한과 hello 유형과 수, 클러스터 노드를 배포할 수에 영향을 줍니다. 자세한 내용은 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../articles/azure-subscription-service-limits.md)을 참조하세요.
* **Azure powershell 0.8.10 Windows 클라이언트 컴퓨터 또는 나중에 설치 및 구성**: 참조 [Azure PowerShell 시작](/powershell/azureps-cmdlets-docs) 설치 지침과 단계 tooconnect tooyour Azure 구독에 대 한 합니다.
* **HPC Pack IaaS 배포 스크립트**: 다운로드 하 고 hello hello에서 hello 스크립트의 최신 버전을 푸는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=44949)합니다. Hello 버전의 hello 스크립트를 실행 하 여 확인 `New-HPCIaaSCluster.ps1 –Version`합니다. 이 문서는 hello 스크립트의 버전 4.5.2 기반으로 합니다.
* **스크립트 구성 파일**: hello 스크립트 tooconfigure hello HPC 클러스터를 사용 하는 XML 파일을 만듭니다. 내용 및 예제에 대 한이 문서의 뒷부분에 나오는 섹션을 참조 하 고 hello Manual.rtf hello 배포 스크립트를 함께 제공 되는 파일입니다.

## <a name="syntax"></a>구문
```PowerShell
New-HPCIaaSCluster.ps1 [-ConfigFile] <String> [-AdminUserName]<String> [[-AdminPassword] <String>] [[-HPCImageName] <String>] [[-LogFile] <String>] [-Force] [-NoCleanOnFailure] [-PSSessionSkipCACheck] [<CommonParameters>]
```
> [!NOTE]
> 관리자 권한으로 hello 스크립트를 실행 합니다.
> 
> 

### <a name="parameters"></a>매개 변수
* **ConfigFile**: hello 구성 파일 toodescribe hello HPC 클러스터의 hello 파일 경로 지정 합니다. Hello 구성 파일 hello hello 스크립트를 포함 하는 hello 폴더에 있는 Manual.rtf 파일 또는이 항목에 대 한 자세한 정보를 참조 하십시오.
* **AdminUserName**: hello 사용자 이름을 지정 합니다. Hello 스크립트를 hello 도메인 포리스트를 만드는 경우이 모든 Vm에 대 한 hello 로컬 관리자 사용자 이름 및 도메인 관리자 이름을 hello 합니다. Hello 도메인 포리스트가 이미 있는 경우이 로컬 관리자 사용자 이름 tooinstall HPC 팩 hello 같이 hello 도메인 사용자를 지정 합니다.
* **AdminPassword**: hello 관리자 암호를 지정 합니다. Hello 명령줄에 지정 되지 경우 hello 스크립트 tooinput hello 암호를 표시 됩니다.
* **HPCImageName** (선택 사항): toodeploy hello HPC 클러스터를 사용 하는 hello HPC Pack VM 이미지 이름을 지정 합니다. Hello Azure Marketplace에서에서 HPC Pack을 Microsoft에서 제공한 이미지 여야 합니다. 경우 (권장된 일반적으로)을 지정된 하지 않은 hello hello 게시 된 최신 버전을 선택 하는 스크립트 [HPC Pack 2012 R2 이미지](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)합니다. hello 최신 이미지 HPC Pack 2012 R2 업데이트 3이 설치 되어 있는 Windows Server 2012 R2 Datacenter를 기반으로 합니다.
  
  > [!NOTE]
  > 유효한 HPC 팩 이미지를 지정하지 않으면 배포가 실패합니다.
  > 
  > 
* **로그 파일** (선택 사항): hello 배포 로그 파일 경로 지정 합니다. 지정 하지 않으면 hello 스크립트 hello hello 스크립트를 실행 하는 hello 컴퓨터의 임시 디렉터리에 로그 파일을 만듭니다.
* **Force** (선택 사항): 모든 hello 확인 프롬프트를 표시 하지 않습니다.
* **NoCleanOnFailure** (선택 사항): 지정 해당 hello 올바르게 배포 되지 않는 Azure Vm은 제거 되지 않습니다. Hello 스크립트 toocontinue hello 배포를 다시 실행 하기 전에 이러한 Vm을 수동으로 제거 하거나 hello 배포가 실패할 수 있습니다.
* **PSSessionSkipCACheck** (선택 사항):이 스크립트에 의해 배포 된 Vm이 포함 된 모든 클라우드 서비스에 대 한 자체 서명 된 인증서를 자동으로 Azure에서 생성와 기본 Windows hello hello 클라우드 서비스에 모든 hello Vm이이 인증서 사용 원격 관리 (WinRM) 인증서입니다. toodeploy 이러한 Azure Vm에서 HPC 기능을 기본적으로 스크립트 hello이 인증서를 임시로 설치 이러한 hello 로컬 컴퓨터에서에서\\hello 클라이언트 컴퓨터 toosuppress의 신뢰할 수 있는 루트 인증 기관 저장소 hello "신뢰할 수 없는 CA" 보안 스크립트를 실행 하는 동안 오류가 발생 했습니다. hello 스크립트가 완료 되 면 hello 인증서는 제거 됩니다. 이 매개 변수를 지정 하는 경우 hello 인증서 hello 클라이언트 컴퓨터에 설치 되지 않은 및 hello 보안 경고가 표시 되지 않습니다.
  
  > [!IMPORTANT]
  > 이 매개 변수는 프로덕션 배포에 권장되지 않습니다.
  > 
  > 

### <a name="example"></a>예제
hello 다음 예제에서는 구성 파일을 사용 하 여 HPC Pack 클러스터 *에서는 MyConfigFile.xml*, hello 클러스터 설치를 위한 관리자 자격 증명을 지정 합니다.

```PowerShell
.\New-HPCIaaSCluster.ps1 –ConfigFile MyConfigFile.xml -AdminUserName <username> –AdminPassword <password>
```

### <a name="additional-considerations"></a>추가 고려 사항
* hello 스크립트 hello HPC Pack 웹 포털 또는 hello HPC Pack REST API를 통해 작업 제출을 선택적으로 사용할 수 있습니다.
* 필요에 따라 hello 스크립트 tooinstall 추가 소프트웨어를 선택 하거나 다른 설정을 구성 하는 경우 hello 헤드 노드에서 사용자 지정 전 / 구성 후 스크립트를 실행할 수 있습니다.

## <a name="configuration-file"></a>구성 파일
hello 배포 스크립트에 대 한 hello 구성 파일은 XML 파일입니다. hello 스키마 파일이 HPCIaaSClusterConfig.xsd hello HPC Pack IaaS 배포 스크립트 폴더입니다. **IaaSClusterConfig** 는 hello hello 배포 스크립트 폴더에 있는 Manual.rtf 파일에 자세히 설명 하는 hello 자식 요소를 포함 하는 hello 구성 파일의 hello 루트 요소입니다.

