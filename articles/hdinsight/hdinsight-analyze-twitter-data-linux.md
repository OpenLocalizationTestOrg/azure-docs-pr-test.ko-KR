---
title: "Twitter 데이터 Apache Hive-Azure HDInsight를 aaaAnalyze | Microsoft Docs"
description: "어떻게 toouse Hive 및 Hadoop 데이터에 사용할 HDInsight tootransform 원시 TWitter 검색 가능한 Hive 테이블에 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1e249ed-5f57-40d6-b3bc-a1b4d9a871d3
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 02c4d027c7bbf390ac1c3724c14f8d549ea5195e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a><span data-ttu-id="6a394-103">HDInsight에서 Hive 및 Hadoop을 사용하여 Twitter 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="6a394-103">Analyze Twitter data using Hive and Hadoop on HDInsight</span></span>

<span data-ttu-id="6a394-104">자세한 내용은 방법 toouse Apache Hive tooprocess Twitter 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-104">Learn how toouse Apache Hive tooprocess Twitter data.</span></span> <span data-ttu-id="6a394-105">hello 결과 hello 특정 단어를 포함 하는 대부분 트 윗을 보낼 Twitter 사용자의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-105">hello result is a list of Twitter users who sent hello most tweets that contain a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a394-106">이 문서의 단계 hello HDInsight 3.6에서 테스트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-106">hello steps in this document were tested on HDInsight 3.6.</span></span>
>
> <span data-ttu-id="6a394-107">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6a394-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a394-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="get-hello-data"></a><span data-ttu-id="6a394-109">Hello 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="6a394-109">Get hello data</span></span>

<span data-ttu-id="6a394-110">Twitter 있습니다 tooretrieve hello [각 트 윗에 대 한 데이터](https://dev.twitter.com/docs/platform-objects/tweets) REST API를 통해 개체 JSON (JavaScript Notation) 문서와 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-110">Twitter allows you tooretrieve hello [data for each tweet](https://dev.twitter.com/docs/platform-objects/tweets) as a JavaScript Object Notation (JSON) document through a REST API.</span></span> <span data-ttu-id="6a394-111">[OAuth](http://oauth.net) 인증 toohello API에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-111">[OAuth](http://oauth.net) is required for authentication toohello API.</span></span>

### <a name="create-a-twitter-application"></a><span data-ttu-id="6a394-112">Twitter 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="6a394-112">Create a Twitter application</span></span>

1. <span data-ttu-id="6a394-113">웹 브라우저에서 로그인 너무[https://apps.twitter.com/](https://apps.twitter.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-113">From a web browser, sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="6a394-114">Hello 클릭 **등록 지금** Twitter 계정이 없는 경우 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-114">Click hello **Sign-up now** link if you don't have a Twitter account.</span></span>

2. <span data-ttu-id="6a394-115">**Create New App**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-115">Click **Create New App**.</span></span>

3. <span data-ttu-id="6a394-116">**Name**, **Description**, **Website**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-116">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="6a394-117">Hello에 대 한 URL을 만들 수 **웹 사이트** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-117">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="6a394-118">다음 표에서 hello 몇 가지 샘플 값 toouse를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-118">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="6a394-119">필드</span><span class="sxs-lookup"><span data-stu-id="6a394-119">Field</span></span> | <span data-ttu-id="6a394-120">값</span><span class="sxs-lookup"><span data-stu-id="6a394-120">Value</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="6a394-121">이름</span><span class="sxs-lookup"><span data-stu-id="6a394-121">Name</span></span> |<span data-ttu-id="6a394-122">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="6a394-122">MyHDInsightApp</span></span> |
   | <span data-ttu-id="6a394-123">설명</span><span class="sxs-lookup"><span data-stu-id="6a394-123">Description</span></span> |<span data-ttu-id="6a394-124">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="6a394-124">MyHDInsightApp</span></span> |
   | <span data-ttu-id="6a394-125">Website</span><span class="sxs-lookup"><span data-stu-id="6a394-125">Website</span></span> |<span data-ttu-id="6a394-126">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="6a394-126">http://www.myhdinsightapp.com</span></span> |

4. <span data-ttu-id="6a394-127">**Yes, I agree**를 선택한 후 **Create your Twitter application**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-127">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>

5. <span data-ttu-id="6a394-128">Hello 클릭 **권한을** 탭 hello 기본 권한은 **읽기 전용**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-128">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span>

6. <span data-ttu-id="6a394-129">Hello 클릭 **키와 액세스 토큰이** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-129">Click hello **Keys and Access Tokens** tab.</span></span>

7. <span data-ttu-id="6a394-130">**Create my access token**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-130">Click **Create my access token**.</span></span>

8. <span data-ttu-id="6a394-131">클릭 **테스트 OAuth** hello 페이지의 hello 오른쪽 위 모서리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-131">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>

9. <span data-ttu-id="6a394-132">**consumer key**, **Consumer secret**, **Access token** 및 **Access token secret**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-132">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span>

### <a name="download-tweets"></a><span data-ttu-id="6a394-133">트윗 다운로드</span><span class="sxs-lookup"><span data-stu-id="6a394-133">Download tweets</span></span>

<span data-ttu-id="6a394-134">hello Python 코드 다음에 저장 하 고 Twitter에서 10, 000 트 윗 다운로드 라는 tooa 파일 **tweets.txt**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-134">hello following Python code downloads 10,000 tweets from Twitter and save them tooa file named **tweets.txt**.</span></span>

> [!NOTE]
> <span data-ttu-id="6a394-135">단계를 수행 하는 hello Python가 이미 설치 되어 있으므로 hello HDInsight 클러스터에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-135">hello following steps are performed on hello HDInsight cluster, since Python is already installed.</span></span>

1. <span data-ttu-id="6a394-136">SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-136">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="6a394-137">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a394-137">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="6a394-138">사용 하 여 hello 다음 명령을 tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2), 및 기타 필요한 패키지:</span><span class="sxs-lookup"><span data-stu-id="6a394-138">Use hello following commands tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2), and other required packages:</span></span>

   ```bash
   sudo apt install python-dev libffi-dev libssl-dev
   sudo apt remove python-openssl
   pip install virtualenv
   mkdir gettweets
   cd gettweets
   virtualenv gettweets
   source gettweets/bin/activate
   pip install tweepy progressbar pyOpenSSL requests[security]
   ```

4. <span data-ttu-id="6a394-139">사용 하 여 hello 다음 명령은 toocreate 이라는 파일로 내보내집니다 **gettweets.py**:</span><span class="sxs-lookup"><span data-stu-id="6a394-139">Use hello following command toocreate a file named **gettweets.py**:</span></span>

   ```bash
   nano gettweets.py
   ```

5. <span data-ttu-id="6a394-140">콘텐츠로 사용 hello hello 텍스트를 다음으로 사용 하 여 hello **gettweets.py** 파일:</span><span class="sxs-lookup"><span data-stu-id="6a394-140">Use hello following text as hello contents of hello **gettweets.py** file:</span></span>

   ```python
   #!/usr/bin/python

   from tweepy import Stream, OAuthHandler
   from tweepy.streaming import StreamListener
   from progressbar import ProgressBar, Percentage, Bar
   import json
   import sys

   #Twitter app information
   consumer_secret='Your consumer secret'
   consumer_key='Your consumer key'
   access_token='Your access token'
   access_token_secret='Your access token secret'

   #hello number of tweets we want tooget
   max_tweets=10000

   #Create hello listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set hello counter toozero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append hello tweet toohello 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment hello number of tweets
               self.num_tweets += 1
               #Check toosee if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment hello progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get hello OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use hello listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > <span data-ttu-id="6a394-141">Hello twitter 응용 프로그램에서 다음 hello 정보로는 항목에 대 한 hello 개체 틀 텍스트를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-141">Replace hello placeholder text for hello following items with hello information from your twitter application:</span></span>
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. <span data-ttu-id="6a394-142">사용 하 여 **Ctrl + X**, 다음 **Y** toosave hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-142">Use **Ctrl + X**, then **Y** toosave hello file.</span></span>

7. <span data-ttu-id="6a394-143">다음 명령은 toorun hello 파일 hello를 사용 하 여 트 윗을 다운로드 및:</span><span class="sxs-lookup"><span data-stu-id="6a394-143">Use hello following command toorun hello file and download tweets:</span></span>

    ```bash
    python gettweets.py
    ```

    <span data-ttu-id="6a394-144">진행률 표시기가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-144">A progress indicator appears.</span></span> <span data-ttu-id="6a394-145">트 윗 다운로드 hello로 too100 %를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-145">It counts up too100% as hello tweets are downloaded.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6a394-146">진행률 표시줄 tooadvance hello에 대 한 시간이 오래 걸리면, hello 필터 tootrack 추세 항목을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-146">If it is taking a long time for hello progress bar tooadvance, you should change hello filter tootrack trending topics.</span></span> <span data-ttu-id="6a394-147">필터에 hello 항목에 대 한 많은 트 윗을 hello를 필요한 10000 트 윗 신속 하 게 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-147">When there are many tweets about hello topic in your filter, you can quickly get hello 10000 tweets needed.</span></span>

### <a name="upload-hello-data"></a><span data-ttu-id="6a394-148">Hello 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="6a394-148">Upload hello data</span></span>

<span data-ttu-id="6a394-149">tooupload hello 데이터 tooHDInsight 저장소에서 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="6a394-149">tooupload hello data tooHDInsight storage, use hello following commands:</span></span>

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

<span data-ttu-id="6a394-150">이 명령은 hello 클러스터의 모든 노드에 액세스할 수 있는 위치에 hello 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-150">These commands store hello data in a location that all nodes in hello cluster can access.</span></span>

## <a name="run-hello-hiveql-job"></a><span data-ttu-id="6a394-151">Hello HiveQL 작업 실행</span><span class="sxs-lookup"><span data-stu-id="6a394-151">Run hello HiveQL job</span></span>

1. <span data-ttu-id="6a394-152">다음 명령은 toocreate HiveQL 문을 포함 하는 파일 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-152">Use hello following command toocreate a file containing HiveQL statements:</span></span>

   ```bash
   nano twitter.hql
   ```

    <span data-ttu-id="6a394-153">콘텐츠로 사용 hello hello 파일 텍스트를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-153">Use hello following text as hello contents of hello file:</span></span>

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward hello tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate hello destination table
   DROP TABLE tweets;
   CREATE TABLE tweets
   (
       id BIGINT,
       created_at STRING,
       created_at_date STRING,
       created_at_year STRING,
       created_at_month STRING,
       created_at_day STRING,
       created_at_time STRING,
       in_reply_to_user_id_str STRING,
       text STRING,
       contributors STRING,
       retweeted STRING,
       truncated STRING,
       coordinates STRING,
       source STRING,
       retweet_count INT,
       url STRING,
       hashtags array<STRING>,
       user_mentions array<STRING>,
       first_hashtag STRING,
       first_user_mention STRING,
       screen_name STRING,
       name STRING,
       followers_count INT,
       listed_count INT,
       friends_count INT,
       lang STRING,
       user_location STRING,
       time_zone STRING,
       profile_image_url STRING,
       json_response STRING
   );
   -- Select tweets from hello imported data, parse hello JSON,
   -- and insert into hello tweets table
   FROM tweets_raw
   INSERT OVERWRITE TABLE tweets
   SELECT
       cast(get_json_object(json_response, '$.id_str') as BIGINT),
       get_json_object(json_response, '$.created_at'),
       concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
       substr (get_json_object(json_response, '$.created_at'),27,4)),
       substr (get_json_object(json_response, '$.created_at'),27,4),
       case substr (get_json_object(json_response,    '$.created_at'),5,3)
           when "Jan" then "01"
           when "Feb" then "02"
           when "Mar" then "03"
           when "Apr" then "04"
           when "May" then "05"
           when "Jun" then "06"
           when "Jul" then "07"
           when "Aug" then "08"
           when "Sep" then "09"
           when "Oct" then "10"
           when "Nov" then "11"
           when "Dec" then "12" end,
       substr (get_json_object(json_response, '$.created_at'),9,2),
       substr (get_json_object(json_response, '$.created_at'),12,8),
       get_json_object(json_response, '$.in_reply_to_user_id_str'),
       get_json_object(json_response, '$.text'),
       get_json_object(json_response, '$.contributors'),
       get_json_object(json_response, '$.retweeted'),
       get_json_object(json_response, '$.truncated'),
       get_json_object(json_response, '$.coordinates'),
       get_json_object(json_response, '$.source'),
       cast (get_json_object(json_response, '$.retweet_count') as INT),
       get_json_object(json_response, '$.entities.display_url'),
       array(
           trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
       array(
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
       trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
       trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
       get_json_object(json_response, '$.user.screen_name'),
       get_json_object(json_response, '$.user.name'),
       cast (get_json_object(json_response, '$.user.followers_count') as INT),
       cast (get_json_object(json_response, '$.user.listed_count') as INT),
       cast (get_json_object(json_response, '$.user.friends_count') as INT),
       get_json_object(json_response, '$.user.lang'),
       get_json_object(json_response, '$.user.location'),
       get_json_object(json_response, '$.user.time_zone'),
       get_json_object(json_response, '$.user.profile_image_url'),
       json_response
   WHERE (length(json_response) > 500);
   ```

2. <span data-ttu-id="6a394-154">키를 눌러 **Ctrl + X**, 키를 누릅니다 **Y** toosave hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-154">Press **Ctrl + X**, then press **Y** toosave hello file.</span></span>
3. <span data-ttu-id="6a394-155">다음 명령 toorun hello HiveQL hello 파일에 포함 된 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-155">Use hello following command toorun hello HiveQL contained in hello file:</span></span>

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    <span data-ttu-id="6a394-156">이 명령은 실행 hello hello **twitter.hql** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-156">This command runs hello hello **twitter.hql** file.</span></span> <span data-ttu-id="6a394-157">Hello 쿼리가 완료 되 면 표시 되 면 한 `jdbc:hive2//localhost:10001/>` 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-157">Once hello query completes, you see a `jdbc:hive2//localhost:10001/>` prompt.</span></span>

4. <span data-ttu-id="6a394-158">Hello beeline 프롬프트에서 다음 데이터를 가져온 쿼리 tooverify hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-158">From hello beeline prompt, use hello following query tooverify that data was imported:</span></span>

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    <span data-ttu-id="6a394-159">이 쿼리는 최대 10 개의 트 윗 hello 단어를 포함 하는 반환 **Azure** hello 메시지 텍스트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-159">This query returns a maximum of 10 tweets that contain hello word **Azure** in hello message text.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a394-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6a394-160">Next steps</span></span>

<span data-ttu-id="6a394-161">배웠습니다 어떻게 tootransform 구조화 된 Hive 테이블에는 구조화 되지 않은 JSON 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="6a394-161">You have learned how tootransform an unstructured JSON dataset into a structured Hive table.</span></span> <span data-ttu-id="6a394-162">toolearn 하이브 HDInsight에 대 한 자세한 정보 hello 다음 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6a394-162">toolearn more about Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="6a394-163">HDInsight 시작</span><span class="sxs-lookup"><span data-stu-id="6a394-163">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="6a394-164">HDInsight를 사용하여 비행 지연 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="6a394-164">Analyze flight delay data using HDInsight</span></span>](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
