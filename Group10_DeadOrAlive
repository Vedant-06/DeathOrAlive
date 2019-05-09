//Project Statement : To detect whether a person is dead or alive using xd-58c bpm sensor and XCTU Module
//Group ID : 10
//date: 28 March, 2019
//Assigned by: Prof. Rutu Parekh

//  Variables
int PulseSensorPurplePin = 0;                  // Pulse Sensor Signal WIRE connected to ANALOG PIN 0
int LED13 = 13;                                //  The on-board Arduino LED
bool on = false;
int Signal_BPM;                                // holds the incoming raw data. Signal value can range from 0-1024
int Threshold = 550;
int t[6]={0};                                  //difference of consecutive signal values
int td = 0;                                    //Total Difference
int Counter = 1;                               //counter for first 5 signal values
int c = 0;                                     // Array counter
int Died_count = 0;                            //dead count
int Alive_count = 0;                           //alive count
int j = 1,i = 1;                               //counter for 3 seconds

// The SetUp Function:
void setup() {
   pinMode(LED13,OUTPUT);        // pin that will blink to your heartbeat!
   Serial.begin(115200);         // Set's up Serial Communication at certain speed.
}

// The Main Loop Function
void loop() {

  Signal_BPM = analogRead(PulseSensorPurplePin);  
  if(Signal_BPM > Threshold)
  { 
      Serial.println("disconnected.");
      on = false;
      digitalWrite(LED13,HIGH);
  }
  else 
  {
      c = i%6;
      digitalWrite(LED13,LOW);
        if(Signal_BPM < 10)
        {
          on = true;
          Serial.println("Connecting...");
        }
        else if(c>0 && c<6)
        {
          t[c] = Signal_BPM;                                            
        }
        else if(c == 0)
        {
          td = abs(t[1] - t[2]) + abs(t[2] - t[3]) + abs(t[3] - t[4]) + abs(t[4] - t[5]);
          td = td/4;
          
          if(td < 2)
          {
              Serial.println(td);
              Died_count++;
              Serial.print(".");
          }
          
          else if(td >= 2 && td < 20)
          {
              Alive_count++;
              Serial.print(".");
              Serial.println(td);
          }  
          else if(td > 50)
          {
              Serial.println("Please Hold Properly...");                                                        
          }
      }
   }
   
   i = (i+1)%6;
   j = (j+1)%120;
   if(j == 0 && on == true)
   {
    if((2)*Alive_count >= Died_count)
    {
      Serial.println(" ");
      Serial.println("Alive!");
      Serial.println(" ");
    }
    else
    {
      Serial.println(" ");
      Serial.println("Dead!");
      Serial.println(" "); 
    }
    Alive_count = 0;
    Died_count = 0;
   }
delay(50);
}
