Chap 4
對這兩個程式更改能夠增加需要用到的LED數量
#define NUM_LEDS 10(+1新增預設腳位)
const uint led_pads[NUM_LEDS] = {0,1,2,3,4,5,6,7,8,9};(在陣列中新增對應腳位)

for (int i = 0; i < NUM_LEDS; i++) {
        char name[11];                                                                                     //腳位對應數量
        sprintf(name, "LED%02d", i);
        leds[i]->start(name, BASE_PRIORITY + (i % 4)); // priority cycles 0~3
        vTaskDelay(50 * i); // stagger start                                                        //讓LED能夠不同步閃爍
    }
Chap 5
任務建立
blink.start("Blink", TASK_PRIORITY);     // 不受 semaphore 控制
worker1.start("Worker 1", TASK_PRIORITY);
worker2.start("Worker 2", TASK_PRIORITY);
worker3.start("Worker 3", TASK_PRIORITY);


Semaphore 控制同時運作的任務數量 
4 個 BlinkWorker、2 個 token → 同時最多 2 個任務運作 
其餘任務會阻塞等待 token 
觀察任務行為 
前 2 個任務成功取得 token → 開始 LED 閃爍 
第 3、4 個任務 → 阻塞等待 
前任務釋放 token → 後續任務恢復執行



