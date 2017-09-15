## <a name="next-steps"></a><span data-ttu-id="166f3-101">다음 단계</span><span class="sxs-lookup"><span data-stu-id="166f3-101">Next steps</span></span>

<span data-ttu-id="166f3-102">Azure Key Vault 통합을 설정한 후에는 SQL VM에서 SQL Server 암호화를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166f3-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="166f3-103">먼저, 키 자격 증명 모음 내에서 비대칭 키를 만들고 VM의 SQL Server 내에서 대칭 키를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="166f3-103">First, you will need to create an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="166f3-104">그러면 T-SQL 문을 실행하여 데이터베이스 및 백업에 대해 암호화를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166f3-104">Then, you will be able to execute T-SQL statements to enable encryption for your databases and backups.</span></span>

<span data-ttu-id="166f3-105">여러 형태의 암호화를 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="166f3-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="166f3-106">TDE(투명한 데이터 암호화)</span><span class="sxs-lookup"><span data-stu-id="166f3-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="166f3-107">암호화된 백업</span><span class="sxs-lookup"><span data-stu-id="166f3-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="166f3-108">CLE(열 수준 암호화)</span><span class="sxs-lookup"><span data-stu-id="166f3-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="166f3-109">다음 Transact-SQL 스크립트는 이러한 각 영역에 대한 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="166f3-109">The following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="166f3-110">예에 대한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="166f3-110">Prerequisites for examples</span></span>

<span data-ttu-id="166f3-111">각 예제는 두 가지 필수 조건을 기반으로 합니다. 하나는 주요 자격 증명 모음의 비대칭 키인 **CONTOSO_KEY**이고, 다른 하나는 AKV 통합 기능을 통해 생성되는 자격 증명인 **Azure_EKM_TDE_cred**입니다.</span><span class="sxs-lookup"><span data-stu-id="166f3-111">Each example is based on the two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by the AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="166f3-112">다음 Transact-SQL 명령은 예를 실행하기 위한 필수 구성 요소를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="166f3-112">The following Transact-SQL commands setup these prerequisites for running the examples.</span></span>

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

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="166f3-113">TDE(투명한 데이터 암호화)</span><span class="sxs-lookup"><span data-stu-id="166f3-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="166f3-114">TDE용 데이터베이스 엔진에서 사용할 SQL Server 로그인을 만든 후 자격 증명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="166f3-114">Create a SQL Server login to be used by the Database Engine for TDE, then add the credential to it.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with the asymmetric key
   -- for the Database engine to use when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the TDE Login to add the credential for use by the
   -- Database Engine to access the key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. <span data-ttu-id="166f3-115">TDE에 사용할 데이터베이스 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="166f3-115">Create the database encryption key that will be used for TDE.</span></span>

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the database to enable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a><span data-ttu-id="166f3-116">암호화된 백업</span><span class="sxs-lookup"><span data-stu-id="166f3-116">Encrypted backups</span></span>

1. <span data-ttu-id="166f3-117">백업 암호화용 데이터베이스 엔진에서 사용할 SQL Server 로그인을 만든 후 자격 증명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="166f3-117">Create a SQL Server login to be used by the Database Engine for encrypting backups, and add the credential to it.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with the asymmetric key
   -- for the Database engine to use when it is encrypting the backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the Encrypted Backup Login to add the credential for use by
   -- the Database Engine to access the key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. <span data-ttu-id="166f3-118">키 자격 증명 모음에 저장된 비대칭 키를 사용하여 암호화를 지정하는 데이터베이스를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="166f3-118">Backup the database specifying encryption with the asymmetric key stored in the key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   TO DISK = N'[PATH TO BACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="166f3-119">CLE(열 수준 암호화)</span><span class="sxs-lookup"><span data-stu-id="166f3-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="166f3-120">이 스크립트는 키 자격 증명 모음의 비대칭 키를 통해 보호되는 대칭 키를 만든 후 그 대칭 키를 사용하여 데이터베이스의 데이터를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="166f3-120">This script creates a symmetric key protected by the asymmetric key in the key vault, and then uses the symmetric key to encrypt data in the database.</span></span>

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open the symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close the symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a><span data-ttu-id="166f3-121">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="166f3-121">Additional resources</span></span>

<span data-ttu-id="166f3-122">이러한 암호화 기능을 사용하는 방법에 대한 자세한 내용은 [SQL Server 암호화 기능과 함께 EKM 사용](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="166f3-122">For more information on how to use these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="166f3-123">이 문서의 단계는 Azure 가상 컴퓨터에서 이미 SQL Server가 실행되고 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="166f3-123">Note that the steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="166f3-124">아직 실행하고 있지 않다면 [Azure에서 SQL Server 가상 컴퓨터 프로비전](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="166f3-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="166f3-125">Azure VM에서 SQL Server 실행과 관련된 기타 참고 자료는 [Azure Virtual Machines의 SQL Server 개요](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="166f3-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>