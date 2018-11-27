This application provides executable binaries for demonstrating our stereo scene flow method in the following paper.
If you use our algorithm, please cite our CVPR 2017 paper.
We do not plan to release our original source code of the algorithm due to the lisence issue.

@InProceedings{Taniai2017,
  author    = {Tatsunori Taniai and
               Sudipta N. Sinha and
               Yoichi Sato},
  title     = {{Fast Multi-frame Stereo Scene Flow with Motion Segmentation}},
  booktitle = {IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
  pages     = {6891--6900},
  year      = {2017}
}

Note that the software will produce slighly different results than those reported in the paper
due to a different feature tracking method used in the algorithm.
When comparing results of our method on KITTI and Sintel dataset, please use the original results
available from KITTI online leader board or from our project site (see Data section below).


---------
Download :
---------
You can download the binaries at https://github.com/t-taniai/FSF_CVPR2017_Demo/releases
Note that this software requires a CPU with SSE intrinsics.


---------
Usage    :
---------
Run the demo.bat file. The algorithm runs for three example sequences:
1) Sequence "alley_1" from Sintel training (in dataset/Sintel/training/...)
2) Sequence "000000" from KITTI training (in dataset/kitti_scene_flow_multiview/training/...)
3) A custom scequence without ground truth data (in dataset/Custom/...)

In "results" directory, you will get for each scene following data.
/data ---------- /disp_0/frame_****.png  : Encoded disparity map of first frame.
      ---------- /disp_1/frame_****.png  : Encoded disparity map of second frame.
      ---------- /flow/frame_****.png    : Encoded flow map (see below for decoding).
      ---------- /label/frame_****.png   : Binary motion segmentation

/debug --------- Visualization of results (use -vizSaveFlags to choose which steps we visualize).
                 This is disabled if -debug 0 is given.

log.txt -------- Log of comandline messages.

timestamp.txt -- Running times of individual steps of the algorithm in each frame.
                 Times for logging and saving data are excluded from time stamps.

---------
Format   :
---------
For KITTI scenes (when "-datasetType kitti" or "-saveAsKittiFormat 1"),
the data format is the same with KITTI's submission format, that is,

Disparity image: 16 bit 1-channel png where intensities I = 256*disparity and I = 0 mean "invalid" disparity.
Flow image     : 16 bit 3-channel png where intensities of RGB channels represent following values.
                 R = 64 * u - 1^15
                 G = 64 * v - 1^15
                 B = 1 if a pixel has a valid flow and 0 if invalid

For other scenes (when "-saveAsKittiFormat 1"), the scaling factor of disparity is changed from 256 to 64.


--------
Data    :
--------
Please visit our project site (https://taniai.space/projects/cvpr17_fsf/) where you can find
1) Results of our method as well as PRSM and OSF on Sintel dataset
2) Ground truth binary motion segmentation mask of Sintel dataset.

Note that "cave_2" and "sleeping_1" in Sintel are excluded from evaluations
because camera parameters K are not constant (due to zooming) in those scenes.

--------
History :
--------
11/27/2018  v1.0 Released the demonstration software.
