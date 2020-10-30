# Dart with Linear Time Stable PD

Adopt [Linear Time Stable PD](https://arpspoof.github.io/project/spd/spd.html) (SCA2020) to DART.

### Usage
If you don't need to get actual torques,

    skeleton->setSPDTarget(target_pose, k_p, k_d);
    world->step();

Or, if you need to get actual torques,

    Eigen::VectorXd torques = skeleton->getSPDForces(target_pose, k_p, k_d, world->getConstraintSolver());
    // do someting with torques
    ...
    
    skeleton->setForces(torques);
    world->step();
 
### Notes

* Recommended to call world->step() right after using setSPDTarget method. ( after using setSPDTarget method, some functions like mass matrix, coriolis force don't work properly. )
* Don't use setForces after using setSPDTarget in one time step.
* Performance increased up to 40% compared to the conventional SPD with same timestep.
* You can lower the time step to 1/30 ~ 1/60s. (1/100s ~ 1/300s recommended.)
