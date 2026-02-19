\# Register-Level GPIO Documentation



\## 1️⃣ Enable GPIO Clock (RCC Register)



Before using any GPIO peripheral, its clock must be enabled.



In STM32F103, GPIO ports are connected to the APB2 bus.



The register responsible is:



RCC->APB2ENR



To enable GPIOB clock:



RCC->APB2ENR |= (1 << 3);



Explanation:

\- APB2ENR = APB2 Peripheral Clock Enable Register

\- Bit 3 enables GPIOB

\- Without this step, GPIOB will not function





\## 2️⃣ Configure GPIO Pin Mode



In STM32F1 series:



\- CRL → Pins 0 to 7

\- CRH → Pins 8 to 15



Since we use PB0, we configure:



GPIOB->CRL



Each pin uses 4 bits:



\- MODE\[1:0] → Speed

\- CNF\[1:0]  → Configuration



For Output Push-Pull 2 MHz:



\- MODE = 10

\- CNF = 00



Code:



GPIOB->CRL \&= ~(0xF << (0 \* 4));   // Clear configuration bits

GPIOB->CRL |=  (0x2 << (0 \* 4));   // Output 2 MHz Push-Pull





\## 3️⃣ Writing Output (ODR \& BSRR)



There are two main registers to control output:



\### ODR – Output Data Register



Used to directly write or toggle the output.



Example:



GPIOB->ODR ^= (1 << 0);   // Toggle PB0





\### BSRR – Bit Set Reset Register (Recommended)



Used for atomic set/reset operations.



Turn ON:



GPIOB->BSRR = (1 << 0);



Turn OFF:



GPIOB->BSRR = (1 << (0 + 16));



Why BSRR is better?



\- Atomic operation

\- No read-modify-write issue

\- Safer in interrupt environments

