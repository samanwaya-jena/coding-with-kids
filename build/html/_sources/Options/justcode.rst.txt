
JustCode
============

Key Goals
----------

Options
----------

Scratch
~~~~~~~
KidsRuby
~~~~~~~~

Python
~~~~~~~

Here is some code::

    # open a file and split imu,can and gnss data
    with open(datalog_path) as f1:
        for line in f1:
            words = eval(line)
            #print(words)
            if words[0] == 21:
                imu_data.append(words)
                imu_ts.append(words[1])
                imu_acel.append(words[2:5])
                imu_gyro.append(words[5:8])
                imu_dc.append(words[-1])

            elif words[0] == 22:
                can_data.append(words)
            elif words[0] == 23:
                gnss_data.append(words)
            else:
                junk_data.append(words)

    


And here is some c code:

.. code-block:: c

    static ImuMode check_button() {
    
        HAL_GPIO_WritePin(GPIOB,GPIO_PIN_7,GPIO_PIN_SET);                             // Turn on blue LED for 1 sec to prompt button press
        osDelay(1000);
        HAL_GPIO_WritePin(GPIOB,GPIO_PIN_7,GPIO_PIN_RESET);
        osDelay(1);
    
        if(HAL_GPIO_ReadPin(GPIOC,GPIO_PIN_13) == GPIO_PIN_SET) {                     // If the button was pressed, blink the LED twice and return ASYNC enum
            osDelay(500);
            HAL_GPIO_WritePin(GPIOB,GPIO_PIN_7,GPIO_PIN_SET);
            osDelay(100);
            HAL_GPIO_WritePin(GPIOB,GPIO_PIN_7,GPIO_PIN_RESET);
            osDelay(100);
            HAL_GPIO_WritePin(GPIOB,GPIO_PIN_7,GPIO_PIN_SET);
            osDelay(100);
            HAL_GPIO_WritePin(GPIOB,GPIO_PIN_7,GPIO_PIN_RESET);
            osDelay(1);
            return ASYNC; 
        }
        else { 
        return SYNC; 
        }                                                         // If the button was not pressed, return SYNC enum
    }



Hopscotch
~~~~~~~~~~~~