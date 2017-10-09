---
title: "aaaCreate HDInsight 클러스터 데이터 레이크 저장소와 기본 저장소로 PowerShell을 사용 하 여 | Microsoft Docs"
description: "Azure PowerShell toocreate를 사용 하 고 HDInsight 클러스터를 사용 하 여 Azure 데이터 레이크 저장소"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a>PowerShell을 사용하여 Data Lake Store를 기본 저장소로 사용한 HDInsight 클러스터 만들기
> [!div class="op_single_selector"]
> * [Hello Azure 포털을 사용 하 여](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [PowerShell 사용(기본 저장소의 경우)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [PowerShell 사용(추가 저장소의 경우)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Resource Manager 사용](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

기본 저장소로 Azure 데이터 레이크 저장소와 toouse Azure PowerShell tooconfigure Azure HDInsight 클러스터 하는 방법에 대해 알아봅니다. Data Lake Store를 추가 저장소로 사용하여 HDInsight 클러스터를 만드는 방법에 대한 지침은 [Data Lake Store를 추가 저장소로 사용하여 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-powershell.md)를 참조하세요.

Data Lake Store에서 HDInsight를 사용하는 몇 가지 중요한 고려 사항은 다음과 같습니다.

* hello 옵션 toocreate HDInsight 클러스터에 액세스할 수 있는 기본 저장소로 tooData Lake 저장소는 HDInsight 버전 3.5 및 3.6 수 있습니다.

* 기본 저장소는 HDInsight 클러스터를 hello 옵션 toocreate 액세스할 tooData Lake 저장소 *사용할 수 없는* 프리미엄 HDInsight 클러스터에 대 한 합니다.

PowerShell을 사용 하 여 데이터 레이크 저장소와 tooconfigure HDInsight toowork hello 다음 5 개의 섹션에 hello 지침을 따르십시오.

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 hello 요구 사항을 준수를 충족 하는지 확인 합니다.

* **Azure 구독**: 너무 이동[가져오기 Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다.
* **Azure PowerShell 1.0 이상**: 참조 [어떻게 tooinstall PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
* **Windows 소프트웨어 개발 키트 (SDK)**: Windows SDK tooinstall 너무 이동[다운로드 및 Windows 10 용 도구](https://dev.windows.com/en-us/downloads)합니다. hello SDK에 사용 되는 toocreate 보안 인증서입니다.
* **Azure Active Directory 서비스 사용자**:이 자습서에서는 설명 방법을 toocreate Azure Active Directory (Azure AD)에 서비스 사용자입니다. 그러나 toocreate 서비스 사용자 여야 Azure AD 관리자입니다. 관리자 인 경우이 필수 구성이 요소를 건너뛰고 hello 자습서를 진행할 수 있습니다.

    >[!NOTE]
    >Azure AD 관리자인 경우에만 서비스 주체를 만들 수 있습니다. Azure AD 관리자가 서비스 주체를 만들어야 Data Lake Store와 HDInsight 클러스터를 만들 수 있습니다. hello 서비스 사용자에서 만들어야 합니다는 인증서에 설명 된 대로 [인증서로 서비스 사용자를 만들](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)합니다.
    >

## <a name="create-a-data-lake-store-account"></a>Data Lake 저장소 계정 만들기
데이터 레이크 저장소 계정 toocreate 다음 hello지 않습니다.

1. 바탕 화면에서 PowerShell 창을 열고 하 고 아래 hello 조각은 입력 합니다. 사용자가 hello 구독 관리자 또는 소유자 중 하나로 로그인에서 증명된 toosign 합니다. 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > Hello 데이터 레이크 저장소 리소스 공급자를 등록 하 고 다음과 같은 오류가 발생 너무`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, 사용자 구독 데이터 레이크 저장소에 대 한 허용 목록에 없을 수 있습니다. tooenable hello 데이터 레이크 저장소 공개 미리 보기에서는 Azure 구독에 hello 지침에 따라 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다.
    >

2. Data Lake Store 계정은 Azure 리소스 그룹과 연결됩니다. 리소스 그룹을 만들기 시작합니다.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    다음과 유사한 출력이 표시됩니다.

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Data Lake Store 계정을 만듭니다. hello 계정 이름을 지정 하는 유일한 소문자와 숫자만 포함 해야 합니다.

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

4. 기본 저장소로 데이터 레이크 저장소를 사용 하려면 toospecify 루트 경로 toowhich hello 클러스터 관련 파일은 클러스터를 만드는 동안 복사 됩니다. 루트 경로 toocreate **/클러스터/hdiadlcluster** hello 코드 조각에서 cmdlet 뒤 hello를 사용 하 여:

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>역할 기반 인증에 대 한 설정 tooData 레이크 스토어에 액세스
모든 Azure 구독은 Azure AD 엔터티와 연결됩니다. 사용자 및 서비스를 사용 하 여 구독 리소스에 액세스 hello Azure 포털 또는 Azure 리소스 관리자 API hello 먼저 Azure AD에 인증 해야 합니다. 액세스가는 hello Azure 리소스에 적절 한 역할을 지정 하 여 tooAzure 구독 및 서비스 허용 됩니다. 서비스에 대 한 서비스 사용자는 Azure AD에서 hello 서비스를 식별합니다.

이 섹션에서는 HDInsight에 대 한 액세스 tooan Azure 리소스 (hello 앞에서 만든 데이터 레이크 저장소 계정)와 같은 응용 프로그램 toogrant 서비스 방법을 보여 줍니다. 이렇게 하면 서비스 hello 응용 프로그램에 대 한 주 만들고 역할 tooit PowerShell 통해 할당 됩니다.

Azure 데이터 레이크에 대 한 Active Directory 인증을 tooset hello 다음 두 섹션에서에서 hello 작업을 수행 합니다.

### <a name="create-a-self-signed-certificate"></a>자체 서명된 인증서 만들기
있는지 [Windows SDK](https://dev.windows.com/en-us/downloads) 이 섹션의 단계를 hello 계속 하기 전에 설치 합니다. 또한 만들었어야 디렉터리와 같은 *C:\mycertdir*hello 인증서를 만들어야 합니다.

1. Hello PowerShell 창에서 Windows SDK를 설치한 toohello 위치로 이동 합니다 (일반적으로 *C:\Program Files (x86) \Windows Kits\10\bin\x86*) hello를 사용 하 여 [MakeCert] [ makecert] 유틸리티 toocreate 자체 서명 된 인증서와 개인 키입니다. 다음 명령을 사용 하 여 hello:

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    입력 정보 요청된 tooenter hello 개인 키 암호 됩니다. Hello 명령을 성공적으로 실행 된 후 표시 되어야 **CertFile.cer** 및 **mykey.pvk** 지정한 hello 인증서 디렉터리에 있습니다.
2. 사용 하 여 hello [Pvk2Pfx] [ pvk2pfx] 유틸리티 tooconvert hello.pvk와.cer 파일 MakeCert 만든된 tooa.pfx 파일에 해당 합니다. Hello 다음 명령을 실행 합니다.

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    메시지가 표시 되 면 hello 개인 키 암호를 이전에 지정한 입력 합니다. hello에 대 한 사용자가 지정한 값 hello **po** 매개 변수는 hello.pfx 파일을 연관 된 hello 암호입니다. Hello 명령을 성공적으로 완료 된 후 또한 표시는 **CertFile.pfx** 지정한 hello 인증서 디렉터리에 있습니다.

### <a name="create-an-azure-ad-and-a-service-principal"></a>Azure AD 및 서비스 주체 만들기
이 섹션에서는 Azure AD 응용 프로그램에 대 한 서비스 사용자 역할 toohello 서비스 사용자를 할당 만들고 인증서를 제공 하 여 hello 서비스 사용자로 인증 합니다. toocreate hello 다음 명령을 실행 합니다. Azure AD에서 응용 프로그램:

1. Hello를 hello PowerShell 콘솔 창에서 cmdlet 뒤에 붙여 넣습니다. Hello에 대 한 사용자가 지정한 해당 hello 값 확인 **-DisplayName** 속성은 고유 합니다. 에 대 한 값을 hello **-홈 페이지** 및 **-IdentiferUris** 자리 표시자 값 이며 확인 되지 않습니다.

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
3. Hello 서비스 보안 주체 액세스 toohello 데이터 레이크 저장소 루트 및 이전에 지정한 hello 루트 경로에 모든 hello 폴더에 권한을 부여 합니다. Hello 다음 cmdlet을 사용 합니다.

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a>Hello 기본 저장소로 데이터 레이크 저장소 HDInsight Linux 클러스터 만들기

이 섹션에서는 hello 기본 저장소로 데이터 레이크 저장소와 HDInsight Hadoop Linux 클러스터를 만듭니다. 이 릴리스의 경우 HDInsight 클러스터를 hello 및 데이터 레이크 저장소 hello에 있어야 합니다. 동일한 위치입니다.

1. Hello 구독 테 넌 트 ID를 검색 하 고 저장 toouse 나중에 키를 누릅니다.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. Hello 다음 cmdlet을 사용 하 여 hello HDInsight 클러스터를 만듭니다.

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    Hello cmdlet 성공적으로 완료 된 후에 hello 클러스터 세부 정보를 나열 하는 출력을 표시 됩니다.

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a>Hello HDInsight 클러스터 toouse 데이터 레이크 저장소에서 테스트 작업 실행
HDInsight 클러스터를 구성 하 고 나면 tooensure 데이터 레이크 저장소에 액세스할 수 있는지를 테스트 작업이 실행할 수 있습니다. toodo 따라서 실행 샘플 하이브 작업 toocreate에 데이터 레이크 저장소에서 이미 사용할 수 있는 hello 예제 데이터를 사용 하는 테이블  *<cluster root>/example/data/sample.log*합니다.

이 섹션에서는 hello 만든 HDInsight Linux 클러스터에 SSH (보안 셸) 연결을 만들고 샘플 하이브 쿼리를 실행 합니다.

* Windows 클라이언트 toomake hello 클러스터에 대 한 SSH 연결을 사용 하는 경우 참조 [SSH를 Windows에서 HDInsight의 Linux 기반 Hadoop 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)합니다.
* Linux 클라이언트 toomake hello 클러스터에 대 한 SSH 연결을 사용 하는 경우 참조 [SSH Linux에서 HDInsight의 Hadoop Linux 기반를 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)합니다.

1. Hello 연결을 만든 후 다음 명령을 hello를 사용 하 여 hello 하이브 CLI (명령줄 인터페이스)를 시작 합니다.

        hive
2. 다음 문을 toocreate 라는 새 테이블이 사용 하 여 hello CLI tooenter hello **차량** 데이터 레이크 저장소의 hello 예제 데이터를 사용 하 여:

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Hello 쿼리 출력 hello SSH 콘솔에 표시 됩니다.

    >[!NOTE]
    >hello hello CREATE TABLE 명령 앞에 경로 toohello 예제 데이터는 `adl:///example/data/`여기서 `adl:///` hello 클러스터 루트입니다. 이 자습서에 지정 된 hello 클러스터 루트의 hello 예제에서는 다음 hello 명령은 `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`합니다. Hello 더 짧은 대체를 사용 하거나 hello 전체 경로 toohello 클러스터 루트를 제공할 수 있습니다.
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a>HDFS 명령을 사용하여 Data Lake Store에 액세스
Hello HDInsight 클러스터 toouse Data Lake 저장소를 구성 하 고 나면 Hadoop 분산 파일 시스템 (HDFS) 셸 명령을 tooaccess hello 저장소를 사용할 수 있습니다.

이 섹션에서는 hello 만든 HDInsight Linux 클러스터에 대 한 SSH 연결을 확인 하 고 hello HDFS 명령을 실행 합니다.

* Windows 클라이언트 toomake hello 클러스터에 대 한 SSH 연결을 사용 하는 경우 참조 [SSH를 Windows에서 HDInsight의 Linux 기반 Hadoop 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)합니다.
* Linux 클라이언트 toomake hello 클러스터에 대 한 SSH 연결을 사용 하는 경우 참조 [SSH Linux에서 HDInsight의 Hadoop Linux 기반를 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)합니다.

Hello 연결을 완료 한 후 다음 HDFS 파일 시스템 명령을 hello를 사용 하 여 데이터 레이크 저장소의 hello 파일을 나열 합니다.

    hdfs dfs -ls adl:///

Hello를 사용할 수도 있습니다 `hdfs dfs -put` 일부 파일 tooData Lake 저장소 tooupload 명령을 클릭 한 다음 사용 하 여 `hdfs dfs -ls` tooverify hello 파일이 성공적으로 업로드 된 여부.

## <a name="see-also"></a>참고 항목
* [Azure 포털: HDInsight 클러스터 toouse 데이터 레이크 저장소 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
