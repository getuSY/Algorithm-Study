### Algorithm_20220510 : 2022 카카오 Recruitment

### lv.1- 신고 결과 받기

```python
def solution(id_list, report, k):
    print(id_list)
    print(k)
    people = len(id_list)
    singo = len(report)
    repo_lst = set()
    reported = [[] for _ in range(people)]
    mail = dict()
    for p in range(people):
        mail[id_list[p]] = 0
    print(mail)
    for i in range(singo):
        tmp = tuple(report[i].split())
        repo_lst.add(tmp)
    print(repo_lst)
    repo_lst = list(repo_lst)
    print(repo_lst)
    for j in range(len(repo_lst)):
        for k in range(people):
            if id_list[k] == repo_lst[j][1]:
                reported[k].append(repo_lst[j][0])
    print(reported)
    for r in reported:
        print(len(r))
        if len(r) >= k:
            print('k 이상')
            for person in r:
                mail[person] = mail[person] + 1
    print(mail)
    answer = [[0] for sth in range(people)]
    for a in range(people):
        answer[a] = mail[id_list[a]]
    print(answer)
    return answer
```

- 헤맨 부분 :  신고가 k번 이상 들어간 유저를 정지시키고 그 유저를 신고한 유저에게 메일을 보내주는 if문, `if len(r) >= k:`를 설정하였는데 반대로 작동했다. `if len(r) < k:`로 작성하면 또 애매한 경우가 있는데 일단 반대로 작동하는 걸 대체 어떻게 해결해야 할 지 모르겠다...

```python
def solution(id_list, report, k):
    people = len(id_list)
    repo_lst = set()
    reported = [[] for _ in range(people)]
    mail = dict()
    for p in range(people):
        mail[id_list[p]] = 0
    for i in range(len(report)):
        tmp = tuple(report[i].split())
        repo_lst.add(tmp)
    repo_lst = list(repo_lst)
    for j in range(len(repo_lst)):
        for k in range(people):
            if id_list[k] == repo_lst[j][1]:
                reported[k].append(repo_lst[j][0])
    for r in reported:
        if len(r) == k or len(r) > k:      # 여기 조건문 왜 안 맞지???
            print('k 이상')
            for person in r:
                mail[person] = mail[person] + 1
    answer = [[0] for sth in range(people)]
    for a in range(people):
        answer[a] = mail[id_list[a]]
    return answer
```

- 헤맨 부분 : k가 왜 자꾸 조건문에 안 걸리는지 찾음!! 앞에 for j 문 안에 for k 로 변수를 작성해서 이전의 k를 자꾸 읽어오는 거였음. for문 밖에서는 k가 안 읽혀야 하는 것 아닌가 싶지만 변수 바꾸면 해결될 것 같다.
- 테스 3, 11 시간 초과가 뜬다.

```python
def solution(id_list, report, k):
    people = len(id_list)
    repo_lst = set()
    reported = [[] for _ in range(people)]
    mail = dict()
    for p in range(people):
        mail[id_list[p]] = 0
    for i in range(len(report)):
        tmp = tuple(report[i].split())
        repo_lst.add(tmp)
    repo_lst = list(repo_lst)
    for j in range(len(repo_lst)):
        for p in range(people):
            if id_list[p] == repo_lst[j][1]:
                reported[p].append(repo_lst[j][0])
    for r in reported:
        if len(r) == k or len(r) > k:
            for person in r:
                mail[person] = mail[person] + 1
    answer = [[0] for sth in range(people)]
    for a in range(people):
        answer[a] = mail[id_list[a]]
    return answer
```

- 어려웠던 부분 : 테스트 3과 11에서 시간 초과가 뜨는데 어떻게 해야할지 모르겠다. 확인해보니 테스트케이스 9, 10, 14, 15, 20, 21에서 유독 시간이 오래 걸린다.

```python
def solution(id_list, report, k):
    people = len(id_list)
    repo_lst = set()
    reported = [set() for _ in range(people)]
    mail = dict()
    for p in range(people):
        mail[id_list[p]] = 0
    for i in range(len(report)):
        tmp = tuple(report[i].split())
        for p in range(people):
            if id_list[p] == tmp[1]:
                reported[p].add(tmp[0])
    for r in reported:
        if len(r) >= k:
            for person in r:
                mail[person] = mail[person] + 1
    answer = [[0] for sth in range(people)]
    for a in range(people):
        answer[a] = mail[id_list[a]]
    return answer
```

- 시간 초과가 필요 없는 과정에서 일어나는 것은 아닐까 싶어 생략할 수 있는 부분을 생략했더니 오히려 3, 11, 15, 21에서 시간 초과가 일어났다.



### lv.2 - k진수에서 소수 개수 구하기

```python
def solution(n, k):
    result = ''
    num = int(n)
    print(num)
    while num > 0:
        tmp = num % k
        result = result + str(tmp)
        num = num // k
    print(result)
    answer = -1
    return answer
```



### lv2. 주차 요금 계산

```python
def solution(fees, records):
    print(fees)
    std_time= fees[0]
    std_fee = fees[1]
    ex_time = fees[2]
    ex_fee = fees[3]
    print(records)
    parking = dict()
    parked = []
    acc = dict()
    for i in range(len(records)):
        tmp = tuple(records[i].split())
        print(tmp)
        time = list(tmp[0].split(':'))
        print(time)
        h = int(time[0])
        m = int(time[1])
        if tmp[2] == 'IN':
            if parking.get(tmp[1], None) == None:
                parking[tmp[1]] = tmp[0]
                parked.append(tmp[1])
            elif parking.get(tmp[1]) != None:
                in_time = list(parking[tmp[1]].split(':'))
                print(time)
                in_h = int(in_time[0])
                in_m = int(in_time[1])
                acc[tmp[1]] = acc.get(tmp[1], 0) + (h - in_h)*60 + (m - in_m)
                parking[tmp[1]] = tmp[0]
        elif tmp[2] == 'OUT':
            in_time = list(parking[tmp[1]].split(':'))
            print(time)
            in_h = int(in_time[0])
            in_m = int(in_time[1])
            print(in_h, in_m, h, m)
            acc[tmp[1]] = acc.get(tmp[1], 0) + (h - in_h)*60 + (m - in_m)
            parking[tmp[1]] = None
            parked.remove(tmp[1])
    for p in parked:
        in_time = list(parking[p].split(':'))
        print(time)
        in_h = int(in_time[0])
        in_m = int(in_time[1])
        acc[p] = acc.get(p, 0) + (23 - in_h)*60 + (59 - in_m)
        
    print(acc)
    car_nums = list(acc.keys())
    print(car_nums)
    car_nums.sort()
    answer = []
    for car in car_nums:
        t = acc[car]
        if t <= std_time:
            answer.append(std_fee)
        else:
            calc = 0
            if t % ex_time == 0:
                calc = (t - std_time)/ex_time
            else:
                calc = (t - std_time)//ex_time + 1
            topay = std_fee + ex_fee*calc
            answer.append(topay)
    return answer
```

- 헤맨 부분:

```python
def solution(fees, records):
    std_time= fees[0]
    std_fee = fees[1]
    ex_time = fees[2]
    ex_fee = fees[3]
    parking = dict()
    parked = []
    acc = dict()
    for i in range(len(records)):
        tmp = tuple(records[i].split())
        time = list(tmp[0].split(':'))
        h = int(time[0])
        m = int(time[1])
        if tmp[2] == 'IN':
            if parking.get(tmp[1], None) == None:
                parking[tmp[1]] = tmp[0]
                parked.append(tmp[1])
            elif parking.get(tmp[1]) != None:
                in_time = list(parking[tmp[1]].split(':'))
                in_h = int(in_time[0])
                in_m = int(in_time[1])
                acc[tmp[1]] = acc.get(tmp[1], 0) + (h - in_h)*60 + (m - in_m)
                parking[tmp[1]] = tmp[0]
        elif tmp[2] == 'OUT':
            in_time = list(parking[tmp[1]].split(':'))
            in_h = int(in_time[0])
            in_m = int(in_time[1])
            acc[tmp[1]] = acc.get(tmp[1], 0) + (h - in_h)*60 + (m - in_m)
            parking[tmp[1]] = None
            parked.remove(tmp[1])
    for p in parked:
        in_time = list(parking[p].split(':'))
        in_h = int(in_time[0])
        in_m = int(in_time[1])
        acc[p] = acc.get(p, 0) + (23 - in_h)*60 + (59 - in_m)
    car_nums = list(acc.keys())
    car_nums.sort()
    answer = []
    for car in car_nums:
        t = acc[car]
        if t <= std_time:
            answer.append(std_fee)
        else:
            calc = 0
            if t % ex_time == 0:
                calc = (t - std_time)/ex_time
            else:
                calc = (t - std_time)//ex_time + 1
            topay = std_fee + ex_fee*calc
            answer.append(topay)
    return answer
```

- 16개 테스트 케이스 중 10개 통과
- 중복되는 코드가 너무 많아서 일단 축약하고자 함

```python
```



### lv2. 양궁대회

```python
def solution(n, info):
    arrow = n
    print(info)
    target = [[0] for _ in range(11)]
    answer = [-1]
    for i in range(11):
        if info[i] == 0:
            pass
        else:
            if info[]
        
    
    return answer
```



### lv 3. 양과 늑대

```python
def solution(info, edges):
    num = len(info)
    lines = [[0]*2 for _ in range(num)]
    child = [0]*num
    for edge in edges:
        if lines[edge[0]][0] == 0:
            lines[edge[0]][0] = edge[1]
        else:
            lines[edge[0]][1] = edge[1]
        child[edge[1]] = edge[0]
    print(lines)
    print(child)
    visited = [0]*num
    
    ramb = 1
    wolf = 0
    visited[0] = 1
    start = 0
    # while True:
    #     if sum(lines[start]) == 2:
    #         ramb += 2
    #         visited[lines[start][0]] = 1
    #         visited[lines[start][1]] = 1
    #     elif info[lines[start][0]] == 0 or info[lines[start][1]] == 0:
    #         ramb += 1
    #     elif sum(lines[start]) == 0:
    #         pass
        
    answer = 0
    return answer
```

- 문제 풀이 : 처음에는 부모 노드에 대한 자식 노드를 표현해서 root에서부터 타고내려가는 방식을 생각했는데, 늑대의 수가 적은 길로 먼저 가야한다는 것을 생각해서 자식 노드에 대해 부모 노드를 표현하여 양이 있는 자식 노드에서부터 root까지 타고 올라가는 방식으로 풀이하고자 함.

```python
# 자식 노드에 대해 부모를 표현 > 조상 파악
def solution(info, edges):
    num = len(info)
    lines = [[0]*2 for _ in range(num)]
    child = [0]*num
    for edge in edges:
        if lines[edge[0]][0] == 0:
            lines[edge[0]][0] = edge[1]
        else:
            lines[edge[0]][1] = edge[1]
        child[edge[1]] = edge[0]
    print(lines)
    print(child)
    visited = [0]*num
    cnt = [0]*num
    for i in range(1, num):
        next = i
        r = 0
        w = 0
        while next != 0:
            next = child[next]
            if info[next] == 0:
                r += 1
            elif info[next] == 1:
                w += 1
        cnt[i] = (r, w)
    print(cnt)
    start = 0
    visited[0] = 1
    while True:
        left = lines[start][0]
        right = lines[start][1]
        if child[left][0] > child[left][1] and child[right][0] > child[right][1]:
            pass
        elif child[left][0] > child[left][1] and child[right][0] < child[right][1]:
            pass
        elif child[left][0] < child[left][1] and child[right][0] > child[right][1]:
            pass
        elif child[left][0] < child[left][1] and child[right][0] < child[right][1]:
            for j in range(1, start):
                if visited[j] == 0:
                    start = j
                    break
                
                    
        
    answer = 0
    return answer
```

