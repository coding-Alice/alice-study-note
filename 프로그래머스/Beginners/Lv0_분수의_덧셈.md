# 분수의 덧셈

### **문제 설명**

첫 번째 분수의 분자와 분모를 뜻하는 denum1, num1, 두 번째 분수의 분자와 분모를 뜻하는 denum2, num2가 매개변수로 주어집니다. 두 분수를 더한 값을 기약 분수로 나타냈을 때 분자와 분모를 순서대로 담은 배열을 return 하도록 solution 함수를 완성해보세요.

---

### **제한사항**

0 <denum1, num1, denum2, num2 < 1,000

---

### **입출력 예**

|denum1|num1|denum2|num2|result|
|-|-|-|-|-|
|1	|2	|3	|4	|[5, 4]|
|9	|2	|1	|3	|[29, 6]|

---

### **입출력 예 설명**

입출력 예 #1

- 1 / 2 + 3 / 4 = 5 / 4입니다. 따라서 [5, 4]를 return 합니다.

입출력 예 #2

- 9 / 2 + 1 / 3 = 29 / 6입니다. 따라서 [29, 6]을 return 합니다.

---

### **Solution.js**

```javascript
function getFactors(n)
{
    var res = [];
    while (n%2 == 0) {
        res.push(2)
        n = n/2
    }
    
    for (var i=3;i*i <= n;i=i+2) {
        while (n%i==0) {
            res.push(i)
            n = n/i
        }
    }
    if (n>2) {
        res.push(n)
    }
    return res;
}

const intersection = (arr1, arr2) => {
   const dict = {};
   const res = [];
    
    // dictionary 생성해서 array1의 숫자별로 횟수 추가 
    arr1.forEach(a => {
      dict[a] = dict[a] ? dict[a] + 1 : 1;
   })
   

    // 똑같은 숫자가 있는 경우에 횟수 차감하고 array에 추가
    for(let key of arr2) {
      if(key in dict && dict[key] > 0) {
         res.push(key);
         dict[key]--;
      }
   }
   return res;
};

function solution(denum1, num1, denum2, num2) {
    let denum, num, res;
    denum = denum1*num2 + denum2*num1;
    num = num1*num2;
    
    //소인수 분해
    numSet = getFactors(num);
    denumSet = getFactors(denum);
    // 교집합, 반복되는 숫자 포함
    res = intersection(numSet, denumSet);
    // 최소 공배수 
    mulNum = res.reduce((a,b) => a*b, 1)
    
    if(res.length == 0)
        return [denum, num]
    else
    {
        return [denum/mulNum, num/mulNum]
    }
    
}

```
