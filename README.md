# Platform-Code

vex::brain brain;
vex::motor baseFLeft (vex::PORT1,vex::gearSetting::ratio18_1,false);
vex::motor baseFRight (vex::PORT4,vex::gearSetting::ratio18_1,true);
vex::motor baseBLeft (vex::PORT5,vex::gearSetting::ratio18_1,false);
vex::motor baseBRight (vex::PORT6,vex::gearSetting::ratio18_1,true);
vex::motor flipper (vex::PORT7,vex::gearSetting::ratio18_1,false);
vex::motor cascadeLeft (vex::PORT8,vex::gearSetting::ratio18_1,false);
vex::motor cascadeRight (vex::PORT9,vex::gearSetting::ratio18_1,true);
vex::motor claw (vex::PORT10,vex::gearSetting::ratio18_1,true);

vex::competition;

void pre_auton( void ) {

}

void autonomous( void ) {
    BaseFRight.startRotateFor(-560,rotationUnits::deg,70,velocityUnits::pct);
    BaseBRight.rotateFor(-560,rotationUnits::deg,70,velocityUnits::pct,false);
    BaseFLeft.rotateFor(-560,rotationUnits::deg,70,velocityUnits::pct,false);
    BaseBLeft.rotateFor(-560,rotationUnits::deg,70,velocityUnits::pct);
    
    BaseFRight.startRotateFor(-210,rotationUnits::deg,40,velocityUnits::pct);
    BaseBRight.rotateFor(-210,rotationUnits::deg,40,velocityUnits::pct,false);
    BaseFLeft.rotateFor(210,rotationUnits::deg,40,velocityUnits::pct,false);
    BaseBLeft.rotateFor(210,rotationUnits::deg,40,velocityUnits::pct);
    
    BaseFRight.startRotateFor(-1200,rotationUnits::deg,90,velocityUnits::pct);
    BaseBRight.rotateFor(-1200,rotationUnits::deg,90,velocityUnits::pct,false);
    BaseFLeft.rotateFor(-1200,rotationUnits::deg,90,velocityUnits::pct,false);
    BaseBLeft.rotateFor(-1200,rotationUnits::deg,90,velocityUnits::pct);

}

void usercontrol( void ) {
  while (1){
        BaseTopLeft.spin(directionType::fwd,(Controller1.Axis3.value()),velocityUnits::pct);
        BaseBottomLeft.spin(directionType::fwd,(Controller1.Axis3.value()),velocityUnits::pct);
           
        BaseTopRight.spin(directionType::fwd,(Controller1.Axis2.value()),velocityUnits::pct);
        BaseBottomRight.spin(directionType::fwd,(Controller1.Axis2.value()),velocityUnits::pct);
       
        if (Controller1.ButtonDown.pressing()){
            CascadeRight.spin(directionType::fwd,60,velocityUnits::pct);
            CascadeLeft.spin(directionType::fwd,60,velocityUnits::pct);
        }   
        else if (Controller1.ButtonB.pressing()){
            CascadeRight.spin(directionType::fwd,-60,velocityUnits::pct);
            CascadeLeft.spin(directionType::fwd,-60,velocityUnits::pct);
        }
       
        else if (Controller1.ButtonL2.pressing()){
            Claw.spin(directionType::fwd,60,velocityUnits::pct);
        } 
        
        else if (Controller1.ButtonL1.pressing()){
            Claw.spin(directionType::fwd,-60,velocityUnits::pct);
        }
        
        else if (Controller1.ButtonR1.pressing()){
            Flipper.spin(directionType::fwd,40,velocityUnits::pct);
        }   
        else if (Controller1.ButtonR2.pressing()){
            Flipper.stop(brakeType::coast);
        }
        else{
            Claw.stop(brakeType::hold);
            CascadeRight.stop(brakeType::hold);
            CascadeLeft.stop(brakeType::hold);
        }
        task::sleep(20);
    }    

 
    vex::task::sleep(20); 
  }

int main() {
    
    pre_auton();
   
    Competition.autonomous( autonomous );
    Competition.drivercontrol( usercontrol );

}
