---
title: "Apache Hive 및 Pig-Azure HDInsight UDF aaaPython | Microsoft Docs"
description: "Azure에서 Python UDF 사용자 정의 함수 ()에서 Hive 및 Pig에서 HDInsight Hadoop 기술 hello toouse 스택 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 26d8160cc6ed7fc22c3f06f7c1c9954c224b2366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a>HDInsight의 Hive 및 Pig에서 Python UDF(사용자 정의 함수) 사용

어떻게 toouse Python 사용자 정의 알아봅니다 Apache Hive 및 Pig Azure HDInsight의 Hadoop에서 사용 하 여 함수 (UDF).

## <a name="python"></a>HDInsight의 Python

Python2.7은 기본적으로 HDInsight 3.0 이상에 설치됩니다. 스트림 처리를 위해 이 버전의 Python에서 Apache Hive를 사용할 수 있습니다. Hive 및 UDF hello 간의 STDOUT 및 STDIN toopass 데이터를 사용 하는 스트림 처리 합니다.

HDInsight에는 Java로 작성된 Python 구현인 Jython도 포함되어 있습니다. Jython은 hello Java 가상 컴퓨터에서 직접 실행 되며 스트리밍을 사용 하지 않습니다. Jython는 hello Pig에서 Python 사용 때 Python 인터프리터를 권장 됩니다.

> [!WARNING]
> 이 문서의 단계 hello hello 가정을 다음을 확인 합니다. 
>
> * Hello Python 스크립트에 만들면 로컬 개발 환경입니다.
> * Hello 중 하나를 사용 하 여 hello 스크립트 tooHDInsight 업로드 `scp` 명령을 로컬 Bash 세션 또는 hello PowerShell 스크립트를 제공 합니다.
>
> Toouse hello를 원하는 경우 [Azure 클라우드 셸 (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) 해야 합니다 toowork HDInsight와 미리 보기:
>
> * Hello 클라우드 셸 환경 내 hello 스크립트를 만듭니다.
> * 사용 하 여 `scp` hello에서 tooupload hello 파일 셸 tooHDInsight 클라우드입니다.
> * 사용 하 여 `ssh` hello 클라우드 셸 tooconnect tooHDInsight 및 실행된 hello 예제에서 합니다.

## <a name="hivepython"></a>Hive UDF

Python hello HiveQL 통해 Hive에서 UDF로 사용할 수 있습니다 `TRANSFORM` 문. HiveQL를 수행 하는 hello hello를 호출 하는 예를 들어 `hiveudf.py` hello 클러스터에 대 한 hello 기본 Azure 저장소 계정에 저장 된 파일입니다.

**Linux 기반 HDInsight**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

**Windows 기반 HDInsight**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> Windows 기반 HDInsight 클러스터에서 hello `USING` hello 전체 경로 toopython.exe 절을 지정 해야 합니다.

다음은 이 예제에서 수행하는 작업입니다.

1. hello `add file` hello 파일의 문 hello 시작 부분에 추가 하는 hello `hiveudf.py` 파일 toohello 분산 캐시를 hello 클러스터의 모든 노드에 액세스할 수 있도록 합니다.
2. hello `SELECT TRANSFORM ... USING` hello에서 데이터를 선택 하는 문을 `hivesampletable`합니다. Hello clientid, devicemake, 및 devicemodel 값 toohello도 전달 `hiveudf.py` 스크립트입니다.
3. hello `AS` 절에서 반환 하는 hello 필드 설명 `hiveudf.py`합니다.

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a>Hello hiveudf.py 파일 만들기


개발 환경에서 `hiveudf.py`라는 텍스트 파일을 만듭니다. Hello 파일의 내용을 hello로 코드를 다음 hello를 사용 합니다.

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

이 스크립트는 hello 다음 작업을 수행 합니다.

1. STDIN에서 데이터 줄을 읽습니다.
2. 사용 하 여 hello 후행 줄 바꿈 문자가 제거 됩니다 `string.strip(line, "\n ")`합니다.
3. 스트림 처리를 수행할 때 한 줄 각 값 사이 탭 문자를 사용 하 여 모든 hello 값을 포함 합니다. 따라서 `string.split(line, "\t")` 사용된 toosplit hello 방금 hello 필드를 반환 합니다. 각 탭에 입력 될 수 있습니다.
4. 처리가 완료 되 면 hello 출력은 각 필드 사이 탭을 한 줄으로 tooSTDOUT 작성 합니다. 예: `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.
5. hello `while` 아니요 될 때까지 루프 반복 `line` 읽혀집니다.

hello 스크립트 출력은 hello에 대 한 입력된 값의 연결을 `devicemake` 및 `devicemodel`, 되었고 hello의 해시 값을 연결 합니다.

참조 [hello 예제 실행](#running) 방법에 대 한 toorun HDInsight 클러스터에서이 예제에서는 합니다.

## <a name="pigpython"></a>Pig UDF

Python 스크립트 hello 통해 Pig에서 UDF로 사용할 수 있습니다 `GENERATE` 문. Jython 또는 C Python 중 하나를 사용 하 여 hello 스크립트를 실행할 수 있습니다.

* Jython은 hello JVM에서 실행 되며 Pig에서 고유 하 게 호출할 수 있습니다.
* C Python 외부 프로세스를 되므로 hello에 hello 데이터로 Pig JVM 전송 되기 toohello 스크립트 Python 프로세스에서 실행 합니다. hello Python 스크립트의 출력을 hello Pig로 다시 전송 됩니다.

toospecify hello Python 인터프리터를 사용 하 여 `register` hello Python 스크립트를 참조 하는 경우. hello 다음 예제에서는 스크립트를 등록으로 Pig `myfuncs`:

* **toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`
* **C Python toouse**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`

> [!IMPORTANT]
> 로컬 경로 또는 WASB hello toohello pig_jython 파일 경로 가능 Jython를 사용할 때는: / / 경로입니다. 그러나 C Python을 사용 하는 경우에 toosubmit hello Pig 작업을 사용 하는 hello 노드의 hello 로컬 파일 시스템에 파일을 참조 해야 합니다.

이 예제에 대 한 hello Pig 라틴 문자, 등록을 지 나 되 면 둘 다에 대해 동일 hello:

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

다음은 이 예제에서 수행하는 작업입니다.

1. hello 샘플 데이터 파일을 로드 하는 첫 번째 줄 hello `sample.log` 에 `LOGS`합니다. 각 레코드를 `chararray`로도 정의합니다.
2. hello 다음 줄에 hello 연산의 hello 결과 저장 하는 모든 null 값을 필터링 `LOG`합니다.
3. Hello 레코드에서 반복 하는 다음으로, `LOG` 사용 하 여 `GENERATE` tooinvoke hello `create_structure` 메서드 hello Python/Jython 스크립트에 포함 된 로드 `myfuncs`합니다. `LINE`사용 되는 toopass hello 현재 레코드 toohello 함수입니다.
4. 마지막으로, hello 출력은 hello를 사용 하 여 덤프 tooSTDOUT `DUMP` 명령입니다. 이 명령은 hello 작업이 완료 된 후 hello 결과 표시 합니다.

### <a name="create-hello-pigudfpy-file"></a>Hello pigudf.py 파일 만들기

개발 환경에서 `pigudf.py`라는 텍스트 파일을 만듭니다. Hello 파일의 내용을 hello로 코드를 다음 hello를 사용 합니다.

<a name="streamingpy"></a>

```python
# Uncomment hello following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

Hello Pig 라틴 예에서 hello 정의 `LINE` hello 입력에 대 한 일관성 있는 스키마가 없습니다 있기 때문에 입력 한 chararray로 합니다. hello 데이터 출력에 대 한 일관성 있는 스키마로 변환 하는 hello Python 스크립트입니다.

1. hello `@outputSchema` 문은 tooPig 반환 되는 hello 데이터의 hello 형식을 정의 합니다. 이 경우 Pig 데이터 형식은 **데이터 모음**입니다. hello 모음 필드는 모두 chararray (문자열)를 수행 하는 hello를 포함 되어 있습니다.

   * 날짜-hello 날짜 hello 로그 항목 생성
   * 시간-hello 로그 항목이 생성 된 hello 시간
   * 응용 프로그램 이름-hello 클래스 이름 hello 항목에 대해 만들어진
   * 수준-hello 로그 수준
   * 세부 정보-hello에 대 한 자세한 정보 로그 항목

2. 다음으로 hello `def create_structure(input)` Pig 품목을 전달 하는 hello 함수를 정의 합니다.

3. 예제 데이터의 경우 hello `sample.log`, 주로 toohello 날짜, 시간, classname, 수준, 준수 및 tooreturn 원하는 스키마에 자세히 설명 합니다. 그러나 `*java.lang.Exception*`으로 시작하는 몇 개의 줄이 포함됩니다. 이 줄에는 수정 된 toomatch hello 스키마 여야 합니다. hello `if` 문은를 검사 한 다음 마사지 hello 입력된 데이터 toomove hello `*java.lang.Exception*` 문자열 toohello 끝나도 hello 데이터와 동일한 줄에 예상된 출력 스키마를 전환 합니다.

4. 다음으로 hello `split` 명령 hello 처음 4 개의 공백 문자가에서 사용 되는 toosplit hello 데이터입니다. hello 출력에 할당 된 `date`, `time`, `classname`, `level`, 및 `detail`합니다.

5. 마지막으로, tooPig hello 값이 반환 됩니다.

Hello에 정의 된 일관성 있는 스키마가 hello 데이터 tooPig 반환 되 면 `@outputSchema` 문.

## <a name="running"></a>업로드 하 고 hello 예 실행

> [!IMPORTANT]
> hello **SSH** 단계는 Linux 기반 HDInsight 클러스터와만 작동 합니다. hello **PowerShell** 단계는 Linux 또는 Windows 기반 HDInsight 클러스터를 사용할 수 없지만 Windows 클라이언트가 필요 합니다.

### <a name="ssh"></a>SSH

SSH를 사용하는 방법에 대한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

1. 사용 하 여 `scp` toocopy hello 파일 tooyour HDInsight 클러스터입니다. 예를 들어 다음 명령을 복사 hello 라는 파일 tooa 클러스터 hello **mycluster**합니다.

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. SSH tooconnect toohello 클러스터를 사용 합니다.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. Hello SSH 세션에서 hello python 파일은 이전에 업로드 hello 클러스터에 대 한 toohello WASB 저장소를 추가 합니다.

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

Hello 파일을 업로드 한 후 사용 하 여 hello 다음 toorun hello Hive 및 Pig 작업 단계입니다.

#### <a name="use-hello-hive-udf"></a>Hello 하이브 UDF를 사용 하 여

1. 사용 하 여 hello `hive` toostart hello 하이브 셸 명령입니다. 표시 됩니다는 `hive>` hello 셸 로드 되 면 메시지를 표시 합니다.

2. 다음 쿼리에서 hello에 hello 입력 `hive>` 프롬프트:

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. Hello 마지막 줄을 입력 한 후 hello 작업을 시작 해야 합니다. Hello 작업이 완료 되 면 다음 예제 출력 유사한 toohello를 반환 합니다.

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a>Hello Pig UDF를 사용 하 여

1. 사용 하 여 hello `pig` toostart hello 셸 명령입니다. 표시는 `grunt>` hello 셸 로드 되 면 메시지를 표시 합니다.

2. 다음 조건에서 hello hello 입력 `grunt>` 프롬프트:

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. Hello 다음 줄을 입력 한 후 hello 작업을 시작 해야 합니다. Hello 작업이 완료 되 면 출력 유사한 toohello를 다음 데이터를 반환 합니다.

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. 사용 하 여 `quit` tooexit Grunt 셸 hello 및 다음 hello 로컬 파일 시스템에 tooedit hello pigudf.py 파일 hello를 사용 하 여:

    ```bash
    nano pigudf.py
    ```

5. 한 번 hello 편집기에서 hello hello를 제거 하 여 다음 줄을 주석 처리 제거 `#` hello 줄의 시작 부분 hello에서에서 문자:

    ```bash
    #from pig_util import outputSchema
    ```

    Hello 변경 된 내용이 되 면 Ctrl + X tooexit hello 편집기를 사용 합니다. Y를 선택한 다음 toosave hello 변경 입력 합니다.

6. 사용 하 여 hello `pig` toostart hello 셸 명령을 다시 합니다. Hello 되 면 `grunt>` hello toorun hello Python 스크립트 hello C Python 인터프리터를 사용 하 여 다음을 사용 하 여, 메시지를 표시 합니다.

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    이 작업이 완료 되 면 동일한 출력 hello Jython를 사용 하 여 hello 스크립트를 이전에 실행으로 표시 됩니다.

### <a name="powershell-upload-hello-files"></a>PowerShell: hello 파일을 업로드

PowerShell tooupload hello 파일 toohello HDInsight 서버를 사용할 수 있습니다. 다음 스크립트 tooupload hello Python 파일이 hello를 사용 합니다.

> [!IMPORTANT] 
> 이 섹션의 단계 hello Azure PowerShell을 사용 합니다. Azure PowerShell을 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
# Change hello path toomatch hello file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

Set-AzureStorageBlobContent `
    -File $pathToStreamingFile `
    -Blob "hiveudf.py" `
    -Container $container `
    -Context $context

Set-AzureStorageBlobContent `
    -File $pathToJythonFile `
    -Blob "pigudf.py" `
    -Container $container `
    -Context $context
```
> [!IMPORTANT]
> 변경 hello `C:\path\to` 개발 환경에서 toohello 경로 toohello 파일 값입니다.

이 스크립트 HDInsight 클러스터에 대 한 정보를 검색 한 다음 hello 계정 및 hello 기본 저장소 계정에 대 한 키를 추출 하 고 업로드 hello hello 컨테이너의 toohello 루트 파일입니다.

> [!NOTE]
> 파일 업로드에 대 한 자세한 내용은 참조 hello [HDInsight에서 Hadoop 작업에 대 한 데이터 업로드](hdinsight-upload-data.md) 문서.

#### <a name="powershell-use-hello-hive-udf"></a>PowerShell: hello 하이브 UDF를 사용 합니다.

PowerShell을 실행 하는 사용 되는 tooremotely 하이브 쿼리 될 수도 있습니다. 다음 PowerShell 스크립트 toorun 사용 하는 하이브 쿼리를 사용 하 여 hello **hiveudf.py** 스크립트:

> [!IMPORTANT]
> 를 실행 하기 전에 hello 스크립트가 hello HDInsight 클러스터에 대 한 HTTPs/Admin 계정 정보를 표시 합니다.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

# If using a Windows-based HDInsight cluster, change hello USING statement to:
# "USING 'D:\Python27\python.exe hiveudf.py' AS " +
$HiveQuery = "add file wasb:///hiveudf.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python hiveudf.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for hello Hive job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

hello에 대 한 출력 hello **하이브** 작업에는 다음 예제와 비슷한 toohello 표시 되어야 합니다.

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a>Pig (Jython)

PowerShell 사용된 toorun Pig 라틴 작업이 될 수도 있습니다. toorun hello를 사용 하는 Pig 라틴 작업 **pigudf.py** 스크립트, PowerShell 스크립트 뒤 hello를 사용 하 여:

> [!NOTE]
> PowerShell을 사용 하는 작업을 원격으로 제출할 때 아닙니다 가능한 toouse C Python 인터프리터 hello로.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

$PigQuery = "Register wasb:///pigudf.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for hello Pig job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

hello에 대 한 출력 hello **Pig** 작업 비슷한 toohello 같은 데이터가 표시 됩니다.

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <a name="troubleshooting"></a>문제 해결

### <a name="errors-when-running-jobs"></a>작업 실행 중 오류 발생

Hello 하이브 작업을 실행할 때 텍스트 다음 오류와 비슷한 toohello를 발생할 수 있습니다.

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

이 문제는 hello Python 파일의 줄 끝에 hello 때문일 수 있습니다. 여러 Windows 편집기를 종료 하는 hello 선으로 toousing CRLF 기본 하지만 Linux 응용 프로그램은 일반적으로 LF을 예상 합니다.

Hello PowerShell 문을 tooremove hello CR 문자 hello 파일 tooHDInsight 업로드 하기 전에 다음을 사용할 수 있습니다.

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a>PowerShell 스크립트

모두 toorun hello 예제 PowerShell 스크립트를 사용 하는 hello 예제 hello 작업에 대 한 오류 출력을 표시 하는 주석 처리 된 줄을 포함 합니다. Hello 작업에 대 한 예상 hello 출력이 표시 되지 않는 경우 주석 처리를 제거 hello 다음 줄을 참조 하는 경우 hello 오류 정보에서 문제가 있음을 나타냅니다.

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

hello 오류 (STDERR) 정보와 hello 작업 (STDOUT)의 hello 결과로 로깅된 tooyour HDInsight 저장 됩니다.

| 이 작업의 경우 | Hello blob 컨테이너에서 이러한 파일을 확인 |
| --- | --- |
| Hive |/HivePython/stderr<p>/HivePython/stdout |
| Pig |/PigPython/stderr<p>/PigPython/stdout |

## <a name="next"></a>다음 단계

기본적으로 제공 되지 않습니다 tooload Python 모듈 필요한 경우 참조 [어떻게 toodeploy 모듈 tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx)합니다.

다른 방법으로 toouse Pig, Hive, 및 toolearn MapReduce 사용에 대 한 hello 다음 문서를 참조 하세요.

* [HDInsight에서 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)
* [HDInsight와 함께 MapReduce 사용](hdinsight-use-mapreduce.md)
