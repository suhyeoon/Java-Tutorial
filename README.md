#  μλ°(Java)

## πμ€λ λ(thread)μ μν
μλ°μ μ€λ λλ μμμ μμ μμ μλμ μν μ€ νλλ‘ μ‘΄μ¬ν©λλ€.

1. New
2. Runnable
3. Blocked
4. Waiting
5. Timed Waiting
6. Terminated

μλμ λ€μ΄μ΄κ·Έλ¨μ μμμ μκ°μ λ€μν μ€λ λμ μνλ₯Ό λνλλλ€.

![thread status diagram](https://i.imgur.com/WaCy0Jf.png)

μΆμ²: <https://www.geeksforgeeks.org/lifecycle-and-states-of-a-thread-in-java/>

1. New Thread: μλ‘μ΄ μ€λ λκ° μμ±λλ©΄, `new` μνμλλ€. μ΄ μνμ μλ μ€λ λλ μμ§ μ€νλμ§ μμμ΅λλ€. μ€λ λκ° `new` μνμ μμΌλ©΄, μ½λκ° μμ§ μ€νλμ§ μμκ³ , μμλμ§ μμ κ²μλλ€.
2. Runnable μν: μ€νν  μ€λΉκ° λ μ€λ λλ `runnable` μνλ‘ μ΄λν©λλ€. μ΄ μνμμλ μ€λ λκ° μ΄λ―Έ μ€νμ€μ΄κ±°λ, μΈμ λ μ§ μ€νλ  μ€λΉκ° λμ΄μμ μ μμ΅λλ€. μ€λ λκ° μ€νλ  μκ°μ μ£Όλ κ²μ μ€λ λ μ€μΌμ₯΄λ¬μ μ±μμλλ€.  
   λ©ν° μ€λ λ νλ‘κ·Έλ¨μμλ κ° μ€λ λμ κ³ μ λ μκ°μ΄ ν λΉλ©λλ€. κ°κ°μ λͺ¨λ  μ€λ λλ μ μλμ μ€ν λ λ€μ μΌμ μ€μ§νκ³  λ€λ₯Έ μ€λ λκ° μ€ν λ  μ μλλ‘ CPUλ₯Ό λ€λ₯Έ μ€λ λμ μλν©λλ€. μ΄λ κ² λλ©΄, μ€νν  μ€λΉκ° λμκ±°λ, CPUλ₯Ό κΈ°λ€λ¦¬κ³  μκ±°λ, μ΄λ―Έ μ€νμ€μΈ λͺ¨λ  μ€λ λλ€μ΄ `runnable` μνλ‘ μκ²λ©λλ€.
3. Blocked/Waiting μν: μ€λ λκ° μΌμμ μΌλ‘ λΉνμ±μνκ° λ¬μ λ, μ€λ λλ λ€μ λ κ°μ§ μν μ€ νλμ μνκ° λ©λλ€.

   - Blocked
   - Waiting

   μλ₯Ό λ€μ΄, μ€λ λκ° I/Oκ° λλκΈΈ λκ°λ¦¬κ³  μμ λ, μ€λ λλ `blocked` μνκ° λ©λλ€.  
   `blocked/waiting` μ€λ λλ₯Ό λ€μ νμ±ννκ³  μ€μΌμ€λ§νλ κ²μ μ€λ λ μ€μΌμ₯΄λ¬μ μ±μμλλ€. μ΄λ° μνμ μλ `runnable` μνλ‘ μ΄λν  λ κΉμ§ λμ΄μ μ€νμ κ³μ ν  μ μμ΅λλ€. μ΄λ μ€λ λκ±΄ μ΄ μνμ μμΌλ©΄ CPU cycleμ μλΉνμ§ μμ΅λλ€.  
   `blocked` μνμ μλ μ€λ λλ νμ¬ λ€λ₯Έ μ€λ λμ μν΄ lock λμ΄μλ λ³΄νΈλ μ½λ μμ­μ μ‘μΈμ€νλ €κ³  νμ λ, μ°¨λ¨λ μνμλλ€. λ³΄νΈλ μμ­μ΄ unlockλλ©΄ μ€μΌμ₯΄λ¬λ blockλ μ€λ λ μ€ νλλ₯Ό μ νν΄μ μ€ν κ°λ₯ μνλ‘ μ΄λν©λλ€.  
   λ, μ€λ λλ μ‘°κ±΄μ λ°λΌ λ€λ₯Έ μ€λ λλ₯Ό κΈ°λ€λ¦¬λ μνμ μμ μλ μμ΅λλ€. μ΄ μ‘°κ±΄μ΄ μΆ©μ‘±λλ©΄ μ€μΌμ₯΄λ¬μ μλ¦Όμ΄ μ μ‘λκ³ , λκΈ°μ€μΈ μ€λ λκ° μ€ν κ°λ₯ μνλ‘ μ΄λλ©λλ€.  
   νμ¬ μ€νμ€μΈ μ€λ λκ° `blocked/waiting` μνλ‘ μ΄λνλ©΄, `runnable` μνμ λ€λ₯Έ μ€λ λκ° μ€λ λ μ€μΌμ₯΄λ¬μ μν΄ μ€νλλλ‘ μ€μΌμ₯΄λ©λλ€.  
4. Timed Waiting: μ€λ λλ `time out` λ§€κ°λ³μκ° μλ λ©μλλ₯Ό νΈμΆν  λ, `waiting` μνμ μκ²λ©λλ€. μ€λ λλ `timeout`μ΄ μλ£λ  λκΉμ§ κΈ°λ€λ¦¬κ±°λ, μλ¦Όμ΄ μμ λ  λκΉμ§ μ΄ μνμ μμ΅λλ€. μλ₯Ό λ€μ΄, μ€λ λκ° sleep λλ μ‘°κ±΄λΆ λκΈ°λ₯Ό νΈμΆνλ©΄, `timed waiting` μνλ‘ μ΄λνκ² λ©λλ€.
5. Terminated State: μ€λ λλ λ€μκ³Ό κ°μ μ΄μ λ‘ μ’λ£λ©λλ€.

   - μΌλ°μ μΌλ‘ μ’λ£λμκΈ° λλ¬Έμλλ€. μ΄λ μ€λ λμ μ½λκ° μμ ν νλ‘κ·Έλ¨μ μν΄ μ€νλμμ λ λ°μν©λλ€.
   - `segmentation`(?) μ€ν¨ λλ μ²λ¦¬λμ§ μμ μμΈμ κ°μ λΉμ μμ μΈ μ€λ₯ μ΄λ²€νΈκ° λ°μνκΈ° λλ¬Έμλλ€.

   `terminated` μνμ μλ μ€λ λλ λμ΄μ CPU cycleμ μλΉνμ§ μμ΅λλ€.

### π μλ° μ½λλ‘ μ€λ λμ μν κ΅¬ννκΈ°

Javaμμ νμ¬ μ€λ λμ μνλ₯Ό μ»λ λ°©λ²μ `Thread.getState()` λ©μλλ₯Ό μ¬μ©νλ κ²μλλ€. μλ°λ `java.lang.Thread.State` λΌλ ν΄λμ€λ₯Ό EnumμΌλ‘ μ μΈνμ¬, μ€λ λμ μνλ₯Ό μ μν©λλ€.

1. `Thread.State NEW`
2. `Thread.State RUNNABLE`
3. `Thread.State BLOCKED`
4. `Thread.State WAITING`
5. `Thread.State TIMED_WAITING`
   - timeoutμ΄ μλ `Object.wait`
   - timeoutμ΄ μλ `Thread.join`
   - `LockSupport.park`
6. `Thread.State TERMINATED`
   - `Thread.sleep`
   - timeoutμ΄ μλ `Object.wait`
   - timeoutμ΄ μλ `Thread.join`
   - `LockSupport.parkNanos`
   - `LockSupport.parkUntil`
