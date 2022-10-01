# 1308-
'''캠프에 오게 된 송유진은 캠프가 너무 지루해서 오늘로부터 캠프가 끝날 때 까지 며칠이나 남았는지 알아보고 싶었다. 
그런데 캠프는 비상식적으로 길지도 몰라서 (윤년을 포함할지도 모른다) 손으로 하나하나 세기에는 힘들어 보였다.

더욱 정확한 계산을 위해, 유진이는 윤년이 정해지는 기준을 찾아보았고, 그것은 다음과 같았다.

서력기원 연수가 4로 나누어떨어지는 해는 우선 윤년으로 한다. (2004년, 2008년, …)
100으로 나누어떨어지는 해는 평년으로 한다. (2100년, 2200년, …)
400으로 나누어떨어지는 해는 다시 윤년으로 한다. (1600년, 2000년, …)
그런데 캠프가 너무 길 경우, 사춘기인 유진이는 캠프에 무단으로 빠질지도 모른다.

입력
첫째 줄에 오늘의 날짜가 주어지고, 두 번째 줄에 D-Day인 날의 날짜가 주어진다. 
날짜는 연도, 월, 일순으로 주어지며, 공백으로 구분한다. 입력 범위는 1년 1월 1일부터 9999년 12월 31일 까지 이다. 
오늘의 날짜는 항상 D-Day보다 앞에 있다.

출력
오늘부터 D-Day까지 x일이 남았다면, "D-"를 출력하고 그 뒤에 공백 없이 x를 출력한다. 
만약 캠프가 천년 이상 지속된다면 (오늘이 y년 m월 d일이고, D-Day가 y+1000년 m월 d일과 같거나 늦다면) 대신 "gg"를 출력한다.
오늘이 2월 29일인 경우는 주어지지 않는다.'''

a=input()
b=input()

a=a.split()
b=b.split()
for i in range(3):
    a[i]=int(a[i])
    b[i]=int(b[i])
def day(x,y,z):    
    result=0
    result=x*365
    for i in range(x):
        if i%4==0:
            result+=1
            if i%100==0:
                result+=-1
                if i%400==0:
                    result+=1
                    
    lst=[i for  i in range(x+1) if i%4==0]
    lst1=[i for i in range(x+1) if i%100==0]
    lst2=[i for i in range(x+1) if i%400==0]
    for i in lst1:
        lst.remove(i)
    for j in lst2:
        lst.append(j)
    
    for i in range(1,y):
        if ((x in lst) and i==2):
            result+=29
        elif ((x not in lst) and i==2):
            result+=28
        elif i in (4,6,9,11):
            result+=30
        else:
            result+=31
    result= z+result
    return result
if b[0]>a[0]+1000:
    print("gg")
elif b[0]==a[0]+1000 and b[1]>a[1]:
    print("gg")
elif b[0]==a[0]+1000 and b[1]==a[1]and b[2]>=a[2]:
    print("gg")
else:
    print('D-{}'.format(int(day(b[0],b[1],b[2]))-int(day(a[0],a[1],a[2]))))
