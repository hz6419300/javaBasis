读写锁demo
```
class MyCach{
	
	private volatile Map<String, Object> h=new HashMap<>();
	
	
	private ReentrantReadWriteLock readWriteLock=new ReentrantReadWriteLock();
	//写方法
	public void write(String k,Object v) {
			readWriteLock.writeLock().lock();
		try {
			System.err.println(Thread.currentThread().getName()+"正在写入");
			try {
				Thread.sleep(100);
			} catch (InterruptedException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			h.put(k, v);
			System.err.println(Thread.currentThread().getName()+"正在写入完成");
		} finally {
			// TODO: handle finally clause
			readWriteLock.writeLock().unlock();
		}
		
		
	}
	
	public Object read(String k) {
		readWriteLock.readLock().lock();
		try {
			System.err.println(Thread.currentThread().getName()+"正在读");
			try {
				Thread.sleep(100);
			} catch (InterruptedException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			Object object = h.get(k);
			System.err.println(Thread.currentThread().getName()+"杜万成"+object);
			return object;
			
		} finally {
			// TODO: handle finally clause
			readWriteLock.readLock().unlock();
		}
		
	}
	
}

/**
 * 读写锁
 * @author thinkpad
 *
 */
public class ReadWriteLockDemo {
	
	public static void main(String[] args) {
		MyCach myCach = new MyCach();
		
		for (int i = 0; i < 5; i++) {//五个线程写
			final int iv=i;
			new Thread(()->{
				myCach.write(iv+"", iv+"");
				
			},String.valueOf(i)).start();
		}
		
		for (int i = 0; i < 5; i++) {//五个线程读
			final int iv=i;
			new Thread(()->{
				myCach.read(iv+"");
			},String.valueOf(i)).start();
		}
		
		
	}

}


```

