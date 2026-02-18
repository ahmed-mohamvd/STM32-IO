\# Pull-Up vs Pull-Down Explanation



\## Pull-Up

When using internal pull-up:

\- Default state = HIGH

\- When button is pressed → pin becomes LOW

\- Button is connected between GPIO and GND



\## Pull-Down

When using pull-down:

\- Default state = LOW

\- When button is pressed → pin becomes HIGH

\- Button is connected between GPIO and Vcc



\## Why we used Pull-Up?

Pull-up is commonly used because:

\- It is more stable

\- Less noise issues

\- STM32 internal pull-up is reliable

