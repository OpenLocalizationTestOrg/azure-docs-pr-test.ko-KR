## <a name="prepare-for-akv-integration"></a>AKV 통합 준비
Azure 키 자격 증명 모음 통합 tooconfigure toouse SQL Server VM에는 몇 가지 필수 구성 요소: 

1. [Azure Powershell 설치](#install-azure-powershell)
2. [Azure Active Directory 만들기](#create-an-azure-active-directory)
3. [키 자격 증명 모음 만들기](#create-a-key-vault)

hello 다음 섹션에서는 이러한 필수 구성 요소 및 설명 hello 정보 toocollect 실행 toolater hello PowerShell cmdlet을 사용 해야 합니다.

### <a name="install-azure-powershell"></a>Azure Powershell 설치
설치 했는지 확인 최신 Azure PowerShell SDK hello 합니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs)합니다.

### <a name="create-an-azure-active-directory"></a>Azure Active Directory 만들기
먼저 toohave는 [Azure Active Directory](https://azure.microsoft.com/trial/get-started-active-directory/) (AAD) 구독에 있습니다. 많은 이점은 있습니다 toogrant 권한 tooyour 주요 자격 증명 모음을 특정 사용자와 응용 프로그램.

다음으로 AAD에 응용 프로그램을 등록합니다. 이렇게 하면 얻을 수 있는 서비스 사용자 계정을 액세스 tooyour 키 있는 자격 증명 모음이 VM이 필요 합니다. Hello Azure 키 자격 증명 모음 문서의 hello에서 다음이 단계를 찾을 수 있습니다 [응용 프로그램을 Azure Active Directory 등록](../articles/key-vault/key-vault-get-started.md#register) 구역 또는 있습니다 hello에 스크린 샷을 사용 하 여 hello 단계를 확인할 수 **hello 응용 프로그램에 대 한 id 가져오기 섹션** 의 [이 블로그 게시물](http://blogs.technet.com/b/kv/archive/2015/01/09/azure-key-vault-step-by-step.aspx)합니다. 완료 하기 전에 다음이 단계를 확인 정보는 나중에 SQL VM에 Azure 키 자격 증명 모음 통합을 사용 하도록 설정 하면이 기능을이 등록 하는 동안 다음 toocollect hello가 필요 합니다.

* Hello 응용 프로그램을 추가한 다음 찾기 hello **클라이언트 ID** hello에 **구성** 탭 합니다.   ![Azure Active Directory 클라이언트 ID](./media/virtual-machines-sql-server-akv-prepare/aad-client-id.png)
  
    hello 클라이언트 ID는 나중 toohello 할당 **$spName** hello PowerShell 스크립트 tooenable Azure 키 자격 증명 모음 통합 (서비스 사용자 이름) 매개 변수입니다. 
* 또한이 단계에서 사용자의 키를 만들 때 암호를 복사할 hello 트 키에 대 한 hello 스크린 샷 뒤에 표시 된 대로 합니다. 이 키의 비밀 이후 toohello 할당 **$spSecret** hello PowerShell 스크립트의 매개 변수 (서비스 사용자 secret 입니다).  
    ![Azure Active Directory 비밀](./media/virtual-machines-sql-server-akv-prepare/aad-sp-secret.png)
* 다음 액세스 권한을 하이 새 클라이언트 ID toohave hello에 권한을 부여 해야: **암호화**, **해독**, **wrapKey**, **unwrapKey**, **기호**, 및 **확인**합니다. Hello로 이렇게 [Set-azurermkeyvaultaccesspolicy](https://msdn.microsoft.com/library/azure/mt603625.aspx) cmdlet. 자세한 내용은 참조 [Authorize hello 응용 프로그램 toouse hello 키 또는 암호](../articles/key-vault/key-vault-get-started.md#authorize)합니다.

### <a name="create-a-key-vault"></a>키 자격 증명 모음 만들기
순서 toouse Azure 키 자격 증명 모음 toostore hello 키에 VM에서 암호화에 사용할 액세스 tooa 주요 자격 증명 모음을 해야 합니다. 아직 주요 자격 증명 모음을 설정 하지 않은 경우 hello hello 단계를 수행 하 여 만들 [Azure 키 자격 증명 모음 시작](../articles/key-vault/key-vault-get-started.md) 항목입니다. 이 단계를 완료 하기 전에 toocollect이이 설정 중 필요한 일부 정보는 나중에 때 필요한 SQL VM에 Azure 키 자격 증명 모음 통합을 사용 합니다.

얻으면 toohello 단계를 만들려면 주요 자격 증명 모음, 참고 hello 반환 **vaultUri** hello 주요 자격 증명 모음 URL에 해당 하는 속성이 있습니다. 아래 표시 된 해당 단계에서 제공 하는 hello 예제의 hello 주요 자격 증명 모음 이름은 ContosoKeyVault를 이므로 hello 주요 자격 증명 모음 URL https://contosokeyvault.vault.azure.net/ 됩니다 합니다.

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

hello 주요 자격 증명 모음 URL 이후 toohello 할당 **$akvURL** hello PowerShell 스크립트 tooenable Azure 키 자격 증명 모음 통합에에서 대 한 매개 변수입니다.

