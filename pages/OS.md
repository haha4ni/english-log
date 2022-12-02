- *面試用, 沒考不會寫上去
-
- Ch2 中斷、I/O、系統呼叫、OS 結構設計、虛擬機
  id:: 631f1998-ee6d-4c69-a7f0-a63f7de6f6c4
	- explain interrupt step
	  background-color:: #264c9b
	- Interrupt 的處理流程
		- 暫停目前process 之執行。
		- 保存此process 當時執行狀況。
		- OS 會根據Interrupt ID 查尋Interrupt vector。
		- 取得ISR（Interrupt Service Routine）的起始位址。
		- ISR 執行。
		- ISR 執行完成，回到原先中斷前的執行。
	- explain kernel space and user space
	  background-color:: #264c9b
		- 即Linux kernel的運作空間.
		- kernel space : 只要是CPU可以管的硬體, kernel space的程式就能透過machine code來操作該硬體
		- user process : 若需要在user space調用系統資源(如I/O作業), 則必須通過system call.
		- 簡單說kernel space可以執行比user space更高權限的動作.
	- explain  System Call
	  background-color:: #264c9b
		- Programming interface to the services provided by the OS.
		- 簡單來說，system call 是 process 和 OS 之間的介面，當使用者程式需要 OS 的服務時，使用者程式便去呼叫 system call
		- ![system call.png](../assets/system_call_1663039365360_0.png){:height 240, :width 415}
		- ![X6q0RjR.png](../assets/X6q0RjR_1663039590653_0.png){:height 245, :width 411}
	- explain DMA(Direct memory access)
	  background-color:: #264c9b
		- 提供一個裝置控制器，讓 I/O 裝置能夠直接在記憶體做資料的傳輸，不需要 CPU 的參與。
		- ex. ADC, HDD
		- #+BEGIN_TIP
		  cycle stealing :
		  DMA 向 CPU 竊用機器週期，而直接向記憶體存取資料，因此 CPU 可與週邊裝置的工作同時進行。萬一 CPU 與 DMA 對記憶體存取發生衝突，則給 DMA 較高的優先權 (執行消耗小的先執行)。
		   #+END_TIP
- Ch3 行程 Process
	- process 在記憶體中的配置
		- stack : 存放函數的參數、區域變數等。(會稱作 stack 是由於其配置遵守 LIFO)
		- heap : 一般由程式設計師分配釋放，執行時才會知道配置大小，如 malloc/new 和 free/delete。(注意其資料結構不是 DS 中的 heap 而是 link-list)
		- BSS : 未初始化的靜態變數
		- data : 全域變數、靜態變數
		- text/code : 常量字元串
		- ![memory-layout-of-c-program-diagram-20170301.png](../assets/memory-layout-of-c-program-diagram-20170301_1662982934418_0.png){:height 531, :width 391}
	- ```C++
	  int a=0;   //global 初始化區
	  char *p1;  //global 未初始化區
	  main(){
	      int b;             // stack
	      char s[]="abc";    // stack
	      char *p2;          // stack
	      char *p3="123456"; // 123456\0 在常量區，p3在stack。
	      static int c=0;   // global (static) 初始化區
	      p1 = (char*)malloc(10);
	      p2 = (char*)malloc(20);  //分配得來得10和20位元組的區域在heap
	      strcpy(p1,"123456");  
	      //123456\0 在常量區，編譯器可能會將它與 p3 中的 123456\0 優化成一個地方。
	  }
	  ```
- Ch4 多執行緒 Multithread Programming
	- Explain program, process and thread?
	  background-color:: #264c9b
		- Program是還尚未load入記憶體的bin file, 相同 Program 的 Process 可以多個同時存在
		- Process 意旨已經執行並且 load 到記憶體中的 Program, 是 OS 分配資源的對象
		- Thread 是 OS 分配 CPU 時間的對象, 實際執行對象
		- ref : [Program/Process/Thread 差異](https://totoroliu.medium.com/program-process-thread-%E5%B7%AE%E7%95%B0-4a360c7345e5)
	- user threads and kernel threads
		- 在 user mode 下進行，OS 不知道有這些 thread 存在不需要 OS 介入管理
			- Pthreads (POSIX threads)
			- Win32 threads
			- Java threads
		- 在 kernel mode 下進行，OS 知道有這些 thread 存在，由 OS 介入管理
			- Windows XP/2000
			- Solaris
			- Linux
			- Tru64 UNIX
	- Multi-threading models
		- a. Many-to-one Model
		- b. One-to-one Model
		- c. Many-to-Many Model
			- ![4_07_ManyToMany.jpg](../assets/4_07_ManyToMany_1663038278145_0.jpg){:height 324, :width 336}
	- #+BEGIN_TIP
	  [用心去感覺] When you write multithreaded programs, It should not be assumed that which model is adopted by the thread library!
	  
	  程式設計師寫 multithread 程式是呼叫 thread API 來撰寫 (也就是 thread libraries)，而該 API 內部實作是用哪一種模型 (Many-to-one, One-to-one 或 Many-to-Many) 在規範中是沒有規定的，所以程式設計師不應該預設內部是某一種模型，以避免預期之外的錯誤。
	   #+END_TIP
-
- Ch6 同步問題 Synchronization
	- explain mutex and semaphore?
	  background-color:: #264c9b
		- spin lock是busy waiting，而semaphore是sleep
		- semaphore有counter, Mutex counter = 1
- Ch7 死結 Deadlock
	- explain deadlock?
	  background-color:: #264c9b
- Ch8 記憶體管理 Memory Management
	-
- Ch9 虛擬記憶體 Virtual Memory
	- Page Replacement Algorithms
		- FIFO：最先載入的 page 優先視為 victim page。
		- OPT(Optimal Page Replacement)：以將來長期不會使用的 page 視為 victim Page。
		- LRU(Least Recently Used)：以最近不常使用的 page 視為 victim page。
		- LFU(Least Frequently Used)：參考次數最少的 page 作為 victim page
-
-
- ref:
	- https://mropengate.blogspot.com/2017/09/operating-system-concepts.html