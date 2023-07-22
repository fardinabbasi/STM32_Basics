# STM32 Basics
Implementation of basic components such as a timer, LCD display, external interrupt, and digital pins on the STM32 microcontroller. The microcontroller used is the **STM32F103R6** model, operating at a **clock frequency** of **44MHz**.
## [Digital Pin](https://github.com/fardinabbasi/STM32_Basics/tree/main/Digital_Pin)
Two green and red LEDs are connected to digital pins in the microcontroller. We want to turn them on and off periodically.

The important part of the code corresponding to this component is in the main.c while loop as below:
```ruby
int main(void)
{
  /* USER CODE BEGIN 1 */

  /* USER CODE END 1 */

  /* MCU Configuration--------------------------------------------------------*/

  /* Reset of all peripherals, Initializes the Flash interface and the Systick. */
  HAL_Init();

  /* USER CODE BEGIN Init */

  /* USER CODE END Init */

  /* Configure the system clock */
  SystemClock_Config();

  /* USER CODE BEGIN SysInit */

  /* USER CODE END SysInit */

  /* Initialize all configured peripherals */
  MX_GPIO_Init();
  /* USER CODE BEGIN 2 */
  /* USER CODE END 2 */

  /* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {
	  HAL_GPIO_WritePin(X1_GPIO_Port,X1_Pin,GPIO_PIN_SET);
	  HAL_Delay(500);
	  HAL_GPIO_WritePin(X1_GPIO_Port,X1_Pin,GPIO_PIN_RESET);
	  HAL_Delay(500);
    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
  /* USER CODE END 3 */
}
```
