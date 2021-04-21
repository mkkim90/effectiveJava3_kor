클라이언트에서 직접 형변환해야 하는 타입보다 제너릭 타입이 더 안전-> 새로운 타입을 설계할 떄는 형변환 없이도 사용할 수 있도록 하라.

//String의 toUpperCase 메서드를 호출할 때 명시적 형변환을 수행하지 않으며 이형변환이 항상 성공함을 보장 
```  
public static void main(String[] args) { 
  Stack stack = new Stack<>(); 
                                          
  for (String arg : args) stack.push(arg); 
                                          
  while (!stack.isEmpty()); System.out.println(stack.pop().toUpperCase()); 
}
```
