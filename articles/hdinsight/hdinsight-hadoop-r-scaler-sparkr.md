---
title: "aaaUse ScaleR 및 Azure HDInsight와 SparkR | Microsoft Docs"
description: "R Server와 HDInsight에서 ScaleR 및 SparkR을 사용합니다."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: da732ff0235cf465a1452b81750c7cdd0351eed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a><span data-ttu-id="f8541-103">HDInsight에서 ScaleR과 SparkR 결합</span><span class="sxs-lookup"><span data-stu-id="f8541-103">Combine ScaleR and SparkR in HDInsight</span></span>

<span data-ttu-id="f8541-104">이 문서에서는 toopredict 도착 지연을 사용 하 여 비행 하는 방법을 보여 줍니다.는 **ScaleR** 비행 연착 정보와 날씨 데이터에서 로지스틱 회귀 모델에 조인 된 **SparkR**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-104">This article shows how toopredict flight arrival delays using a **ScaleR** logistic regression model from data on flight delays and weather joined with **SparkR**.</span></span> <span data-ttu-id="f8541-105">이 시나리오에서 분석에 대 한 Microsoft R Server와 함께 사용 되는 Spark 데이터 조작에 ScaleR의 hello 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-105">This scenario demonstrates hello capabilities of ScaleR for data manipulation on Spark used with Microsoft R Server for analytics.</span></span> <span data-ttu-id="f8541-106">이러한 기술 조합 hello 분산된 처리에서 tooapply hello 최신 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-106">hello combination of these technologies enables you tooapply hello latest capabilities in distributed processing.</span></span>

<span data-ttu-id="f8541-107">두 패키지 모두 Hadoop의 Spark 실행 엔진에서 실행되지만 각각 고유한 각 Spark 세션이 필요하므로 메모리 내 데이터 공유에서 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-107">Although both packages run on Hadoop’s Spark execution engine, they are blocked from in-memory data sharing as they each require their own respective Spark sessions.</span></span> <span data-ttu-id="f8541-108">이 문제는 향후 버전의 R 서버에서 될 때까지 toomaintain 겹치지 않는 Spark 세션 및 tooexchange 데이터 중간 파일을 통해 hello 해결 방법이.</span><span class="sxs-lookup"><span data-stu-id="f8541-108">Until this issue is addressed in an upcoming version of R Server, hello workaround is toomaintain non-overlapping Spark sessions, and tooexchange data through intermediate files.</span></span> <span data-ttu-id="f8541-109">여기에 지침이 hello 이러한 요구 사항이 간단한 tooachieve 되는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-109">hello instructions here show that these requirements are straightforward tooachieve.</span></span>

<span data-ttu-id="f8541-110">여기 처음 여에서 공유 층 2016에서 talk mario 씨 Inchiosa 및 hello 웹 세미나를 통해서도 사용할 수 있는 Roni Burd 예로 사용 하 여 [R 사용 하는 확장 가능한 데이터 과학 플랫폼 빌드](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). SparkR toojoin hello를 사용 하 여 hello 예제 잘 알려진 airlines 도착 지연 된 데이터 집합에 도착 및 출발 공항 날씨 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-110">We use an example here initially shared in a talk at Strata 2016 by Mario Inchiosa and Roni Burd that is also available through hello webinar [Building a Scalable Data Science Platform with R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). hello example uses SparkR toojoin hello well-known airlines arrival delay data set with weather data at departure and arrival airports.</span></span> <span data-ttu-id="f8541-111">조인 hello 데이터 도착 항공편 지연 예측 하기 위해 입력된 tooa ScaleR 로지스틱 회귀 모델로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-111">hello data joined is then used as input tooa ScaleR logistic regression model for predicting flight arrival delay.</span></span>

<span data-ttu-id="f8541-112">hello 코드 연습에서는 azure HDInsight 클러스터의 Spark에서 실행 되는 R 서버에 대 한 기록 되었으나 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-112">hello code we walkthrough was originally written for R Server running on Spark in an HDInsight cluster on Azure.</span></span> <span data-ttu-id="f8541-113">하지만 혼합을 하나의 스크립트에 SparkR 및 ScaleR의 hello 사용의 hello 개념도 온-프레미스 환경의 hello 컨텍스트에서 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-113">But hello concept of mixing hello use of SparkR and ScaleR in one script is also valid in hello context of on-premises environments.</span></span> <span data-ttu-id="f8541-114">Hello 다음 예제에서 우리 것으로 가정할 중간 수준의 R and R hello에 대 한 지식이 [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) R 서버의 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-114">In hello following, we presume an intermediate level of knowledge of R and R hello [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) library of R Server.</span></span> <span data-ttu-id="f8541-115">이 시나리오를 진행하면서 [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html)을 사용하는 방법도 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-115">We also introduce use of [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) while walking through this scenario.</span></span>

## <a name="hello-airline-and-weather-datasets"></a><span data-ttu-id="f8541-116">hello airline와 날씨 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="f8541-116">hello airline and weather datasets</span></span>

<span data-ttu-id="f8541-117">hello **AirOnTime08to12CSV** 에서 항공편 도착 및 출발 세부 정보 hello usa에 있고, 내에서 모든 상용 내리지 않는 항공편에 대 한 정보를 포함 하는 공용 데이터 집합 (주) 2012 년 10 월 1987 tooDecember 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-117">hello **AirOnTime08to12CSV** airlines public dataset contains information on flight arrival and departure details for all commercial flights within hello USA, from October 1987 tooDecember 2012.</span></span> <span data-ttu-id="f8541-118">이는 총 1억 5천만 개의 레코드를 포함하고 있는 큰 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-118">This is a large dataset: there are nearly 150 million records in total.</span></span> <span data-ttu-id="f8541-119">압축을 풀면 4GB에 해당하는 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-119">It is just under 4 GB unpacked.</span></span> <span data-ttu-id="f8541-120">Hello에서 다운로드할 수 [미국 정부 아카이브](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-120">It is available from hello [U.S. government archives](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span></span> <span data-ttu-id="f8541-121">별도 hello에서 월별 303 CSV 파일의 집합을 포함 하는 zip 파일 (AirOnTimeCSV.zip)로 제공 하는 더 편리 하 게 [Revolution Analytics 데이터 집합 리포지토리](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span><span class="sxs-lookup"><span data-stu-id="f8541-121">More conveniently, it is available as a zip file (AirOnTimeCSV.zip) containing a set of 303 separate monthly CSV files from hello [Revolution Analytics dataset repository](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span></span>

<span data-ttu-id="f8541-122">toosee hello 효과 날씨의 비행 연착 정보에도 필요 hello 날씨 데이터에 각각 hello 공항 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-122">toosee hello effects of weather on flight delays, we also need hello weather data at each of hello airports.</span></span> <span data-ttu-id="f8541-123">월별 hello에서이 데이터를 원시 형태로 zip 파일로 다운로드할 수 있습니다 [National Oceanic 및 대기 관리 저장소](http://www.ncdc.noaa.gov/orders/qclcd/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-123">This data can be downloaded as zip files in raw form, by month, from hello [National Oceanic and Atmospheric Administration repository](http://www.ncdc.noaa.gov/orders/qclcd/).</span></span> <span data-ttu-id="f8541-124">이 예제에서는 hello에 대 한 2007 년 5 월에서에서 – 2012 년 12 월 날씨 데이터를 가져올 म 및 각 hello 68 월별 zips hello 시간별 데이터 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-124">For hello purposes of this example, we pull weather data from May 2007 – December 2012 and used hello hourly data files within each of hello 68 monthly zips.</span></span> <span data-ttu-id="f8541-125">또한 hello 월별 zip 파일 매핑 (YYYYMMstation.txt) hello 날씨 스테이션 ID (WBAN), (CallSign)와 연결 되어 있음을 hello 공항 사이의 문자를 포함 하 고 hello 공항의 표준 시간대 오프셋이 UTC (표준 시간대) 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-125">hello monthly zip files also contain a mapping (YYYYMMstation.txt) between hello weather station ID (WBAN), hello airport that it is associated with (CallSign), and hello airport’s time zone offset from UTC (TimeZone).</span></span> <span data-ttu-id="f8541-126">이 정보를 모두 hello airline 지연과 날씨 데이터와 조인할 때 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-126">All of this information is needed when joining with hello airline delay and weather data.</span></span>

## <a name="setting-up-hello-spark-environment"></a><span data-ttu-id="f8541-127">Hello Spark 환경 설정</span><span class="sxs-lookup"><span data-stu-id="f8541-127">Setting up hello Spark environment</span></span>

<span data-ttu-id="f8541-128">hello 첫 번째 단계는 tooset hello Spark 환경 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-128">hello first step is tooset up hello Spark environment.</span></span> <span data-ttu-id="f8541-129">에서는 먼저 우리의 입력된 데이터 디렉터리를 포함 하는 toohello 디렉터리를 가리키는 Spark 계산 컨텍스트 만들고 toohello 콘솔 정보 로깅에 대 한 로깅 함수 만들기:</span><span class="sxs-lookup"><span data-stu-id="f8541-129">We begin by pointing toohello directory that contains our input data directories, creating a Spark compute context, and creating a logging function for informational logging toohello console:</span></span>

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session tooreduce startup times 
#   (remember toostop it later!)
 
sparkCC        <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort, persistentRun=TRUE)

# create working directories 

rxHadoopMakeDir('/user')
rxHadoopMakeDir('user/RevoShare')
rxHadoopMakeDir('user/RevoShare/remoteuser')

(dataDir <- '/share')
rxHadoopMakeDir(dataDir)
rxHadoopListFiles(dataDir) 

setwd(workDir)
getwd()

# version of rxRoc that runs in a local CC 
rxRoc <- function(...){
  rxSetComputeContext(RxLocalSeq())
  roc <- RevoScaleR::rxRoc(...)
  rxSetComputeContext(sparkCC)
  return(roc)
}

logmsg <- function(msg) { cat(format(Sys.time(), "%Y-%m-%d %H:%M:%S"),':',msg,'\n') } 
t0 <- proc.time() 

#..start 

logmsg('Start') 
(trackers <- system("mapred job -list-active-trackers", intern = TRUE))
logmsg(paste('Number of task nodes=',length(trackers)))
```

<span data-ttu-id="f8541-130">다음 म SparkR를 사용 하 고 SparkR 세션을 초기화할 수 있도록 R 패키지에 대 한 "Spark_Home" toohello 검색 경로 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-130">Next we add “Spark_Home” toohello search path for R packages so that we can use SparkR, and initialize a SparkR session:</span></span>

```
#..setup for use of SparkR  

logmsg('Initialize SparkR') 

.libPaths(c(file.path(Sys.getenv("SPARK_HOME"), "R", "lib"), .libPaths()))
library(SparkR)

sparkEnvir <- list(spark.executor.instances = '10',
                   spark.yarn.executor.memoryOverhead = '8000')

sc <- sparkR.init(
  sparkEnvir = sparkEnvir,
  sparkPackages = "com.databricks:spark-csv_2.10:1.3.0"
)

sqlContext <- sparkRSQL.init(sc)
```

## <a name="preparing-hello-weather-data"></a><span data-ttu-id="f8541-131">Hello 날씨 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="f8541-131">Preparing hello weather data</span></span>

<span data-ttu-id="f8541-132">tooprepare hello 날씨 데이터에서는 하위 집합 것 모델링에 필요한 toohello 열:</span><span class="sxs-lookup"><span data-stu-id="f8541-132">tooprepare hello weather data, we subset it toohello columns needed for modeling:</span></span> 

- <span data-ttu-id="f8541-133">"Visibility"</span><span class="sxs-lookup"><span data-stu-id="f8541-133">"Visibility"</span></span>
- <span data-ttu-id="f8541-134">"DryBulbCelsius"</span><span class="sxs-lookup"><span data-stu-id="f8541-134">"DryBulbCelsius"</span></span>
- <span data-ttu-id="f8541-135">"DewPointCelsius"</span><span class="sxs-lookup"><span data-stu-id="f8541-135">"DewPointCelsius"</span></span>
- <span data-ttu-id="f8541-136">"RelativeHumidity"</span><span class="sxs-lookup"><span data-stu-id="f8541-136">"RelativeHumidity"</span></span>
- <span data-ttu-id="f8541-137">"WindSpeed"</span><span class="sxs-lookup"><span data-stu-id="f8541-137">"WindSpeed"</span></span>
- <span data-ttu-id="f8541-138">"Altimeter"</span><span class="sxs-lookup"><span data-stu-id="f8541-138">"Altimeter"</span></span>

<span data-ttu-id="f8541-139">다음 hello 날씨 스테이션 연관는 공항 코드를 추가 하 고 tooUTC 현지 시간에서에서 hello 측정값을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-139">Then we add an airport code associated with hello weather station and convert hello measurements from local time tooUTC.</span></span>

<span data-ttu-id="f8541-140">파일 toomap hello 날씨 스테이션 (WBAN) 정보 tooan 공항 코드를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-140">We begin by creating a file toomap hello weather station (WBAN) info tooan airport code.</span></span> <span data-ttu-id="f8541-141">Hello 날씨 데이터에 포함 된 hello 매핑 파일에서이 상관 관계를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-141">We could get this correlation from hello mapping file included with hello weather data.</span></span> <span data-ttu-id="f8541-142">매핑 hello로 *CallSign* (예: LAX) 너무 hello 날씨 데이터 파일의 필드*원점* hello airline 데이터에서입니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-142">By mapping hello *CallSign* (for example, LAX) field in hello weather data file too*Origin* in hello airline data.</span></span> <span data-ttu-id="f8541-143">그러나 우리 일이 일어났는지 toohave 다른 매핑 가까이 매핑하는 *WBAN* 너무*AirportID* (LAX에 대 한 예를 들어 12892) 작성과 *표준 시간대* tooa 저장 하는 CSV 파일 이라는 "wban-에-공항-id-tz 합니다. CSV "는 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-143">However, we just happened toohave another mapping on hand that maps *WBAN* too*AirportID* (for example, 12892 for LAX) and includes *TimeZone* that has been saved tooa CSV file called “wban-to-airport-id-tz.CSV” that we can use.</span></span> <span data-ttu-id="f8541-144">예:</span><span class="sxs-lookup"><span data-stu-id="f8541-144">For example:</span></span>

| <span data-ttu-id="f8541-145">AirportID</span><span class="sxs-lookup"><span data-stu-id="f8541-145">AirportID</span></span> | <span data-ttu-id="f8541-146">WBAN</span><span class="sxs-lookup"><span data-stu-id="f8541-146">WBAN</span></span> | <span data-ttu-id="f8541-147">TimeZone</span><span class="sxs-lookup"><span data-stu-id="f8541-147">TimeZone</span></span>
|-----------|------|---------
| <span data-ttu-id="f8541-148">10685</span><span class="sxs-lookup"><span data-stu-id="f8541-148">10685</span></span> | <span data-ttu-id="f8541-149">54831</span><span class="sxs-lookup"><span data-stu-id="f8541-149">54831</span></span> | <span data-ttu-id="f8541-150">-6</span><span class="sxs-lookup"><span data-stu-id="f8541-150">-6</span></span>
| <span data-ttu-id="f8541-151">14871</span><span class="sxs-lookup"><span data-stu-id="f8541-151">14871</span></span> | <span data-ttu-id="f8541-152">24232</span><span class="sxs-lookup"><span data-stu-id="f8541-152">24232</span></span> | <span data-ttu-id="f8541-153">-8</span><span class="sxs-lookup"><span data-stu-id="f8541-153">-8</span></span>
| <span data-ttu-id="f8541-154">..</span><span class="sxs-lookup"><span data-stu-id="f8541-154">..</span></span> | <span data-ttu-id="f8541-155">..</span><span class="sxs-lookup"><span data-stu-id="f8541-155">..</span></span> | <span data-ttu-id="f8541-156">..</span><span class="sxs-lookup"><span data-stu-id="f8541-156">..</span></span>

<span data-ttu-id="f8541-157">hello 코드 읽기 각 hello 시간별 원시 날씨 데이터의 다음 파일을 하위 집합 toohello 열, hello 날씨 스테이션 매핑 파일을 병합, 조정 hello 측정 tooUTC의 날짜 시간 및 필요 다음 새 버전의 hello 파일 작성:</span><span class="sxs-lookup"><span data-stu-id="f8541-157">hello following code reads each of hello hourly raw weather data files, subsets toohello columns we need, merges hello weather station mapping file, adjusts hello date times of measurements tooUTC, and then writes out a new version of hello file:</span></span>

```
# Look up AirportID and Timezone for WBAN (weather station ID) and adjust time

adjustTime <- function(dataList)
{
  dataset0 <- as.data.frame(dataList)
  
  dataset1 <- base::merge(dataset0, wbanToAirIDAndTZDF1, by = "WBAN")

  if(nrow(dataset1) == 0) {
    dataset1 <- data.frame(
      Visibility = numeric(0),
      DryBulbCelsius = numeric(0),
      DewPointCelsius = numeric(0),
      RelativeHumidity = numeric(0),
      WindSpeed = numeric(0),
      Altimeter = numeric(0),
      AdjustedYear = numeric(0),
      AdjustedMonth = numeric(0),
      AdjustedDay = integer(0),
      AdjustedHour = integer(0),
      AirportID = integer(0)
    )
    
    return(dataset1)
  }
  
  Year <- as.integer(substr(dataset1$Date, 1, 4))
  Month <- as.integer(substr(dataset1$Date, 5, 6))
  Day <- as.integer(substr(dataset1$Date, 7, 8))
  
  Time <- dataset1$Time
  Hour <- ceiling(Time/100)
  
  Timezone <- as.integer(dataset1$TimeZone)
  
  adjustdate = as.POSIXlt(sprintf("%4d-%02d-%02d %02d:00:00", Year, Month, Day, Hour), tz = "UTC") + Timezone * 3600

  AdjustedYear = as.POSIXlt(adjustdate)$year + 1900
  AdjustedMonth = as.POSIXlt(adjustdate)$mon + 1
  AdjustedDay   = as.POSIXlt(adjustdate)$mday
  AdjustedHour  = as.POSIXlt(adjustdate)$hour
  
  AirportID = dataset1$AirportID
  Weather = dataset1[,c("Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", "Altimeter")]
  
  data.set = data.frame(cbind(AdjustedYear, AdjustedMonth, AdjustedDay, AdjustedHour, AirportID, Weather))
  
  return(data.set)
}

wbanToAirIDAndTZDF <- read.csv("wban-to-airport-id-tz.csv")

colInfo <- list(
  WBAN = list(type="integer"),
  Date = list(type="character"),
  Time = list(type="integer"),
  Visibility = list(type="numeric"),
  DryBulbCelsius = list(type="numeric"),
  DewPointCelsius = list(type="numeric"),
  RelativeHumidity = list(type="numeric"),
  WindSpeed = list(type="numeric"),
  Altimeter = list(type="numeric")
)

weatherDF <- RxTextData(file.path(inputDataDir, "WeatherRaw"), colInfo = colInfo)

weatherDF1 <- RxTextData(file.path(inputDataDir, "Weather"), colInfo = colInfo,
                filesystem=hdfsFS)

rxSetComputeContext("localpar")
rxDataStep(weatherDF, outFile = weatherDF1, rowsPerRead = 50000, overwrite = T,
           transformFunc = adjustTime,
           transformObjects = list(wbanToAirIDAndTZDF1 = wbanToAirIDAndTZDF))
```

## <a name="importing-hello-airline-and-weather-data-toospark-dataframes"></a><span data-ttu-id="f8541-158">Hello airline와 날씨 데이터 tooSpark 데이터 프레임을 가져오기</span><span class="sxs-lookup"><span data-stu-id="f8541-158">Importing hello airline and weather data tooSpark DataFrames</span></span>

<span data-ttu-id="f8541-159">Hello SparkR 사용 하 여 이제 [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) tooimport hello 날씨, airline 데이터 tooSpark 프레임 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-159">Now we use hello SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) function tooimport hello weather and airline data tooSpark DataFrames.</span></span> <span data-ttu-id="f8541-160">이 함수는 다른 많은 Spark 메서드와 마찬가지로 느리게 실행됩니다. 즉 실행 큐에 있지만 필요할 때까지는 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-160">This function, like many other Spark methods, are executed lazily, meaning that they are queued for execution but not executed until required.</span></span>

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for hello airline data

logmsg('create a SparkR DataFrame for hello airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for hello weather data

logmsg('create a SparkR DataFrame for hello weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a><span data-ttu-id="f8541-161">데이터 정리 및 변환</span><span class="sxs-lookup"><span data-stu-id="f8541-161">Data cleansing and transformation</span></span>

<span data-ttu-id="f8541-162">그런 다음 작업을 수행 하기 몇 가지 정리 hello airline 데이터에 대해 toorename 열 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-162">Next we do some cleanup on hello airline data we’ve imported toorename columns.</span></span> <span data-ttu-id="f8541-163">म만 유지 hello 변수 필요 하 고 hello 출발 최신 날씨 데이터와 병합 하는 시간 tooenable 가장 가까운 toohello 아래로 출발 한 예약 된 시간을 반올림:</span><span class="sxs-lookup"><span data-stu-id="f8541-163">We only keep hello variables needed, and round scheduled departure times down toohello nearest hour tooenable merging with hello latest weather data at departure:</span></span>

```
logmsg('clean hello airline data') 
airDF <- rename(airDF,
                ArrDel15 = airDF$ARR_DEL15,
                Year = airDF$YEAR,
                Month = airDF$MONTH,
                DayofMonth = airDF$DAY_OF_MONTH,
                DayOfWeek = airDF$DAY_OF_WEEK,
                Carrier = airDF$UNIQUE_CARRIER,
                OriginAirportID = airDF$ORIGIN_AIRPORT_ID,
                DestAirportID = airDF$DEST_AIRPORT_ID,
                CRSDepTime = airDF$CRS_DEP_TIME,
                CRSArrTime =  airDF$CRS_ARR_TIME
)

# Select desired columns from hello flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time toofull hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

<span data-ttu-id="f8541-164">이제 hello 날씨 데이터에 대 한 유사한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-164">Now we perform similar operations on hello weather data:</span></span>

```
# Average weather readings by hour
logmsg('clean hello weather data') 
weatherDF <- agg(groupBy(weatherDF, "AdjustedYear", "AdjustedMonth", "AdjustedDay", "AdjustedHour", "AirportID"), Visibility="avg",
                  DryBulbCelsius="avg", DewPointCelsius="avg", RelativeHumidity="avg", WindSpeed="avg", Altimeter="avg"
                  )

weatherDF <- rename(weatherDF,
                    Visibility = weatherDF$'avg(Visibility)',
                    DryBulbCelsius = weatherDF$'avg(DryBulbCelsius)',
                    DewPointCelsius = weatherDF$'avg(DewPointCelsius)',
                    RelativeHumidity = weatherDF$'avg(RelativeHumidity)',
                    WindSpeed = weatherDF$'avg(WindSpeed)',
                    Altimeter = weatherDF$'avg(Altimeter)'
)
```

## <a name="joining-hello-weather-and-airline-data"></a><span data-ttu-id="f8541-165">Hello 날씨, airline 데이터 조인</span><span class="sxs-lookup"><span data-stu-id="f8541-165">Joining hello weather and airline data</span></span>

<span data-ttu-id="f8541-166">이제 hello SparkR 사용 [join ()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) toodo AirportID 출발 하 여 hello airline와 날씨 데이터 및 날짜/시간 왼쪽된 우선 외부 조인을 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-166">We now use hello SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) function toodo a left outer join of hello airline and weather data by departure AirportID and datetime.</span></span> <span data-ttu-id="f8541-167">외부 조인 hello tooretain을 날씨 데이터가 없는 일치 하는 경우에 모든 hello airline 데이터 레코드 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-167">hello outer join allows us tooretain all hello airline data records even if there is no matching weather data.</span></span> <span data-ttu-id="f8541-168">Hello 조인에서는 일부 중복 열을 제거 및 보관 하는 hello 열 tooremove hello 들어오는 데이터 프레임 접두사 hello 조인에 의해 도입 된 이름 바꾸기.</span><span class="sxs-lookup"><span data-stu-id="f8541-168">Following hello join, we remove some redundant columns, and rename hello kept columns tooremove hello incoming DataFrame prefix introduced by hello join.</span></span>

```
logmsg('Join airline data with weather at Origin Airport')
joinedDF <- SparkR::join(
  airDF,
  weatherDF,
  airDF$OriginAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF1 <- select(joinedDF, varsToKeep)

joinedDF2 <- rename(joinedDF1,
                    VisibilityOrigin = joinedDF1$Visibility,
                    DryBulbCelsiusOrigin = joinedDF1$DryBulbCelsius,
                    DewPointCelsiusOrigin = joinedDF1$DewPointCelsius,
                    RelativeHumidityOrigin = joinedDF1$RelativeHumidity,
                    WindSpeedOrigin = joinedDF1$WindSpeed,
                    AltimeterOrigin = joinedDF1$Altimeter
)
```

<span data-ttu-id="f8541-169">유사한 방식 hello 날씨, airline 데이터 도착 AirportID 및 날짜/시간에 따라 조인 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-169">In a similar fashion, we join hello weather and airline data based on arrival AirportID and datetime:</span></span>

```
logmsg('Join airline data with weather at Destination Airport')
joinedDF3 <- SparkR::join(
  joinedDF2,
  weatherDF,
  airDF$DestAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF3)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF4 <- select(joinedDF3, varsToKeep)

joinedDF5 <- rename(joinedDF4,
                    VisibilityDest = joinedDF4$Visibility,
                    DryBulbCelsiusDest = joinedDF4$DryBulbCelsius,
                    DewPointCelsiusDest = joinedDF4$DewPointCelsius,
                    RelativeHumidityDest = joinedDF4$RelativeHumidity,
                    WindSpeedDest = joinedDF4$WindSpeed,
                    AltimeterDest = joinedDF4$Altimeter
                    )
```

## <a name="save-results-toocsv-for-exchange-with-scaler"></a><span data-ttu-id="f8541-170">Exchange에 대 한 결과 tooCSV ScaleR으로 저장</span><span class="sxs-lookup"><span data-stu-id="f8541-170">Save results tooCSV for exchange with ScaleR</span></span>

<span data-ttu-id="f8541-171">Hello 조인 SparkR와 toodo 해야 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-171">That completes hello joins we need toodo with SparkR.</span></span> <span data-ttu-id="f8541-172">Hello 최종 Spark 데이터 프레임 "joinedDF5" tooa CSV에 대 한 입력된 tooScaleR에서에서 hello 데이터를 저장 하 고 hello SparkR 세션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-172">We save hello data from hello final Spark DataFrame “joinedDF5” tooa CSV for input tooScaleR and then close out hello SparkR session.</span></span> <span data-ttu-id="f8541-173">명시적으로 위치도 제공 SparkR toosave 80 별도 파티션 tooenable 충분 한 병렬 처리를 ScaleR 처리의 결과 CSV를 hello:</span><span class="sxs-lookup"><span data-stu-id="f8541-173">We explicitly tell SparkR toosave hello resultant CSV in 80 separate partitions tooenable sufficient parallelism in ScaleR processing:</span></span>

```
logmsg('output hello joined data from Spark tooCSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result toodirectory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down hello SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-tooxdf-for-use-by-scaler"></a><span data-ttu-id="f8541-174">ScaleR에서 사용 하기 위해 tooXDF 가져오기</span><span class="sxs-lookup"><span data-stu-id="f8541-174">Import tooXDF for use by ScaleR</span></span>

<span data-ttu-id="f8541-175">Hello CSV 파일의 조인 된 airline와 날씨 데이터를 사용 하 여-ScaleR 텍스트 데이터 원본을 통해 모델링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-175">We could use hello CSV file of joined airline and weather data as-is for modeling via a ScaleR text data source.</span></span> <span data-ttu-id="f8541-176">하지만 म 가져와서 tooXDF 먼저 hello 데이터 집합에 여러 개의 작업을 실행 하는 경우 더 효율적 이므로:</span><span class="sxs-lookup"><span data-stu-id="f8541-176">But we import it tooXDF first, since it is more efficient when running multiple operations on hello dataset:</span></span>

```
logmsg('Import hello CSV toocompressed, binary XDF format') 

# set hello Spark compute context for R Server 
rxSetComputeContext(sparkCC)
rxGetComputeContext()

colInfo <- list(
  ArrDel15 = list(type="numeric"),
  Year = list(type="factor"),
  Month = list(type="factor"),
  DayofMonth = list(type="factor"),
  DayOfWeek = list(type="factor"),
  Carrier = list(type="factor"),
  OriginAirportID = list(type="factor"),
  DestAirportID = list(type="factor"),
  RelativeHumidityOrigin = list(type="numeric"),
  AltimeterOrigin = list(type="numeric"),
  DryBulbCelsiusOrigin = list(type="numeric"),
  WindSpeedOrigin = list(type="numeric"),
  VisibilityOrigin = list(type="numeric"),
  DewPointCelsiusOrigin = list(type="numeric"),
  RelativeHumidityDest = list(type="numeric"),
  AltimeterDest = list(type="numeric"),
  DryBulbCelsiusDest = list(type="numeric"),
  WindSpeedDest = list(type="numeric"),
  VisibilityDest = list(type="numeric"),
  DewPointCelsiusDest = list(type="numeric")
)

joinedDF5Txt <- RxTextData(file.path(dataDir, "joined5Csv"),
                           colInfo = colInfo, fileSystem = hdfsFS)
rxGetInfo(joinedDF5Txt) 

destData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

rxImport(inData = joinedDF5Txt, destData, overwrite = TRUE)

rxGetInfo(destData, getVarInfo = T)

# File name: /user/RevoShare/dev/delayDataLarge/joined5XDF 
# Number of composite data files: 80 
# Number of observations: 148619655 
# Number of variables: 22 
# Number of blocks: 320 
# Compression type: zlib 
# Variable information: 
#   Var 1: ArrDel15, Type: numeric, Low/High: (0.0000, 1.0000)
# Var 2: Year
# 26 factor levels: 1987 1988 1989 1990 1991 ... 2008 2009 2010 2011 2012
# Var 3: Month
# 12 factor levels: 10 11 12 1 2 ... 5 6 7 8 9
# Var 4: DayofMonth
# 31 factor levels: 1 3 4 5 7 ... 29 30 2 18 31
# Var 5: DayOfWeek
# 7 factor levels: 4 6 7 1 3 2 5
# Var 6: Carrier
# 30 factor levels: PI UA US AA DL ... HA F9 YV 9E VX
# Var 7: OriginAirportID
# 374 factor levels: 15249 12264 11042 15412 13930 ... 13341 10559 14314 11711 10558
# Var 8: DestAirportID
# 378 factor levels: 13303 14492 10721 11057 13198 ... 14802 11711 11931 12899 10559
# Var 9: CRSDepTime, Type: integer, Low/High: (0, 24)
# Var 10: CRSArrTime, Type: integer, Low/High: (0, 2400)
# Var 11: RelativeHumidityOrigin, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 12: AltimeterOrigin, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 13: DryBulbCelsiusOrigin, Type: numeric, Low/High: (-46.1000, 47.8000)
# Var 14: WindSpeedOrigin, Type: numeric, Low/High: (0.0000, 81.0000)
# Var 15: VisibilityOrigin, Type: numeric, Low/High: (0.0000, 90.0000)
# Var 16: DewPointCelsiusOrigin, Type: numeric, Low/High: (-41.7000, 29.0000)
# Var 17: RelativeHumidityDest, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 18: AltimeterDest, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 19: DryBulbCelsiusDest, Type: numeric, Low/High: (-46.1000, 53.9000)
# Var 20: WindSpeedDest, Type: numeric, Low/High: (0.0000, 136.0000)
# Var 21: VisibilityDest, Type: numeric, Low/High: (0.0000, 88.0000)
# Var 22: DewPointCelsiusDest, Type: numeric, Low/High: (-43.0000, 29.0000)

finalData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

```

## <a name="splitting-data-for-training-and-test"></a><span data-ttu-id="f8541-177">학습 및 테스트를 위한 데이터 분할</span><span class="sxs-lookup"><span data-stu-id="f8541-177">Splitting data for training and test</span></span>

<span data-ttu-id="f8541-178">RxDataStep toosplit hello 2012 데이터를 사용 하 여 테스트를 위한 하 고 학습에 대 한 hello rest를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-178">We use rxDataStep toosplit out hello 2012 data for testing and keep hello rest for training:</span></span>

```
# split out hello training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out hello testing data

logmsg('split out hello test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a><span data-ttu-id="f8541-179">로지스틱 회귀 모델 학습 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f8541-179">Train and test a logistic regression model</span></span>

<span data-ttu-id="f8541-180">이제는 준비 toobuild 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-180">Now we are ready toobuild a model.</span></span> <span data-ttu-id="f8541-181">toosee hello에 미치는 영향은 날씨 데이터 hello 도착 시간 지연, ScaleR의 로지스틱 회귀 루틴 사용.</span><span class="sxs-lookup"><span data-stu-id="f8541-181">toosee hello influence of weather data on delay in hello arrival time, we use ScaleR’s logistic regression routine.</span></span> <span data-ttu-id="f8541-182">사용할 수 toomodel 여부는 도착 지연 시간을 15 분 이상 hello 날씨 hello 도착 및 출발 공항에 따라 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-182">We use it toomodel whether an arrival delay of greater than 15 minutes is influenced by hello weather at hello departure and arrival airports:</span></span>

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use hello scalable rxLogit() function but set max iterations too3 for hello purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

<span data-ttu-id="f8541-183">이제 어떻게 것 않습니다 hello에 테스트 데이터는 일부 예측을 만드는 살펴보고 ROC 및 AUC를 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-183">Now let’s see how it does on hello test data by making some predictions and looking at ROC and AUC.</span></span>

```
# Predict over test data (Logistic Regression).

logmsg('predict over hello test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use hello scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under hello Curve (AUC).

logmsg('calculate hello roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a><span data-ttu-id="f8541-184">다른 곳에서 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="f8541-184">Scoring elsewhere</span></span>

<span data-ttu-id="f8541-185">다른 플랫폼에서 점수 매기기 데이터에 대 한 hello 모델을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-185">We can also use hello model for scoring data on another platform.</span></span> <span data-ttu-id="f8541-186">가져오는 방식으로 tooan RDS 파일을 저장 하 고 다음 전송 해당 RDS SQL Server R Services와 같은 환경 점수 매기기를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-186">By saving it tooan RDS file and then transferring and importing that RDS into a destination scoring environment such as SQL Server R Services.</span></span> <span data-ttu-id="f8541-187">중요 한 tooensure 모델이 있는 hello에 빌드된 hello 요소 수준의 점수가 매겨진 hello 데이터 toobe 일치 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f8541-187">It is important tooensure that hello factor levels of hello data toobe scored match those on which hello model was built.</span></span> <span data-ttu-id="f8541-188">일치를 추출 하 여 수행할 수 있습니다 및 ScaleR의를 통해 데이터를 모델링 하는 hello와 관련 된 hello 열 정보를 저장 `rxCreateColInfo()` 함수 하 고 예측에 대 한 해당 열 정보 toohello 입력된 데이터 원본에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-188">That match can be achieved by extracting and saving hello column infomation associated with hello modeling data via ScaleR’s `rxCreateColInfo()` function and then applying that column information toohello input data source for prediction.</span></span> <span data-ttu-id="f8541-189">Hello 다음에서는 hello 테스트 데이터 집합의 행을 몇 개 저장 및 추출 하 고 hello 예측 스크립트에서이 샘플에서 hello 열 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-189">In hello following we save a few rows of hello test dataset and extract and use hello column information from this sample in hello prediction script:</span></span>

```
# save hello model and a sample of hello test dataset 

logmsg('save serialized version of hello model and a sample of hello test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop hello spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a><span data-ttu-id="f8541-190">요약</span><span class="sxs-lookup"><span data-stu-id="f8541-190">Summary</span></span>

<span data-ttu-id="f8541-191">이 문서에서는 SparkR ScaleR Hadoop Spark에 모델 개발에 대 한 데이터 조작에 대 한 가능한 toocombine 사용 방법은 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-191">In this article, we’ve shown how it’s possible toocombine use of SparkR for data manipulation with ScaleR for model development in Hadoop Spark.</span></span> <span data-ttu-id="f8541-192">이 시나리오에서는 한 번에 하나의 세션만 실행하면서 별도의 Spark 세션을 유지하고 CSV 파일을 통해 데이터를 교환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-192">This scenario requires that you maintain separate Spark sessions, only running one session at a time, and exchange data via CSV files.</span></span> <span data-ttu-id="f8541-193">SparkR과 ScaleR에서 Spark 세션을 공유하고 이에 따라 Spark DataFrame을 공유할 수 있는 경우 이 프로세스가 간단하지만 예정된 R Server 릴리스에서 훨씬 더 쉽게 수행될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f8541-193">Although straightforward, this process should be even easier in an upcoming R Server release, when SparkR and ScaleR can share a Spark session and so share Spark DataFrames.</span></span>

## <a name="next-steps-and-more-information"></a><span data-ttu-id="f8541-194">다음 단계 및 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f8541-194">Next steps and more information</span></span>

- <span data-ttu-id="f8541-195">Spark에 R server 사용에 자세한 내용은 참조 hello [MSDN 시작 가이드](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span><span class="sxs-lookup"><span data-stu-id="f8541-195">For more information on use of R Server on Spark, see hello [Getting started guide on MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span></span>

- <span data-ttu-id="f8541-196">R 서버에 대 한 일반적인 정보를 참조 hello [R 시작](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) 문서.</span><span class="sxs-lookup"><span data-stu-id="f8541-196">For general information on R Server, see hello [Get started with R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) article.</span></span>

- <span data-ttu-id="f8541-197">HDInsight의 R Server에 대한 자세한 내용은 [Azure HDInsight의 R Server 개요](hdinsight-hadoop-r-server-overview.md) 및 [Azure HDInsight의 R Server](hdinsight-hadoop-r-server-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8541-197">For information on R Server on HDInsight, see [R Server on Azure HDInsight overview](hdinsight-hadoop-r-server-overview.md) and [R Server on Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span>

<span data-ttu-id="f8541-198">SparkR 사용에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8541-198">For more information on use of SparkR, see:</span></span>

- [<span data-ttu-id="f8541-199">Apache SparkR 문서</span><span class="sxs-lookup"><span data-stu-id="f8541-199">Apache SparkR document</span></span>](https://spark.apache.org/docs/2.1.0/sparkr.html)

- <span data-ttu-id="f8541-200">Databricks의 [SparkR 개요](https://docs.databricks.com/spark/latest/sparkr/overview.html)(영문)</span><span class="sxs-lookup"><span data-stu-id="f8541-200">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) from Databricks</span></span>
