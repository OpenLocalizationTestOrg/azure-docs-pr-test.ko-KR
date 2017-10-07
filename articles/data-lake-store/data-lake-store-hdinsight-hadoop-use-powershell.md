---
제목: aaa "PowerShell: 추가 기능 저장소로 데이터 레이크 저장소와 Azure HDInsight 클러스터 | Microsoft Docs "서비스: 데이터 레이크-저장소, hdinsight documentationcenter: ' 작성자: nitinme 관리자: jhubbard 편집기: cgronlun

ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: 데이터 레이크 저장소 ms.devlang: na ms.topic: article ms.tgt_pltfrm: na ms.workload: 빅 데이터 ms.date: 06/08/2017 ms.author: nitinme

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a>데이터 레이크 저장소와 Azure PowerShell toocreate HDInsight 클러스터를 사용 하 여 (으로 추가 저장소)
> [!div class="op_single_selector"]
> * [포털 사용](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [PowerShell 사용(기본 저장소의 경우)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [PowerShell 사용(추가 저장소의 경우)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Resource Manager 사용](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Azure 데이터 레이크 저장소와 toouse Azure PowerShell tooconfigure HDInsight 클러스터 되는 방법에 대해 알아봅니다 **추가 저장소로**합니다. 기본 저장소로 Azure 데이터 레이크 저장소와 toocreate HDInsight 클러스터 되는 방법에 지침은 [기본 저장소로 데이터 레이크 저장소와 HDInsight 클러스터를 만드는](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)합니다.

> [!NOTE]
> HDInsight 클러스터에 대 한 추가 저장소로 toouse Azure 데이터 레이크 저장소 하려는 경우 이렇게 하는 동안이 문서에 설명 된 대로 hello 클러스터를 만드는 것이 좋습니다. 추가 저장소 tooan로 Azure 데이터 레이크 저장소 추가 기존 HDInsight 클러스터는 복잡 한 프로세스 및 tooerrors 발생 하기 쉽습니다.
>

지원되는 클러스터 유형의 경우 Data Lake Store는 기본 저장소 또는 추가 저장소 계정으로 사용될 수 있습니다. 데이터 레이크 저장소는 추가 저장소로 사용 되는, hello 클러스터에 대 한 기본 저장소 계정 hello 계속 Azure 저장소 Blob (WASB) 이며 hello 클러스터 관련 파일 (예: 로그 등) 동안 hello 데이터 toohello 기본 저장소 계속 기록 했는지 원하는 tooprocess 데이터 레이크 저장소 계정에 저장할 수 있습니다. 데이터 레이크 저장소를 사용 하 여 추가 저장소 계정으로 영향을 주지 않습니다 성능이 나 hello 기능 tooread/쓰기 toohello hello 클러스터에서 저장소입니다.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>HDInsight 클러스터 저장소에서 Data Lake Store 사용

Data Lake Store에서 HDInsight를 사용하는 몇 가지 중요한 고려 사항은 다음과 같습니다.

* 옵션 toocreate HDInsight 클러스터에 액세스할 수 있는 추가 저장소로 tooData Lake 저장소는 HDInsight 버전 3.2, 3.4, 3.5, 및 3.6 수 있습니다.

PowerShell을 사용 하 여 데이터 레이크 저장소와 toowork HDInsight를 구성할 hello 다음 단계를 수행 합니다.

* Azure 데이터 레이크 저장소 만들기
* 역할 기반 인증에 대 한 설정 tooData 레이크 스토어에 액세스
* 인증 tooData Lake 저장소에 HDInsight 클러스터를 만듭니다.
* Hello 클러스터에서 테스트 작업 실행

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure PowerShell 1.0 이상**. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
* **Windows SDK**. [여기](https://dev.windows.com/en-us/downloads)에서 설치할 수 있습니다. 이 toocreate 보안 인증서를 사용 합니다.
* **Azure Active Directory 서비스 사용자**. 이 자습서의 단계는 방법에 지침을 제공 toocreate Azure AD에서 서비스 사용자입니다. 그러나는 Azure AD 관리자 toobe 수 toocreate 서비스 사용자 여야 합니다. Azure AD 관리자 인 경우이 필수 구성이 요소를 건너뛰고 hello 자습서를 진행할 수 있습니다.

    **Azure AD 관리자가 아닌 경우**, 수 tooperform hello 단계 필요한 toocreate 서비스 사용자 됩니다. 이 경우 먼저 Azure AD 관리자가 서비스 사용자를 만들어야 Data Lake Store와 HDInsight 클러스터를 만들 수 있습니다. 또한 hello 서비스 사용자 사용 하 여 만들어야는 인증서에 설명 된 대로 [인증서로 서비스 사용자를 만들](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)합니다.

## <a name="create-an-azure-data-lake-store"></a>Azure 데이터 레이크 저장소 만들기
이러한 단계 toocreate 데이터 레이크 저장소를 따릅니다.

1. 바탕 화면에서 새 Azure PowerShell 창을 열고 다음 코드 조각 hello를 입력 합니다. , 입력 정보 요청된 toolog 있는지 확인 하는 경우 로그인 할 hello 구독 관리자/소유자 중 하나로:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > 너무 유사한 오류가 나타나면`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` 구독이 허용 목록 Azure 데이터 레이크 저장소에 있지 않기 수 있기 hello 데이터 레이크 저장소 리소스 공급자를 등록할 때. 이 [지침](data-lake-store-get-started-portal.md)에 따라 Data Lake 저장소 공개 미리 보기에 대한 Azure 구독을 활성화해야 합니다.
   >
   >
2. Azure 데이터 레이크 저장소 계정은 Azure 리소스 그룹과 연결됩니다. Azure 리소스 그룹을 만드는 작업부터 시작합니다.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    다음과 유사한 출력이 표시됩니다.

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Azure 데이터 레이크 저장소 계정을 만듭니다. 지정한 이름은 소문자와 숫자만 포함 해야 하는 hello 계정입니다.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    Hello 다음과 같은 출력을 표시 되어야 합니다.

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. 데이터 레이크 몇 가지 샘플 데이터 tooAzure 업로드 합니다. 이 문서 tooverify hello 데이터는 HDInsight 클러스터에서 액세스할 수 있는 뒷부분에 나오는이 사용 합니다. 몇 가지 샘플 데이터 tooupload를 찾고 hello를 얻을 수 있습니다 **Ambulance 데이터** hello 폴더 [Azure 데이터 레이크 Git 리포지토리](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)합니다.

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>역할 기반 인증에 대 한 설정 tooData 레이크 스토어에 액세스
모든 Azure 구독은 Azure Active Directory와 연결됩니다. 사용자 및 서비스의 hello Azure 클래식 포털 또는 Azure 리소스 관리자 API를 사용 하 여 hello 구독 리소스에 액세스 하는 먼저 해당 Azure Active Directory에 인증 해야 합니다. 액세스가는 hello Azure 리소스에 적절 한 역할을 지정 하 여 tooAzure 구독 및 서비스 허용 됩니다.  서비스에 대 한 서비스 사용자는 Azure Active Directory (AAD) hello에 hello 서비스를 식별합니다. 이 섹션에서는 HDInsight에 대 한 액세스 tooan Azure 리소스 (hello 이전에 만든 Azure 데이터 레이크 저장소 계정)와 같은 응용 프로그램 toogrant 서비스 어떻게 hello 응용 프로그램에 대 한 서비스 사용자를 만들고 Azure 통해 역할 toothat 할당 하 여 PowerShell입니다.

Azure 데이터 레이크에 대 한 Active Directory 인증을 tooset, hello 다음 작업을 수행 해야 합니다.

* 자체 서명된 인증서 만들기
* Azure Active Directory 및 서비스 주체의 응용 프로그램 만들기

### <a name="create-a-self-signed-certificate"></a>자체 서명된 인증서 만들기
있는지 [Windows SDK](https://dev.windows.com/en-us/downloads) 이 섹션의 단계를 hello 계속 하기 전에 설치 합니다. 또한 만들었어야 디렉터리와 같은 **C:\mycertdir**, hello 인증서를 만들어야 합니다.

1. Hello PowerShell 창에서 Windows SDK를 설치한 toohello 위치로 이동 합니다 (일반적으로 `C:\Program Files (x86)\Windows Kits\10\bin\x86` hello를 사용 하 여 [MakeCert] [ makecert] 유틸리티 toocreate 자체 서명 된 인증서와 개인 키입니다. 다음 명령을 hello를 사용 합니다.

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    입력 정보 요청된 tooenter hello 개인 키 암호 됩니다. 실행 된 후 hello 명령을 성공적으로 표시 됩니다는 **CertFile.cer** 및 **mykey.pvk** 지정한 hello 인증서 디렉터리에 있습니다.
2. 사용 하 여 hello [Pvk2Pfx] [ pvk2pfx] 유틸리티 tooconvert hello.pvk와.cer 파일 MakeCert 만든된 tooa.pfx 파일에 해당 합니다. Hello 다음 명령을 실행 합니다.

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    메시지가 표시 되 면 이전에 지정한 hello 개인 키 암호를 입력 합니다. hello에 대 한 사용자가 지정한 값 hello **po** 매개 변수는 hello 암호 hello.pfx 파일과 연결 된입니다. Hello 명령이 성공적으로 완료 된 후 지정한 hello 인증서 디렉터리에서 CertFile.pfx 나타납니다.

### <a name="create-an-azure-active-directory-and-a-service-principal"></a>Azure Active Directory 및 서비스 주체 만들기
Azure Active Directory 응용 프로그램에 대 한 hello 단계 toocreate 서비스 사용자를 수행이 섹션에서는 역할 toohello 서비스 사용자를 할당 한 인증서를 제공 하 여 hello 서비스 사용자로 인증 합니다. Azure Active Directory에서 다음 명령을 toocreate hello 응용 프로그램을 실행 합니다.

1. Hello를 hello PowerShell 콘솔 창에서 cmdlet 뒤에 붙여 넣습니다. Hello에 대 한 지정 hello 값이 있는지 확인 **-DisplayName** 속성은 고유 합니다. 또한에 대 한 값을 hello **-홈 페이지** 및 **-IdentiferUris** 자리 표시자 값 이며 확인 되지 않습니다.

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. Hello 응용 프로그램 ID를 사용 하 여 서비스 사용자 만들기

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Hello 서비스 보안 주체 액세스 toohello Data Lake 저장소 폴더와 hello 파일 hello HDInsight 클러스터에서 액세스할 수 있는 권한을 부여 합니다. 아래 hello 조각 hello 데이터 레이크 저장소 (복사한 hello 예제 데이터 파일), 계정 및 hello 파일 자체의 toohello 루트 액세스를 제공 합니다.

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a>Data Lake Store를 추가 저장소로 사용하여 HDInsight 클러스터 만들기

이 섹션에서는 Data Lake Store를 추가 저장소로 사용하여 HDInsight 클러스터를 만듭니다. 이 릴리스에 대 한 hello HDInsight 클러스터와 hello Data Lake 저장소에에서 있어야 hello 동일한 위치입니다.

1. Hello 구독 테 넌 트 id입니다. 검색 시작 나중에 필요합니다.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. 이 릴리스의 Hadoop 클러스터에 대 한 데이터 레이크 저장소만 사용할 수 추가 저장소로 hello 클러스터에 대 한 합니다. hello 기본 저장소 (WASB) hello Azure 저장소 blob을 수 있습니다. 따라서 먼저 만들겠습니다 hello hello 클러스터에 필요한 저장소 계정 및 저장소 컨테이너.

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. Hello HDInsight 클러스터를 만듭니다. Hello 다음 cmdlet을 사용 합니다.

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    Hello cmdlet이 성공적으로 완료 된 후 hello 클러스터 세부 정보를 나열 하는 출력을 표시 되어야 합니다.


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Hello HDInsight 클러스터 toouse hello 데이터 레이크 저장소에서 테스트 작업 실행
HDInsight 클러스터를 구성 하 고 나면에서 실행할 수 있습니다 테스트 작업이 hello 클러스터 tootest 해당 hello HDInsight 클러스터 Data Lake 저장소에 액세스할 수 있습니다. toodo, 이전 tooyour 데이터 레이크 저장소를 업로드 하는 hello 샘플 데이터를 사용 하 여 테이블을 만드는 예제 Hive 작업을 수행 됩니다.

이 섹션에서 HDInsight Linux 클러스터 만들고 hello 샘플 Hive 쿼리를 실행 하는 hello에 SSH 됩니다.

* Windows 클라이언트 tooSSH hello 클러스터를 사용 하는 경우 참조 [SSH를 Windows에서 HDInsight의 Linux 기반 Hadoop 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)합니다.
* Linux 클라이언트 tooSSH hello 클러스터를 사용 하는 경우 참조 [SSH Linux에서 HDInsight의 Hadoop Linux 기반를 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

1. 연결 되 면 다음 명령을 hello를 사용 하 여 hello 하이브 CLI를 시작 합니다.

        hive
2. Hello CLI를 사용 하 여 hello 문을 toocreate 라는 새 테이블을 다음 입력 **차량** hello 데이터 레이크 저장소의에서 hello 예제 데이터를 사용 하 여:

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    출력 유사한 toohello 다음을 나타나야 합니다.

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a>HDFS 명령을 사용한 액세스 데이터 레이크 저장소
Hello HDInsight 클러스터 toouse Data Lake 저장소를 구성한 후에 hello HDFS 셸 명령을 tooaccess hello 저장소를 사용할 수 있습니다.

이 섹션에서 HDInsight Linux 클러스터 만들고 hello HDFS 명령을 실행 하는 hello에 SSH 됩니다.

* Windows 클라이언트 tooSSH hello 클러스터를 사용 하는 경우 참조 [SSH를 Windows에서 HDInsight의 Linux 기반 Hadoop 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)합니다.
* Linux 클라이언트 tooSSH hello 클러스터를 사용 하는 경우 참조 [SSH Linux에서 HDInsight의 Hadoop Linux 기반를 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

연결 되 면 hello Data Lake 저장소에 있는 HDFS 파일 시스템 명령 toolist hello 파일을 다음 hello를 사용 합니다.

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

이전 toohello 데이터 레이크 저장소를 업로드 하는 hello 파일을 나열 됩니다.

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

Hello를 사용할 수도 있습니다 `hdfs dfs -put` 일부 파일 toohello 데이터 레이크 저장소 tooupload 명령을 클릭 한 다음 사용 하 여 `hdfs dfs -ls` tooverify hello 파일이 성공적으로 업로드 된 여부.

## <a name="see-also"></a>참고 항목
* [HDInsight 클러스터 toouse Data Lake 저장소를 만듭니다 포털:](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
