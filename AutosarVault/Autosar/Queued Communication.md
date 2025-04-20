
**Buffering Mechanism(Unqueued)**: To store the latest value of a data element and decouple the timing between the sender and receiver. Rte allocates shared buffer for each data element, which is written and read by RTE calls:

`static float RTE_Buffer_Temperature;`

`Std_ReturnType Rte_Write_Temperature(float value) {`
    `RTE_Buffer_Temperature = value;`
    `return RTE_E_OK;`
`}`

`Std_ReturnType Rte_Read_Temperature(float* value) {`
    `*value = RTE_Buffer_Temperature;`
    `return RTE_E_OK;`
`}`

**Queued Mechanism**: Stores **multiple values** for a data element in a **FIFO** queue. No data lost. ARXML config as "IS-QUEUED=true", "QUEUE_LENGTH = 5". Circular queue is implemented. Used when every signal matters. 

`#define QUEUE_SIZE 5`
`static float queue[QUEUE_SIZE];`
`static uint8_t writeIndex = 0;`
`static uint8_t readIndex = 0;`

`bool IsQueueFull() {`
    `return ((writeIndex + 1) % QUEUE_SIZE) == readIndex;`
`}`

`bool IsQueueEmpty() {`
    `return writeIndex == readIndex;`
`}`

`Std_ReturnType Rte_Write_Temperature(float value) {`
    `if (IsQueueFull()) {`
        `return RTE_E_LIMIT; // Prevent overwriting unread data`
    `}`
    `queue[writeIndex] = value;`
    `writeIndex = (writeIndex + 1) % QUEUE_SIZE;`
    `return RTE_E_OK;`
`}`

`Std_ReturnType Rte_Read_Temperature(float* value) {`
    `if (IsQueueEmpty()) {`
        `return RTE_E_NO_DATA;`
    `}`
    `*value = queue[readIndex];`
    `readIndex = (readIndex + 1) % QUEUE_SIZE;`
    `return RTE_E_OK;`
`}`

**Disadvantage:** Memory overhead due to queue buffer size. Needs careful queue size design to avoid overflow.
**Additional Configurations:** 
- "USE-UPDATE-INDICATOR = true" -> maintains bool value for each value to show if the value read
- Rtw_write() will return `RTE_E_LIMIT` if the queue is full