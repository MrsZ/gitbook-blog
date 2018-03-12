Plan: superfly migration

![](/assets/superfly migration.png)

难点： 迁移时间很长，在迁移的过程中，用户仍然在存储新的图片

问题： 不需要cache inactive user

Final result

MaaS

![](/assets/MasS.png)

1. 如果有新用户，在两个存储位置同时创建新用户
2. 如果有新相册，在两个存储位置同时创建新相册



