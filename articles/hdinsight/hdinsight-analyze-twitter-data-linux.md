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
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a>HDInsight에서 Hive 및 Hadoop을 사용하여 Twitter 데이터 분석

자세한 내용은 방법 toouse Apache Hive tooprocess Twitter 데이터입니다. hello 결과 hello 특정 단어를 포함 하는 대부분 트 윗을 보낼 Twitter 사용자의 목록입니다.

> [!IMPORTANT]
> 이 문서의 단계 hello HDInsight 3.6에서 테스트 되었습니다.
>
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a name="get-hello-data"></a>Hello 데이터 가져오기

Twitter 있습니다 tooretrieve hello [각 트 윗에 대 한 데이터](https://dev.twitter.com/docs/platform-objects/tweets) REST API를 통해 개체 JSON (JavaScript Notation) 문서와 합니다. [OAuth](http://oauth.net) 인증 toohello API에 필요 합니다.

### <a name="create-a-twitter-application"></a>Twitter 응용 프로그램 만들기

1. 웹 브라우저에서 로그인 너무[https://apps.twitter.com/](https://apps.twitter.com/)합니다. Hello 클릭 **등록 지금** Twitter 계정이 없는 경우 연결 합니다.

2. **Create New App**을 클릭합니다.

3. **Name**, **Description**, **Website**를 입력합니다. Hello에 대 한 URL을 만들 수 **웹 사이트** 필드입니다. 다음 표에서 hello 몇 가지 샘플 값 toouse를 보여 줍니다.

   | 필드 | 값 |
   |:--- |:--- |
   | 이름 |MyHDInsightApp |
   | 설명 |MyHDInsightApp |
   | Website |http://www.myhdinsightapp.com |

4. **Yes, I agree**를 선택한 후 **Create your Twitter application**을 클릭합니다.

5. Hello 클릭 **권한을** 탭 hello 기본 권한은 **읽기 전용**합니다.

6. Hello 클릭 **키와 액세스 토큰이** 탭 합니다.

7. **Create my access token**을 클릭합니다.

8. 클릭 **테스트 OAuth** hello 페이지의 hello 오른쪽 위 모서리에 있습니다.

9. **consumer key**, **Consumer secret**, **Access token** 및 **Access token secret**을 기록해 둡니다.

### <a name="download-tweets"></a>트윗 다운로드

hello Python 코드 다음에 저장 하 고 Twitter에서 10, 000 트 윗 다운로드 라는 tooa 파일 **tweets.txt**합니다.

> [!NOTE]
> 단계를 수행 하는 hello Python가 이미 설치 되어 있으므로 hello HDInsight 클러스터에서 수행 됩니다.

1. SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다.

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

3. 사용 하 여 hello 다음 명령을 tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2), 및 기타 필요한 패키지:

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

4. 사용 하 여 hello 다음 명령은 toocreate 이라는 파일로 내보내집니다 **gettweets.py**:

   ```bash
   nano gettweets.py
   ```

5. 콘텐츠로 사용 hello hello 텍스트를 다음으로 사용 하 여 hello **gettweets.py** 파일:

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
    > Hello twitter 응용 프로그램에서 다음 hello 정보로는 항목에 대 한 hello 개체 틀 텍스트를 바꿉니다.
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. 사용 하 여 **Ctrl + X**, 다음 **Y** toosave hello 파일입니다.

7. 다음 명령은 toorun hello 파일 hello를 사용 하 여 트 윗을 다운로드 및:

    ```bash
    python gettweets.py
    ```

    진행률 표시기가 나타납니다. 트 윗 다운로드 hello로 too100 %를 계산 합니다.

   > [!NOTE]
   > 진행률 표시줄 tooadvance hello에 대 한 시간이 오래 걸리면, hello 필터 tootrack 추세 항목을 변경 해야 합니다. 필터에 hello 항목에 대 한 많은 트 윗을 hello를 필요한 10000 트 윗 신속 하 게 가져올 수 있습니다.

### <a name="upload-hello-data"></a>Hello 데이터 업로드

tooupload hello 데이터 tooHDInsight 저장소에서 다음 명령을 사용 하 여 hello:

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

이 명령은 hello 클러스터의 모든 노드에 액세스할 수 있는 위치에 hello 데이터를 저장 합니다.

## <a name="run-hello-hiveql-job"></a>Hello HiveQL 작업 실행

1. 다음 명령은 toocreate HiveQL 문을 포함 하는 파일 hello를 사용 합니다.

   ```bash
   nano twitter.hql
   ```

    콘텐츠로 사용 hello hello 파일 텍스트를 다음 hello를 사용 합니다.

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

2. 키를 눌러 **Ctrl + X**, 키를 누릅니다 **Y** toosave hello 파일입니다.
3. 다음 명령 toorun hello HiveQL hello 파일에 포함 된 hello를 사용 합니다.

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    이 명령은 실행 hello hello **twitter.hql** 파일입니다. Hello 쿼리가 완료 되 면 표시 되 면 한 `jdbc:hive2//localhost:10001/>` 프롬프트입니다.

4. Hello beeline 프롬프트에서 다음 데이터를 가져온 쿼리 tooverify hello를 사용 합니다.

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    이 쿼리는 최대 10 개의 트 윗 hello 단어를 포함 하는 반환 **Azure** hello 메시지 텍스트에 있습니다.

## <a name="next-steps"></a>다음 단계

배웠습니다 어떻게 tootransform 구조화 된 Hive 테이블에는 구조화 되지 않은 JSON 데이터 집합입니다. toolearn 하이브 HDInsight에 대 한 자세한 정보 hello 다음 문서를 참조 하세요.

* [HDInsight 시작](hdinsight-hadoop-linux-tutorial-get-started.md)
* [HDInsight를 사용하여 비행 지연 데이터 분석](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
