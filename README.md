编译方法：
1. mkdir build
2. cd build
3. cmake..
4. make
5. 生成在 build/devel/lib/imu_utils 下

----------------------------------------------

输出

```
gyr x  num of Cluster 100
gyr y  num of Cluster 100
gyr z  num of Cluster 100
acc x  num of Cluster 100
acc y  num of Cluster 100
acc z  num of Cluster 100
wait for imu data.
gyr x  numData 1200017
gyr x  start_t 1.51954e+09
gyr x  end_t 1.51956e+09
gyr x dt 
-------------12000.3 s
-------------200.005 min
-------------3.33342 h
gyr x  freq 99.9986
gyr x  period 0.0100001
gyr y  numData 1200017
gyr y  start_t 1.51954e+09
gyr y  end_t 1.51956e+09
gyr y dt 
-------------12000.3 s
-------------200.005 min
-------------3.33342 h
gyr y  freq 99.9986
gyr y  period 0.0100001
gyr z  numData 1200017
gyr z  start_t 1.51954e+09
gyr z  end_t 1.51956e+09
gyr z dt 
-------------12000.3 s
-------------200.005 min
-------------3.33342 h
gyr z  freq 99.9986
gyr z  period 0.0100001
Gyro X 
C    0.337159     27.3329     7.07386    0.236514 -0.00191803
 Bias Instability 9.57595e-05 rad/s
 Bias Instability 6.41789e-05 rad/s, at 418.686 s
 White Noise 5.25062 rad/s
 White Noise 0.00159214 rad/s
  bias -0.124198 degree/s
-------------------
Gyro y 
C     0.111842      27.2638      5.54463     0.381286 -0.000888626
 Bias Instability 9.63883e-05 rad/s
 Bias Instability 6.68627e-05 rad/s, at 96.9113 s
 White Noise 4.99841 rad/s
 White Noise 0.00152942 rad/s
  bias -0.0208066 degree/s
-------------------
Gyro z 
C    -0.11102     29.2664     2.72724    0.463507 -0.00461278
 Bias Instability 6.11902e-05 rad/s
 Bias Instability 4.6245e-05 rad/s, at 96.9113 s
 White Noise 5.60188 rad/s
 White Noise 0.00161581 rad/s
  bias 0.134288 degree/s
-------------------
==============================================
==============================================
acc x  numData 1200017
acc x  start_t 1.51954e+09
acc x  end_t 1.51956e+09
acc x dt 
-------------12000.3 s
-------------200.005 min
-------------3.33342 h
acc x  freq 99.9986
acc x  period 0.0100001
acc y  numData 1200017
acc y  start_t 1.51954e+09
acc y  end_t 1.51956e+09
acc y dt 
-------------12000.3 s
-------------200.005 min
-------------3.33342 h
acc y  freq 99.9986
acc y  period 0.0100001
acc z  numData 1200017
acc z  start_t 1.51954e+09
acc z  end_t 1.51956e+09
acc z dt 
-------------12000.3 s
-------------200.005 min
-------------3.33342 h
acc z  freq 99.9986
acc z  period 0.0100001
acc X 
C  2.12866e-05  0.000632738  0.000120405  5.63399e-05 -7.05642e-07
 Bias Instability 0.000507817 m/s^2
 White Noise 0.00829264 m/s^2
-------------------
acc y 
C -1.47851e-06    0.0007568  1.18022e-05  1.25705e-05 -1.75771e-07
 Bias Instability 0.000184108 m/s^2
 White Noise 0.00767715 m/s^2
-------------------
acc z 
C  1.15343e-05  0.000666672  7.00974e-05  2.26047e-05 -3.07754e-07
 Bias Instability 0.000305756 m/s^2
 White Noise 0.0075902 m/s^2
```

--------------------------------------------------

# imu_utils

A ROS package tool to analyze the IMU performance. C++ version of Allan Variance Tool. 
The figures are drawn by Matlab, in `scripts`.

Actually, just analyze the Allan Variance for the IMU data. Collect the data while the IMU is Stationary, with a two hours duration.

## refrence

Refrence technical report: [`Allan Variance: Noise Analysis for Gyroscopes`](http://cache.freescale.com/files/sensors/doc/app_note/AN5087.pdf "Allan Variance: Noise Analysis for Gyroscopes"), [`vectornav gyroscope`](https://www.vectornav.com/support/library/gyroscope "vectornav gyroscope") and 
[`An introduction to inertial navigation`](http://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-696.html "An introduction to inertial navigation").

```
Woodman, O.J., 2007. An introduction to inertial navigation (No. UCAM-CL-TR-696). University of Cambridge, Computer Laboratory.
```
Refrence Matlab code: [`GyroAllan`](https://github.com/XinLiGitHub/GyroAllan "GyroAllan")

## IMU Noise Values

Parameter | YAML element | Symbol | Units
--- | --- | --- | ---
Gyroscope "white noise" | `gyr_n` | <img src="https://latex.codecogs.com/svg.latex?{%5Csigma_g}"> | <img src="https://latex.codecogs.com/svg.latex?{%5Cfrac%7Brad%7D%7Bs%7D%5Cfrac%7B1%7D%7B%5Csqrt%7BHz%7D%7D}">
Accelerometer "white noise" | `acc_n` | <img src="https://latex.codecogs.com/svg.latex?{%5Csigma_a}"> | <img src="https://latex.codecogs.com/svg.latex?{%5Cfrac%7Bm%7D%7Bs^2%7D%5Cfrac%7B1%7D%7B%5Csqrt%7BHz%7D%7D}">
Gyroscope "bias Instability" | `gyr_w` | <img src="https://latex.codecogs.com/svg.latex?{%5Csigma_b_g}"> | <img src="http://latex.codecogs.com/svg.latex?\frac{rad}{s}&space;\sqrt{Hz}" title="\frac{rad}{s} \sqrt{Hz}" />
Accelerometer "bias Instability" | `acc_w` | <img src="https://latex.codecogs.com/svg.latex?{%5Csigma_b_a}"> | <img src="http://latex.codecogs.com/svg.latex?\frac{m}{s^2}&space;\sqrt{Hz}" title="\frac{m}{s^2} \sqrt{Hz}" />

* White noise is at tau=1;

* Bias Instability is around the minimum;

(according to technical report: [`Allan Variance: Noise Analysis for Gyroscopes`](http://cache.freescale.com/files/sensors/doc/app_note/AN5087.pdf "Allan Variance: Noise Analysis for Gyroscopes"))

## sample test

<img src="figure/gyr.jpg">
<img src="figure/acc.jpg">

* blue  : Vi-Sensor, ADIS16448, `200Hz`
* red   : 3dm-Gx4, `500Hz`
* green : DJI-A3, `400Hz`
* black : DJI-N3, `400Hz`
* circle : xsens-MTI-100, `100Hz`

## How to build and run?

### to build

```
sudo apt-get install libdw-dev
```

* download required [`code_utils`](https://github.com/gaowenliang/code_utils "code_utils");

* put the ROS package `imu_utils` and `code_utils` into your workspace, usually named `catkin_ws`;

* cd to your workspace, build with `catkin_make`;


### to run

* collect the data while the IMU is Stationary, with a two hours duration;

* (or) play rosbag dataset;

```
 rosbag play -r 200 imu_A3.bag
```

* roslaunch the rosnode;

```
roslaunch imu_utils A3.launch
```

Be careful of your roslaunch file:

```
<launch>
    <node pkg="imu_utils" type="imu_an" name="imu_an" output="screen">
        <param name="imu_topic" type="string" value= "/djiros/imu"/>
        <param name="imu_name" type="string" value= "A3"/>
        <param name="data_save_path" type="string" value= "$(find imu_utils)/data/"/>
        <param name="max_time_min" type="int" value= "120"/>
        <param name="max_cluster" type="int" value= "100"/>
    </node>
</launch>
```

### sample output:

```
type: IMU
name: A3
Gyr:
   unit: " rad/s"
   avg-axis:
      gyr_n: 1.0351286977809465e-04
      gyr_w: 2.9438676109223402e-05
   x-axis:
      gyr_n: 1.0312669892959053e-04
      gyr_w: 3.3765827874234673e-05
   y-axis:
      gyr_n: 1.0787155789128671e-04
      gyr_w: 3.1970693666470835e-05
   z-axis:
      gyr_n: 9.9540352513406743e-05
      gyr_w: 2.2579506786964707e-05
Acc:
   unit: " m/s^2"
   avg-axis:
      acc_n: 1.3985049290745563e-03
      acc_w: 6.3249251509920116e-04
   x-axis:
      acc_n: 1.1687799474421937e-03
      acc_w: 5.3044554054317266e-04
   y-axis:
      acc_n: 1.2050535351630543e-03
      acc_w: 6.0281218607825414e-04
   z-axis:
      acc_n: 1.8216813046184213e-03
      acc_w: 7.6421981867617645e-04
```

## dataset

DJI A3: `400Hz`

Download link: [`百度网盘`](https://pan.baidu.com/s/1jJYg8R0 "DJI A3")


DJI A3: `400Hz`

Download link: [`百度网盘`](https://pan.baidu.com/s/1pLXGqx1 "DJI N3")


ADIS16448: `200Hz`
 
Download link:[`百度网盘`](https://pan.baidu.com/s/1dGd0mn3 "ADIS16448")

3dM-GX4: `500Hz`

Download link:[`百度网盘`](https://pan.baidu.com/s/1ggcan9D "GX4")

xsens-MTI-100: `100Hz`

Download link:[`百度网盘`](https://pan.baidu.com/s/1i64xkgP "MTI-100")
