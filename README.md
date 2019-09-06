# Analog Gauge Reader

This application takes an image of an analog gauge and reads the value using functions from the OpenCV\* computer vision library.
It consists of two parts: calibration and measurement.  During calibration, the application calibrates an image 
of a gauge (provided by the user) by providing an easy to read degrees pattern.  It then uses these 
calibrated values in the measurement stage to convert the angle of the dial into a meaningful value.

## Gather your materials
  *	Python\* 3.7 or greater
  * OpenCV version 3.3.0 or greater
  *	An image of a gauge (or you can use the sample one provided)

## Setup
1. Take a picture of a gauge.
2. measure the rough size of the gauge in pixels using an image editor.
3. Run the application `python analog_gauge_reader.py --calibrate` and take note of the minimum and maximum values (angles and values) 

### Optimization tips:
If you're struggling to get your gauge to work, here are some tips:
* Good lighting is key.  Make sure there are no shadows if possible.
* Gauges with very thin or small dials may not work well, thicker dials work better.
* `diff1LowerBound, diff1UpperBound, diff2LowerBound, diff2UpperBound` determine the filtering of lines that don't represent the dial.  You may need to adjust this if it's not returning any lines found.


There is a considerable amount of trigonometry involved to create the calibration image, mainly sine and cosine to plot the calibration image lines and arctangent to get the angle of the dial.  This approach sets 0/360 to be the -y axis (if the image has a cartesian grid in the middle) and it goes clock-wise. There is a slight modification to make the 0/360 degrees be at the -y axis, by an addition (i+9) in the calculation of p_text[i][j]. Without this +9 the 0/360 point would be on the +x axis.  So this
implementation assumes the gauge is aligned in the image, but it can be adjusted by changing the value of 9 to something else.

# credits:
This is basically a refactor of https://github.com/intel-iot-devkit/python-cv-samples
