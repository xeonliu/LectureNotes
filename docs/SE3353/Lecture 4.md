# Transaction

怎么让操作具有原子性

is a series of actions that must all complete successfully, or else all the changes in each action are backed out. Transactions end in either a commit or a rollback.

![](assets/Pasted%20image%2020241009080947.png)

线程进入Bean-1，创建TX1事务？

## 6种状态
### Required
MethodA是Required，创建一个新的事务TX1.

如果已经有了事务，调用Required的MethodB，因而继续这个事务，仍在原线
程执行。

事务知道退出Bean-2，结束Bean-1才能提交

### RequiresNew
挂起TX1，开启TX2.
MethodB结束后可以提交或者回滚。
然后恢复到TX1。

比如记录Log失败不能让转账失败。

### Supports
假设1和2都是Support。
一直都是非事务状态执行。

假设1是Required，2是Support
2会加入到1的事务。

### NotSupported
挂起A，在非事务执行B

### Mandatory
> 强制在事务中

MethodA Support 而没事务，
MethodB Mandatory 不在事务中就抛异常。
### Never
> 永不在事务中

不在事务就正常，否则抛异常

![](assets/Pasted%20image%2020241009082441.png)



```java
@TransactionAttribute(REQUIRES_NEW)
public void firstMethod();
```

```java
@Service
public class BankServiceImpl implements BankService {
    
    @Autowired
    private BankDao bankDao;

    @Override
    @Transactional
    public void transfer(String from, String to, int amount) {
        System.out.println(from + " " + to + " " + amount);
        bankDao.withdraw(from, amount);
        // int result = 10/0
        // If Error Happened Here, WithDraw will Roll Back
        try {
            bankDao.deposit(to, amount);
        } catch (Exception e) {
            e.printStackTrace();
        }
        // If Error Happened Here. Only Withdraw will RollBack here.
    }
}
```


```java
@Repository
public class BankDaoImpl implements BankDao {
  @Autowired    
  private BankRepository bankRepository;
  @Transactional    
  public void withdraw(String from, int amount) {
            Bank out = bankRepository.findById(from).get();
            out.setBalance(out.getBalance() - amount);
		    // int result = 10 / 0;
		    // Transfer & Withdraw Roll Back
    };   

    @Transactional(propagation = Propagation.REQUIRES_NEW)    
    public void deposit(String to, int amount) {
              Bank in = bankRepository.findById(to).get();
              in.setBalance(in.getBalance() + amount);
		      // int result = 10 / 0;
		      // If Deposite Error Here. Only Rollback Deposit  
      };
    }
```

# Dirty Read

啥也不加。
读取到为提交的数据
读到事务中间状态。
内存会被读

# Nonrepeatable Reads
读已提交的数据
写的时候发现被写过了
数据库数据要加锁

# Phantom Reads

可重复读
其他记录被写了，导致读出别的玩意

表级别要加锁


分布式事务管理
两个阶段提交协议。

TOmcat管。

不能避免第二阶段网络导致的概率

# 事务隔离级别

