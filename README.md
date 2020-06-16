# 51% 공격

본 실험에서는 51% 공격을 재현하는것을 목표로 한다. 특히 6컨펌 이후 51% 공격이 일어난다면 확정된 거래도 무효가 되는지 확인한다.

실험의 시나리오는 다음 사진과 같다

<img width="838" alt="내가 하려는거 개요도" src="https://user-images.githubusercontent.com/33947681/84632268-9e258380-af29-11ea-8250-ed3e6e25fee6.png">

실험환경은 비트코인 하드포크를 진행해 영석코인을 만들고 진행하였다.

해시파워의 경우 cpuminer(cpu채굴기)를 이용해 각각 블록을 100개씩 생성하였을때 나온 해시파워의 평균값을 기준으로 하였다.

이때 공격자는 평균 40928 khash/s 가 측정되었고 정상적인 유저는 평균 10145.5 khash/s가 측정되었다.

그래서 같은 환경의 정상적인 유저를 4명이라 가정하였고 이때 해시파워는 40580 khash/s가 되어 

공격자 50.2% 정상적인 유저들 49.8% 해시파워를 가진 환경을 구성하였다.

다음 사진은 공격자와 정상적 유저의 해시파워 값이다.



실험은 영석코인의 459번째 블록을 만든후 공격자가 정상적유저1에게 1000YSC를 보냈다. 
그후 공격자는 정상적 유저와 연결을 끊고 460번째 블록부터 467번째 블록까지 만들었다.
이때 공격자가 만든 블록은 본인에게 돌아가는 블록보상을 제외하고 어느 트랜잭션도 포함시키지 않는다.
정상적인 유저들도 460번째 블록에 정상적유저1에 1000YSC가 전송된 거래를 포함한 블록을 생성후 466번째 블록까지 만들었다.

다음 사진은 실제 생성된 블록들의 해시값을 가져와 보여준다.

[정상적 유저들의 블록해시값]

<img width="496" alt="정상적 사용자 해시블록" src="https://user-images.githubusercontent.com/33947681/84633873-ffe6ed00-af2b-11ea-80ae-6cba94fbac7e.png">

[공격자의 블록 해시값]

<img width="328" alt="공격자가 만든 블록해시" src="https://user-images.githubusercontent.com/33947681/84633879-01b0b080-af2c-11ea-84cb-82b204de2aaf.png">


이를 보기 쉽게 그림으로 표현하면

[정상적 유저와 공격자 해시값]
<img width="1033" alt="정상적 유저와 공격자 해시값" src="https://user-images.githubusercontent.com/33947681/84632282-a1b90a80-af29-11ea-85a2-7c73c745d5d9.png">

이와같은 해시값을 가지는 블록을 생산하였다.


이때 정상적유저1은 1000YSC를 받고 6컨펌이 지났기에 1000YSC의 거래를 확정짓고 본인 잔액에 포함시킨다.

[6컨펌 이후 트랜잭션], [6컨펌 이후 잔액]
<img width="526" alt="공격전 잔액" src="https://user-images.githubusercontent.com/33947681/84633882-02e1dd80-af2c-11ea-8ed8-eca6a611b127.png"><img width="472" alt="벤치1컴 6컨펌 이후 1000비트코인 전송 트랜잭션 상태 복사본" src="https://user-images.githubusercontent.com/33947681/84633886-04130a80-af2c-11ea-9c85-da3e7a1687bd.png">


마지막으로 공격자는 본인의 블록을 정상적인 유저들과 연결한다.

[공격받은사진]<img width="1062" alt="공격받은사진" src="https://user-images.githubusercontent.com/33947681/84632288-a2ea3780-af29-11ea-96d7-0bf49275bd95.png">

이 사진에서 알수있는점은 공격자가 정상적인 유저들보다 블록을 하나 더 만들었기에 공격자의 블록이 정상적인 블록이라 판단하고 

공격자와 블록값이 달라지는 시점인 460번째 블록부터 467번째 블록까지는 기존의 블록을 버리고 공격자의 블록과 동기화 한다.

또한 정상적인 유저들이 만든 1000YSC가 포함된 460번째 블록이 사라지게 되므로 정상적인 유저1이 받았던 1000YSC또한 받기 이전으로 돌아가게 된다.

이를통해 거래가 확정되는 6컨펌 이후에도 51% 공격이 일어나게 된다면 거래내역이 과거로 돌아가게 되는 치명적인 일이 일어날수 있음을 확인하였다.
