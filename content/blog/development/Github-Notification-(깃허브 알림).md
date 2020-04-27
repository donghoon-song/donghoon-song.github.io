---
title: 'Github Notification (깃허브 알림)'
date: 2020-04-27 21:32:13
category: 'development'
draft: false
---

# Github Notification
### 깃허브에서 알림 기능을 활용하는 방법입니다!

[Managing notifications from your inbox](https://help.github.com/en/github/managing-subscriptions-and-notifications-on-github/managing-notifications-from-your-inbox#supported-queries-for-custom-filters)

![image](https://user-images.githubusercontent.com/32301380/80373073-7a51a400-88cf-11ea-98ba-b6def5408142.png)

기존에 알림 기능으로 사용하던 종모양 버튼을 누르면 알림을 관리할 수 있는 페이지로 이동합니다.
<br><br><br>

![image](https://user-images.githubusercontent.com/32301380/80373409-ff3cbd80-88cf-11ea-92da-5931dd34fc60.png)

오른쪽 리스트에는 전체적인 알림들이 보입니다.
왼쪽 파란부분은 필터 기능으로, 속성값에 따라서 모아볼 수 있습니다. 필터의 설정버튼을 클릭하면 필터를 커스터마이징할 수 있습니다.
<br><br><br>

![image](https://user-images.githubusercontent.com/32301380/80373611-462ab300-88d0-11ea-9bbf-d81492f1322d.png)
<br><br><br>

그림에서 제 KNUCafeMap이라는 repository에서 review-request를 필터링하는 커스텀 필터를 만들어보았습니다.
```
Name : KNUCafeMap review-requested
Filter inbox by... : repo:Donghoon759/KNUCafeMap reason:review-requested
```
![image](https://user-images.githubusercontent.com/32301380/80374193-3fe90680-88d1-11ea-83a2-27420527aeaf.png)
커스텀 필터는 15개까지 등록할 수 있다고 합니다.
커스텀 필터는 필터 쿼리를 사용해 커스터마이징할 수 있으며, 쿼리의 종류는 다음과 페이지에서 확인할 수 있습니다. [Supported queries for custom filters](https://help.github.com/en/github/managing-subscriptions-and-notifications-on-github/managing-notifications-from-your-inbox#supported-queries-for-custom-filters)<br><br>

`repo:아이디/저장소이름` 형식으로 작성하시면 됩니다 :)
<br><br><br>
![image](https://user-images.githubusercontent.com/32301380/80374265-63ac4c80-88d1-11ea-8d73-3548a00a115c.png)
필터 만드는게 익숙하지 않으시다면 검색창에서 마우스로 클릭하여 쿼리를 만들수도 있으니 너무 겁먹지 마세요.

깃허브에서 받고 싶은 알림들만 받을 수 있어서 좋은 거 같습니다! 다양한 활용 케이스들이 공유되었으면 하네요