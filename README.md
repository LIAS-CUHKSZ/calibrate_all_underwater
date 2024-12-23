README for datashare/datasets of the paper Monocular Event-Based Vision for Obstacle Avoidance with a Quadrotor (2024).

The dataset files are in h5 file format. Each file has keys associated to the initial timestamp of each data trajectory collected; simulated data holds trajectories from a privileged expert policy executed in simulation and real data has pseudo-trajectories collected from the handheld event camera-depth camera rig.

DATA DESCRIPTION

Recursively printing the keys, data types, and shapes of a single trajectory in a dataset file yields the following:

        ,'-',172816552361,':',<HDF5 group "/172816552361" (8 members)>
                ,'-',data,':',<HDF5 dataset "data": shape (276, 21), type "<f4">
                ,'-',depths,':',<HDF5 dataset "depths": shape (276, 480, 640), type "<f4">
                ,'-',desvel,':',<HDF5 dataset "desvel": shape (276,), type "<f4">
                ,'-',dirs,':',<HDF5 dataset "dirs": shape (), type "|O">
                ,'-',dirs_ids,':',<HDF5 dataset "dirs_ids": shape (), type "<i8">
                ,'-',evs,':',<HDF5 dataset "evs": shape (275, 480, 640), type "<f4">
                ,'-',ims,':',<HDF5 dataset "ims": shape (276, 480, 640), type "<f4">
                ,'-',trajlength,':',<HDF5 dataset "trajlength": shape (), type "<i8">

`data`: file containing the followingcolumns of information at every timestamp: timestamp,desired_vel,quat_1,quat_2,quat_3,quat_4,pos_x,pos_y,pos_z,vel_x,vel_y,vel_z,velcmd_x,velcmd_y,velcmd_z,ct_cmd,br_cmd_x,br_cmd_y,br_cmd_z,is_collide. Note that quat 1,2,3,4 is arranged as w,x,y,z. velcmd is the expert command that is learned by V(phi) during training. ct and br refer to collective thrust and bodyrate commands by the lower-level controller provided in the DodgeDrone (2022) code package (not used in this work).
`depths`: depth images.
`desvel`: desired forward velocity for the trajectory.
`dirs`: list of directory names used for dataloading.
`dirs_ids`: list of directory ids used for dataloading.
`evs`: events batched into frames of datatype float.
`ims`: intensity images if available.
`trajlength`: length of the trajectory.

Much of the above data (telemetry, intensity images) is spoofed in real datasets, since only the depth images and events are used for the fine-tuning procedure of D(theta).

PROVIDED DATASETS

sim_forest.h5 - simulated rollout of the expert policy with corresponding, approximated events as well (100 trajectories).
real_forest-*.h5 - real handheld depth image and event data collected in a real pine forest, used to fine-tune D(theta) for forest experiments in the paper.
