# DesafioFisico
Seguidor con Semaforo
-------------------
#include <DCMotor.h>

DCMotor motor_der(M0_EN, M0_D0, M0_D1);
DCMotor motor_izq(M1_EN, M1_D0, M1_D1);

int s_der;
int s_izq;
int s_ext_der;
int s_ext_izq;


int LDR_der;
int LDR_izq;

void setup(){
Serial.begin(9600);
pinMode(19,INPUT);
pinMode(14,INPUT);
}

void loop(){

  s_ext_der = analogRead(19);
  s_ext_izq = analogRead(14);
  
  if(s_ext_izq >= 90){
     motor_izq.setClockwise(false);
     motor_der.setSpeed(-30);
     motor_izq.setSpeed(30);
  }
  else if(s_ext_der >=200){
     motor_der.setSpeed(30);
     motor_izq.setSpeed(-30);
 }
  else{
     motor_der.setSpeed(25);
     motor_izq.setSpeed(25);
}
  LDR_der= analogRead(15);
  LDR_izq = analogRead(17);
  if(LDR_der > 800){
     motor_der.setSpeed(-30);
     motor_izq.setSpeed(-30);
     delay(900);
     motor_der.setSpeed(30);
     motor_izq.setSpeed(-30);
     delay(1400);
 }
     else if(LDR_izq > 800){
       motor_der.setSpeed(-30);
       motor_izq.setSpeed(-30);
       delay(900);
        motor_der.setSpeed(30);
        motor_izq.setSpeed(-30);
        delay(1400);
     }
     
   if(s_ext_der >= 210 && s_ext_izq >= 90){
        motor_der.setSpeed(30);
        motor_izq.setSpeed(30);
        delay(500);
   
   }
}
