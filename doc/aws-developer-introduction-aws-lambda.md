# aws-developer-introduction-aws-lambda

## 作業

### 作業01 建立 Policy準備進行 demo

* [AWS Policy Generator](https://awspolicygen.s3.amazonaws.com/policygen.html)

1. 前往 AWS Policy Generator
2. 在step1, 選擇 IAM Policy
3. 在step2, 將 Effect = allow, AWS Service = Amazon SES, Action = 打星(全允許), ARN也是打星星。
4. 添加 statement，Condition = ArnEquals, Key = aws:CurrentTime
5. 在step3, 產生 Policy, 產生出一個 JSON Document 包含 policy的內容。


