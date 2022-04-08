# Actuation

## Configuration




## Actuation Flowchart
```mermaid
  flowchart RL;
    LF[libfranka::Robot];
    franka_ros_interface-->LF;
    IK(Inverse Kinematics)-->franka_ros_interface;
    Admittance(Admittance Controller)-->IK;
    FTSensor(Force Torque Sensor)-->Admittance;
    HPInput(Hybrid Pose)-->Admittance;
    
    
    classDef editable fill:#b6c1cc;
    classDef standard fill:#598fc2;
    class LF,franka_ros_interface,IK,Admittance,FTSensor standard;
    class HPInput editable;
```

### Low Level Control (Joint Commands)

```mermaid
  flowchart RL;
      FCNTopics-->FRC;
      FGNTopics-->FGN;
      FRITopics-->CM;
      
      subgraph franka_ros_interface
        subgraph franka_ros
          CM{Controller Manager}:::standard;
          CM-->PJP[position_joint_position_controller]:::editable;
          CM-->EJP[effort_joint_position_controller]:::editable;
          CM-->etc[new controller here]:::editable;
        end
        
        FRC{franka_ros_control}:::standard;%%-->LF;
        FGN{franka_gripper}:::standard;%%-->LF;
      end
      
      franka_ros_interface-->LF;
      
      subgraph ROSInterface
        FCNTopics(Configuration Services):::editable;
        FGNTopics(Gripper Commands):::editable;
        FRITopics(Joint Commands):::editable;
      end
      
      LF[libfranka::Robot]:::standard;
      
      classDef editable fill:#b6c1cc;
      classDef standard fill:#598fc2;
      class ROSControl standard;
      class franka_ros standard;
      class franka_ros_interface editable;
```
Documentation for the standard nodes:
* [libfranka](https://frankaemika.github.io/docs/libfranka.html)
* [franka_control](https://frankaemika.github.io/docs/franka_ros.html#franka-control)
* [franka_gripper](https://frankaemika.github.io/docs/franka_ros.html#franka-gripper)

[franka_ros_interface](https://github.com/justagist/franka_ros_interface) was forked, and this repo contains a minimally modified version.
