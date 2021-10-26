# Lab 5: Jiří Navrátil

Link to your `Digital-electronics-2` GitHub repository:

   [https://github.com/GeorgeNavratil/Digital-electronics-2](https://github.com/GeorgeNavratil/Digital-electronics-2)


### 7-segment library

1. In your words, describe the difference between Common Cathode and Common Anode 7-segment display.
   * CC SSD - has all the cathodes of the 7-segments connected directly together controlled by a logical 1 and connected to ground
   * CA SSD - has all the anodes of the 7-segments connected together controlled by a logical 0 and connected to a voltage supply

2. Code listing with syntax highlighting of two interrupt service routines (`TIMER1_OVF_vect`, `TIMER0_OVF_vect`) from counter application with at least two digits, ie. values from 00.00 to 59.59:

```c
/**********************************************************************
 * Function: Timer/Counter1 overflow interrupt
 * Purpose:  Increment counter value from 00 to 59.
 **********************************************************************/
ISR(TIMER1_OVF_vect)
{
    dis[0]++;
    
    if (dis[0] == 10)
    {
        dis[1]++;
        dis[0] = 0;
    }
    else if (dis[1] == 6)
    {
        dis[2]++;
        dis[1] = 0;
    }
    else if (dis[2] == 10)
    {
        dis[3]++;
        dis[2] = 0;
    }
    else if (dis[3] == 6)
    {
        dis[] = 0;
    }
}
```

```c
/**********************************************************************
 * Function: Timer/Counter0 overflow interrupt
 * Purpose:  Display tens and units of a counter at SSD.
 **********************************************************************/
ISR(TIMER0_OVF_vect)
{
    static uint8_t posit = 0;
    
    if (posit == 2)
    {
        SEG_update_shift_regs(dis[posit], posit, 1);
    }
    else
    {
        SEG_update_shift_regs(dis[posit], posit, 0);
    }
    
    posit++;
    
    if (posit == 3)
    {
        posit = 0;
    }
}
```

3. Flowchart figure for function `SEG_clk_2us()` which generates one clock period on `SEG_CLK` pin with a duration of 2&nbsp;us. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

   ![Flowchart diagram](../05-segment/images/flowchart.png)


### Kitchen alarm

Consider a kitchen alarm with a 7-segment display, one LED and three push buttons: start, +1 minute, -1 minute. Use the +1/-1 minute buttons to increment/decrement the timer value. After pressing the Start button, the countdown starts. The countdown value is shown on the display in the form of mm.ss (minutes.seconds). At the end of the countdown, the LED will start blinking.

1. Scheme of kitchen alarm; do not forget the supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values.

   ![Kitchen alarm](../05-segment/images/KitchenAlarm.svg)