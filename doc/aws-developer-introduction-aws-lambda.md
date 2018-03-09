# aws-developer-introduction-aws-lambda

## 作業

### 作業01 建立 Policy準備進行 demo

* [AWS Policy Generator](https://awspolicygen.s3.amazonaws.com/policygen.html)

1. 前往 AWS Policy Generator
2. 在step1, 選擇 IAM Policy
3. 在step2, 將 Effect = allow, AWS Service = Amazon SES, Action = 打星(全允許), ARN也是打星星。
4. 添加 statement，Condition = ArnEquals, Key = aws:CurrentTime
5. 在step3, 產生 Policy, 產生出一個 JSON Document 包含 policy的內容。

### 作業02 新增一個 Lambda function

1. Lambda -> New Function -> Select blueprint, 找 lambda-canary (選2.7)
2. 在 Basic info區，
    2.1. Name = the_woof_garden_canary2 , 
    2.2. Role = "Choose new role from template(s), 
    2.3. Role name = woof_garden_canary
    2.4. Policy templates = <不選>
3. 在 cloudwatch-events區，建立新 rule, name = five_min, schedule expression = rate(5 minutes)。記得 Enable trigger 先不要勾，因為我們要先測試。
4. 填入環境變數，site = http://thewoofgarden.com/ , expected = "We help all of your pets grow"
5. 設定 handler = lambda_function.lambda_handler (PS: file_name.function_name)
6. (舊介面可以設定) 記憶體 = 128, 0~10秒
7. 創造 function 完畢之後可以在 "select a test event" 選擇測試。(1) create new test event, (2)Scheduled Event, (3) name=testFiveMinLambdaCanary1
8. 測試結果可以點開 Cloud Watch , 先點在左側清單 Alarms, 點選 create Alarm。選Lambda Metrics的 By Function Name。選 the_woof_garden_canary2 的 Metric Name = Errors -> Next
9. 替 Alarm 取名字。並且選擇 is >= 1. 加一個 notification list 加上我的 email 。系統會要求確認該 email.


測試 template如下
```
{
  "account": "123456789012",
  "region": "us-east-1",
  "detail": {},
  "detail-type": "Scheduled Event",
  "source": "aws.events",
  "time": "1970-01-01T00:00:00Z",
  "id": "cdc73f9d-aea9-11e3-9d5a-835b769c0d9c",
  "resources": [
    "arn:aws:events:us-east-1:123456789012:rule/my-schedule"
  ]
}
```
