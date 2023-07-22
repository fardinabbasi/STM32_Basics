# STM32 Basics
Implementation of basic components such as a timer, LCD display, external interrupt, and digital pins on the STM32 microcontroller. The microcontroller used is the **STM32F103R6** model, operating at a **clock frequency** of **44MHz**.
## [Digital Pin](https://github.com/fardinabbasi/STM32_Basics/tree/main/Digital_Pin)
Two green and red LEDs are connected to digital pins in the microcontroller. We want to turn them on and off periodically.

The important part of the code corresponding to this component is in the main.c while loop as below:
```ruby
  while (1)
  {
	  HAL_GPIO_WritePin(X1_GPIO_Port,X1_Pin,GPIO_PIN_SET);
	  HAL_Delay(500);
	  HAL_GPIO_WritePin(X1_GPIO_Port,X1_Pin,GPIO_PIN_RESET);
	  HAL_Delay(500);
    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
```
## [Digital Pin Digital Input](https://github.com/fardinabbasi/STM32_Basics/tree/main/Digital_Input_Pin)
Two push buttons with pull-up resistors connected to them as their output are connected to a STM32 microcontroller. The goal is to turn the LED's on and off by pushing those buttons.

The important part of the code corresponding to this component is in the main.c while loop as below:
```ruby
  while (1)
  {
	  if(HAL_GPIO_ReadPin(Y2_GPIO_Port,Y2_Pin)==0){
		  HAL_GPIO_WritePin(X2_GPIO_Port,X2_Pin,GPIO_PIN_SET);
		  HAL_GPIO_WritePin(X1_GPIO_Port,X1_Pin,GPIO_PIN_RESET);
	  }
	  if(HAL_GPIO_ReadPin(Y1_GPIO_Port,Y1_Pin)==0){
		  HAL_GPIO_WritePin(X2_GPIO_Port,X2_Pin,GPIO_PIN_RESET);
		  HAL_GPIO_WritePin(X1_GPIO_Port,X1_Pin,GPIO_PIN_SET);
	  }
    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
```
## [External Interrupt](https://github.com/fardinabbasi/STM32_Basics/tree/main/External_Interrupt)
Two pins are defined on the microcontroller. We have a pushup button and a digital input connected to them. The goal is to have the LED's blink in a certain speed when pushing the buttons.

The important part of the code corresponding to this component is in the main.c while loop as below:
```ruby
  while (1)
  {
	  if (condition == 0){
	  	  HAL_GPIO_WritePin(X1_GPIO_Port,X1_Pin,GPIO_PIN_SET);
	  	  HAL_GPIO_WritePin(X2_GPIO_Port,X2_Pin,GPIO_PIN_SET);
	  }
	  if (condition == 1){
		  HAL_GPIO_WritePin(X1_GPIO_Port,X1_Pin,GPIO_PIN_RESET);
		  HAL_GPIO_TogglePin(X2_GPIO_Port, X2_Pin);
		  		  HAL_Delay(100);
	  }
	  if(HAL_GPIO_ReadPin(Y1_GPIO_Port,Y1_Pin)==1){
	  	  HAL_GPIO_WritePin(X1_GPIO_Port,X1_Pin,GPIO_PIN_SET);
	  	  HAL_GPIO_WritePin(X2_GPIO_Port,X2_Pin,GPIO_PIN_SET);
		  condition = 0;
	  }
    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
```
```ruby
void HAL_GPIO_EXTI_Callback ( uint16_t GPIO_Pin)
	{
	if(GPIO_Pin == Y2_Pin)
		condition = 1;
	else if(GPIO_Pin == Y1_Pin)
		condition = 0;
	}
```
## LCD Display
### [Part A](https://github.com/fardinabbasi/STM32_Basics/tree/main/LCD/PartA)
Connected an LCD to the STM32 microcontroller, and printed my name and student number in its first two lines. The ports and pins corresponding to the LCD are as follows:
```ruby
  Lcd_PortType ports [] = {
  		D4_GPIO_Port, D5_GPIO_Port, D6_GPIO_Port, D7_GPIO_Port
  };
  Lcd_PinType pins [] = {
  		D4_Pin, D5_Pin, D6_Pin, D7_Pin
  };

  Lcd_HandleTypeDef lcd = Lcd_create(ports, pins, RS_GPIO_Port, RS_Pin, E_GPIO_Port, E_Pin, LCD_4_BIT_MODE);
```
```ruby
  while (1)
  {
	  Lcd_cursor(&lcd, 0,0);
	  Lcd_string(&lcd, "Fardin");

	  Lcd_cursor(&lcd, 1,0);
	  Lcd_string(&lcd, "810199456");
    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
  /* USER CODE END 3 */
}
```
### [Part B](https://github.com/fardinabbasi/STM32_Basics/tree/main/LCD/PartB)
The last three digits of my student number will be stored in a variable called 'a', and 'a' will be divided by 7 and stored in a variable named 'b'. On the first line, 'a' will be displayed, and on the second line, 'b' will be shown with four decimal places.
```ruby
  Lcd_PortType ports [] = {
  		D4_GPIO_Port, D5_GPIO_Port, D6_GPIO_Port, D7_GPIO_Port
  };
  Lcd_PinType pins [] = {
  		D4_Pin, D5_Pin, D6_Pin, D7_Pin
  };

  Lcd_HandleTypeDef lcd = Lcd_create(ports, pins, RS_GPIO_Port, RS_Pin, E_GPIO_Port, E_Pin, LCD_4_BIT_MODE);
```
```ruby
  int StNumber = 456;
  float FloatNumber = (float)StNumber/7;
  char String [50];
  while (1)
  {
	  sprintf(String, (char*)"%d" , StNumber);
	  Lcd_cursor(&lcd, 0,0);
	  Lcd_string(&lcd, String);
	  sprintf(String, (char*)"%.4f" , FloatNumber);
	  Lcd_cursor(&lcd, 1,0);
	  Lcd_string(&lcd, String);
    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
  /* USER CODE END 3 */
}
```
