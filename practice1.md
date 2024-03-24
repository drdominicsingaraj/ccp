1. QUESTION

Which service offers volume discounts when you enable Consolidated Billing? 

    Amazon SNS
    Amazon S3 (Answer)
    AWS CloudTrail
    Amazon CloudFront

Explanation: 

When you enable Consolidated Billing in AWS, some services offer volume discounts. For billing purposes, AWS treats all the accounts in the organization as if they were one account. Services such as Amazon S3 have volume pricing tiers that give you lower prices the more you use the service. With consolidated billing, AWS combines the usage from all accounts to determine which volume pricing tiers to apply, potentially giving you a lower overall price1.

So, among the options you’ve provided, Amazon S3 is the service that offers volume discounts when you enable Consolidated Billing.

For example, let's say that Bob's consolidated bill includes both Bob's own account and Susan's account. Bob's account is the management account, so he pays the charges for both himself and Susan.
Bob transfers 8 TB of data during the month and Susan transfers 4 TB.

For the purposes of this example, AWS charges $0.17 per GB for the first 10 TB of data transferred and $0.13 for the next 40 TB. This translates into $174.08 per TB (= .17*1024) for the first 10 TB, and $133.12 per TB (= .13*1024) for the next 40 TB. Remember that 1 TB = 1024 GB.

Reference : 
https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/useconsolidatedbilling-effective.html#useconsolidatedbilling-discounts
