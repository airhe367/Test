* CountDownLatch、CyclicBarrier和Semaphore

** CountDownLatch
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
** CyclicBarrier
```java
public class Test {
    public static void main(String[] args) 
	{
        int N = 4;
        CyclicBarrier barrier  = new CyclicBarrier(N);
        for(int i=0;i<N;i++)
	{
		      Thread.run();
	}
    }
        @Override
        public void run() 
	{
		Thread.sleep(5000);
		cyclicBarrier.await();//cyclicBarrier.await(2000, TimeUnit.MILLISECONDS);
		System.out.println("所有线程写入完毕，继续处理其他任务...");
        }
}
```

** CyclicBarrier
```java
public class Test {
    public static void main(String[] args) {
        int N = 8;            //工人数
        Semaphore semaphore = new Semaphore(5); //机器数目
        for(int i=0;i<N;i++)
            new Worker(i,semaphore).start();
    }
     
    static class Worker extends Thread{
        private int num;
        private Semaphore semaphore;
        public Worker(int num,Semaphore semaphore){
            this.num = num;
            this.semaphore = semaphore;
        }
         
        @Override
        public void run() {
            try {
                semaphore.acquire();
                System.out.println("工人"+this.num+"占用一个机器在生产...");
                Thread.sleep(2000);
                System.out.println("工人"+this.num+"释放出机器");
                semaphore.release();           
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```
