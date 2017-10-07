---
title: "Hadoop-Microsoft Avro Library-Azure의 데이터를 aaaSerialize | Microsoft Docs"
description: "자세한 내용은 방법 tooserialize hello Microsoft Avro Library toopersist toomemory, 데이터베이스 또는 파일을 사용 하 여 HDInsight의 Hadoop에서 데이터를 deserialize 합니다."
keywords: avro,hadoop avro
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: f364f8e855a54c0fc160e9a106ec8d5b30c6db23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a><span data-ttu-id="9fb2a-104">Hello Microsoft Avro Library를 사용 하 여 Hadoop에서 데이터를 serialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-104">Serialize data in Hadoop with hello Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="9fb2a-105">hello Avro SDK는 더 이상 Microsoft에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-105">hello Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="9fb2a-106">hello 라이브러리는 오픈 소스 커뮤니티를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-106">hello library is open source community supported.</span></span> <span data-ttu-id="9fb2a-107">hello 라이브러리에 대 한 hello 소스에 살고 있는 [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro)합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-107">hello sources for hello library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="9fb2a-108">이 항목에서는 방법을 toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize 개체 및 기타 데이터 구조 스트림 toopersist에 이러한 toomemory, 데이터베이스나 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-108">This topic shows how toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objects and other data structures into streams toopersist them toomemory, a database, or a file.</span></span> <span data-ttu-id="9fb2a-109">또한 표시 방법을 toodeserialize toorecover hello 원래 개체에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-109">It also shows how toodeserialize them toorecover hello original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="9fb2a-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="9fb2a-110">Apache Avro</span></span>
<span data-ttu-id="9fb2a-111">hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> 구현 hello hello Microsoft.NET 환경에 대 한 Apache Avro 데이터 직렬화 시스템이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-111">hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements hello Apache Avro data serialization system for hello Microsoft.NET environment.</span></span> <span data-ttu-id="9fb2a-112">Apache Avro는 직렬화를 위한 압축 이진 데이터 교환 형식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="9fb2a-113">사용 하 여 <a href="http://www.json.org" target="_blank">JSON</a> toodefine 언어 간 상호 운용성 underwrites 하는 언어를 알 수 없는 스키마.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> toodefine a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="9fb2a-114">한 언어로 직렬화된 데이터는 다른 언어로 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="9fb2a-115">현재 C, C++, C#, Java, PHP, Python 및 Ruby가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="9fb2a-116">Hello에서 hello 형식에 대 한 자세한 정보를 찾을 수 있습니다 <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro 사양</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-116">Detailed information on hello format can be found in hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="9fb2a-117">Microsoft Avro Library hello hello 원격 프로시저 호출 (Rpc)이이 사양에 포함을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-117">hello Microsoft Avro Library does not support hello remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="9fb2a-118">hello Avro 시스템에에서 있는 개체의 직렬화 된 hello 표현을 두 부분으로 이루어져: 스키마 및 실제 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-118">hello serialized representation of an object in hello Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="9fb2a-119">hello Avro 스키마 JSON 사용 하 여 hello serialize 된 데이터의 hello 언어에 관계 없이 데이터 모델을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-119">hello Avro schema describes hello language-independent data model of hello serialized data with JSON.</span></span> <span data-ttu-id="9fb2a-120">이 스키마는 데이터의 이진 표현 옆에 나란히 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="9fb2a-121">Serialization 빠르고 고 만드는 hello 표현 작은 없는 값 당 오버 헤드로 작성 된 각 개체 toobe를 허용 hello 이진 표현에서 별도 hello 스키마 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-121">Having hello schema separate from hello binary representation permits each object toobe written with no per-value overheads, making serialization fast, and hello representation small.</span></span>

## <a name="hello-hadoop-scenario"></a><span data-ttu-id="9fb2a-122">hello Hadoop 시나리오</span><span class="sxs-lookup"><span data-stu-id="9fb2a-122">hello Hadoop scenario</span></span>
<span data-ttu-id="9fb2a-123">hello Apache Avro 직렬화 형식은 Azure HDInsight 및 기타 Apache Hadoop 환경에서 널리 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-123">hello Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="9fb2a-124">Avro 편리 toorepresent Hadoop MapReduce 작업 내에서 복잡 한 데이터 구조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-124">Avro provides a convenient way toorepresent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="9fb2a-125">Avro 파일 (Avro 개체 컨테이너 파일)의 hello 형식이 toosupport 설계 된 distributed hello MapReduce 프로그래밍 모델 선택 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-125">hello format of Avro files (Avro object container file) has been designed toosupport hello distributed MapReduce programming model.</span></span> <span data-ttu-id="9fb2a-126">hello 키 hello 배포를 지원 기능은 hello 파일은 "분할 가능한" hello 관점 하나 수 파일의 모든 지점 검색을 특정 블록에서 읽기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-126">hello key feature that enables hello distribution is that hello files are “splittable” in hello sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="9fb2a-127">Avro 라이브러리의 직렬화</span><span class="sxs-lookup"><span data-stu-id="9fb2a-127">Serialization in Avro Library</span></span>
<span data-ttu-id="9fb2a-128">hello Avro 용.NET 라이브러리는 직렬화 된 개체의 두 가지 방법으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-128">hello .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="9fb2a-129">**리플렉션** -hello 형식에 대 한 JSON 스키마 hello 자동으로 데이터에서 작성 되 hello hello.NET 형식 toobe 직렬화의 계약 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-129">**reflection** - hello JSON schema for hello types is automatically built from hello data contract attributes of hello .NET types toobe serialized.</span></span>
* <span data-ttu-id="9fb2a-130">**제네릭 레코드** -hello 나타내는 레코드에는 JSON 스키마를 명시적으로 지정 [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) 없는.NET 유형은 데이터 toobe hello에 대 한 현재 toodescribe hello 스키마 클래스 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-130">**generic record** - A JSON schema is explicitly specified in a record represented by hello [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present toodescribe hello schema for hello data toobe serialized.</span></span>

<span data-ttu-id="9fb2a-131">Hello 데이터 스키마 tooboth hello 기록기 스레드와 판독기 hello 스트림의 알려져, 있는 경우 해당 스키마 없이 hello 데이터를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-131">When hello data schema is known tooboth hello writer and reader of hello stream, hello data can be sent without its schema.</span></span> <span data-ttu-id="9fb2a-132">경우 Avro 개체 컨테이너 파일을 사용 하는 경우 hello 스키마 hello 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-132">In cases when an Avro object container file is used, hello schema is stored within hello file.</span></span> <span data-ttu-id="9fb2a-133">데이터 압축에 사용 되는 hello 코덱 등의 기타 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-133">Other parameters, such as hello codec used for data compression, can be specified.</span></span> <span data-ttu-id="9fb2a-134">이러한 시나리오는 자세히 설명 된 되며 hello 다음 코드 예제에에서 나와 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-134">These scenarios are outlined in more detail and illustrated in hello following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="9fb2a-135">Avro 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="9fb2a-135">Install Avro Library</span></span>
<span data-ttu-id="9fb2a-136">hello 라이브러리를 설치 하기 전에 hello 다음 요소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-136">hello following are required before you install hello library:</span></span>

* <span data-ttu-id="9fb2a-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="9fb2a-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="9fb2a-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a>(6.0.4 이상)</span><span class="sxs-lookup"><span data-stu-id="9fb2a-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="9fb2a-139">Note 해당 hello Newtonsoft.Json.dll 종속성 hello Microsoft Avro Library의 hello 설치와 함께 자동으로 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-139">Note that hello Newtonsoft.Json.dll dependency is downloaded automatically with hello installation of hello Microsoft Avro Library.</span></span> <span data-ttu-id="9fb2a-140">hello 프로시저 hello 다음 섹션에서에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-140">hello procedure is provided in hello following section:</span></span>

<span data-ttu-id="9fb2a-141">Microsoft Avro Library hello 절차를 수행 하는 hello를 통해 Visual Studio에서 설치할 수 있는 NuGet 패키지로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-141">hello Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via hello following procedure:</span></span>

1. <span data-ttu-id="9fb2a-142">선택 hello **프로젝트** 탭 **NuGet 패키지 관리...**</span><span class="sxs-lookup"><span data-stu-id="9fb2a-142">Select hello **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="9fb2a-143">Hello에 "Microsoft.Hadoop.Avro"에 대 한 검색 **온라인 검색** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-143">Search for "Microsoft.Hadoop.Avro" in hello **Search Online** box.</span></span>
3. <span data-ttu-id="9fb2a-144">Hello 클릭 **설치** 너무 단추 옆**Microsoft Azure HDInsight Avro Library**합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-144">Click hello **Install** button next too**Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="9fb2a-145">해당 hello Newtonsoft.Json.dll 참고 (> = 6.0.4) 종속성은 Microsoft Avro Library hello로 자동으로 다운로드도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-145">Note that hello Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with hello Microsoft Avro Library.</span></span>

<span data-ttu-id="9fb2a-146">hello Microsoft Avro Library 소스 코드에서 사용할 수는 [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro)합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-146">hello Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="9fb2a-147">Avro 라이브러리를 사용하여 스키마 컴파일</span><span class="sxs-lookup"><span data-stu-id="9fb2a-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="9fb2a-148">Microsoft Avro Library hello C# 형식 hello에 따라 자동으로 만들 수 있는 유틸리티에 대 한 JSON 스키마 이전에 정의 된 코드 생성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-148">hello Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on hello previously defined JSON schema.</span></span> <span data-ttu-id="9fb2a-149">hello 코드 생성 유틸리티 실행 파일은 이진 배포 되지 않는 하지만 절차를 수행 하는 hello를 통해 쉽게 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-149">hello code generation utility is not distributed as a binary executable, but can be easily built via hello following procedure:</span></span>

1. <span data-ttu-id="9fb2a-150">Hello에서 HDInsight SDK 소스 코드의 최신 버전으로 hello.zip 파일을 다운로드 <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft.NET SDK에 대 한 Hadoop</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-150">Download hello .zip file with hello latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="9fb2a-151">(Hello 클릭 **다운로드** 아이콘, 하지 hello **다운로드** 탭 합니다.)</span><span class="sxs-lookup"><span data-stu-id="9fb2a-151">(Click hello **Download** icon, not hello **Downloads** tab.)</span></span>
2. <span data-ttu-id="9fb2a-152">Hello HDInsight SDK tooa 디렉터리.NET Framework 4를 사용 하 여 hello 컴퓨터에 설치 하 고 필요한 종속성 NuGet 패키지를 다운로드 하기 위한 toohello 인터넷 연결을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-152">Extract hello HDInsight SDK tooa directory on hello machine with .NET Framework 4 installed and connected toohello Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="9fb2a-153">아래 hello 소스 코드는 추출 된 tooC:\SDK 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-153">Below, we assume that hello source code is extracted tooC:\SDK.</span></span>
3. <span data-ttu-id="9fb2a-154">Toohello 폴더 C:\SDK\src\Microsoft.Hadoop.Avro.Tools 이동한 다음 build.bat를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-154">Go toohello folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="9fb2a-155">(hello 파일 MSBuild의에서 호출 hello.NET Framework의 hello 32 비트 분포입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-155">(hello file calls MSBuild from hello 32-bit distribution of hello .NET Framework.</span></span> <span data-ttu-id="9fb2a-156">Toouse hello 64 비트 버전을 원하는 hello 파일 안에 hello 주석을 다음 build.bat 편집 합니다.) Hello 빌드 성공 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-156">If you would like toouse hello 64-bit version, edit build.bat, following hello comments inside hello file.) Ensure that hello build is successful.</span></span> <span data-ttu-id="9fb2a-157">(일부 시스템에서는 MSBuild로 인해 경고가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="9fb2a-158">이러한 경고 영향을 주지 않습니다 hello 유틸리티도 빌드 오류가 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="9fb2a-158">These warnings do not affect hello utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="9fb2a-159">컴파일된 hello 유틸리티는 C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-159">hello compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="9fb2a-160">hello 명령줄 구문에 잘 알고 tooget hello hello 코드 생성 유틸리티 위치한 hello 폴더에서 다음 명령을 실행 합니다.`Microsoft.Hadoop.Avro.Tools help /c:codegen`</span><span class="sxs-lookup"><span data-stu-id="9fb2a-160">tooget familiar with hello command-line syntax, execute hello following command from hello folder where hello code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="9fb2a-161">tootest hello 유틸리티 hello 소스 코드와 함께 제공 하는 hello 샘플 JSON 스키마 파일에서 C# 클래스를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-161">tootest hello utility, you can generate C# classes from hello sample JSON schema file provided with hello source code.</span></span> <span data-ttu-id="9fb2a-162">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-162">Execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="9fb2a-163">Tooproduce 두 개의 C# 파일 hello 현재 디렉터리에 있어야이: SensorData.cs 및 Location.cs 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-163">This is supposed tooproduce two C# files in hello current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="9fb2a-164">hello JSON 스키마 tooC # 형식을 변환 하는 동안 hello 코드 생성 유틸리티를 사용 하는 toounderstand hello 논리 GenerationVerification.feature C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc에 있는 hello 파일을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-164">toounderstand hello logic that hello code generation utility is using while converting hello JSON schema tooC# types, see hello file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="9fb2a-165">네임 스페이스는 hello 이전 단락에서 설명한 hello 파일에 설명 된 hello 논리를 사용 하 여 hello JSON 스키마에서 추출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-165">Namespaces are extracted from hello JSON schema, using hello logic described in hello file mentioned in hello previous paragraph.</span></span> <span data-ttu-id="9fb2a-166">Hello 스키마에서 추출 된 네임 스페이스 우선 무엇이 든 hello 유틸리티 명령줄에서 hello /n 매개 변수와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-166">Namespaces extracted from hello schema take precedence over whatever is provided with hello /n parameter in hello utility command line.</span></span> <span data-ttu-id="9fb2a-167">Toooverride hello hello 스키마 내에 포함 된 네임 스페이스를 원하는 hello 없음 /nf 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-167">If you want toooverride hello namespaces contained within hello schema, use hello /nf parameter.</span></span> <span data-ttu-id="9fb2a-168">모든 네임 스페이스 hello SampleJSONSchema.avsc toomy.own.nspace에서 실행 하는 toochange 예를 들어 다음 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="9fb2a-168">For example, toochange all namespaces from hello SampleJSONSchema.avsc toomy.own.nspace, execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a><span data-ttu-id="9fb2a-169">Hello 예제에 대 한</span><span class="sxs-lookup"><span data-stu-id="9fb2a-169">About hello samples</span></span>
<span data-ttu-id="9fb2a-170">이 항목에서 제공 하는 6 개의 예제 hello Microsoft Avro Library에서 지 원하는 다양 한 시나리오를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-170">Six examples provided in this topic illustrate different scenarios supported by hello Microsoft Avro Library.</span></span> <span data-ttu-id="9fb2a-171">Microsoft Avro Library hello 모든 스트림 사용 하 여 디자인 된 toowork입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-171">hello Microsoft Avro Library is designed toowork with any stream.</span></span> <span data-ttu-id="9fb2a-172">이러한 예에서는 간편성과 일관성을 위해 데이터가 파일 스트림이나 데이터베이스가 아닌 메모리 스트림을 사용하여 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="9fb2a-173">프로덕션 환경에서 사용 하는 hello 접근 방식 hello 정확한 시나리오 요구 사항, 데이터 원본 및 볼륨, 성능 제약 조건 및 기타 요인에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-173">hello approach taken in a production environment depends on hello exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="9fb2a-174">첫 번째 두 예제에서는 표시를 어떻게 hello tooserialize 리플렉션 및 제네릭 레코드를 사용 하 여 메모리 스트림 버퍼에 데이터를 deserialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-174">hello first two examples show how tooserialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="9fb2a-175">hello이 두 가지 경우에는 스키마 가정 toobe hello 판독기와 작성기 간에 공유 대역폭을 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-175">hello schema in these two cases is assumed toobe shared between hello readers and writers out-of-band.</span></span>

<span data-ttu-id="9fb2a-176">hello 세 번째와 네 번째 예제에서는 보여 어떻게 tooserialize hello Avro 개체 컨테이너 파일을 사용 하 여 데이터를 deserialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-176">hello third and fourth examples show how tooserialize and deserialize data by using hello Avro object container files.</span></span> <span data-ttu-id="9fb2a-177">Avro 컨테이너 파일에 데이터가 저장 되는 경우 해당 스키마 deserialization에 대 한 hello 스키마를 공유 해야 하기 때문에 항상 함께 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-177">When data is stored in an Avro container file, its schema is always stored with it because hello schema must be shared for deserialization.</span></span>

<span data-ttu-id="9fb2a-178">hello이 포함 된 샘플 hello 첫 4 개 hello에서 예제를 다운로드할 수 있습니다 <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure 코드 예제의</a> 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-178">hello sample containing hello first four examples can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="9fb2a-179">다섯 번째 예제와 hello 방법을 toouse Avro에 대 한 사용자 지정 압축 코덱을 개체 컨테이너 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-179">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="9fb2a-180">이 예제는 hello에서 다운로드할 수 있습니다에 대 한 hello 코드를 포함 하는 샘플 <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure 코드 예제의</a> 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-180">A sample containing hello code for this example can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="9fb2a-181">hello 여섯 번째 샘플 toouse Avro serialization tooupload 데이터 tooAzure이 Blob 저장소 하 고 다음 하이브 (Hadoop) HDInsight 클러스터를 사용 하 여 분석 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-181">hello sixth sample shows how toouse Avro serialization tooupload data tooAzure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="9fb2a-182">Hello에서 다운로드할 수 있습니다 <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure 코드 예제의</a> 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-182">It can be downloaded from hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="9fb2a-183">다음 링크를 toohello hello 항목에서에서 설명 하는 6 개의 샘플은:</span><span class="sxs-lookup"><span data-stu-id="9fb2a-183">Here are links toohello six samples discussed in hello topic:</span></span>

* <span data-ttu-id="9fb2a-184"><a href="#Scenario1">**리플렉션 사용 하 여 serialization** </a> -계약 특성 형식 toobe 직렬화에 대 한 JSON 스키마 hello는 자동으로 hello 데이터에서 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-184"><a href="#Scenario1">**Serialization with reflection**</a> - hello JSON schema for types toobe serialized is automatically built from hello data contract attributes.</span></span>
* <span data-ttu-id="9fb2a-185"><a href="#Scenario2">**제네릭 레코드와 serialization** </a> -리플렉션에 사용할 수 있는.NET 유형이 없는 경우 레코드에 명시적으로 hello JSON 스키마가 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-185"><a href="#Scenario2">**Serialization with generic record**</a> - hello JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="9fb2a-186"><a href="#Scenario3">**리플렉션을 사용 하 여 개체 컨테이너 파일을 사용 하 여 직렬화** </a> -hello JSON 스키마가 자동으로 빌드되고 Avro 개체 컨테이너 파일을 통해 hello serialize 된 데이터와 함께 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - hello JSON schema is automatically built and shared together with hello serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="9fb2a-187"><a href="#Scenario4">**제네릭 레코드와 개체 컨테이너 파일을 사용 하 여 직렬화** </a> -hello JSON 스키마를 명시적으로 hello serialization 전에 지정 하 고 Avro 개체 컨테이너 파일을 통해 hello 데이터와 함께 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - hello JSON schema is explicitly specified before hello serialization and shared together with hello data via an Avro object container file.</span></span>
* <span data-ttu-id="9fb2a-188"><a href="#Scenario5">**사용자 지정 압축 코덱을 사용 하 여 개체 컨테이너 파일을 사용 하 여 직렬화** </a> -hello 예제는 Avro toocreate hello Deflate 데이터 압축 코덱의 사용자 지정된.NET 구현으로 컨테이너 파일 개체 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - hello example shows how toocreate an Avro object container file with a customized .NET implementation of hello Deflate data compression codec.</span></span>
* <span data-ttu-id="9fb2a-189"><a href="#Scenario6">**Avro tooupload 데이터를 사용 하 여 Microsoft Azure HDInsight 서비스 hello에 대 한** </a> -hello 예제 Avro serialization hello HDInsight 서비스와 상호 작용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-189"><a href="#Scenario6">**Using Avro tooupload data for hello Microsoft Azure HDInsight service**</a> - hello example illustrates how Avro serialization interacts with hello HDInsight service.</span></span> <span data-ttu-id="9fb2a-190">현재 Azure 구독 및 액세스 tooan Azure HDInsight 클러스터는이 예제에서는 toorun를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-190">An active Azure subscription and access tooan Azure HDInsight cluster are required toorun this example.</span></span>

## <span data-ttu-id="9fb2a-191"><a name="Scenario1"></a>샘플 1: 리플렉션을 사용한 직렬화</span><span class="sxs-lookup"><span data-stu-id="9fb2a-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="9fb2a-192">hello 형식에 대 한 JSON 스키마 hello 자동으로 여 빌드할 수 있습니다 hello 데이터에서 리플렉션을 통해 Microsoft Avro Library hello hello C# 개체 toobe 직렬화의 계약 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-192">hello JSON schema for hello types can be automatically built by hello Microsoft Avro Library via reflection from hello data contract attributes of hello C# objects toobe serialized.</span></span> <span data-ttu-id="9fb2a-193">hello Microsoft Avro Library 만듭니다는 [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello 필드 toobe 직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-193">hello Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello fields toobe serialized.</span></span>

<span data-ttu-id="9fb2a-194">이 예제에서는 개체 (한 **SensorData** 클래스 멤버와 **위치** 구조체) 직렬화 된 tooa 메모리 스트림이 되며이 스트림을 다시 deserialize 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized tooa memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="9fb2a-195">hello 결과 초기 비교 toohello 인스턴스 tooconfirm 해당 hello 다음 **SensorData** 복구 하는 개체는 원래 동일 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-195">hello result is then compared toohello initial instance tooconfirm that hello **SensorData** object recovered is identical toohello original.</span></span>

<span data-ttu-id="9fb2a-196">이 예에서 hello 스키마 hello Avro 개체 컨테이너 형식이 필요 하지 않도록 hello 판독기와 기록기, 공유 toobe를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-196">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="9fb2a-197">방법의 예에 대 한 tooserialize 데이터를 deserialize 하 고 hello 스키마 hello 데이터와 공유 해야 하는 경우 hello 개체 컨테이너 형식으로 리플렉션을 사용 하 여 메모리 버퍼로 참조 <a href="#Scenario3">리플렉션을사용하여개체컨테이너파일을사용하여직렬화</a>.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-197">For an example of how tooserialize and deserialize data into memory buffers by using reflection with hello object container format when hello schema must be shared with hello data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize hello data toohello specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from hello stream and cast it toohello same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches hello original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization toomemory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="9fb2a-198">샘플 2: 제네릭 레코드로 직렬화</span><span class="sxs-lookup"><span data-stu-id="9fb2a-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="9fb2a-199">리플렉션 데이터 계약을 사용 하 여.NET 클래스를 통해 hello 데이터를 표현할 수 없기 때문에 사용할 수 없는 경우 JSON 스키마 제네릭 레코드에 명시적으로 지정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because hello data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="9fb2a-200">이 방법은 리플렉션 사용보다 더 느립니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-200">This method is slower than using reflection.</span></span> <span data-ttu-id="9fb2a-201">이러한 경우 hello 데이터에 대 한 hello 스키마 수도 있습니다 동적, 즉, 컴파일 타임에 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-201">In such cases, hello schema for hello data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="9fb2a-202">데이터는 스키마 알 수 없는 변환 될 때까지 실행 시 toohello Avro 형식은 이런이 종류의 동적 시나리오의 예 (CSV) 파일 쉼표로 구분 된 값으로 표현 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed toohello Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="9fb2a-203">보여 주는이 예제 방법을 toocreate 사용 및는 [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly JSON 스키마를 어떻게 지정 toopopulate hello 데이터 및 다음 방법으로 tooserialize 및 역직렬화 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-203">This example shows how toocreate and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly specify a JSON schema, how toopopulate it with hello data, and then how tooserialize and deserialize it.</span></span> <span data-ttu-id="9fb2a-204">그런 다음 hello 결과 비교 복구 레코드 hello toohello 초기 인스턴스 tooconfirm는 원래 동일 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-204">hello result is then compared toohello initial instance tooconfirm that hello record recovered is identical toohello original.</span></span>

<span data-ttu-id="9fb2a-205">이 예에서 hello 스키마 hello Avro 개체 컨테이너 형식이 필요 하지 않도록 hello 판독기와 기록기, 공유 toobe를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-205">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="9fb2a-206">방법의 예에 대 한 tooserialize 데이터를 deserialize 하 고 hello 스키마 hello serialize 된 데이터와 함께 포함 해야 하는 경우 제네릭 레코드 hello 개체 컨테이너 형식으로 사용 하 여 메모리 버퍼로 hello 참조 <a href="#Scenario4">개체 컨테이너를 사용 하 여 직렬화 제네릭 레코드를 사용 하 여 파일</a> 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-206">For an example of how tooserialize and deserialize data into memory buffers by using a generic record with hello object container format when hello schema must be included with hello serialized data, see hello <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //hello usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with hello schema explicitly defined in JSON.
        //All serialized data should be mapped toohello fields of hello generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

            //Define hello schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on hello schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record toorepresent hello data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize hello data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize hello data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify hello results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization toomemory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key tooexit.");
            Console.Read();
        }
    }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="9fb2a-207">샘플 3: 개체 컨테이너 파일을 사용한 직렬화 및 리플렉션을 사용한 직렬화</span><span class="sxs-lookup"><span data-stu-id="9fb2a-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="9fb2a-208">이 예제는 hello에 비슷한 toohello 시나리오 <a href="#Scenario1"> 첫 번째 예에서는</a>hello 스키마 리플렉션을 사용 하 여 암시적으로 지정 되는 위치, 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-208">This example is similar toohello scenario in hello <a href="#Scenario1"> first example</a>, where hello schema is implicitly specified with reflection.</span></span> <span data-ttu-id="9fb2a-209">hello 차이점은 hello 스키마를 deserialize 하는 toohello 판독기 알려진 toobe를 취하지 않는 여기에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-209">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span> <span data-ttu-id="9fb2a-210">hello **SensorData** 개체 toobe 직렬화 및 암시적으로 지정 된 스키마 hello 나타내는 Avro 개체 컨테이너 파일에 저장 됩니다 [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-210">hello **SensorData** objects toobe serialized and their implicitly specified schema are stored in an Avro object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="9fb2a-211">이 예제와 hello 데이터를 serialize [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) 와 deserialize 된 및 [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx).</span><span class="sxs-lookup"><span data-stu-id="9fb2a-211">hello data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="9fb2a-212">hello 결과는 다음 비교 toohello 초기 인스턴스 tooensure id입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-212">hello result then is compared toohello initial instances tooensure identity.</span></span>

<span data-ttu-id="9fb2a-213">hello hello에 데이터 개체를 통해 hello 기본 컨테이너 파일은 압축 [ **Deflate** ] [ deflate-100] .NET Framework 4에서 압축 코덱 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-213">hello data in hello object container file is compressed via hello default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="9fb2a-214">Hello 참조 <a href="#Scenario5"> 다섯 번째 예에서는</a> 이 항목 toolearn에 어떻게 toouse 더 뛰어난 한 최신 버전의 hello [ **Deflate** ] [ deflate-110] 압축 .NET Framework 4.5에서 사용할 수 있는 코덱 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-214">See hello <a href="#Scenario5"> fifth example</a> in this topic toolearn how toouse a more recent and superior version of hello [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes hello sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is compressed using hello Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="9fb2a-215">샘플 4: 개체 컨테이너 파일을 사용한 직렬화 및 일반 레코드를 사용한 직렬화</span><span class="sxs-lookup"><span data-stu-id="9fb2a-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="9fb2a-216">이 예제는 hello에 비슷한 toohello 시나리오 <a href="#Scenario2"> 두 번째 예에서는</a>, 여기서 hello 스키마가 명시적으로 JSON으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-216">This example is similar toohello scenario in hello <a href="#Scenario2"> second example</a>, where hello schema is explicitly specified with JSON.</span></span> <span data-ttu-id="9fb2a-217">hello 차이점은 hello 스키마를 deserialize 하는 toohello 판독기 알려진 toobe를 취하지 않는 여기에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-217">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span>

<span data-ttu-id="9fb2a-218">hello 테스트 데이터 집합은 수집 된 목록으로 [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) 는 명시적으로 정의 된 JSON 스키마를 통해 개체를 나타내는 hello 개체 컨테이너 파일에 저장 한 다음 [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-218">hello test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="9fb2a-219">이 컨테이너 파일 tooa 메모리 스트림을 tooa 파일을 저장 한 다음 되는 사용 되는 tooserialize hello 데이터 압축을 해제 되는 작성기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-219">This container file creates a writer that is used tooserialize hello data, uncompressed, tooa memory stream that is then saved tooa file.</span></span> <span data-ttu-id="9fb2a-220">hello [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) hello 판독기를 만드는 데 사용 하는 매개 변수 지정이 데이터 압축 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-220">hello [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating hello reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="9fb2a-221">hello 데이터 hello 파일에서 읽은 되어 개체의 컬렉션으로 deserialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-221">hello data is then read from hello file and deserialized into a collection of objects.</span></span> <span data-ttu-id="9fb2a-222">이 컬렉션은 동일한 지 Avro 레코드 tooconfirm의 비교 toohello 초기 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-222">This collection is compared toohello initial list of Avro records tooconfirm that they are identical.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

                //Define hello schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on hello schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record toorepresent hello data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data toofile.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data toofile...");

                    //Save stream toofile
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing hello data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify hello results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using hello given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of hello AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="9fb2a-223">샘플 5: 사용자 지정 압축 코덱과 함께 개체 컨테이너 파일을 사용한 직렬화</span><span class="sxs-lookup"><span data-stu-id="9fb2a-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="9fb2a-224">다섯 번째 예제와 hello 방법을 toouse Avro에 대 한 사용자 지정 압축 코덱을 개체 컨테이너 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-224">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="9fb2a-225">이 예제는 hello에서 다운로드할 수 있습니다에 대 한 hello 코드를 포함 하는 샘플 [Azure 코드 예제의](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-225">A sample containing hello code for this example can be downloaded from hello [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="9fb2a-226">hello [Avro 사양](http://avro.apache.org/docs/current/spec.html#Required+Codecs) 선택적 압축 코덱의 사용 허용 (또한 너무**Null** 및 **Deflate** 기본값).</span><span class="sxs-lookup"><span data-stu-id="9fb2a-226">hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition too**Null** and **Deflate** defaults).</span></span> <span data-ttu-id="9fb2a-227">이 예제는 Snappy 등 새로운 코덱을 구현 하지 않는 (hello에서 지원 되는 선택적 코덱을 변수로 언급 된 [Avro 사양](http://avro.apache.org/docs/current/spec.html#snappy)).</span><span class="sxs-lookup"><span data-stu-id="9fb2a-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="9fb2a-228">Toouse hello의.NET Framework 4.5 구현 hello 하는 방법을 보여 줍니다 [ **Deflate** ] [ deflate-110] hello에따라더나은압축알고리즘을제공하는코덱을[zlib](http://zlib.net/) hello 기본.NET Framework 4 버전 보다 압축 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-228">It shows how toouse hello .NET Framework 4.5 implementation of hello [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on hello [zlib](http://zlib.net/) compression library than hello default .NET Framework 4 version.</span></span>

    //
    // This code needs toobe compiled with hello parameter Target Framework set as ".NET Framework 4.5"
    // tooensure hello desired implementation of hello Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are hello key ones for data compression.
        //tooenable a custom codec, one needs tooimplement these methods for hello required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs tooimplement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed toobe null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define hello actual codec class containing hello required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory toobe used in hello reader.
        //It catches hello attempt toouse "Deflate" and provide  a custom codec.
        //For all other cases, it relies on hello base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related tooserialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Here hello custom codec is introduced. For convenience, hello next commented code line shows how toouse built-in Deflate.
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment hello line below if you want toouse built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    //Here hello custom codec factory is introduced.
                    //For convenience, hello next commented code line shows how toouse built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a><span data-ttu-id="9fb2a-229">예제 6: Avro tooupload 데이터를 사용 하 여 Microsoft Azure HDInsight 서비스 hello에 대 한</span><span class="sxs-lookup"><span data-stu-id="9fb2a-229">Sample 6: Using Avro tooupload data for hello Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="9fb2a-230">hello 여섯 번째 예제 hello Azure HDInsight 서비스와 프로그래밍 기술이 관련된 toointeracting을 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-230">hello sixth example illustrates some programming techniques related toointeracting with hello Azure HDInsight service.</span></span> <span data-ttu-id="9fb2a-231">이 예제는 hello에서 다운로드할 수 있습니다에 대 한 hello 코드를 포함 하는 샘플 [Azure 코드 예제의](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-231">A sample containing hello code for this example can be downloaded from hello [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="9fb2a-232">hello 샘플은 다음 작업 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-232">hello sample does hello following tasks:</span></span>

* <span data-ttu-id="9fb2a-233">Tooan 기존 HDInsight 서비스 클러스터를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-233">Connects tooan existing HDInsight service cluster.</span></span>
* <span data-ttu-id="9fb2a-234">CSV 파일을 여러 개 또는 그 반대로 serialize 하 고 hello 결과 tooAzure Blob 저장소를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-234">Serializes several CSV files and uploads hello result tooAzure Blob storage.</span></span> <span data-ttu-id="9fb2a-235">(hello CSV 파일 hello 예제와 함께 배포 및 배포 된 AMEX 재고 기록 데이터에서 추출한 것을 나타내는 [Infochimps](http://www.infochimps.com/) hello 기간 1970-2010에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-235">(hello CSV files are distributed together with hello sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for hello period 1970-2010.</span></span> <span data-ttu-id="9fb2a-236">hello 샘플 CSV 파일 데이터를 읽고, 변환의 hello 레코드 tooinstances hello **재고** 클래스 하 고 리플렉션을 사용 하 여 개체를 serialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-236">hello sample reads CSV file data, converts hello records tooinstances of hello **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="9fb2a-237">스톡 형식 정의 hello Microsoft Avro Library 코드 생성 유틸리티를 통해 JSON 스키마에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-237">Stock type definition is created from a JSON schema via hello Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="9fb2a-238">라는 새 외부 테이블을 만듭니다 **주식** 하이브에, toohello 데이터 연결 및 hello 이전 단계에서 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-238">Creates a new external table called **Stocks** in Hive, and links it toohello data uploaded in hello previous step.</span></span>
* <span data-ttu-id="9fb2a-239">Hello 통해 하이브를 사용 하 여 쿼리를 실행 **주식** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-239">Executes a query by using Hive over hello **Stocks** table.</span></span>

<span data-ttu-id="9fb2a-240">또한 hello 샘플 전과 주요 작업을 수행한 후 정리 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-240">In addition, hello sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="9fb2a-241">Hello 정리 하는 동안 모든 hello 관련 Azure Blob 데이터 및 폴더 제거 되 고 hello 하이브 테이블을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-241">During hello clean-up, all of hello related Azure Blob data and folders are removed, and hello Hive table is dropped.</span></span> <span data-ttu-id="9fb2a-242">Hello 예제 명령줄에서 hello 정리 프로시저를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-242">You can also invoke hello clean-up procedure from hello sample command line.</span></span>

<span data-ttu-id="9fb2a-243">hello 샘플 hello 다음 필수 구성 요소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-243">hello sample has hello following prerequisites:</span></span>

* <span data-ttu-id="9fb2a-244">활성 Microsoft Azure 구독 및 해당 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="9fb2a-245">Hello 해당 개인 키를 사용 하 여 hello 구독에 대 한 관리 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-245">A management certificate for hello subscription with hello corresponding private key.</span></span> <span data-ttu-id="9fb2a-246">hello 현재 사용자 개인 저장소에 사용 되는 컴퓨터 toorun hello 샘플 hello hello 인증서를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-246">hello certificate should be installed in hello current user private storage on hello machine used toorun hello sample.</span></span>
* <span data-ttu-id="9fb2a-247">활성 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="9fb2a-248">Azure 저장소 계정, 주 또는 보조 액세스 키를 해당 하는 hello와 함께 hello 이전 필수에서 toohello HDInsight 클러스터를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-248">An Azure Storage account linked toohello HDInsight cluster from hello previous prerequisite, together with hello corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="9fb2a-249">모든 필수 구성 요소 hello hello 정보 해야 입력 한 toohello 샘플 구성 파일 hello 예제를 실행 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-249">All of hello information from hello prerequisites should be entered toohello sample configuration file before hello sample is run.</span></span> <span data-ttu-id="9fb2a-250">두 가지 방법이 toodo 하기:</span><span class="sxs-lookup"><span data-stu-id="9fb2a-250">There are two possible ways toodo it:</span></span>

* <span data-ttu-id="9fb2a-251">Hello 샘플 루트 디렉터리에 hello app.config 파일을 편집한 다음 hello 예제를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-251">Edit hello app.config file in hello sample root directory and then build hello sample</span></span>
* <span data-ttu-id="9fb2a-252">먼저 hello 샘플을 빌드 및 AvroHDISample.exe.config hello 빌드 디렉터리에서 편집</span><span class="sxs-lookup"><span data-stu-id="9fb2a-252">First build hello sample, and then edit AvroHDISample.exe.config in hello build directory</span></span>

<span data-ttu-id="9fb2a-253">두 경우 모두 hello에서 모든 편집을 수행  **<appSettings>**  설정 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-253">In both cases, all edits should be done in hello **<appSettings>** settings section.</span></span> <span data-ttu-id="9fb2a-254">Hello 파일의 주석에 hello를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-254">Follow hello comments in hello file.</span></span>
<span data-ttu-id="9fb2a-255">hello 샘플은 명령줄에서 실행 hello hello (여기서 hello hello 샘플에.zip 파일 추출 toobe tooC:\AvroHDISample 가정 했습니다; 경우 이렇게 하지 않으면 사용 하 여 hello 관련 파일 경로) 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="9fb2a-255">hello sample is run from hello command line by executing hello following command (where hello .zip file with hello sample was assumed toobe extracted tooC:\AvroHDISample; if otherwise, use hello relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="9fb2a-256">tooclean hello 클러스터를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb2a-256">tooclean up hello cluster, run hello following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
