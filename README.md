**CountDownLatch、CyclicBarrier和Semaphore

```java
public class Test {
     public static void main(String[] args) {   
         final CountDownLatch latch = new CountDownLatch(2);
         new Thread(){
             public void run() 
			 {
                    Thread.sleep(3000);
                    latch.countDown();
             };
         }.start();
         new Thread(){
             public void run() 
			 {
                    Thread.sleep(3000);
                    latch.countDown();
             };
         }.start();
        latch.await();
     }
}
```
