# ECE-5-Project
How Fast Can You Chug?

Our device allows one to test the amount of time that it takes for them to chug a drink and
then allows them to compare their score to the scores of their friends. It does this using a force
sensor that is able to register when the drink is picked up and will start a timer. This timer will
continue until the drink is placed back on the sensor. Once the timer has stopped, the player can
compare their score to other competitors using the leaderboard. In order to scroll through the
leaderboard and reset the game, the player uses a remote that is registered through an IR receiver.
Furthermore, our device can also be used as a Rubix cube timer in that instead you would be
using a Rubix cube instead of a drink.

HARDWARE COMPONENTS:                              
(Main hardware needed for the project)

● Arduino UNO R3 Controller Board

● Breadboard

● LCD1602 Module

● Remote Control

● IR Receiver Module

● Force Sensing Resistor (0.5in ,circle, 1oz-22LB,Flexible) 

● 10k Potentiometer

● Alligator Clips (10 pack)




SOFTWARE DESIGN:

Our function included 3 main libraries: Liquid Crystal, IRremote, and KickSort library,
each responsible for the LCD, the remote controller and the leaderboard function. The setup
function defined all the pins and set the appropriate ones to send and receive signals. The sort
speeds function utilized the KickSort library to sort an array from low to high. The tone and pitch
function were also present but not used in the project because it caused conflicts with the internal
Arduino timer and created bugs in our project.

The general pseudo code in loop function is presented:      
● If the IR receiver decodes something       
  ○ Continue to receive signal         
  ○ Switch case for the signals decoded      
  ○ If 1 is pressed on the controller     
    ■ Goes into the timer function     
      ● If a force is detected, let the timer be ready to start    
      ● If a force disappears, start the timer    
       ○ Save the score in scores variable                               
      ● If a force is again detected, stop the timer and print the score                    
       ○ Sorts the array in which scores are stored                    
    ■ Stop the case       
  ○ If 2 is pressed            
    ■ Enter the leaderboard                           
      ● Display the leaderboard and the first speed.                
    ■ If the down button is pressed                  
      ● Print the next two scores (2, 3) on the LCD                           
    ■ If << button is pressed                          
      ● Print the next two scores (4, 5) on the LCD                           
    ■ If the up button is pressed                         
      ● Print the scores before (2, 3) on the LCD                        
    ■ If the >> button is pressed                          
      ● Print the first page of the leaderboard                      
    ■ Stop the case                  
  ○ If the power button is pressed                     
    ■ Return the main menu of the game                        
    ■ Continue listening for IR signal                     
  ○ If the reset button is pressed                  
    ■ Resets all scores in the leaderboard         
    
    
    
    
TESTING:                     

In terms of testing, one of the main things we wanted to ensure was that the sensor would
be able to register an empty cup on the sensor. This is important because if the sensor didn’t
register the empty cup, the timer wouldn't stop and the score wouldn’t be recorded. In order to
test this we tried placing an empty plastic cup on the sensor with different amounts of force. The
force sensor was able to register every single case except for if it was put down as softly as
possible. We also tested it by allowing people to play our game, and we found that it was able to
register the empty cup every time. This is because when people were being timed they always
placed the cup down with more force than the minimum threshold.       

We performed tests for the speed of the remote controller and how fast the IR receiver
can receive a signal for the best results. However, the IR receiver still had bugs in which it would
receive random signals for the up and down buttons, causing the scrolling function of our leader
board a bit buggy. We tried a lot of different approaches and the bug was left unresolved as the
signal it was receiving had different hexadecimal values causing delays in scrolling. This was not
a huge problem because the function would still work. However, multiple clicks were required.

Furthermore, the timer involved a lot of testing because of the various extraneous
behaviors that it produces. There were issues involving the timer being setup completely
backwards where it would start when the force sensor detects the weight. There is the issue of the
timer going straight to the scores page, not showing the incremented time. There were also issues
involving the integration of the EEprom library into the timer which caused integer overflow and
weird behaviors to occur in the leaderboard. However, after various testing and debugging by our
team and the assistance of the TAs, we were able to fix all the issues with the timer and
successfully run our game.
