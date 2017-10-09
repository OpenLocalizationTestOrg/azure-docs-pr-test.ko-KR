## <a name="next-steps"></a><span data-ttu-id="bdc5e-101">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bdc5e-101">Next steps</span></span>

<span data-ttu-id="bdc5e-102">Azure Key Vault 통합을 설정한 후에는 SQL VM에서 SQL Server 암호화를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="bdc5e-103">첫째, 해야 toocreate 비대칭 키 주요 자격 증명 모음 및 SQL Server 내에서 대칭 키 내부 VM에.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-103">First, you will need toocreate an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="bdc5e-104">그런 다음 데이터베이스 및 백업에 대 한 수 tooexecute T-SQL 문을 tooenable 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-104">Then, you will be able tooexecute T-SQL statements tooenable encryption for your databases and backups.</span></span>

<span data-ttu-id="bdc5e-105">여러 형태의 암호화를 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="bdc5e-106">TDE(투명한 데이터 암호화)</span><span class="sxs-lookup"><span data-stu-id="bdc5e-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="bdc5e-107">암호화된 백업</span><span class="sxs-lookup"><span data-stu-id="bdc5e-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="bdc5e-108">CLE(열 수준 암호화)</span><span class="sxs-lookup"><span data-stu-id="bdc5e-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="bdc5e-109">hello 다음 Transact SQL 스크립트 예제를 제공 각이 영역에 대 한.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-109">hello following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="bdc5e-110">예에 대한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="bdc5e-110">Prerequisites for examples</span></span>

<span data-ttu-id="bdc5e-111">Hello 두 필수 구성 요소를 기반으로 하는 각 예제: 주요 자격 증명 모음에서 비대칭 키 호출 **CONTOSO_KEY** 고 hello AKV 통합 기능을 호출 하 여 만든 자격 증명 **Azure_EKM_TDE_cred**합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-111">Each example is based on hello two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by hello AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="bdc5e-112">hello 다음 TRANSACT-SQL 명령을 설정 hello 예제를 실행 하기 위한 필수 구성이 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-112">hello following Transact-SQL commands setup these prerequisites for running hello examples.</span></span>

``` sql
USE master;
GO

sp_configure [show advanced options], 1;
GO
RECONFIGURE;
GO

-- Enable EKM provider
sp_configure [EKM provider enabled], 1;
GO
RECONFIGURE;

--create provider
CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov
FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';
GO

--create credential
CREATE CREDENTIAL sysadmin_ekm_cred
    WITH IDENTITY = 'keytestvault', --keyvault
    SECRET = '<<SECRET>>'
FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;


--must have sysadmin
ALTER LOGIN [TDE_Login]
ADD CREDENTIAL sysadmin_ekm_cred;


CREATE ASYMMETRIC KEY CONTOSO_KEY
FROM PROVIDER [AzureKeyVault_EKM_Prov]
WITH PROVIDER_KEY_NAME = 'keytestvault',  --key name
CREATION_DISPOSITION = OPEN_EXISTING;
```

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="bdc5e-113">TDE(투명한 데이터 암호화)</span><span class="sxs-lookup"><span data-stu-id="bdc5e-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="bdc5e-114">TDE에 대 한 hello 데이터베이스 엔진에서 사용 하는 SQL Server 로그인 toobe 만들기 다음 자격 증명 tooit hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-114">Create a SQL Server login toobe used by hello Database Engine for TDE, then add hello credential tooit.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello TDE Login tooadd hello credential for use by the
   -- Database Engine tooaccess hello key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. <span data-ttu-id="bdc5e-115">TDE에 사용 될 hello 데이터베이스 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-115">Create hello database encryption key that will be used for TDE.</span></span>

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello database tooenable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a><span data-ttu-id="bdc5e-116">암호화된 백업</span><span class="sxs-lookup"><span data-stu-id="bdc5e-116">Encrypted backups</span></span>

1. <span data-ttu-id="bdc5e-117">Hello, 백업을 암호화 하기 위해 데이터베이스 엔진에서 사용 하는 SQL Server 로그인 toobe 만들고 hello 자격 증명 tooit를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-117">Create a SQL Server login toobe used by hello Database Engine for encrypting backups, and add hello credential tooit.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it is encrypting hello backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello Encrypted Backup Login tooadd hello credential for use by
   -- hello Database Engine tooaccess hello key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. <span data-ttu-id="bdc5e-118">백업 hello 데이터베이스 hello 주요 자격 증명 모음에 저장 된 hello 비대칭 키를 사용 하 여 암호화를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-118">Backup hello database specifying encryption with hello asymmetric key stored in hello key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="bdc5e-119">CLE(열 수준 암호화)</span><span class="sxs-lookup"><span data-stu-id="bdc5e-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="bdc5e-120">이 스크립트 hello hello 주요 자격 증명 모음에 비대칭 키로 보호 되는 대칭 키를 만들고 hello 대칭 키 tooencrypt 데이터를 사용 하 여 hello 데이터베이스에 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-120">This script creates a symmetric key protected by hello asymmetric key in hello key vault, and then uses hello symmetric key tooencrypt data in hello database.</span></span>

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open hello symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data tooencrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close hello symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a><span data-ttu-id="bdc5e-121">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="bdc5e-121">Additional resources</span></span>

<span data-ttu-id="bdc5e-122">이러한 암호화 기능을 확인 하는 toouse 방법에 대 한 자세한 내용은 [SQL Server 암호화 기능과 함께 EKM 사용 하 여](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM)합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-122">For more information on how toouse these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="bdc5e-123">이 문서의 hello 단계에서는 Azure 가상 컴퓨터에서 실행 중인 SQL Server 이미 있다고 가정 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-123">Note that hello steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="bdc5e-124">아직 실행하고 있지 않다면 [Azure에서 SQL Server 가상 컴퓨터 프로비전](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="bdc5e-125">Azure VM에서 SQL Server 실행과 관련된 기타 참고 자료는 [Azure Virtual Machines의 SQL Server 개요](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bdc5e-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
