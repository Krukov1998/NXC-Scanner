#include "Button+-.nxc"

task main()
  {
  SetSensor(SENSOR_3,SENSOR_LIGHT);
  byte threshold=50;
  while (true)
    {
    while (!ButtonPressed(BTNCENTER))
      {
      TextOut(30,56,"SCANNER",0);
      threshold=senseButton(threshold,true,5,100,true);
      TextOut(8,48,StrCat("Threshold: ",NumToStr(threshold),"  "),0);
      Wait(10);
      }
    ClearScreen();
    for (byte yPos=63; yPos>0; yPos--)
      {
      OnRev(OUT_A,58);
      for (byte xPos=0; xPos<100; xPos++)
        {
        byte light;
        light=Sensor(S3);
        PointOut(xPos,yPos,(light>threshold)*4);
        //PlayTone(1000,25);
        Wait(25);
        }
      Off(OUT_A);
      while (ButtonPressed(BTNCENTER)){}
      OnFwd(OUT_A,50);
      Wait(3100);
      Off(OUT_A);
      while (ButtonPressed(BTNCENTER)){}
      OnFwd(OUT_BC,15);
      Wait(500);
      Off(OUT_BC);
      while (ButtonPressed(BTNCENTER)){}
      }
    until (ButtonPressed(BTNCENTER)){}
    while (ButtonPressed(BTNCENTER)){}
    until (ButtonPressed(BTNCENTER)){}
    }
  }
