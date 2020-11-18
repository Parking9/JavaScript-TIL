# Algorithms By JS

## 프로그래머스 기능개발

> [문제](https://programmers.co.kr/learn/courses/30/lessons/42586?language=javascript)

```javascript
function solution(progresses, speeds) {
    let len = progresses.length
    let days =0
    let answer =[]
    let now =0
    while(len>0){
        let progress = progresses.shift()
        let speed = speeds.shift()
        if(progress + days*speed >=100){
            len-=1
            answer[answer.length-1]+=1
        }else{
            days  +=  Math.ceil((100-progress-speed*days)/speed)
            len-=1
            answer.push(1)
        }
    }
    return answer;
}
```

