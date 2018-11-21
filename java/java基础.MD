## java

* java.lang.reflect
  * Modifier
  * Field





## javax

* script

  ```
  生日：JDK6引入javax.script.*
  用途：把任何脚本或动态语言无缝地嵌入到具有一致编程API的JAVA应用程序中
  父母：Mike Grogan
  支持：groovy   JavaScript
  ```

  * ScriptEngineFactory
  * ScriptEngineManager
  * ScriptEngine

  ```java
  public String cal(){
      ScriptEngineManager factory = new ScriptEngineManager();
      ScriptEngine engine = factory.getEngineByName("groovy");
      engine.eval(configDO.getScript());
      return (String) ((Invocable) engine).invokeFunction(configDO.getFunctionName(), 		params);
  } 
  ```

  ```java
  public class ScriptTest {
  
      public static void main(String[] args) {
          // create a script engine manager  
          ScriptEngineManager factory = new ScriptEngineManager();
          // create a JavaScript engine  
          ScriptEngine engine = factory.getEngineByName("JavaScript");
  
          try{
              Compilable compEngine = (Compilable)engine;
              CompiledScript script = compEngine.compile("function max_num(a,b){return (a>b)?a:b;}");
              script.eval();
              Invocable invoke = (Invocable) engine;
              Object maxNum = invoke.invokeFunction("max_num", 4, 6);
              System.out.println(maxNum);
          } catch(Exception e){
              e.printStackTrace();
          }
      }
  }
  ```
