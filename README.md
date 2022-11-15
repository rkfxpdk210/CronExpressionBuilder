# CronExpressionBuilder
#### 사용 방법
```
String exp = "10_0*_0*_0_0"
CronExpressionBuilder cronExpBuilder = new CronExpressionBuilder(exp);
String cronExp = cronExpBuilder.build(); // "10 * * * * ?"
String startTime = "2022-10-10 12:12:30"
String nextStartTime = cronExpBuilder.getNextStartTime(startTime,null) // "2022-10-10 12:12:40"
```

#### Method
```
build(): 저장된 날짜 정보에 맞게 Cron식 생성
getNextStartTime(String startTime, String format): startTime 이후 해당 Cron식을 적용한 다음 시작 시간을 입력한 format에 맞게 변환하여 return.
startTime의 포맷은 입력한 format과 같아야한다.
format의 default는 "yyyy-mm-dd hh:MM:ss"이며 default로 설정하고 싶으면 format을 null로 선언한다. ex) getNextStartTIme(startTime,null)
```

#### 유의 사항
```
"Second(*)_Minute(*)_Hour(*)_Date(*)_Month(*)" 형식으로 입력된 포맷을 파싱하여 Cron식 생성
*이 붙을 경우 "마다"로 인식
Date, Month는 0일 경우 "*"로 대체
DayOfWeek, Year는 고려하지 않는다.
```

#### 예시
```
EX) "10*_0_0_0_0" ==> "0/10 0 0 * * ?" ==> 매일 00시 00분에 00초부터 10초마다 작업
EX) "0_0*_0_0_0" ==> "0 * 0 * * ?"  ==> 매일 00시 00분부터 1분마다 00초에 작업
EX) "0_20_0*_3*_0" ==> "0 20 * 0/3 0" ==> 매월 00일부터 3일마다 매시 20분 00초에 작업
```
